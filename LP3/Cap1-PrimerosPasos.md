## Índice General

- [[#Objetivo del Capítulo]]
- [[#1.1 Edición con Emacs]]
    - [[#Abrir un archivo fuente]]
    - [[#Formato automático]]
    - [[#Resaltado de sintaxis]]
- [[#1.2 Compilación con GCC]]
    - [[#Compilación de un solo archivo fuente]]
    - [[#Vinculación (Linking)]]
    - [[#Macros y optimización]]
    - [[#Buscando bibliotecas]]
- [[#1.3 Automatización con GNU Make]]
    - [[#Concepto básico]]
    - [[#Anatomía de un Makefile]]
    - [[#Recompilación inteligente]]
    - [[#Uso de variables]]
- [[#1.4 Depuración con GDB]]
    - [[#Compilando con información de depuración]]
    - [[#Comandos principales de GDB]]
    - [[#Ejecutando GDB desde Emacs]]
- [[#1.5 Fuentes de información]]
    - [[#Man Pages]]
    - [[#Info]]
    - [[#Archivos de cabecera (Header Files)]]
    - [[#Código fuente]]

---

# Objetivo del Capítulo

Este capítulo muestra los pasos básicos para crear un programa en C o C++ sobre Linux: crear y modificar código fuente, compilarlo y depurar el resultado. Se asume conocimiento previo de C/C++ y operaciones básicas en la terminal Linux.

---

# 1.1 Edición con Emacs

Un **editor de código** es la herramienta con la que escribes tus archivos fuente. Aunque existen muchos editores disponibles para Linux, el más popular y completo es **GNU Emacs**.

> [!info] Emacs no es obligatorio
> Puedes usar cualquier editor que prefieras (VS Code, vim, nano, etc.). Nada del resto del libro depende de Emacs.

### Abrir un archivo fuente

Para iniciar Emacs se ejecuta `emacs` en la terminal. Los atajos de teclado más útiles son:

| Atajo | Acción |
|:--|:--|
| `C-x C-f` | Abrir / crear archivo |
| `C-x C-s` | Guardar archivo |
| `C-x C-c` | Salir de Emacs |

Las extensiones habituales son `.c` / `.h` para C, y `.cpp` / `.hpp` / `.cc` / `.hxx` / `.cxx` / `.C` para C++.

---

### Formato automático

Emacs detecta automáticamente que estás editando código fuente. Si presionas **Tab** en una línea vacía, el cursor salta a la posición de sangría correcta; si la línea ya tiene texto, lo sangra adecuadamente. Esto se puede personalizar ampliamente con código LISP.

---

### Resaltado de sintaxis

Emacs puede colorear distintos elementos del código (palabras clave, tipos integrados, comentarios), lo que facilita detectar errores de sintaxis. Para activarlo, se agrega lo siguiente al archivo `.emacs`:

```lisp
(global-font-lock-mode t)
```

> [!info] Emacs está escrito en LISP
> Gran parte de la funcionalidad de Emacs se programa en LISP. Se puede extender con módulos para editar casi cualquier tipo de documento, e incluso crear juegos y bases de datos.

---

# 1.2 Compilación con GCC

Un **compilador** transforma código fuente legible por humanos en código máquina ejecutable. En Linux, los compiladores son parte de la **GNU Compiler Collection (GCC)**, que incluye compiladores para C, C++, Java, Objective-C, Fortran y Chill.

---

### Compilación de un solo archivo fuente

| Herramienta | Lenguaje | Comando típico |
|:--|:--|:--|
| `gcc` | C | `gcc -c archivo.c` |
| `g++` | C++ | `g++ -c archivo.cpp` |

El flag `-c` compila el archivo a un objeto (`.o`) **sin enlazar**. Sin este flag, GCC intenta generar un ejecutable directamente.

Flags útiles:

| Flag | Función |
|:--|:--|
| `-c` | Compilar solamente (generar objeto `.o`) |
| `-I directorio` | Indicar dónde buscar archivos de cabecera (`.h`) |
| `-l biblioteca` | Vincular una biblioteca (ej: `-lpam`) |
| `-L directorio` | Indicar dónde buscar bibliotecas |
| `-o nombre` | Nombrar el ejecutable de salida |

Ejemplo completo de compilación e enlazado:

```bash
gcc -c main.c
g++ -c reciprocal.cpp
g++ -o reciprocal main.o reciprocal.o
```

> [!info] ¿Por qué usar `g++` para enlazar?
> Si el programa contiene código C++, **siempre** se usa `g++` para el enlazado, incluso si también tiene archivos `.c`. Solo se usa `gcc` cuando el proyecto es 100 % C.

---

### Vinculación (Linking)

La vinculación une los archivos de objetos (`.o`) en un único ejecutable. Si se necesita enlazar una biblioteca, se usa el flag `-l`:

```bash
g++ -o servidor servidor.o -lpam
```

El compilador agrega automáticamente el prefijo `lib` y el sufijo `.so` (o `.a`). Para buscar bibliotecas en directorios no estándar se usa `-L`:

```bash
g++ -o servidor servidor.o -L/mi/ruta/lib -lpam
```

---

### Macros y optimización

Se pueden definir macros desde la línea de comandos con `-D`:

```bash
g++ -D NDEBUG -c main.c   # Desactiva asserts()
g++ -D NDEBUG=1 -c main.c  # Igual, con valor explícito
```

Para **optimizar** el código en producción:

```bash
g++ -O2 -c main.c
```

> [!warning] Optimización y depuración
> Compilar con optimización puede dificultar la depuración con GDB y a veces revela bugs ocultos en el código.

---

# 1.3 Automatización con GNU Make

En Linux, la mayoría de programadores usan **GNU Make** en lugar de un IDE para recompilar automáticamente el código.

---

### Concepto básico

Make se basa en tres conceptos:

- **Objetivos (targets):** los archivos que se quieren generar.
- **Dependencias:** archivos que deben existir (y estar actualizados) antes de generar el objetivo.
- **Reglas:** comandos que se ejecutan para construir el objetivo.

---

### Anatomía de un Makefile

Un archivo `Makefile` tiene este formato:

```makefile
# Variables
CXXFLAGS = -Wall

# Objetivo final
reciprocal: main.o reciprocal.o
	g++ -o reciprocal main.o reciprocal.o

# Reglas para cada objeto
main.o: main.c reciprocal.hpp
	gcc -c main.c

reciprocal.o: reciprocal.cpp reciprocal.hpp
	g++ -c reciprocal.cpp

# Limpieza
clean:
	rm -f *.o reciprocal
```

> [!info] Sangría con Tab
> Las líneas de comando (reglas) **deben** comenzar con un carácter de tabulación, no con espacios. Emacs lo maneja automáticamente.

---

### Recompilación inteligente

Make analiza las **fechas de modificación** de los archivos para decidir qué recompilar. Si modificas solo `main.c`, Make solo recompila `main.o` y re-enlaza; `reciprocal.o` no se toca porque none de sus dependencias cambiaron.

---

### Uso de variables

Las variables en Make se definen así:

```makefile
CXXFLAGS = -Wall -O2
```

Se usan con `$(...)`:

```makefile
reciprocal.o: reciprocal.cpp reciprocal.hpp
	g++ $(CXXFLAGS) -c reciprocal.cpp
```

También se pueden sobreescribir desde la línea de comandos:

```bash
make clean && make CXXFLAGS="-O2"
```

---

# 1.4 Depuración con GDB

El **depurador** es la herramienta que se usa para encontrar por qué un programa no se comporta como se espera. **GNU Debugger (GDB)** es el depurador estándar en Linux.

---

### Compilando con información de depuración

Para usar GDB, se debe compilar con el flag `-g`:

```bash
make CXXFLAGS=-g
```

El flag `-g` incluye información extra en los archivos de objeto que permite a GDB mapear direcciones de máquina a líneas del código fuente, nombres de variables locales, etc.

---

### Comandos principales de GDB

| Comando | Abreviatura | Función |
|:--|:--|:--|
| `run [args]` | `r [args]` | Ejecutar el programa dentro de GDB |
| `break [función/línea]` | `b [función/línea]` | Establecer un punto de interrupción |
| `next` | `n` | Ejecutar la siguiente línea (sin entrar en funciones) |
| `step` | `s` | Ejecutar la siguiente línea (entrando en funciones) |
| `continue` | `c` | Continuar ejecución hasta el siguiente breakpoint |
| `backtrace` | `bt` | Mostrar la pila de llamadas |
| `up` / `down` | `u` / `d` | Subir / bajar en la pila de llamadas |
| `print variable` | `p variable` | Imprimir el valor de una variable |
| `quit` | `q` | Salir de GDB |

---

### Ejecutando GDB desde Emacs

Para integrar GDB dentro de Emacs se usa:

```
M-x gdb
```

Emacs mostrará el código fuente y se detendrá automáticamente en los puntos de interrupción, lo que facilita ver el contexto completo en lugar de una sola línea de texto.

---

# 1.5 Fuentes de información

Linux incluye mucha documentación útil. El desafío es saber dónde buscar.

---

### Man Pages

Las **páginas de manual (man pages)** documentan comandos, system calls y funciones de la librería estándar. Están divididas en secciones numeradas:

| Sección | Contenido |
|:--|:--|
| `(1)` | Comandos de usuario |
| `(2)` | System calls |
| `(3)` | Funciones de la librería estándar |
| `(8)` | Comandos de administración del sistema |

```bash
man ls         # Página del comando ls
man 2 open     # System call open (sección 2)
man -k archivo # Buscar en las líneas de resumen
```

---

### Info

El sistema **Info** contiene documentación más detallada que man para muchos componentes GNU/Linux. Es un sistema de hipertexto basado en texto.

```bash
info            # Navegador Info general
info gcc        # Documentación específica de GCC
info libc       # Documentación de la librería C
```

Dentro de Emacs se accede con `C-h i`.

---

### Archivos de cabecera (Header Files)

Los archivos de cabecera en `/usr/include` y sus subdirectarios son una fuente útil de información sobre la interfaz de los system calls y funciones disponibles. Contienen las definiciones de señales, estructuras de datos, constantes, etc.

> [!warning] No incluir directamente
> No se deben incluir archivos de cabecera internos (de `/usr/include/bits`, `/usr/include/sys` o `/usr/include/linux`) directamente en los programas. Siempre usar los archivos de cabecera públicos listados en las man pages.

---

### Código fuente

En el mundo del software libre, el código fuente es la máxima autoridad. Las distribuciones de Linux suelen incluir el código fuente completo de todo el sistema. El código del kernel Linux se almacena típicamente en `/usr/src`.
