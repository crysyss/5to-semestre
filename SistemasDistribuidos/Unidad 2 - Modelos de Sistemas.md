# Unidad 2 - Modelos de Sistemas

Esta unidad se enfoca en la conceptualización de los sistemas distribuidos mediante tres tipos de modelos: **Físicos** (diseño del hardware), **Arquitectónicos** (organización lógica y patrones de componentes) y **Fundamentales** (abstracciones formales sobre interacción, fallos y seguridad).

---

## 1. Modelos Físicos

Un **Modelo Físico** es la representación explícita del hardware subyacente de un sistema distribuido, abstrayendo los detalles tecnológicos específicos de las redes y computadores. Se clasifican históricamente en tres generaciones:



| Generación | Periodo | Características Principales | Escala típica |
| :--- | :--- | :--- | :--- |
| **Sistemas Distribuidos Tempranos** | Décadas 1970/1980 | Surgimiento de redes de área local (LAN), específicamente Ethernet. Computadores de escritorio conectados en red local. | 10 a 100 nodos |
| **Sistemas a Escala de Internet** | Décadas 1990/2000 | Crecimiento explosivo de Internet. Conjunto de subredes heterogéneas interconectadas a nivel global. Alta heterogeneidad en hardware, redes y S.O. | Miles a millones de nodos |
| **Sistemas Contemporáneos** | Actualidad (2010+) | Surgimiento de Cloud Computing, computación móvil, ubicua y wearables. Conectividad masiva a través de múltiples tipos de red. | Miles de millones de nodos |

---

## 2. Modelos Arquitectónicos

La **arquitectura de un sistema** es su estructura interna en términos de componentes de software especificados de forma separada y la manera en que se relacionan y ubican en la red.

### Arquitectura de Software
* **Capas de servicio:** Estructuración de servicios de forma modular. Un servicio distribuido puede ser implementado por uno o más procesos servidores interactuando entre sí y con clientes.
* **Plataforma:** Nivel de hardware y software base (S.O. y librerías de red) que exponen interfaces de bajo nivel para comunicación y coordinación.
* **Middleware:** Capa de software intermedia cuyo propósito es ocultar la heterogeneidad y proporcionar un modelo de programación conveniente para las aplicaciones. Proporciona bloques útiles como invocación remota (RMI/RPC), comunicación de grupo (multicast), notificación de eventos y replicación de datos.

### Roles y Responsabilidades (Patrones de Diseño)

#### A. Cliente-Servidor
Es la arquitectura clásica e históricamente más importante. Los procesos clientes realizan peticiones a servidores individuales, los cuales procesan la solicitud y devuelven una respuesta.

#### B. Servicios proporcionados por múltiples servidores
Para mejorar escalabilidad y tolerancia a fallos, un único servicio puede ser provisto por varios procesos servidores que interactúan de forma interna (coordinándose) para mantener la consistencia de los datos (ejemplo: clústeres de bases de datos o motores de búsqueda).

#### C. Servidores Proxy y Cachés
* **Caché:** Almacén local de datos utilizados recientemente para acelerar accesos posteriores y reducir tráfico de red.
* **Proxy (Servidor Intermedio):** Actúa en representación de las máquinas cliente. Usualmente aloja un caché web compartido por múltiples clientes para optimizar el acceso a recursos externos e implementar políticas de seguridad corporativas.

#### D. Procesos de Igual a Igual (Peer-to-Peer - P2P)
Todos los procesos del sistema desempeñan tareas semejantes e interactúan de manera directa sin necesidad de coordinadores centralizados. Ofrece excelente escalabilidad y resistencia a fallos. Ejemplo: una aplicación de pizarra interactiva distribuida o redes de compartición de archivos.

### Variaciones de la Arquitectura Cliente-Servidor

* **Código Móvil:** El código se descarga de un servidor remoto y se ejecuta localmente en el cliente (ejemplo: Applets de Java ejecutándose en navegadores). Reduce el retardo de interacción pero requiere entornos locales seguros.
* **Agentes Móviles:** Programas autónomos (que contienen tanto el código ejecutable como su estado de datos) que viajan de un computador a otro en la red completando tareas intensivas. Ejemplo histórico: el "gusano" (*worm*) desarrollado en Xerox PARC para aprovechar CPUs inactivas en red. *Riesgo:* Pueden constituir amenazas críticas de seguridad para las máquinas anfitrionas.
* **Clientes Ligeros (*Thin Clients*):** Capa de aplicación local mínima que solo se encarga de renderizar la interfaz de usuario en ventanas y capturar entradas del usuario, delegando toda la computación pesada y el almacenamiento de datos al servidor remoto. Ejemplos: X Window System, VNC, escritorios virtuales.
* **Dispositivos Móviles y Enlace Espontáneo:** Integración ad-hoc y descubrimiento automático de dispositivos inalámbricos (smartphones, cámaras, laptops) al aproximarse físicamente (enlace espontáneo). Afronta problemas de *conectividad limitada* (desconexiones temporales al pasar por túneles, etc.).

---

## 3. Modelos Fundamentales

Los modelos fundamentales permiten razonar formalmente sobre el comportamiento de los sistemas distribuidos abstrayendo detalles de implementación. Se dividen en tres áreas:

### A. Modelo de Interacción

Abstrae la ejecución de los algoritmos distribuidos. El cómputo se realiza en procesos individuales que interactúan mediante el paso de mensajes a través de canales de comunicación.

#### Factores de Rendimiento en Canales de Red
1. **Latencia:** El retardo de tiempo desde que se inicia el envío de un mensaje en el emisor hasta que el receptor lo tiene disponible en su buffer local.
2. **Ancho de banda (*Bandwidth*):** Cantidad total de información (en bytes/segundo) que se puede transmitir por un canal en un intervalo dado.
3. **Fluctuación de retardo (*Jitter*):** Variabilidad del tiempo total que tardan en entregarse mensajes individuales consecutivos. Crucial en transmisiones en tiempo real.

#### Relojes y Desviación
Cada computador posee un oscilador físico interno que mantiene su propio reloj. La diferencia en la velocidad de oscilación física provoca que los relojes diverjan progresivamente de una referencia de tiempo estándar. Esta tasa de divergencia se conoce como **Clock Drift Rate** (Tasa de Desviación del Reloj).

#### Variantes del Modelo de Interacción



| Aspecto | Sistema Distribuido Síncrono | Sistema Distribuido Asíncrono |
| :--- | :--- | :--- |
| **Tiempo de Paso de Proceso** | Acotado (hay un límite superior e inferior conocido para cada instrucción). | No acotado (los procesos ejecutan a velocidades variables e impredecibles). |
| **Transmisión de Mensajes** | Acotado (el tiempo de envío del mensaje por la red tiene un límite superior conocido). | No acotado (un mensaje puede tardar un tiempo indefinidamente largo en llegar). |
| **Desviación del Reloj** | Tasa de desviación (*Clock Drift Rate*) acotada y conocida. | No acotada o arbitraria. |
| **Ejemplo real** | Redes de tiempo real industrial cerradas. | Internet (no presupone cotas de tiempo efectivas). |

#### Ordenamiento Lógico de Eventos (Lamport)
Debido a la inexistencia de relojes físicos globales perfectamente sincronizados, Leslie Lamport propuso ordenar eventos mediante una lógica causal llamada **Relación Ocurrido-Antes** (denotada por el símbolo $\to$).

Las reglas que definen la relación causal de Lamport son:
* Si dos eventos $a$ y $b$ ocurren dentro del mismo proceso y $a$ ocurre antes que $b$, entonces:
$$a \to b$$
* Si $a$ es el evento de envío de un mensaje por un proceso y $b$ es el evento de recepción del mismo mensaje en otro proceso, entonces:
$$a \to b$$
* Si existe un evento $c$ tal que $a \to b$ y $b \to c$, entonces por transitividad se cumple que:
$$a \to c$$
* Si para dos eventos cualesquiera $x$ e $y$ no se puede establecer causalidad (es decir, ni $x \to y$ ni $y \to x$), se dice que los eventos son **concurrentes** (denotado como $x \parallel y$).

---

### B. Modelo de Fallos

Define y clasifica de manera formal las formas en las que el sistema puede dejar de comportarse según su especificación.

#### 1. Fallos por Omisión
Un proceso o canal de comunicación falla al no realizar la acción esperada.

* **Fallos de Proceso (Crash):** El proceso se detiene de forma abrupta. En un modelo *Fail-Stop*, la caída de un proceso es detectable inmediatamente por otros componentes (normalmente mediante latidos o timeouts); en otros esquemas, puede pasar desapercibida.
* **Fallos de Canal (Pérdidas de mensajes):**
  * **Omisión de envío (*Send-omission*):** El mensaje no logra salir del buffer de salida del emisor hacia el canal físico.
  * **Omisión de recepción (*Receive-omission*):** El mensaje llega al receptor pero no logra registrarse en su buffer de entrada.
  * **Omisión de canal (*Channel-omission*):** El mensaje se extravía en tránsito por el medio físico de red.

#### 2. Fallos Arbitrarios (Bizantinos)
Representan el peor escenario posible de falla. Un proceso o canal actúa de manera arbitraria:
* Puede omitir pasos del algoritmo arbitrariamente.
* Puede ejecutar pasos de cómputo corruptos u erróneos de manera voluntaria o involuntaria.
* Puede enviar mensajes modificados, falsos o con contenido malicioso deliberado.

#### 3. Fallos de Temporización
Se aplican a sistemas síncronos y ocurren cuando se exceden los límites de tiempo acotados (ejemplo: un mensaje llega tarde y genera un timeout, o el reloj local tiene una desviación mayor a la tolerancia estipulada).

#### Fiabilidad en Comunicación Uno a Uno
Se define un canal de comunicación fiable mediante el cumplimiento estricto de dos propiedades:
* **Validez (*Validity*):** Cualquier mensaje que se deposite en el buffer de envío es eventualmente entregado al buffer de recepción de destino.
* **Integridad (*Integrity*):** El mensaje entregado al receptor es idéntico al enviado, no hay duplicaciones de paquetes y no se inventan mensajes espurios en tránsito.

---

### C. Modelo de Seguridad

Establece abstracciones para analizar amenazas y proteger los activos del sistema (procesos, canales y objetos).

#### El Enemigo (Adversario)
Se asume la presencia de un enemigo que tiene acceso completo a la infraestructura de red. Este adversario es capaz de:
* Interceptar o copiar cualquier mensaje en tránsito.
* Inyectar mensajes falsificados.
* Modificar el contenido de los mensajes originales.
* Eliminar mensajes de los canales.

#### Amenazas comunes:
1. **Suplantación de Identidad / Enmascaramiento (*Masquerading/Spoofing*):** Un proceso enemigo envía solicitudes simulando ser un cliente autorizado sin serlo.
2. **Reenvío de mensajes (*Replay Attacks*):** El adversario captura mensajes válidos (como tokens de autenticación) y los transmite posteriormente para engañar al receptor.
3. **Manipulación de mensajes (*Tampering / Man-in-the-middle*):** Intercepción y alteración maliciosa del contenido de los mensajes.
4. **Denegación de Servicio (DoS):** Inundación maliciosa de peticiones masivas al servidor para agotar sus recursos y bloquear el acceso a usuarios autorizados.

#### Canales Seguros
Para proteger la comunicación de las amenazas del enemigo, se construyen **Canales Seguros** sobre las redes existentes haciendo uso de criptografía y autenticación. Un canal seguro garantiza:
* **Confidencialidad:** Nadie excepto el emisor y el receptor autorizados puede leer los datos.
* **Integridad:** Se detecta cualquier alteración o manipulación de los datos en tránsito.
* **Autenticación:** Cada proceso tiene certeza de la identidad real del interlocutor.

---

## Ver también (Enlaces de la Unidad)
* [[Unidad 1 - Caracterización de los Sistemas Distribuidos]]
* [[Unidad 3 - Comunicación entre Procesos]]
* [[Unidad 4 - Objetos Distribuidos e Invocación]]
