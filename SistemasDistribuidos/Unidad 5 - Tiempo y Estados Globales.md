# Unidad 5 - Tiempo y Estados Globales

Esta unidad aborda el problema del **tiempo y la coordinación** en sistemas distribuidos: cómo ordenar eventos sin un reloj global, cómo sincronizar los relojes físicos, cómo capturar un estado global consistente del sistema y cómo evaluar predicados para depuración distribuida.

---

## 1. Introducción: Relojes, Eventos y Estados de Proceso

* Un sistema distribuido consiste en una colección $\Omega$ de $N$ procesos $p_i$ ($i = 1, 2, \dots, N$) que **no comparten memoria** (cada uno se ejecuta en su propio procesador).
* Cada proceso $p_i$ tiene un **estado** $s_i$ que se transforma conforme se ejecuta: incluye los valores de sus variables y de los objetos de su entorno (por ejemplo, archivos).
* Cada acción de un proceso (enviar/recibir un mensaje o transformar su estado) es un **evento**.

### Historia y Orden Local
* La **historia** del proceso $p_i$ es la serie ordenada de eventos que ocurren en él:
$$historia(p_i) = h_i = \langle e_i^0, e_i^1, e_i^2, \dots \rangle$$
* Dentro de un mismo proceso, los eventos tienen un **orden único** (la relación $\to_i$): $e \to_i e'$ si y solo si $e$ ocurre antes que $e'$ en $p_i$.

### Relojes Físicos
* Cada computador posee un reloj de hardware que cuenta las **oscilaciones de un cristal** con cierta frecuencia, y un reloj de software que lo escala y compensa:
$$C_i(t) = \alpha H_i(t) + \beta$$
que mide aproximadamente el tiempo físico real $t$ para el proceso $p_i$.
* Los relojes no están en perfecto acuerdo:
  * **Sesgo (*skew*):** diferencia instantánea entre las lecturas de dos relojes.
  * **Deriva (*drift*):** cuentan el tiempo a ritmos distintos y por tanto divergen.

### Ritmo de Deriva y Referencias de Tiempo
* El **ritmo de deriva** es el cambio de compensación por unidad de tiempo, normalmente expresado en **partes por millón (ppm)**.
  * Un cristal de cuarzo típico: ~$10^{-6}$ s/s (1 segundo por cada millón de segundos ≈ 11,6 días).
  * Cristales de alta precisión: $10^{-7}$ o $10^{-8}$.
* **Relojes atómicos:** los más precisos, con deriva ~$10^{-13}$; su salida define el **Tiempo Atómico Internacional (TAI)**.
* **UTC (Tiempo Universal Coordinado):** estándar internacional basado en el tiempo atómico, al que ocasionalmente se le inserta o elimina un **segundo intercalar** para mantenerse en sintonía con el tiempo astronómico. Se difunde desde estaciones de radio terrestres y satélites (ej. WWV).

---

## 2. Sincronización de Relojes Físicos

Para conocer el instante en que ocurren los eventos es necesario sincronizar los relojes de los procesos.

### Tipos de Sincronización

| Tipo | Fórmula | Descripción |
| :--- | :--- | :--- |
| **Externa** | $\lvert S_i(t) - C_i(t) \rvert < D$ | Los relojes se sincronizan con una fuente externa autorizada $S_i$ dentro de un límite conocido $D$. |
| **Interna** | $\lvert C_i(t) - C_j(t) \rvert < D$ | No hay fuente externa; los procesos se sincronizan entre sí con una precisión conocida. |

* **Monotonicidad:** un reloj nunca debe retroceder, es decir, si $t' > t$ entonces $C(t') > C(t)$.
* En un **sistema síncrono** se conocen los límites (mínimo-máximo) de deriva de reloj, retardo de mensajes y tiempo de ejecución de cada paso de un proceso; el **sesgo** entre relojes queda acotado.

### Método de Cristian
* Utiliza un **servidor de tiempo** conectado a una fuente de UTC para sincronizar externamente a los clientes.
* El proceso $p$ envía una solicitud y registra el **tiempo total de ida y vuelta** $T_{round}$.
* Estimación de ajuste (asumiendo que $T_{round}$ se reparte mitad antes y mitad después de que el servidor ponga su marca de tiempo):

$$t_p = t_{server} + \frac{T_{round}}{2}$$

* Es un método **probabilístico**: funciona si los tiempos de ida y vuelta son suficientemente cortos comparados con la precisión requerida.

### Algoritmo de Berkeley
* Para **intranets**, cuando **no existe un servidor de tiempo externo**.
* Un nodo es elegido **maestro (*master*)** y los demás son **esclavos (*slaves*)**. El maestro consulta periódicamente el tiempo de cada esclavo, calcula un promedio y les indica el ajuste que deben aplicar.

### Protocolo de Tiempo de Red (NTP)
* Extiende la sincronización a **Internet**. Objetivos: sincronizar clientes de toda la red a UTC, ser **fiable** ante largas pérdidas de conectividad, compensar la deriva y **proteger el servicio de interferencias** maliciosas o accidentales.
* Organización en una **jerarquía lógica** denominada *subred de sincronización*, con niveles llamados **estratos**:
  * **Estrato 1:** servidores primarios (en la raíz).
  * **Estrato 2:** servidores secundarios sincronizados con los primarios.
  * **Estrato 3, 4, …:** sincronizados con el estrato superior; las hojas se ejecutan en las estaciones de trabajo de los usuarios.
* **Modos de sincronización entre servidores:**
  * **Multidifusión:** para LANs de alta velocidad; el servidor reparte el tiempo periódicamente.
  * **Llamada a procedimiento:** similar al método de Cristian; el servidor responde con su marca de tiempo.
  * **Simétrico:** entre servidores NTP de los estratos altos, como respaldo cuando no pueden alcanzar el servidor externo.
* NTP entrega los mensajes de forma **no fiable**, usando el protocolo de transporte **UDP**.

---

## 3. Tiempo Lógico y Relojes Lógicos

Como no es posible sincronizar perfectamente los relojes físicos de todo el sistema, **no se puede usar el tiempo físico para ordenar eventos arbitrarios** que ocurren en procesos diferentes.

### Relación "Sucedió Antes" (Lamport)
Se define una relación de ordenamiento lógico $\to$ entre eventos:
* Si $a$ y $b$ ocurren en el mismo proceso y $a$ precede a $b$: $a \to b$.
* Si $a$ es el envío de un mensaje y $b$ la recepción de ese mensaje: $a \to b$.
* La relación es **transitiva**: si $a \to b$ y $b \to c$, entonces $a \to c$.
* Si entre dos eventos no existe causalidad en ninguna dirección, se dice que son **concurrentes** ($a \parallel b$).

### Relojes Lógicos de Lamport
Un reloj lógico es un **contador de software que se incrementa monótonamente**; sus valores no guardan relación con ningún reloj físico. Cada proceso $p_i$ mantiene su reloj lógico $L_i$ y asigna marcas de tiempo $L_i(e)$ a sus eventos.

**Reglas de actualización:**
* **RL1:** $L_i$ se incrementa antes de emitir cada evento en $p_i$: $L_i = L_i + 1$.
* **RL2:**
  * (a) Al enviar un mensaje $m$, este lleva consigo el valor $t = L_i$.
  * (b) Al recibir $(m, t)$, el proceso $p_j$ actualiza $L_j = \max(L_j, t)$ y luego aplica RL1 antes de marcar el evento `recibe(m)`.

**Propiedades:**
* Correctitud: $b \to c \implies L(b) < L(c)$.
* Pero el recíproco **no** se cumple: si $L(e) < L(e')$ **no** se puede concluir que $e \to e'$.

### Relojes Vectoriales (Mattern, Fidge)
Para superar la deficiencia de los relojes de Lamport, cada proceso mantiene un **vector de $N$ enteros** $V_i$ (un reloj vectorial), donde $N$ es el número de procesos; $V_i[j]$ estima cuántos eventos del proceso $p_j$ han ocurrido hasta el momento.

**Reglas de actualización:**
* Antes de un evento local, $V_i[i] = V_i[i] + 1$.
* Al enviar el mensaje $m$, se adjunta el vector $V_i$ completo.
* Al recibir $(m, V_t)$, para cada $k$: $V_i[k] = \max(V_i[k], V_t[k])$, y luego $V_i[i] = V_i[i] + 1$ antes de marcar la recepción.

**Propiedad fundamental:** ahora sí es posible la equivalencia completa:
$$e \to e' \iff V(e) < V(e')$$
Y **los eventos concurrentes** son aquellos cuyos vectores no son comparables (por ejemplo, $V(e) \le V(c)$ y $V(c) \le V(e)$ a la vez).

---

## 4. Estados Globales

### Motivación (Aplicaciones)
* **Compactación automática de memoria:** decidir si un objeto es **desechable** (no hay más referencias a él en ningún proceso ni en mensajes en tránsito), pudiendo entonces reclamar su memoria.
* **Detección distribuida de bloqueos indefinidos (*deadlock*):** ocurre cuando un conjunto de procesos se espera mutuamente formando un **ciclo** en el grafo "espera por"; el sistema nunca progresará.
* **Detección de terminación distribuida:** saber cuándo un algoritmo distribuido ha terminado. Un proceso **pasivo** (sin actividad propia, pero listo para responder) no implica que el algoritmo haya finalizado, pues pueden existir mensajes en tránsito entre procesos.

### Cortes Consistentes
* Sin un tiempo global, **no se puede capturar el estado de todos los procesos en un mismo instante**.
* Un **corte** divide la historia de cada proceso en "antes del corte" y "después del corte".
* Un **corte consistente** es aquel cuya frontera incluye, junto con cada evento, **todos los eventos que sucedieron antes de él**.
* El conjunto de estados locales que corresponde a un corte consistente forma un **estado global consistente**. El sistema se modela como una secuencia de transiciones entre estados globales consistentes:
$$S_0 \to S_1 \to S_2 \to \dots$$

### Algoritmo de Instantánea de Chandy y Lamport
Registra el **estado de los procesos y de los canales** (una *instantánea*) tal que, aunque los estados registrados de cada proceso nunca hayan coexistido exactamente en el tiempo, el **estado global resultante sea consistente**.

**Supuestos:**
* No fallan canales ni procesos; la comunicación es fiable (cada mensaje llega intacto exactamente una vez).
* Los canales son **unidireccionales** y entregan mensajes en **orden FIFO**.
* El grafo de procesos y canales está **fuertemente conectado**.
* Cualquier proceso puede iniciar la instantánea en cualquier instante.
* Los procesos **siguen ejecutándose** normalmente durante la captura.

**Reglas del algoritmo (basado en un mensaje especial `M`, el marcador):**
* **Regla de envío del marcador:** después de registrar su estado, el proceso envía un marcador por **cada canal de salida**, antes de enviar cualquier otro mensaje.
* **Regla de recepción del marcador:** al recibir un marcador por el canal $c$:
  * Si aún **no** ha registrado su estado: lo registra ahora, registra el estado de $c$ como **conjunto vacío** y comienza a registrar los mensajes de los demás canales entrantes.
  * Si **ya** registró su estado: registra el estado de $c$ como el **conjunto de mensajes recibidos por $c$ desde que guardó su estado**.

> [!NOTE] Resultado
> El algoritmo registra los estados **localmente** en cada proceso; no recolecta el estado global en un único sitio. El resultado es siempre un **estado global consistente**.

---

## 5. Depuración Distribuida

### Predicados de Estado Global
La ejecución del sistema se caracteriza por las transiciones entre estados globales consistentes $S_0 \to S_1 \to \dots \to S_n$. Un **predicado de estado global** es una función:

$$\{ \text{conjunto de estados globales} \} \to \{ V, F \}$$

Determinar una condición del sistema equivale a **evaluar su predicado**.

### Características de los Predicados

| Propiedad | Significado |
| :--- | :--- |
| **Estabilidad** | El valor del predicado **no varía** con los nuevos sucesos (por ejemplo, interbloqueo o terminación). |
| **Seguridad** | El predicado es **falso** para todo estado alcanzable desde $S_0$ (deseable para errores). |
| **Vitalidad** | El predicado es **verdadero** para algún estado alcanzable desde $S_0$ (deseable para situaciones necesarias). |

### Red de Estados Globales
Se puede representar el espacio de los estados globales como una **red**, donde el estado $S_{ij}$ es el estado global después de $i$ eventos en el proceso 1 y $j$ eventos en el proceso 2.

### Evaluación Instantánea de Predicados
* **Posiblemente $\phi$:** existe al menos un estado global consistente donde el predicado es verdadero.
* **Sin duda alguna $\phi$:** el predicado es verdadero en **todos** los estados globales consistentes alcanzables.

Existen algoritmos específicos para evaluar "posiblemente $\phi$" y "sin duda $\phi$", que se apoyan en la estructura de la red de estados globales consistentes.

---

## Ver también (Enlaces de la Unidad)
* [[Unidad 1 - Caracterización de los Sistemas Distribuidos]]
* [[Unidad 2 - Modelos de Sistemas]]
* [[Unidad 3 - Comunicación entre Procesos]]
* [[Unidad 4 - Objetos Distribuidos e Invocación]]