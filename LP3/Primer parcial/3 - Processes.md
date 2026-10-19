## Índice General

- [[#Objetivo del Capítulo]]
- [[#3.1 Process IDs]]
- [[#3.2 Creating Processes]]
    - [[#Using system]]
    - [[#Using fork and exec]]
        - [[#Calling fork]]
        - [[#Using exec]]
- [[#3.3 Scheduling and Process States]]
- [[#3.4 Terminating a Process]]
    - [[#Exit Codes and Termination Status]]
    - [[#Waiting for Process Termination]]
    - [[#Zombie Processes]]
    - [[#Cleaning Up Zombies Preventatively]]
- [[#3.5 Process Signals]]
- [[#3.6 Process Groups and Sessions]]

---

# Objetivo del Capítulo

Este capítulo explora el modelo de procesos de Linux. Aprenderás qué es un proceso, cómo el sistema operativo lo identifica mediante su ID de proceso (PID), cómo crear nuevos procesos utilizando tanto el método simple `system` como el método de bajo nivel y de alto rendimiento basado en `fork` y `exec`. También veremos cómo se gestiona el ciclo de vida y la terminación de los procesos (evitando "procesos zombi"), cómo interactúan mediante señales y los conceptos de grupos de procesos y sesiones.

---

# 3.1 Process IDs

En Linux, cada programa en ejecución es un **proceso**. El sistema operativo asigna a cada proceso un identificador único conocido como **Process ID (PID)**, que es un número entero positivo.

Para obtener el PID del proceso actual o del proceso padre, se utilizan las siguientes funciones de `<unistd.h>`:

- `getpid()`: Devuelve el PID del proceso que realiza la llamada.
- `getppid()`: Devuelve el PID del proceso padre.

Ambas funciones retornan un tipo `pid_t`.

---

# 3.2 Creating Processes

Existen dos formas principales de crear un nuevo proceso en Linux: la función de alto nivel `system` y la combinación de bajo nivel de `fork` y `exec`.

---

### Using system

La función `system` (declarada en `<stdlib.h>`) es la manera más sencilla de ejecutar un comando del sistema desde un programa C o C++.

```c
#include <stdlib.h>

int main () {
    int return_value = system ("ls -l /");
    return return_value;
}
```

> [!warning] Limitaciones de `system`
> La función `system` invoca internamente una shell (`/bin/sh`) para ejecutar el comando. Esto penaliza severamente el rendimiento y presenta graves riesgos de seguridad (vulnerabilidades de inyección de comandos si la entrada proviene de un usuario).

---

### Using fork and exec

El método estándar, seguro y eficiente en Linux para iniciar procesos consiste en duplicar el proceso actual mediante `fork` y luego reemplazar el programa duplicado por uno nuevo mediante `exec`.

#### Calling fork

La llamada al sistema `fork` duplica el proceso actual, creando un proceso hijo casi idéntico. Después de `fork`, **ambos procesos continúan ejecutándose desde la misma instrucción siguiente**.

Para distinguir si estamos en el proceso padre o en el proceso hijo, examinamos el valor devuelto por `fork()`:

- Si devuelve un valor **negativo**, la creación del proceso hijo falló.
- Si devuelve **0**, nos encontramos en el proceso hijo recién creado.
- Si devuelve un valor **positivo**, nos encontramos en el proceso padre, y el valor devuelto es el PID del hijo.

```c
#include <stdio.h>
#include <sys/types.h> " Necesario para pid_t "
#include <unistd.h>

int main () {
    pid_t child_pid;

    printf ("El PID del programa principal es %d\n", (int) getpid ());

    child_pid = fork ();
    if (child_pid != 0) {
        printf ("Este es el proceso PADRE, con PID %d\n", (int) getpid ());
        printf ("El PID de mi hijo es %d\n", (int) child_pid);
    } else {
        printf ("Este es el proceso HIJO, con PID %d\n", (int) getpid ());
    }

    return 0;
}
```

---

#### Using exec

Las funciones de la familia `exec` reemplazan por completo la imagen del proceso actual por un nuevo programa ejecutable. El PID del proceso no cambia, pero el código, los datos, el heap y el stack son reemplazados por los del nuevo programa.

Existen varias variantes de `exec` (como `execl`, `execv`, `execvp`, etc.) que difieren en cómo se pasan los argumentos y en cómo se busca el archivo ejecutable.

Ejemplo utilizando `execvp` (que busca el ejecutable en las rutas del `PATH` del sistema):

```c
#include <stdio.h>
#include <stdlib.h>
#include <sys/types.h>
#include <unistd.h>

int spawn (char* program, char** arg_list) {
    pid_t child_pid;

    child_pid = fork ();
    if (child_pid != 0) {
        // Este es el proceso padre. Devuelve el PID del hijo.
        return child_pid;
    } else {
        // Este es el proceso hijo. Ejecutamos el programa.
        execvp (program, arg_list);
        
        // La función execvp solo retorna si ocurre un error.
        fprintf (stderr, "Ocurrió un error en execvp\n");
        abort ();
    }
}

int main () {
    // La lista de argumentos para el comando 'ls -l /'
    // El primer argumento debe ser el nombre del programa.
    // La lista debe terminar obligatoriamente con un puntero NULL.
    char* arg_list[] = {
        "ls",
        "-l",
        "/",
        NULL
    };

    spawn ("ls", arg_list);
    printf ("El proceso padre continúa ejecutándose...\n");
    return 0;
}
```

---

# 3.3 Scheduling and Process States

Linux es un sistema operativo multiproceso con tiempo compartido (*time-sharing*). El planificador de tareas (scheduler) del kernel decide qué proceso se ejecuta en la CPU en cada momento.

Un proceso puede encontrarse en varios estados, entre los que destacan:

- **Running (Ejecución):** El proceso se está ejecutando activamente en la CPU o está listo para ejecutarse tan pronto como se le asigne tiempo.
- **Blocked / Sleeping (Bloqueado):** El proceso está esperando a que ocurra un evento externo (entrada de disco, recepción de red, o un temporizador) y no consume CPU.
- **Stopped (Detenido):** El proceso ha sido suspendido, normalmente mediante señales de control como `SIGSTOP` (presionando `Ctrl+Z` en la terminal).

---

# 3.4 Terminating a Process

Un proceso puede finalizar de dos formas: de manera normal (retornando de `main` o llamando a `exit`) o de manera anormal (debido a una señal no capturada, como un error de segmentación `SIGSEGV`).

---

### Exit Codes and Termination Status

Cuando un proceso termina de manera normal, devuelve un código de salida de 8 bits (un valor de `0` a `255`).

- Por convención, un valor de `0` indica que el programa terminó con éxito.
- Cualquier valor diferente de `0` indica un código de error o comportamiento anormal.

---

### Waiting for Process Termination

El proceso padre debe recoger el estado de terminación de sus procesos hijos. Para ello, se utilizan llamadas como `wait` o `waitpid` (definidas en `<sys/wait.h>`).

- `wait(&status)`: Bloquea al proceso padre hasta que alguno de sus hijos termine.
- `waitpid(pid, &status, options)`: Espera a que termine un hijo con un PID específico. Admite el flag `WNOHANG` para realizar una comprobación no bloqueante.

Existen macros estándar para analizar el entero de `status`:

| Macro | Descripción |
|:--|:--|
| `WIFEXITED(status)` | Devuelve verdadero si el hijo terminó normalmente. |
| `WEXITSTATUS(status)` | Devuelve el código de salida real del hijo (solo si `WIFEXITED` es verdadero). |
| `WIFSIGNALED(status)` | Devuelve verdadero si el hijo terminó debido a una señal no capturada (ej: crash). |
| `WTERMSIG(status)` | Devuelve el número de la señal que causó la terminación. |

---

### Zombie Processes

Si un proceso hijo termina y el proceso padre **no** llama a `wait` para recoger su estado, el hijo se convierte en un **proceso zombi**.

Un zombi no consume CPU ni memoria RAM significativa, pero sí ocupa una entrada en la tabla de procesos del kernel. Si la tabla de procesos se llena de zombis, el sistema no podrá crear nuevos procesos.

> [!info] El proceso init como rescatador
> Si el proceso padre muere antes que el hijo, el hijo es adoptado por el proceso especial `init` (PID 1), el cual recoge automáticamente su estado de terminación cuando este finaliza, evitando que se quede como zombi.

---

### Cleaning Up Zombies Preventatively

Si el proceso padre tiene una larga duración y no necesita esperar activamente la finalización de sus hijos de manera bloqueante, puede manejar la señal `SIGCHLD`. El kernel envía `SIGCHLD` al padre cada vez que un hijo termina.

```c
#include <signal.h>
#include <string.h>
#include <sys/types.h>
#include <sys/wait.h>

sig_atomic_t child_exit_status;

void clean_up_child_process (int signal_number) {
    int status;
    // Limpia el proceso hijo zombi
    wait (&status);
    child_exit_status = status;
}

int main () {
    struct sigaction sigchld_action;
    memset (&sigchld_action, 0, sizeof (sigchld_action));
    sigchld_action.sa_handler = &clean_up_child_process;
    
    // Registramos el manejador para la señal SIGCHLD
    sigaction (SIGCHLD, &sigchld_action, NULL);

    /* ... código que crea procesos hijos ... */

    return 0;
}
```

---

# 3.5 Process Signals

Las **señales (signals)** son un mecanismo de comunicación asíncrona que permite enviar notificaciones a los procesos. Cuando un proceso recibe una señal, interrumpe temporalmente su flujo de ejecución para ejecutar un manejador de señales (*signal handler*).

Las señales más comunes en Linux son: 

| Señal | Acción por Defecto | Causa |
|:--|:--|:--|
| `SIGINT` | Termina el proceso | Enviada por la terminal al presionar `Ctrl+C` |
| `SIGTERM` | Termina el proceso | Solicitud genérica de terminación (ej. comando `kill`) |
| `SIGKILL` | Termina inmediatamente | Terminación forzada (no se puede ignorar ni capturar) |
| `SIGSEGV` | Termina y genera core dump | Intento de acceso a memoria inválida (segmentation fault) |
| `SIGUSR1` / `SIGUSR2` | Termina el proceso | Señales definidas para uso personalizado del usuario |

Se utiliza la llamada al sistema `sigaction` (definida en `<signal.h>`) para configurar manejadores de señales personalizados de manera segura.

---

# 3.6 Process Groups and Sessions

- **Process Group (Grupo de Procesos):** Una colección de uno o más procesos (típicamente relacionados en un pipeline de comandos, como `ls | grep txt`). Las señales enviadas a un grupo de procesos afectan a todos sus miembros simultáneamente.
- **Session (Sesión):** Una colección de uno o más grupos de procesos que comparten una terminal de control (por ejemplo, todas las tareas iniciadas dentro de una misma ventana de terminal). Un proceso demonio (*daemon*) se desasocia explícitamente de su sesión y terminal de control para ejecutarse en segundo plano de manera autónoma.