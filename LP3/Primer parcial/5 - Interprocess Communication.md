## Índice General

- [[#Objetivo del Capítulo]]
- [[#5.1 Shared Memory]]
    - [[#Fast Local Communication]]
    - [[#The Memory Model]]
    - [[#Allocation]]
    - [[#Attachment and Detachment]]
    - [[#Deallocation]]
    - [[#Shared Memory Sample Program]]
- [[#5.2 Processes Semaphores]]
    - [[#Allocation and Deallocation]]
    - [[#Initializing Semaphores]]
    - [[#Wait and Post Operations]]
    - [[#Debugging Semaphores]]
- [[#5.3 Mapped Memory]]
    - [[#Mapping an Ordinary File]]
    - [[#Shared Memory Revisited]]
    - [[#The mmap System Call]]
    - [[#Shared Memory with mmap]]
- [[#5.4 Pipes]]
    - [[#Creating Pipes]]
    - [[#Communication Between Parent and Child Processes]]
    - [[#Redirecting Standard Input and Output]]
    - [[#popen and pclose]]
    - [[#FIFOs / Named Pipes]]
- [[#5.5 UNIX Domain Sockets]]
    - [[#Socket Concepts]]
    - [[#System Calls]]
    - [[#UNIX Domain Socket Sample]]

---

# Objetivo del Capítulo

Este capítulo aborda las **Interprocess Communications (IPC)** en Linux, los mecanismos que permiten a procesos independientes intercambiar datos y coordinar su ejecución. Se estudian cinco técnicas fundamentales: memoria compartida (Shared Memory System V), semáforos entre procesos, memoria mapeada (`mmap`), tuberías (*pipes* y *FIFOs*) y sockets de dominio UNIX (UNIX Domain Sockets).

---

# 5.1 Shared Memory

La **memoria compartida System V** es uno de los mecanismos IPC más rápidos disponibles en Linux, ya que permite que dos o más procesos compartan directamente una misma región de memoria RAM sin necesidad de copiar datos entre ellos a través del kernel.

---

### Fast Local Communication

Dado que los procesos acceden directamente a la memoria sin pasar por el kernel para cada operación de lectura/escritura, la velocidad de comunicación es casi equivalente a acceder a una variable global local. Sin embargo, requiere el uso explícito de mecanismos de sincronización (como semáforos) para evitar condiciones de carrera.

---

### The Memory Model

El kernel asigna un bloque especial de memoria que se identifica mediante una clave entera (`key_t`) o un ID único devuelto por el sistema. Cada proceso puede mapear esta región en su propio espacio de direcciones virtuales.

---

### Allocation

Se utiliza la llamada `shmget` (definida en `<sys/shm.h>`) para asignar un segmento de memoria compartida:

```c
int shmget(key_t key, size_t size, int shmflg);
```

- `key`: Clave numérica (o `IPC_PRIVATE` para crear un segmento privado).
- `size`: Tamaño del segmento en bytes (redondeado al tamaño de página del sistema).
- `shmflg`: Permisos de acceso (similares a los permisos de archivos, ej: `0666`) combinados con flags como `IPC_CREAT` (crear si no existe) e `IPC_EXCL`.

Devuelve el identificador del segmento de memoria compartida (`shmid`).

---

### Attachment and Detachment

- **Attachment (Vincular):** Para acceder al bloque, un proceso debe vincular el segmento a su espacio de direcciones mediante `shmat`:

```c
void* shmat(int shmid, const void *shmaddr, int shmflg);
```

Devuelve un puntero a la memoria compartida (o `(void*) -1` en caso de error).

- **Detachment (Desvincular):** Cuando un proceso termina de usar el segmento, lo desvincula con `shmdt`:

```c
int shmdt(const void *shmaddr);
```

---

### Deallocation

Desvincular un segmento con `shmdt` **no** lo elimina del kernel. Para liberar la memoria compartida del sistema se debe invocar `shmctl`:

```c
shmctl(shmid, IPC_RMID, 0);
```

---

### Shared Memory Sample Program

```c
#include <stdio.h>
#include <sys/shm.h>
#include <sys/stat.h>

int main () {
    int segment_id;
    char* shared_memory;
    const int segment_size = 0x1000; // 4096 bytes

    // 1. Asignar el segmento de memoria compartida
    segment_id = shmget (IPC_PRIVATE, segment_size,
                         IPC_CREAT | IPC_EXCL | S_IRUSR | S_IWUSR);

    // 2. Vincular el segmento al espacio de direcciones del proceso
    shared_memory = (char*) shmat (segment_id, 0, 0);
    printf ("Memoria compartida vinculada en la dirección %p\n", shared_memory);

    // 3. Escribir datos en la memoria compartida
    sprintf (shared_memory, "¡Hola desde la memoria compartida!");

    // 4. Desvincular la memoria compartida
    shmdt (shared_memory);

    // 5. Vincular de nuevo en otro punto del programa para leer
    shared_memory = (char*) shmat (segment_id, 0, 0);
    printf ("Contenido leído: %s\n", shared_memory);

    // 6. Limpieza
    shmdt (shared_memory);
    shmctl (segment_id, IPC_RMID, 0);

    return 0;
}
```

---

# 5.2 Processes Semaphores

Dado que la memoria compartida no ofrece sincronización implícita, se utilizan **semáforos System V** para coordinar el acceso entre procesos independientes.

---

### Allocation and Deallocation

A diferencia de los semáforos de POSIX, los semáforos System V se gestionan en "conjuntos" (*sets*).

- Se asignan con `semget`:

```c
int semid = semget(key_t key, int nsems, int semflg);
```

- Se liberan con `semctl`:

```c
semctl(semid, 0, IPC_RMID);
```

---

### Initializing Semaphores

Se inicializa el valor del semáforo con `semctl` utilizando el comando `SETVAL`:

```c
union semun {
    int val;
    struct semid_ds *buf;
    unsigned short *array;
};

union semun argument;
argument.val = 1; // Valor inicial del semáforo (ej: 1 para exclusión mutua)
semctl (semid, 0, SETVAL, argument);
```

---

### Wait and Post Operations

Las operaciones de espera (*wait*) y señalización (*post*) se ejecutan mediante la llamada al sistema `semop` utilizando la estructura `struct sembuf`:

```c
struct sembuf sb;
sb.sem_num = 0;        // Índice del semáforo en el conjunto
sb.sem_op = -1;        // -1 para op. Wait (decrementar), +1 para op. Post (incrementar)
sb.sem_flg = SEM_UNDO; // Libera automáticamente el semáforo si el proceso muere
semop (semid, &sb, 1);
```

> [!info] SEM_UNDO para evitar deadlocks
> La opción `SEM_UNDO` le indica al kernel que deshaga automáticamente las operaciones realizadas sobre el semáforo si el proceso finaliza inesperadamente, evitando que otros procesos queden bloqueados para siempre.

---

### Debugging Semaphores

En Linux, los recursos IPC de System V (memoria compartida, conjuntos de semáforos y colas de mensajes) persisten en el sistema incluso después de que los procesos finalicen. Se administran mediante la línea de comandos:

```bash
ipcs -a     # Muestra todos los recursos IPC activos (memoria, semáforos, etc.)
ipcrm -s ID # Elimina manualmente un conjunto de semáforos por su ID
ipcrm -m ID # Elimina manualmente un segmento de memoria compartida
```

---

# 5.3 Mapped Memory

La **memoria mapeada (Mapped Memory)** permite vincular un archivo del disco directamente a la memoria RAM de un proceso. Al modificar el búfer en memoria, los cambios se reflejan automáticamente en el archivo en disco.

---

### Mapping an Ordinary File

Permite acceder al contenido de un archivo mediante punteros directos a memoria en lugar de llamadas repetidas a `read` o `write`.

---

### Shared Memory Revisited

Si dos o más procesos mapean el mismo archivo en memoria con los permisos adecuados, pueden utilizar ese archivo mapeado como un segmento de memoria compartida persistente.

---

### The mmap System Call

La llamada al sistema `mmap` vincula un archivo a memoria:

```c
void* mmap(void *addr, size_t length, int prot, int flags, int fd, off_t offset);
```

- `length`: Cantidad de bytes a mapear.
- `prot`: Protección de memoria (`PROT_READ`, `PROT_WRITE`, `PROT_EXEC`).
- `flags`: `MAP_SHARED` (los cambios se escriben en el archivo y son visibles por otros procesos) o `MAP_PRIVATE` (copia en escritura, aislada).
- `fd`: Descriptor de archivo abierto previamente con `open`.
- `offset`: Posición dentro del archivo (debe ser múltiplo del tamaño de página).

Para desmapear la memoria se utiliza `munmap(addr, length)`.

---

### Shared Memory with mmap

Ejemplo de cómo escribir datos en un archivo mediante `mmap`:

```c
#include <fcntl.h>
#include <stdio.h>
#include <sys/mman.h>
#include <unistd.h>

int main (int argc, char* argv[]) {
    int fd;
    void* file_memory;

    // Abrir el archivo para lectura/escritura
    fd = open (argv[1], O_RDWR | O_CREAT, S_IRUSR | S_IWUSR);
    lseek (fd, 1000 - 1, SEEK_SET);
    write (fd, "", 1); // Expandir el archivo a 1000 bytes

    // Mapear el archivo a memoria
    file_memory = mmap (0, 1000, PROT_READ | PROT_WRITE, MAP_SHARED, fd, 0);
    close (fd);

    // Escribir datos directamente en memoria
    sprintf ((char*) file_memory, "Datos guardados vía mmap.\n");

    // Desmapear
    munmap (file_memory, 1000);
    return 0;
}
```

---

# 5.4 Pipes

Una **tubería (pipe)** es un canal de comunicación unidireccional entre procesos. Los datos que se escriben en un extremo de la tubería se leen en el mismo orden (FIFO) desde el otro extremo.

---

### Creating Pipes

Se utiliza la llamada al sistema `pipe`, la cual devuelve dos descriptores de archivo abiertos:

```c
int pipe(int pipefd[2]);
```

- `pipefd[0]`: Abierto para **lectura**.
- `pipefd[1]`: Abierto para **escritura**.

---

### Communication Between Parent and Child Processes

Dado que los descriptores de archivo se heredan al llamar a `fork`, las tuberías son ideales para la comunicación entre un proceso padre y su proceso hijo:

```c
#include <stdio.h>
#include <unistd.h>

int main () {
    int my_pipe[2];
    pipe (my_pipe);

    if (fork () == 0) {
        // Proceso Hijo: Cierra el extremo de lectura y escribe
        close (my_pipe[0]);
        char msg[] = "Hola Padre!";
        write (my_pipe[1], msg, sizeof (msg));
        close (my_pipe[1]);
    } else {
        // Proceso Padre: Cierra el extremo de escritura y lee
        close (my_pipe[1]);
        char buffer[100];
        read (my_pipe[0], buffer, sizeof (buffer));
        printf ("Mensaje recibido del hijo: %s\n", buffer);
        close (my_pipe[0]);
    }
    return 0;
}
```

---

### Redirecting Standard Input and Output

Se utiliza la función `dup2` para redirigir la entrada o salida estándar (`stdin`/`stdout`) hacia una tubería. Esto permite conectar la salida de un programa con la entrada de otro, replicando el comportamiento del operador `|` en la shell.

```c
// Redirige la salida estándar (stdout) al extremo de escritura de la tubería
dup2 (my_pipe[1], STDOUT_FILENO);
```

---

### popen and pclose

Las funciones `popen` y `pclose` (de `<stdio.h>`) ofrecen un nivel de abstracción superior: crean un proceso hijo que ejecuta un comando de la shell a través de una tubería y devuelven un flujo `FILE*` para leer o escribir en él.

```c
#include <stdio.h>

int main () {
    FILE* stream = popen ("sort", "w");
    fprintf (stream, "manzana\n");
    fprintf (stream, "banana\n");
    fprintf (stream, "cereza\n");
    pclose (stream); // Ejecuta el comando 'sort' y ordena la entrada
    return 0;
}
```

---

### FIFOs / Named Pipes

Una **FIFO (Named Pipe)** es una tubería con nombre que existe en el sistema de archivos de Linux. A diferencia de las tuberías ordinarias, **permite la comunicación entre procesos no emparentados**.

Se crea mediante la llamada `mkfifo`:

```c
#include <sys/stat.h>

mkfifo ("/tmp/mi_fifo", 0666);
```

Los procesos pueden abrir `/tmp/mi_fifo` usando `open`, `read` y `write` como si fuera un archivo convencional.

---

# 5.5 UNIX Domain Sockets

Los **sockets de dominio UNIX (UNIX Domain Sockets)** son un mecanismo de IPC bidireccional entre procesos que se ejecutan en la misma máquina local. Tienen la misma interfaz de programación basada en sockets de red (TCP/IP), pero operan de forma mucho más eficiente al evitar el overhead de las capas de red del kernel.

---

### Socket Concepts

- Un socket actúa como un punto de comunicación bidireccional (*full-duplex*).
- Los sockets de dominio UNIX se identifican en el sistema por una ruta de archivo (ej. `/tmp/socket_demo`).

---

### System Calls

| Función | Propósito |
|:--|:--|
| `socket` | Crea un nuevo punto de conexión socket |
| `bind` | Asigna un nombre (dirección de archivo) al socket del servidor |
| `listen` | Configura el socket servidor para aceptar conexiones entrantes |
| `accept` | Bloquea el proceso servidor hasta que un cliente se conecta |
| `connect` | Establece una conexión desde un cliente hacia el servidor |

---

### UNIX Domain Socket Sample

Ejemplo de comunicación mediante un socket de servidor UNIX:

```c
#include <stdio.h>
#include <string.h>
#include <sys/socket.h>
#include <sys/un.h>
#include <unistd.h>

int main () {
    const char* const socket_name = "/tmp/demo_socket";
    int socket_fd;
    struct sockaddr_un name;

    // 1. Crear el socket de dominio UNIX
    socket_fd = socket (PF_LOCAL, SOCK_STREAM, 0);

    // 2. Indicar la dirección del socket (ruta del archivo)
    name.sun_family = AF_LOCAL;
    strcpy (name.sun_path, socket_name);

    // 3. Vincular el socket
    bind (socket_fd, (struct sockaddr*) &name, SUN_LEN (&name));

    // 4. Escuchar conexiones entrantes
    listen (socket_fd, 5);

    printf ("Servidor socket listo y escuchando en %s...\n", socket_name);

    // 5. Limpieza al finalizar
    close (socket_fd);
    unlink (socket_name); // Eliminar el archivo especial de socket

    return 0;
}
```

---

### Resumen de Mecanismos IPC

| Mecanismo | Velocidad | Relación entre Procesos | Persistencia | Uso Principal |
|:--|:--|:--|:--|:--|
| **Shared Memory** | Extremadamente alta | Cualquiera | Hasta ser eliminada explícitamente | Transferencia rápida de grandes volúmenes de datos |
| **Mapped Memory** | Muy alta | Cualquiera | Persistente en disco | Compartir datos y sincronizarlos con archivos en disco |
| **Pipes** | Alta | Padre / Hijo | Mientras los descriptores estén abiertos | Comunicación unidireccional simple |
| **FIFOs** | Alta | Cualquiera | En el sistema de archivos | Tuberías entre procesos independientes |
| **UNIX Sockets** | Alta | Cualquiera | Temporal | Comunicación bidireccional estructurada |