## Índice General

- [[#Objetivo del Capítulo]]
- [[#4.1 Thread Creation]]
- [[#4.2 Thread Arguments]]
- [[#4.3 Thread Cancellation and Detaching]]
    - [[#Thread Cancellation]]
    - [[#Thread Detaching and Joining]]
- [[#4.4 Thread-Specific Data]]
- [[#4.5 Thread Synchronization and Critical Sections]]
    - [[#Mutexes]]
    - [[#Semaphore Basics]]
    - [[#Condition Variables]]
- [[#4.6 GNU/Linux Thread Implementation]]

---

# Objetivo del Capítulo

Este capítulo introduce el concepto de hilos de ejecución (*threads*) en Linux utilizando la especificación estándar de hilos POSIX (conocida como **Pthreads**). Aprenderás a crear hilos, pasarles argumentos, controlar su ciclo de vida mediante la finalización, cancelación, espera (*joining*) y desasociación (*detaching*), almacenar datos específicos por hilo, y sincronizar el acceso a recursos compartidos mediante exclusión mutua (*mutexes*), semáforos y variables de condición.

---

# 4.1 Thread Creation

Un **hilo de ejecución** es una unidad secuencial de ejecución dentro de un proceso. A diferencia de los procesos creados con `fork`, todos los hilos creados dentro de un mismo proceso comparten el mismo espacio de direcciones (memoria global, variables estáticas, descriptores de archivos, etc.). Sin embargo, cada hilo mantiene su propio registro de instrucciones, pila (*stack*) para variables locales y estado de CPU.

Para trabajar con hilos en Linux, se utiliza la librería POSIX Threads. Se debe incluir `<pthread.h>` y compilar enlazando la biblioteca con el flag `-pthread` (o `-lpthread`):

```bash
g++ -pthread -o programa programa.cpp
```

Para crear un hilo se utiliza la función `pthread_create`:

```c
int pthread_create(pthread_t *thread, const pthread_attr_t *attr,
                   void *(*start_routine) (void *), void *arg);
```

Ejemplo de un programa básico multihilo:

```c
#include <pthread.h>
#include <stdio.h>

// Función que ejecutará el hilo de forma asíncrona
void* print_xs (void* unused) {
    while (1) {
        fputc ('x', stderr);
    }
    return NULL;
}

int main () {
    pthread_t thread_id;
    
    // Crear el nuevo hilo para ejecutar la función print_xs
    pthread_create (&thread_id, NULL, &print_xs, NULL);
    
    // El hilo principal imprime caracteres 'o' en la salida estándar
    while (1) {
        fputc ('o', stderr);
    }
    
    return 0;
}
```

---

# 4.2 Thread Arguments

La función de inicio de un hilo acepta un único argumento de tipo puntero genérico `void*` y devuelve un resultado del mismo tipo `void*`. Esto permite pasar cualquier tipo de dato (incluyendo estructuras complejas) realizando un moldeado (*cast*).

```c
#include <pthread.h>
#include <stdio.h>

struct thread_args {
    char character;
    int count;
};

void* char_print (void* parameters) {
    struct thread_args* p = (struct thread_args*) parameters;
    for (int i = 0; i < p->count; ++i) {
        fputc (p->character, stderr);
    }
    return NULL;
}

int main () {
    pthread_t thread1_id;
    pthread_t thread2_id;
    struct thread_args args1;
    struct thread_args args2;

    args1.character = 'x';
    args1.count = 30000;
    pthread_create (&thread1_id, NULL, &char_print, &args1);

    args2.character = 'o';
    args2.count = 20000;
    pthread_create (&thread2_id, NULL, &char_print, &args2);

    // Esperamos a que ambos hilos completen antes de salir de main
    pthread_join (thread1_id, NULL);
    pthread_join (thread2_id, NULL);

    return 0;
}
```

> [!warning] Cuidado con el ámbito de las variables
> Si pasas un puntero a una variable local (en el stack) como argumento a un hilo, debes asegurarte de que esa variable no salga de su ámbito antes de que el hilo termine de leerla.

---

# 4.3 Thread Cancellation and Detaching

---

### Thread Cancellation

Un hilo puede solicitar la finalización de otro hilo enviando una petición de cancelación mediante `pthread_cancel(thread_id)`.

El hilo receptor puede reaccionar de tres maneras dependiendo de su configuración de cancelación:
1. **Asynchronous (Asíncrona):** El hilo es destruido de forma inmediata por el sistema en cualquier punto de su ejecución.
2. **Deferred (Diferida, por defecto):** La cancelación se posterga hasta que el hilo alcanza un "punto de cancelación" (*cancellation point*), que son funciones del sistema que bloquean o realizan E/S (como `sleep`, `wait`, `write`, etc.).
3. **Disabled (Deshabilitada):** Las solicitudes de cancelación se ignoran.

---

### Thread Detaching and Joining

Cuando un hilo finaliza, sus recursos (como su stack) no se liberan completamente de inmediato para permitir que otros hilos puedan leer su valor de retorno.

- **Joining (Esperar):** La función `pthread_join` bloquea al hilo llamador hasta que el hilo especificado termina, liberando automáticamente los recursos de este último.
- **Detaching (Desasociar):** Si no necesitas conocer el valor de retorno de un hilo y quieres que el sistema libere sus recursos de manera autónoma tan pronto como termine, puedes "desasociarlo" llamando a `pthread_detach(thread_id)` o creándolo con atributos de desasociación.

```c
// Desasocia el hilo actual a sí mismo
pthread_detach (pthread_self ());
```

---

# 4.4 Thread-Specific Data

En un programa multihilo, las variables locales en funciones son privadas para cada hilo (porque se almacenan en su propio stack), pero las variables globales y estáticas son compartidas.

Si necesitas una variable que actúe como "global" pero que guarde un valor único y separado para cada hilo individual, puedes utilizar **Thread-Specific Data (TSD)**.

Pthreads provee un mecanismo mediante llaves de acceso (`pthread_key_t`):

```c
#include <pthread.h>
#include <stdio.h>

pthread_key_t log_key;

void write_to_log (const char* message) {
    FILE* log_file = (FILE*) pthread_getspecific (log_key);
    fprintf (log_file, "%s\n", message);
}

void close_log_file (void* thread_log) {
    fclose ((FILE*) thread_log);
}

void* thread_function (void* arg) {
    char filename[20];
    sprintf (filename, "thread_%u.log", (unsigned int)pthread_self());
    FILE* log_file = fopen (filename, "w");
    
    // Asociar el puntero del archivo de log a la llave TSD para este hilo
    pthread_setspecific (log_key, log_file);

    write_to_log ("Hilo inicializado.");
    /* ... código ... */
    
    return NULL;
}

int main () {
    // Crear la llave común y registrar una función destructora
    // que se ejecuta automáticamente cuando cada hilo termina.
    pthread_key_create (&log_key, close_log_file);

    /* ... crear hilos que llamen a thread_function ... */

    return 0;
}
```

---

# 4.5 Thread Synchronization and Critical Sections

Cuando múltiples hilos modifican las mismas variables de forma simultánea, se pueden producir **condiciones de carrera (race conditions)**, dando lugar a datos corruptos o comportamientos impredecibles. Las secciones de código que acceden a recursos compartidos se conocen como **secciones críticas (critical sections)** y deben protegerse mediante mecanismos de sincronización.

---

### Mutexes

Un **mutex** (abreviatura de *mutual exclusion*) es un cerrojo lógico que permite que solo un hilo acceda a la sección crítica a la vez.

- `pthread_mutex_init`: Inicializa un mutex.
- `pthread_mutex_lock`: Intenta bloquear el mutex. Si ya está bloqueado por otro hilo, el hilo actual se suspende hasta que quede libre.
- `pthread_mutex_unlock`: Desbloquea el mutex, permitiendo que otros hilos continúen.

```c
#include <pthread.h>

float account_balance = 1000.0;
pthread_mutex_t balance_mutex = PTHREAD_MUTEX_INITIALIZER;

void* withdraw (void* arg) {
    float amount = *(float*)arg;

    pthread_mutex_lock (&balance_mutex);
    // Sección Crítica
    if (account_balance >= amount) {
        account_balance -= amount;
    }
    pthread_mutex_unlock (&balance_mutex);

    return NULL;
}
```

---

### Semaphore Basics

Un **semáforo** es un contador protegido que permite controlar el acceso a un número limitado de recursos compartidos idénticos.

- Si el valor del semáforo es mayor que cero, un hilo puede decrementarlo (`sem_wait`) y continuar de inmediato.
- Si es cero, el hilo se bloquea hasta que otro hilo incremente el semáforo (`sem_post`).

Requiere incluir `<semaphore.h>`.

---

### Condition Variables

Las **variables de condición (condition variables)** permiten que un hilo se suspenda de forma eficiente hasta que se cumpla una condición arbitraria compleja (por ejemplo, "la cola de tareas ya no está vacía"), evitando el consumo innecesario de CPU por consulta continua (*polling*).

Una variable de condición (`pthread_cond_t`) siempre se utiliza en combinación con un mutex:

```c
#include <pthread.h>

int task_ready = 0;
pthread_mutex_t task_mutex = PTHREAD_MUTEX_INITIALIZER;
pthread_cond_t task_cond = PTHREAD_COND_INITIALIZER;

void* consumer (void* arg) {
    pthread_mutex_lock (&task_mutex);
    while (!task_ready) {
        // Libera temporalmente el mutex y suspende el hilo.
        // Al despertar, vuelve a adquirir automáticamente el mutex.
        pthread_cond_wait (&task_cond, &task_mutex);
    }
    // Procesar la tarea...
    pthread_mutex_unlock (&task_mutex);
    return NULL;
}

void set_task_ready () {
    pthread_mutex_lock (&task_mutex);
    task_ready = 1;
    // Despierta a un hilo suspendido en la variable de condición
    pthread_cond_signal (&task_cond);
    pthread_mutex_unlock (&task_mutex);
}
```

---

# 4.6 GNU/Linux Thread Implementation

Históricamente, Linux implementaba hilos mediante la biblioteca **LinuxThreads**, la cual representaba cada hilo como un proceso individual en el kernel. Esto presentaba limitaciones significativas en cuanto a la conformidad con el estándar POSIX (por ejemplo, los hilos tenían PIDs diferentes, y el manejo de señales no se compartía adecuadamente).

Los sistemas modernos GNU/Linux utilizan **NPTL (Native POSIX Thread Library)**. Con NPTL, un proceso multihilo se representa de forma nativa y eficiente en el kernel de Linux. Todos los hilos comparten el mismo PID, permitiendo una conformidad total con POSIX, una sincronización de exclusión mutua de altísimo rendimiento basada en *futexes* (fast userspace mutexes) y la capacidad de gestionar miles de hilos concurrentes de manera fluida.