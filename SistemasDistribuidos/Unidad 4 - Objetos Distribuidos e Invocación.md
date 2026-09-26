# Unidad 4 - Objetos Distribuidos e Invocación

Esta unidad estudia los niveles **altos del middleware**: el protocolo petición-respuesta que sustenta la comunicación cliente/servidor, la **LLamada a Procedimiento Remoto (RPC)**, sus semánticas de invocación frente a fallos y la **Invocación a Métodos Remotos (RMI)** con su modelo de objetos distribuidos.

---

## 1. Protocolo Petición-Respuesta (*Request-Reply*)

Es el protocolo base para las interacciones típicas **cliente-servidor**.

* Normalmente la comunicación es **síncrona**: el cliente se bloquea hasta recibir la respuesta del servidor.
* Puede ser **fiable**: la respuesta del servidor actúa, en la práctica, como un *acuse de recibo* del cliente.
* Existe también una alternativa **asíncrona**, útil cuando los clientes pueden recuperar las respuestas más adelante.

### Primitivas del Protocolo
* **`doOperation(s, args)`:** invoca una operación remota en el servidor `s` con los argumentos dados (parámetros y tipo de operación). Devuelve la respuesta.
* **`getRequest()`:** el servidor espera/adquiere una petición entrante.
* **`sendReply(r, c)`:** el servidor envía el mensaje de respuesta `r` al cliente `c`.

Un mensaje de petición o respuesta transmite: el **tipo de mensaje**, el **identificador de petición**, la **referencia remota** (o identificador de procedimiento en RPC), el **identificador de método** y los **argumentos** (empaquetados).

### Modelo de Fallos (implementación sobre UDP)
* **Fallo por omisión:** el servidor no responde o el mensaje se pierde. Estrategia de *timeout* en `doOperation`:
  * Opción 1: devolver un indicador de fallo.
  * Opción 2: **reintentar** repetidamente hasta obtener respuesta.
* **Fallo bizantino:** mensajes duplicados o desordenados.
  * Opción 1: **descartar duplicados** mientras la operación esté en curso, usando el identificador de petición $id_{cliente} \# id_{peticion}$.
  * Opción 2: si la operación ya se realizó y es **idempotente**, se vuelve a ejecutar; si no lo es, se mantiene un **histórico** de resultados.

### Idempotencia
* Una operación es **idempotente** si ejecutarla varias veces produce el mismo efecto que ejecutarla una sola (por ejemplo, *leer* o *asignar una variable*).
* En retransmisiones, las operaciones **no idempotentes** (por ejemplo, *incrementar un contador*) requieren purgar duplicados o conservar un **historial** de respuestas para no reejecutarlas.

### Estilos de Protocolos RPC


| Protocolo | Descripción |
| :--- | :--- |
| **R (Petición)** | El procedimiento no devuelve valor ni requiere confirmación. El cliente no sabe si se ejecutó. |
| **RR (Petición-Respuesta)** | La respuesta del servidor confirma la ejecución de la petición. |
| **RRA (Petición-Respuesta-Confirmación)** | Intercambio de tres mensajes: petición, respuesta y confirmación de la respuesta. Ofrece mayor fiabilidad. |

### HTTP: un ejemplo de protocolo petición-respuesta
* Basado en el protocolo petición-respuesta, donde el **cliente** es el navegador y el **servidor** el sitio web.
* Los mensajes HTTP contienen: línea de petición/estado, cabeceras (*headers*) y cuerpo (*body*).
* Los **códigos HTTP** (2xx éxito, 3xx redirección, 4xx error del cliente, 5xx error del servidor) informan del resultado de cada petición.

---

## 2. Llamada a Procedimiento Remoto (RPC)

### Objetivo
Hacer que la programación en red se parezca lo más posible a la programación convencional, extendiendo la abstracción de **llamada a procedimiento** a entornos distribuidos y logrando un alto nivel de **transparencia de distribución**.

### Principios
* Un programa cliente llama a un procedimiento que reside en otro programa que se ejecuta en un servidor.
* Los servidores pueden ser a su vez clientes de otros servidores (cadenas de RPC).
* Cada servidor define en su **interfaz de servicio** los procedimientos invocables remotamente.
* RPC suele implementarse sobre un protocolo **petición-respuesta**.
* Los mensajes de petición/respuesta son los mismos que en RMI, **omitiendo el campo ReferenciaObjeto**.

### Componentes del Software de Soporte
* **Procedimiento de resguardo del cliente (*stub* cliente):** se comporta como un procedimiento local; en realidad empaqueta el identificador del procedimiento y los argumentos en un mensaje de petición y lo envía mediante el módulo de comunicación. Al llegar la respuesta, desempaqueta los resultados.
* **Distribuidor (*dispatcher*):** en el servidor, selecciona el procedimiento de resguardo adecuado según el identificador de procedimiento del mensaje.
* **Procedimiento de resguardo del servidor:** desempaqueta los argumentos, llama al procedimiento de servicio correspondiente y empaqueta el resultado.
* **Procedimiento de servicio:** implementa la lógica real del procedimiento de la interfaz.

A diferencia de RMI, en RPC **no se requieren módulos de referencia remota**, porque las llamadas a procedimientos no involucran objetos ni referencias a objetos.

### Interfaces y IDL
* Las **interfaces de servicio** definen los tipos de mensajes que se intercambian y sus resultados.
* Los **Lenguajes de Definición de Interfaces (IDL)** permiten especificar la interfaz de forma independiente del lenguaje de programación, de modo que el código necesario (stubs, etc.) pueda generarse para distintos lenguajes (por ejemplo, los servicios ya escritos en C++ o Java).

---

## 3. Semánticas de Invocación

Definen qué garantías ofrece la invocación remota cuando ocurren fallos de comunicación o de proceso.

### Medidas de Tolerancia a Fallos


| Medida | Función |
| :--- | :--- |
| **Reintento de la petición** | Retransmite el mensaje de petición hasta recibir respuesta o asumir que el servidor falló. |
| **Filtrado de duplicados** | Descarta peticiones duplicadas que llegan al servidor a causa de las retransmisiones. |
| **Retransmisión de resultados** | Mantiene un historial de respuestas para reenviar resultados perdidos **sin reejecutar** la operación en el servidor. |

### Semánticas Resultantes
* **"Pudiera ser" (*maybe*):** se ejecutó una vez o ninguna, y el invocante no puede saberlo. Ocurre cuando **no se aplica ninguna medida** de tolerancia.
* **"Al menos una vez" (*at-least-once*):** el invocante recibe un resultado, pero el método pudo ejecutarse **más de una vez** (por retransmisiones). Se alcanza con el reintento de peticiones. Puede sufrir fallos arbitrarios al reejecutar operaciones. Es la semántica de Sun RPC.
* **"Como máximo una vez" (*at-most-once*):** el invocante recibe un resultado (ejecutado exactamente una vez) o una excepción (ejecutado una vez o ninguna). Se logra aplicando **todas** las medidas de tolerancia. Es la semántica observada por **Java RMI** y **CORBA** (CORBA además permite "pudiera ser" para métodos que no devuelven resultados).

---

## 4. Invocación a Método Remoto (RMI)

### Concepto
RMI extiende el modelo de RPC al mundo de los **objetos distribuidos**: un objeto llamante puede invocar un método sobre un objeto situado en otro proceso, ocultando los detalles subyacentes al usuario.

* **Invocación de método remota:** entre objetos en diferentes procesos (o computadores).
* **Invocación de método local:** entre objetos del mismo proceso.

### El Modelo de Objetos Distribuidos
* **Objetos remotos:** objetos que pueden recibir invocaciones remotas. Todos los objetos pueden recibir invocaciones locales, pero solo los remotos tienen una **interfaz remota** que expone qué métodos pueden invocarse desde otros procesos.
* **Referencia a objeto remoto:** un identificador único válido a lo largo de todo el sistema distribuido, que permite invocar métodos sobre el objeto remoto. Puede pasarse como **argumento o resultado** de invocaciones remotas.
* **Interfaz remota:** la clase del objeto remoto implementa los métodos de su interfaz remota; solo los métodos de esa interfaz son invocables remotamente.
  * En **CORBA** se definen con **IDL**.
  * En **Java RMI**, las interfaces remotas extienden la interfaz marcadora `java.rmi.Remote`, y cada método debe declarar que puede lanzar una excepción remota.

### Implementación de RMI (Componentes del Middleware)
* **Módulo de comunicación:** implementa el protocolo petición-respuesta entre cliente y servidor, retransmitiendo mensajes y ofreciendo una semántica de invocación (por ejemplo, *como máximo una vez*). Solo usa tipo de mensaje, `idPeticion` y referencia remota del objeto.
* **Módulo de referencia remota:** traduce entre referencias locales y referencias a objetos remotos y mantiene una **tabla de objetos remotos** que guarda la correspondencia entre ambas para cada proceso.
* **Proxy:** hace transparente la invocación remota al cliente: se comporta como un objeto local, pero en lugar de ejecutar el método, dirige el mensaje al objeto remoto. Existe un proxy por cada objeto remoto referenciado.
* **Distribuidor (*dispatcher*):** recibe el mensaje de petición en el servidor y, usando el `idMetodo`, selecciona el método apropiado del esqueleto.
* **Esqueleto (*skeleton*):** por cada clase de objeto remoto, desempaqueta los argumentos del mensaje de petición, invoca el método correspondiente en el objeto remoto y empaqueta el resultado.

> [!NOTE] RPC vs RMI
> RPC usa **stubs de procedimiento** y un **distribuidor** sobre procedimientos de servicio, sin referencias a objetos. RMI utiliza **proxy**, **distribuidor** y **esqueleto**, y las invocaciones se dirigen a métodos de objetos mediante referencias a objetos remotos.

---

## 5. Aplicaciones y Ejemplos
* **Apache Kafka:** plataforma distribuida de mensajería basada en un modelo de registros (*logs*) distribuido, que ejemplifica servicios de alto nivel sobre protocolos de comunicación.
* **Servidores de aplicaciones JavaEE:** despliegan objetos distribuidos (EJBs) y exponen servicios que los clientes invocan de forma remota (práctica de laboratorio).

---

## Ver también (Enlaces de la Unidad)
* [[Unidad 1 - Caracterización de los Sistemas Distribuidos]]
* [[Unidad 2 - Modelos de Sistemas]]
* [[Unidad 3 - Comunicación entre Procesos]]
* [[Unidad 5 - Tiempo y Estados Globales]]