# Unidad 3 - Comunicación entre Procesos

Esta unidad profundiza en **el nivel más bajo de comunicación** en los sistemas distribuidos: el intercambio de mensajes entre procesos. Se analizan las primitivas básicas, el paso de mensajes síncrono/asíncrono, los **sockets** (UDP y TCP), la representación y serialización de datos, la comunicación en grupo y la virtualización de redes (*overlay networks*).

---

## 1. Características de la Comunicación entre Procesos

El paso de mensajes entre un par de procesos se basa en dos operaciones fundamentales:



| Operación | Descripción |
| :--- | :--- |
| **`envía`** | El proceso emisor transmite un mensaje (una secuencia de bytes) a un destino. |
| **`recibe`** | El proceso receptor obtiene el mensaje enviado. |

A cada destino de mensajes se le asocia una **cola de mensajes**: los emisores producen mensajes que se añaden a la cola remota, y los receptores consumen mensajes de sus colas locales.

### Comunicación Síncrona vs Asíncrona
* **Síncrona:** Tanto `envía` como `recibe` son **operaciones bloqueantes**. El emisor se bloquea hasta que el receptor emite el correspondiente `recibe`, y el receptor se bloquea esperando el mensaje. Ambos procesos se sincronizan en cada mensaje.
* **Asíncrona:** La operación `envía` es **no bloqueante**: el emisor continúa apenas copia el mensaje a su búfer local, y la transmisión ocurre en paralelo. `recibe` permite variantes bloqueantes y no bloqueantes. En la variante no bloqueante, el receptor sigue su ejecución y los datos llegan a un búfer en segundo plano, debiendo ser notificado por separado mediante **encuesta** (*polling*) o **interrupción**.

> [!NOTE] En la práctica
> En sistemas actuales (y en Java en particular) se suele usar **`envía` no bloqueante** y **`recibe` bloqueante**. Como Java soporta múltiples hilos en un solo proceso, un `recibe` bloqueante solo bloquea un hilo, no a todo el proceso, lo que simplifica la sincronización del receptor.

### Destinos de los Mensajes
En los protocolos Internet, los mensajes se envían a direcciones formadas por el par:

$$( \text{Dirección\_Internet}, \ \text{Puerto\_local} )$$

---

## 2. Sockets

Un **socket** es la abstracción de punto final de comunicación que utilizan tanto UDP como TCP. Cada socket se identifica por la combinación de **dirección Internet + puerto local**. Los procesos pueden usar un mismo socket para enviar y recibir mensajes.

* **Lado servidor:** crea un socket y lo liga (bind) a un puerto de servidor conocido.
* **Lado cliente:** crea un socket ligado a cualquier puerto local libre.
* En UDP, cuando el receptor recibe un datagrama, este trae consigo la dirección y puerto del emisor, lo que permite responder.

---

## 3. Comunicación de Datagramas (UDP)

### Características
* Un datagrama enviado por UDP se transmite **"sin acuse de recibo" ni "reintentos"**: si algo falla, el mensaje puede no llegar.
* No ofrece garantías sobre el orden ni la duplicación de mensajes.

### Modelo de Fallo
* Fallos por **omisión** (mensajes perdidos).
* Mensajes **duplicados** o **desordenados**.
* Como el `recibe` puede bloquearse indefinidamente esperando un datagrama que nunca llega, se utilizan **tiempos límite de espera** (*timeouts*).

### Utilización
Resulta aceptable para aplicaciones tolerantes a pérdidas (por ejemplo, consultas simples, DNS o aplicaciones de tiempo real) donde sea preferible descartar datos viejos a esperar retransmisiones.

### API Java
* `DatagramPacket`: encapsula los datos enviados/recibidos.
* `DatagramSocket`: gestiona el socket de datagramas (envío y recepción).
* `InetAddress`: clase para representar direcciones Internet.

---

## 4. Comunicación de Streams (TCP)

### Características
TCP (originario de UNIX BSD 4.x) proporciona la abstracción de un **flujo de bytes (stream)**, ocultando detalles de la red como:
* El **tamaño de los mensajes** (la aplicación decide cuántos datos lee o escribe; es el flujo TCP quien agrupa los paquetes IP).
* Los mecanismos de **fiabilidad** (los datos se entregan completos y en orden, como si se leyera un archivo).

### Mecanismos Internos


| Problema | Solución de TCP |
| :--- | :--- |
| **Mensajes perdidos** | Esquema de **acuse de recibo** y **retransmisión** por *timeout*. |
| **Paquetes duplicados** | **Números de secuencia** que permiten detectar y eliminar duplicados. |
| **Datos corruptos** | **Sumas de comprobación** (*checksums*) que detectan y descartan paquetes corruptos. |
| **Desbordamiento del receptor** | **Control de flujo**: el escritor es bloqueado hasta que el lector consuma suficientes datos. |

### Modelo de Fallo
* TCP garantiza **validez**: usa *timeouts* y retransmisión para que los datos lleguen aunque se pierdan paquetes.
* Si las pérdidas superan un límite o la red está severamente congestionada, el software TCP declara la **conexión rota**, notificando al proceso que la usa.

### Utilización
Es la base de la mayoría de los servicios de Internet (web, correo, transferencia de archivos).

### API Java
* `ServerSocket`: en el servidor, escucha conexiones entrantes.
* `Socket`: en el cliente (y tras aceptar, en el servidor) para el intercambio de datos por streams de entrada y salida.

---

## 5. Representación Externa de Datos y Empaquetado

### El Problema
* En los programas en ejecución, la información se representa como **estructuras de datos** (objetos interconectados).
* En los mensajes, la información consiste en **secuencias de bytes** (no hay transmisión directa de objetos).

Antes de transmitir, las estructuras deben **aplanarse** (*marshalling* / serialización) a una secuencia de bytes, y al llegar al destino, deben **reconstruirse** (*unmarshalling*).

Además, no todos los computadores representan los datos de la misma forma:
* El **orden de bytes** de los enteros (endianness) puede diferir.
* La representación de **números en coma flotante** también difiere entre arquitecturas.

### Dos Métodos de Intercambio
1. **Formato convenido externo:** convertir los valores a un formato externo estándar antes de transmitirlos y convertirlos a la forma local al recibirlos.
2. **Formato del remitente:** transmitir los valores en el formato de quien los envía, junto a una indicación del formato usado, y que el receptor convierta si es necesario.

### Tecnologías de Empaquetado


| Tecnología | Descripción |
| :--- | :--- |
| **Representación común de datos CORBA (CDR)** | Representación externa de tipos primitivos y estructurados para argumentos y resultados de invocaciones remotas. Usable por gran variedad de lenguajes. |
| **Serialización de objetos Java** | Representación "aplanada" de cualquier objeto o árbol de objetos para su transmisión o almacenamiento en disco. De uso exclusivo de Java. |
| **XML (Extensible Markup Language)** | Formato basado en texto (auto-descriptivo) para la representación y el intercambio de datos entre sistemas heterogéneos. |

---

## 6. Comunicación en Grupo (Multidifusión IP)

* La **multidifusión IP** permite que un emisor transmita un **único paquete IP a un conjunto de computadores** que forman un grupo de multidifusión, sin conocer las identidades de los receptores individuales.
* En IPv4, los grupos se especifican con **direcciones de clase D** (primeros cuatro bits `1110`), en el rango reservado 224.0.0.1 a 224.0.0.255.
* La **pertenencia es dinámica**: un computador puede unirse o abandonar un grupo en cualquier momento.
* **Routers multidifusión:** reenvían los datagramas solo hacia redes con miembros del grupo. Para limitar la propagación se usa el campo **TTL** (*time to live*, número de routers que puede cruzar).

---

## 7. Virtualización de Red (Overlay Networks)

* La **virtualización de red** construye **redes virtuales** sobre una red existente (por ejemplo, Internet), donde cada red virtual se diseña y optimiza para soportar una aplicación distribuida particular (streaming multimedia, juegos en línea multijugador, etc.) **sin cambiar las características de la red subyacente**.
* Una **red de superposición (overlay)** es una red virtual compuesta de **nodos y enlaces virtuales** que se sitúa por encima de una red física (como IP) y ofrece algo que el mismo Internet no brinda:



| Beneficio | Descripción |
| :--- | :--- |
| **Servicio adaptado** | Distribución de contenido multimedia, mensajería, etc., ajustado a una clase de aplicación. |
| **Mayor eficiencia** | Por ejemplo, encaminamiento específico en redes ad hoc. |
| **Características adicionales** | Por ejemplo, comunicación *multicast* o segura. |

> [!EXAMPLE] Ejemplo real
> **Skype** es un ejemplo clásico de overlay network construido sobre Internet.

---

## Ver también (Enlaces de la Unidad)
* [[Unidad 1 - Caracterización de los Sistemas Distribuidos]]
* [[Unidad 2 - Modelos de Sistemas]]
* [[Unidad 4 - Objetos Distribuidos e Invocación]]
* [[Unidad 5 - Tiempo y Estados Globales]]