## Índice General

- [[#Objetivo del Capítulo]]
- [[#2.1 Command-Line Options]]
    - [[#Names of Option Arguments]]
    - [[#getopt_long]]
- [[#2.2 Standard Input, Standard Output, and Standard Error]]
- [[#2.3 Writing Data to Standard Error]]
- [[#2.4 Writing to standard output with printf]]
- [[#2.5 Environment Variables]]
    - [[#Accessing Environment Variables]]
    - [[#Modifying Environment Variables]]
- [[#2.6 System Calls]]
- [[#2.7 Device Drivers and the /dev Directory]]
- [[#2.8 Inline Assembly Code]]

---

# Objetivo del Capítulo

Este capítulo introduce conceptos fundamentales de la programación en Linux para interactuar con el sistema operativo y el entorno de ejecución. Aprenderás a procesar argumentos de la línea de comandos de manera robusta, manejar los flujos de entrada y salida estándar, utilizar variables de entorno, invocar llamadas al sistema (system calls), interactuar con dispositivos a través del sistema de archivos `/dev` e integrar código ensamblador en programas C/C++.

---

# 2.1 Command-Line Options

Los programas en Linux suelen aceptar opciones (también llamadas *flags* o *switches*) en la línea de comandos para modificar su comportamiento. Estas opciones pueden ser cortas (un solo carácter precedido de un guion, ej. `-h`) o largas (palabras descriptivas precedidas de dos guiones, ej. `--help`).

El estándar de GNU establece que los programas deben admitir tanto opciones cortas como opciones largas equivalentes para mejorar la usabilidad.

---

### Names of Option Arguments

Muchas opciones requieren un argumento (por ejemplo, `-o archivo` o `--output archivo`).

- En las opciones cortas, el argumento puede aparecer inmediatamente después de la opción (`-oarchivo`) o separado por un espacio (`-o archivo`).
- En las opciones largas, el argumento se separa con un signo de igual (`--output=archivo`) o con un espacio (`--output archivo`).

---

### getopt_long

La función estándar para procesar opciones complejas en la línea de comandos (cortas y largas) es `getopt_long`, definida en la cabecera `<getopt.h>`.

Para usar `getopt_long`, se define un array de estructuras `struct option`. Cada elemento describe una opción larga:

```c
struct option {
    const char *name;     // Nombre de la opción larga (sin los dos guiones)
    int         has_arg;  // Puede ser no_argument, required_argument o optional_argument
    int        *flag;     // Puntero para almacenar el resultado o NULL
    int         val;      // Carácter o valor a retornar cuando se detecta la opción
};
```

A continuación se muestra un ejemplo básico de procesamiento de opciones que sigue este estándar:

```c
#include <getopt.h>
#include <stdio.h>
#include <stdlib.h>

const char* program_name;

void print_usage (FILE* stream, int exit_code) {
    fprintf (stream, "Uso: %s [opciones]\n", program_name);
    fprintf (stream,
             "  -h  --help             Mostrar esta ayuda.\n"
             "  -o  --output filename  Escribir salida a un archivo.\n"
             "  -v  --verbose          Mostrar mensajes detallados.\n");
    exit (exit_code);
}

int main (int argc, char* argv[]) {
    int next_option;
    const char* const short_options = "ho:v";
    const struct option long_options[] = {
        { "help",    no_argument,       NULL, 'h' },
        { "output",  required_argument, NULL, 'o' },
        { "verbose", no_argument,       NULL, 'v' },
        { NULL,      0,                 NULL, 0   } // Debe terminar con un elemento vacío
    };

    const char* output_filename = NULL;
    int verbose = 0;

    program_name = argv[0];

    do {
        next_option = getopt_long (argc, argv, short_options, long_options, NULL);
        switch (next_option) {
            case 'h':
                print_usage (stdout, 0);
            case 'o':
                output_filename = optarg; // optarg guarda el argumento de la opción
                break;
            case 'v':
                verbose = 1;
                break;
            case '?': // Opción no reconocida
                print_usage (stderr, 1);
            case -1:  // Fin de las opciones
                break;
            default:
                abort ();
        }
    } while (next_option != -1);

    if (verbose) {
        printf ("Modo detallado activo.\n");
    }
    if (output_filename != NULL) {
        printf ("Archivo de salida: %s\n", output_filename);
    }

    // Los argumentos que no son opciones (como nombres de archivos al final)
    // son ordenados por getopt_long al final de argv, comenzando en optind.
    if (optind < argc) {
        printf ("Argumentos adicionales:\n");
        for (int i = optind; i < argc; ++i) {
            printf ("  %s\n", argv[i]);
        }
    }

    return 0;
}
```

---

# 2.2 Standard Input, Standard Output, and Standard Error

Por defecto, cada proceso en Linux se inicia con tres flujos (streams) de comunicación abiertos:

| Flujo | Descriptor de Archivo | Constante C (`<stdio.h>`) | Uso Principal |
|:--|:--|:--|:--|
| **Standard Input (stdin)** | `0` (STDIN_FILENO) | `stdin` | Entrada de datos al programa |
| **Standard Output (stdout)** | `1` (STDOUT_FILENO) | `stdout` | Salida de datos normal / resultados |
| **Standard Error (stderr)** | `2` (STDERR_FILENO) | `stderr` | Diagnósticos y mensajes de error |

---

# 2.3 Writing Data to Standard Error

Es una buena práctica separar la salida normal del programa de los mensajes de error. Los resultados se dirigen a `stdout` y los diagnósticos a `stderr`. Esto permite que el usuario pueda redireccionar la salida del programa de forma limpia.

Ejemplo de redirección en la shell:

```bash
# Redireccionar salida estándar a un archivo (omite errores)
./mi_programa > salida.txt

# Redireccionar errores a un archivo diferente
./mi_programa > salida.txt 2> errores.log
```

---

# 2.4 Writing to standard output with printf

La salida estándar (`stdout`) utiliza **búferes (buffered I/O)** para mejorar el rendimiento de escritura en disco o terminal. Esto significa que los datos enviados con `printf` o `putchar` no se escriben inmediatamente en la consola, sino que se acumulan en un búfer de memoria.

El búfer se vacía (*flushed*) automáticamente bajo las siguientes condiciones:
- Se escribe un carácter de nueva línea (`\n`).
- El programa espera una entrada a través de `stdin`.
- El programa termina normalmente.
- Se fuerza la escritura con `fflush(stdout)`.

Por el contrario, **`stderr` no utiliza búfer (unbuffered I/O)** por defecto. Los mensajes enviados a `stderr` se muestran en pantalla de forma inmediata para asegurar que los errores se reporten incluso si el programa falla justo después de la llamada.

---

# 2.5 Environment Variables

Cada programa que se ejecuta en Linux cuenta con un conjunto de variables de entorno (environment variables), que constan de un par clave-valor en formato `NOMBRE=VALOR`.

Estas variables definen configuraciones del sistema, rutas de directorios, el idioma local, etc.

---

### Accessing Environment Variables

En C/C++, se puede acceder a las variables de entorno de dos maneras:

1. Usando la variable global `environ` (definida en `<unistd.h>`):

```c
#include <stdio.h>
#include <unistd.h>

// Declaración de la variable externa global
extern char** environ;

int main () {
    // Recorre todas las variables de entorno y las imprime
    for (char** env = environ; *env != NULL; ++env) {
        printf ("%s\n", *env);
    }
    return 0;
}
```

2. Usando la función `getenv` (definida en `<stdlib.h>`) para buscar una variable específica:

```c
#include <stdio.h>
#include <stdlib.h>

int main () {
    char* home_dir = getenv ("HOME");
    if (home_dir != NULL) {
        printf ("Tu directorio HOME es: %s\n", home_dir);
    } else {
        printf ("La variable HOME no está definida.\n");
    }
    return 0;
}
```

---

### Modifying Environment Variables

Se pueden modificar o añadir variables de entorno en el proceso actual y en los procesos hijos que este genere mediante `setenv` y `unsetenv`:

```c
#include <stdlib.h>

int main () {
    // Establece la variable "MI_VAR" con el valor "123" (sobrescribiendo si ya existe)
    setenv ("MI_VAR", "123", 1);

    // Elimina la variable "MI_VAR"
    unsetenv ("MI_VAR");

    return 0;
}
```

> [!warning] Las modificaciones son locales al proceso
> Cualquier cambio realizado mediante `setenv` solo afecta al proceso actual y a los subprocesos que inicie a partir de ese momento. No altera el entorno del shell que ejecutó el programa.

---

# 2.6 System Calls

Las **llamadas al sistema (system calls)** son las funciones que proporciona el kernel de Linux para que las aplicaciones de espacio de usuario soliciten servicios de bajo nivel (como leer/escribir archivos, crear procesos, o comunicarse por red).

Cuando una aplicación ejecuta una llamada al sistema:
1. Se transfiere el control del modo de usuario (User Mode) al modo de kernel (Kernel Mode) mediante una interrupción de software.
2. El kernel procesa la solicitud con privilegios elevados de hardware.
3. El control se devuelve a la aplicación en modo de usuario.

En Linux, no se suele invocar la llamada al sistema directamente con código máquina; en su lugar, la **GNU C Library (glibc)** proporciona funciones de envoltura (*wrapper functions*) estándar que realizan el cambio de contexto de forma transparente.

---

# 2.7 Device Drivers and the /dev Directory

En Linux, siguiendo la filosofía de Unix, **todo es un archivo**. Los dispositivos de hardware (discos, puertos serie, teclados, tarjetas de sonido) se representan en el sistema de archivos como archivos especiales dentro del directorio `/dev`.

Los programas interactúan con estos dispositivos usando las mismas system calls estándar de entrada/salida: `open`, `read`, `write` y `close`.

---

### Tipos de Archivos de Dispositivo

- **Character Devices:** Dispositivos que se leen o escriben carácter a carácter (o byte a byte) de forma secuencial (ej. `/dev/tty` para la terminal, `/dev/null`).
- **Block Devices:** Dispositivos que transfieren datos en bloques de tamaño fijo y soportan acceso aleatorio (ej. `/dev/sda` para discos duros).

---

### Dispositivos Especiales Útiles

- `/dev/null`: El "agujero negro" de Linux. Cualquier escritura en él se descarta instantáneamente. Leer de él devuelve inmediatamente un indicador de fin de archivo (EOF).
- `/dev/zero`: Un generador infinito de caracteres nulos (bytes con valor cero). Muy útil para inicializar archivos de datos vacíos o limpiar memoria.
- `/dev/random` y `/dev/urandom`: Generadores de números pseudoaleatorios del sistema que recopilan ruido de fondo de los controladores de dispositivos. `/dev/urandom` es preferido para la mayoría de aplicaciones ya que no se bloquea si el sistema se queda sin entropía.

---

# 2.8 Inline Assembly Code

Aunque la gran parte del software de sistemas se escribe en C o C++, en raras ocasiones es necesario interactuar directamente con el hardware o ejecutar instrucciones de CPU muy específicas que no están disponibles en el compilador. Para esto, GCC proporciona la sintaxis de **ensamblador embebido (inline assembly)**.

La sintaxis general utiliza la palabra clave `asm` o `__asm__`:

```c
__asm__ ("instrucciones" : salidas : entradas : registros_modificados);
```

Ejemplo de cómo obtener el ID de la CPU mediante la instrucción `cpuid` en arquitecturas x86:

```c
#include <stdio.h>

int main () {
    int eax_val, ebx_val;

    // Ejecuta cpuid con el parámetro de entrada eax = 0
    __asm__ ("cpuid"
             : "=a" (eax_val), "=b" (ebx_val) // Salidas: eax va a eax_val, ebx va a ebx_val
             : "a" (0)                         // Entradas: inicializa eax con 0
             : "ecx", "edx"                    // Registros que se corrompen durante la ejecución
    );

    printf ("Código del fabricante: %.4s\n", (char*)&ebx_val);
    return 0;
}
```

> [!warning] Código no portable
> El uso de inline assembly anula la portabilidad de tu aplicación, limitándola a la arquitectura específica (ej. x86, ARM) para la que fue escrito el código ensamblador. Debe utilizarse únicamente cuando no existan alternativas de alto nivel.