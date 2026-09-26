# Unidad 1 - Caracterización de los Sistemas Distribuidos

Esta unidad introduce los conceptos fundamentales de los **Sistemas Distribuidos (SD)**, explicando sus orígenes, definiciones formales, ejemplos del mundo real, tendencias actuales y los desafíos de diseño que se deben afrontar para su desarrollo.

---

## 1. Antecedentes y Definición

### Antecedentes
* El avance continuo de las Tecnologías de la Información y Comunicación (TIC) permitió evolucionar hacia esquemas de trabajo coordinados en entornos separados geográficamente.
* La **Programación Orientada a Objetos (POO)** redefinió la creación de sistemas distribuidos, introduciendo nuevos modelos y abstracciones que facilitan la comunicación de componentes.
* La universalización de Internet generó una fuerte demanda de tecnologías de integración, impulsando lo que hoy conocemos como **Computación Orientada a Servicios (Service Oriented Computing)**.

### Definiciones Principales
Existen dos definiciones de referencia para comprender qué es un Sistema Distribuido:

> [!NOTE] Definición de Tanenbaum
> *"Un sistema distribuido es una colección de computadoras independientes que aparecen ante los usuarios del sistema como una única computadora."*

> [!NOTE] Definición de Coulouris
> *"Un sistema distribuido es aquel en el que los componentes localizados en computadores, conectados en red, comunican y coordinan sus acciones únicamente mediante el paso de mensajes."*

---

## 2. Compartición de Recursos y Características

### Recursos
La motivación central para construir un SD es **compartir recursos**. Estos recursos son administrados por servidores y accedidos por clientes (o encapsulados como objetos que interactúan entre sí).
* **Hardware:** Discos duros, impresoras, procesadores.
* **Software:** Archivos, bases de datos, objetos de software, transmisiones multimedia (video, audio).

### Características Fundamentales de un SD
Los sistemas distribuidos poseen tres particularidades que los distinguen radicalmente de los sistemas centralizados:

1. **Concurrencia:** La ejecución simultánea de múltiples tareas en distintos computadores es la norma. Los recursos compartidos deben gestionarse para evitar estados inconsistentes.
2. **Inexistencia de un reloj global:** Dado que cada computadora tiene su propio reloj interno, existe un límite de precisión para sincronizarlos. No hay una noción física global de tiempo en la que todos coincidan con exactitud absoluta, por lo que la coordinación depende del intercambio de mensajes.
3. **Fallos independientes:** Cualquier parte del sistema (la red, un computador, un proceso) puede fallar de forma autónoma.
   * **Fallos en la red:** Pueden aislar computadoras sin detener su ejecución, y estas computadoras a menudo no pueden discernir si la red cayó o simplemente está lenta.
   * **Caída de un computador (Crash):** Detiene sus procesos de golpe, y los demás componentes no se enteran inmediatamente de este cese de actividades.

---

## 3. Ejemplos de Sistemas Distribuidos

### Internet
Es el sistema distribuido más grande que existe, conformado por una inmensa cantidad de intranets conectadas entre sí por enlaces troncales de gran capacidad (**backbones**) que emplean fibra óptica, satélites, etc. Las comunicaciones se guían mediante protocolos estándar (IP, TCP, UDP). Su conjunto de servicios es abierto y puede ampliarse constantemente añadiendo nuevos servidores y servicios.

### Buscadores Web (Ejemplo: Google)
La tarea de indexar la Web (estimada en decenas de miles de millones de páginas) constituye uno de los mayores hitos de ingeniería de sistemas distribuidos. Su infraestructura incluye:
* Un enorme volumen de ordenadores interconectados en centros de datos mundiales.
* **Google File System (GFS):** Un sistema de archivos distribuido altamente optimizado para leer archivos muy grandes a tasas altas y sostenidas.
* **Bigtable:** Base de datos distribuida estructurada para acceso rápido a conjuntos masivos de información.
* **Chubby:** Servicio de coordinación y bloqueo distribuido para lograr consensos.
* **MapReduce:** Modelo de programación para procesamiento en paralelo masivo de datos.

### Intranet
Una porción de Internet administrada de manera independiente con un límite claro (protegido por cortafuegos o routers) que permite aplicar políticas de seguridad local. Consta de múltiples LANs enlazadas por redes troncales.

---

## 4. Tendencias Actuales

### Computación en la Nube (Cloud Computing)
Visión de la computación como una utilidad (un servicio público).
* La nube proporciona servicios de cómputo, almacenamiento e infraestructura a demanda del usuario, minimizando la necesidad de hardware potente local.
* Se rige por el modelo **Todo como Servicio (XaaS)**: IaaS (Infraestructura), PaaS (Plataforma), SaaS (Software), donde se paga por el uso real en lugar de comprar licencias permanentes.

### Computación Móvil y Ubicua
* **Computación Móvil:** Permite realizar tareas computacionales mientras el usuario está en movimiento físico, utilizando redes inalámbricas y dispositivos portátiles (celulares, notebooks). Posibilita la *computación independiente de la posición* (ej. usar una impresora local que se encuentre cerca).
* **Computación Ubicua:** Utilización integrada y transparente de microcomputadores baratos presentes en el entorno cotidiano (smartwatches, electrodomésticos inteligentes). Los dispositivos se fusionan tan íntimamente con sus funciones físicas que los usuarios casi no perciben su comportamiento computacional de manera diferenciada.

---

## 5. Desafíos de Diseño (Retos)

El diseño de un sistema distribuido robusto y eficiente enfrenta siete desafíos esenciales:

### A. Heterogeneidad
Los sistemas operan sobre una inmensa variedad de redes, hardware de cómputo, sistemas operativos, lenguajes de programación e implementaciones de software.
* **Middleware:** Es una capa de software que se ubica sobre el sistema operativo para unificar y enmascarar dicha heterogeneidad, proveyendo abstracciones potentes (ej. CORBA, RMI).
* **Código Móvil:** Programas transferidos entre computadoras para ser ejecutados localmente (ej. Applets de Java). Para contrarrestar la heterogeneidad del hardware, se utiliza el enfoque de **Máquina Virtual (VM)**, donde se compila a un bytecode universal ejecutable en cualquier máquina que tenga instalada la VM.

### B. Extensibilidad
La capacidad de que el sistema pueda expandirse y reimplementarse en múltiples formas. Depende de que sea un **sistema abierto**, lo cual requiere la publicación oficial de sus interfaces de comunicación y protocolos estándar.

### C. Seguridad
Mantener protegidos los datos y recursos que poseen alto valor económico o estratégico. Consta de tres pilares:
1. **Confidencialidad:** Protección contra accesos no autorizados.
2. **Integridad:** Protección contra alteración o corrupción de la información.
3. **Disponibilidad:** Asegurar el acceso continuo e ininterrumpido a los recursos.

### D. Escalabilidad
Se dice que un sistema es escalable si conserva su efectividad operativa aun cuando se dé un incremento significativo en la cantidad de recursos y usuarios. El diseño escalable requiere:
* Controlar los costos de recursos físicos al expandirse.
* Minimizar las pérdidas de rendimiento.
* Evitar el desbordamiento de recursos de software (ej. el agotamiento de direcciones IP).
* **Evitar cuellos de botella:** Utilizar algoritmos distribuidos y descentralizados en lugar de dependencias centralizadas.

### E. Tratamiento de Fallos
Los sistemas distribuidos deben diseñarse bajo la asunción de que el hardware y el software eventualmente fallarán.
* **Detección de fallos:** Usar técnicas de validación como sumas de verificación (*checksums*).
* **Enmascaramiento de fallos:** Ocultar o atenuar el fallo al cliente (ej. retransmitir un paquete perdido).
* **Tolerancia a fallos:** El sistema sigue operando aceptando ciertos fallos y degradando su servicio de forma controlada (ej. avisando al usuario que intente de nuevo en un navegador).
* **Recuperación frente a fallos:** Mecanismos de recuperación de datos mediante rollback (volver a un estado anterior consistente después de un crash).
* **Redundancia:** Utilizar componentes idénticos redundantes (ej. réplicas de bases de datos) para balancear y respaldar el sistema.

### F. Concurrencia
Permitir que múltiples clientes accedan simultáneamente a los mismos recursos encapsulados en objetos. Se resuelve implementando hilos de ejecución concurrentes (*threads*) y sistemas de bloqueo o exclusión mutua.

### G. Transparencia
Consiste en ocultar la distribución física de los componentes para que el programador y el usuario final perciban el sistema como un todo centralizado. La norma **ISO-RM-ODP** define 8 tipos de transparencias:



| Tipo de Transparencia | Descripción |
| :--- | :--- |
| **Acceso** | Permite acceder a recursos locales y remotos empleando operaciones idénticas. |
| **Ubicación** | Permite acceder a los recursos sin conocer su localización física o de red. |
| **Concurrencia** | Permite que varios procesos operen simultáneamente sobre recursos compartidos sin interferencias. |
| **Replicación** | Permite usar múltiples réplicas físicas de un recurso para mejorar fiabilidad/desempeño sin que el usuario lo note. |
| **Fallos** | Oculta los fallos de componentes para que los programas finalicen sus tareas con éxito. |
| **Movilidad** | Permite reubicar recursos y clientes en el sistema sin alterar la ejecución operativa actual. |
| **Prestaciones** | Permite reconfigurar dinámicamente el sistema para optimizar el rendimiento ante fluctuaciones de carga. |
| **Escalado** | Permite que el sistema y sus aplicaciones crezcan en tamaño sin modificar su arquitectura o algoritmos. |

---

## Ver también (Enlaces de la Unidad)
* [[Unidad 2 - Modelos de Sistemas]]
* [[Unidad 3 - Comunicación entre Procesos]]
* [[Unidad 4 - Objetos Distribuidos e Invocación]]
