---
aliases:
  - Circuitos de Corriente Continua
---
# Circuitos de Corriente Continua

## Índice General

- [[#Introducción]]
- [[#Corriente y Densidad de Corriente]]
    - [[#Corriente Eléctrica]]
    - [[#Tipos de Corriente]]
    - [[#Sentido de la Corriente]]
    - [[#Intensidad de Corriente]]
    - [[#Unidades de Medida]]
    - [[#Densidad de Corriente]]
- [[#Resistencia Eléctrica]]
    - [[#Definición de Resistencia]]
    - [[#Conductividad y Resistividad]]
    - [[#Resistividad y Temperatura]]
    - [[#Resistores y Código de Colores]]
- [[#Ley de Ohm]]
- [[#Potencia en Circuitos Eléctricos]]
- [[#Fuerza Electromotriz (fem) y Fuentes de Energía]]
    - [[#Definición de Fuerza Electromotriz]]
    - [[#Fuente Ideal vs. Fuente con Resistencia Interna]]
- [[#Circuitos Eléctricos y Asociación de Resistores]]
    - [[#Definición de Circuito de Corriente Continua]]
    - [[#Asociación en Serie]]
    - [[#Asociación en Paralelo]]
    - [[#Asociación Mixta]]
- [[#Leyes de Kirchhoff]]
    - [[#Conceptos Previos]]
    - [[#Primera Ley (Ley de los Nodos)]]
    - [[#Segunda Ley (Ley de las Mallas)]]
    - [[#Convención de Signos]]
- [[#Instrumentos de Medición Eléctrica]]
    - [[#Amperímetro]]
    - [[#Voltímetro]]
    - [[#Óhmetro]]
    - [[#Galvanómetro]]
- [[#Circuito RC]]
    - [[#Carga de un Capacitor]]
    - [[#Descarga de un Capacitor]]
- [[#Fuerza Electromotriz de una Pila]]
- [[#Potencial de Contacto y Fuerzas Electromotrices Térmicas]]

---

## Introducción

En esta unidad se estudian las **cargas en movimiento**. Cuando el desplazamiento de cargas eléctricas tiene lugar en una trayectoria de conducción cerrada, esta trayectoria recibe el nombre de **circuito eléctrico**. 

Los circuitos eléctricos son el medio principal para transportar energía de un lugar a otro en los sistemas modernos. A medida que las partículas cargadas se mueven a través del circuito, la energía potencial eléctrica (estudiada en [[Unidad II]]) se transfiere desde una fuente (como una batería o un generador) hacia un dispositivo de consumo, donde se almacena o se transforma en otras formas de energía (como calor, luz, o trabajo mecánico).

---

## Corriente y Densidad de Corriente

### Corriente Eléctrica
La **corriente eléctrica** es el movimiento o flujo libre de electrones a través de un conductor debido a la presencia de un campo eléctrico $\vec{E}$ (estudiado en [[Unidad I]]), el cual es originado por una diferencia de potencial $\Delta V$ ([[Unidad II]]). En términos sencillos, es el **movimiento ordenado de electrones**.
* **Sin campo eléctrico interno:** Los electrones se mueven al azar a velocidades elevadas, chocando continuamente con los iones de la red cristalina del metal. El desplazamiento neto a lo largo del conductor es nulo.
* **Con campo eléctrico interno:** El campo $\vec{E}$ ejerce una fuerza eléctrica $\vec{F} = q\vec{E}$ sobre los electrones, induciendo un movimiento ordenado (deriva) en sentido opuesto al campo eléctrico (debido a la carga negativa del electrón).

### Tipos de Corriente
* **Corriente Continua (C.C. o D.C.):** El movimiento de las cargas se realiza siempre en el **mismo sentido** y su magnitud no varía sustancialmente con el tiempo.
* **Corriente Alterna (C.A.):** Se caracteriza por una variación regular y cíclica de su magnitud y sentido en el tiempo, invirtiendo su polaridad periódicamente.

### Sentido de la Corriente
La deriva de cargas en movimiento genera colisiones con los iones del conductor, transfiriendo energía cinética en forma de vibraciones moleculares, lo que eleva la temperatura del conductor (calentamiento). Dependiendo del material, los portadores de carga pueden ser positivos o negativos. Por convención, existen dos sentidos para la corriente:

>  **Sentidos de la Corriente:**
> * **Sentido Real:** En un conductor sólido, los electrones (carga negativa) se desplazan desde el polo negativo (menor potencial) hacia el polo positivo (mayor potencial), oponiéndose a las líneas del campo eléctrico $\vec{E}$.
> * **Sentido Convencional:** Se define como el flujo de cargas positivas que se desplazarían desde el polo positivo (mayor potencial) hacia el polo negativo (menor potencial), en la misma dirección que el campo eléctrico $\vec{E}$.
> * **Nota de Curso:** En el estudio de circuitos se adopta siempre el **sentido convencional** de la corriente eléctrica.

### Intensidad de Corriente
La intensidad de corriente eléctrica $I$ a través de la sección transversal $A$ de un conductor es la cantidad de carga neta $dQ$ que fluye por unidad de tiempo $dt$:

$$I = \frac{dQ}{dt}$$

La corriente es una **magnitud escalar** (no vectorial), ya que la dirección del flujo está restringida por la geometría del conductor y no requiere vectores para su descripción espacial completa.

### Unidades de Medida
La unidad del Sistema Internacional (SI) para la intensidad de corriente es el **ampere** ($\text{A}$), definido como el paso de un coulomb por segundo:

$$1\text{ A} = 1\text{ C/s}$$

Submúltiplos más utilizados:

* $1\text{ mA} = 10^{-3}\text{ A}$ (miliampere)
* $1\ \mu\text{A} = 10^{-6}\text{ A}$ (microampere)
* $1\text{ nA} = 10^{-9}\text{ A}$ (nanoampere)
* $1\text{ pA} = 10^{-12}\text{ A}$ (picoampere)

### Densidad de Corriente
La **densidad de corriente** $J$ se define como la intensidad de corriente por unidad de área de la sección transversal del conductor:

$$J = \frac{I}{A} = n q v_d$$

Donde:
* $n$ es la densidad de portadores de carga (número de portadores móviles por unidad de volumen).
* $q$ es la carga eléctrica de cada portador.
* $v_d$ es la **velocidad de arrastre** o de deriva (rapidez con la que se desplazan los portadores a lo largo del conductor).

La densidad de corriente puede expresarse como una magnitud vectorial $\vec{J}$ que coincide con la dirección del movimiento de los portadores si su carga $q$ es positiva, o en sentido contrario si es negativa:

$$\vec{J} = n q \vec{v}_d$$

La unidad de medida de $J$ en el SI es el **ampere por metro cuadrado** ($\text{A/m}^2$).

---

## Resistencia Eléctrica

### Definición de Resistencia
La **resistencia eléctrica** $R$ es la medida de la oposición que ofrece un material conductor al paso de la corriente eléctrica, atenuando o disminuyendo el flujo de cargas libres. Su unidad en el SI es el **ohm** ($\Omega$):

$$1\ \Omega \equiv 1\text{ V/A}$$

### Conductividad y Resistividad
En muchos materiales, la densidad de corriente es proporcional al campo eléctrico aplicado:

$$\vec{J} = \sigma \vec{E}$$

Donde la constante de proporcionalidad $\sigma$ es la **conductividad** del material. Los materiales que obedecen esta relación lineal se denominan **materiales óhmicos**.

La inversa de la conductividad es la **resistividad** $\rho$:

$$\rho = \frac{1}{\sigma} = \frac{E}{J}$$

La resistividad $\rho$ es una propiedad característica intrínseca de cada material que mide su oposición al paso de la corriente y se expresa en **ohmios-metro** ($\Omega \cdot \text{m}$).

Para un conductor cilíndrico uniforme de longitud $l$ y área de sección transversal $A$, la resistencia eléctrica total $R$ se calcula como:

$$R = \rho \frac{l}{A}$$

De esta ecuación se deduce que:
* La resistencia es directamente proporcional a la longitud $l$ del conductor.
* La resistencia es inversamente proporcional al área transversal $A$.

### Resistividad y Temperatura
La resistividad de un conductor metálico por lo general se incrementa al aumentar la temperatura, debido al mayor número de colisiones de los electrones con los átomos que vibran más vigorosamente. Para rangos de temperatura moderados, la variación es aproximadamente lineal:

$$\rho(T) = \rho_0 [1 + \alpha(T - T_0)]$$

Dado que la resistencia $R$ es proporcional a $\rho$, esta variación térmica también se manifiesta directamente en la resistencia del dispositivo conductor:

$$R(T) = R_0 [1 + \alpha(T - T_0)]$$

Donde:
* $\rho_0$ y $R_0$ son la resistividad y resistencia a la temperatura de referencia $T_0$ (normalmente $0\ ^\circ\text{C}$ o $20\ ^\circ\text{C}$).
* $\alpha$ es el **coeficiente térmico de resistividad** característico del material (en $^\circ\text{C}^{-1}$ o $\text{K}^{-1}$).

### Resistores y Código de Colores
Los **resistores** son componentes electrónicos diseñados específicamente para introducir un valor conocido de resistencia en un circuito. Para identificar su valor nominal y tolerancia, se utiliza un sistema estándar de bandas de colores:

| Color | 1° Dígito | 2° Dígito | Multiplicador | Tolerancia |
| :--- | :---: | :---: | :---: | :---: |
| Negro | 0 | 0 | $\times 10^0$ | — |
| Marrón | 1 | 1 | $\times 10^1$ | $\pm 1\%$ |
| Rojo | 2 | 2 | $\times 10^2$ | $\pm 2\%$ |
| Naranja | 3 | 3 | $\times 10^3$ | — |
| Amarillo | 4 | 4 | $\times 10^4$ | — |
| Verde | 5 | 5 | $\times 10^5$ | $\pm 0.5\%$ |
| Azul | 6 | 6 | $\times 10^6$ | $\pm 0.25\%$ |
| Violeta | 7 | 7 | $\times 10^7$ | $\pm 0.1\%$ |
| Gris | 8 | 8 | $\times 10^8$ | $\pm 0.05\%$ |
| Blanco | 9 | 9 | $\times 10^9$ | — |
| Dorado | — | — | $\times 0.1$ | $\pm 5\%$ |
| Plateado | — | — | $\times 0.01$ | $\pm 10\%$ |

---

## Ley de Ohm

La **Ley de Ohm** es una relación empírica válida para ciertos materiales (conductores metálicos en su mayoría) que establece que la resistividad $\rho$ es constante e independiente de la magnitud del campo eléctrico $\vec{E}$ que produce la corriente:

$$\vec{E} = \rho \vec{J}$$

A nivel práctico y macroscópico, para un circuito o componente con resistencia constante, se formula como la proporcionalidad directa entre la diferencia de potencial $\Delta V$ aplicada a sus extremos y la intensidad de corriente $I$ resultante:

$$\Delta V = I \cdot R$$

* **Materiales Óhmicos:** Presentan un comportamiento lineal. En un gráfico de $I$ frente a $V$, la curva es una línea recta que pasa por el origen, donde la pendiente es igual a la **conductancia** ($1/R$).
* **Materiales No Óhmicos:** La relación entre $I$ y $V$ no es lineal (su resistencia varía según la tensión o el sentido de la corriente, como ocurre en diodos, transistores o semiconductores).

---

## Potencia en Circuitos Eléctricos

Cuando una carga eléctrica $dQ$ se desplaza a través de un elemento de circuito sometido a una diferencia de potencial $\Delta V$, el sistema experimenta una variación en su energía potencial eléctrica. La rapidez con la que se transfiere o disipa esta energía se define como **potencia eléctrica** ($P$):

$$P = \frac{dU}{dt} = \frac{dq}{dt} \Delta V = I \cdot \Delta V$$

Para elementos puramente resistivos que obedecen la Ley de Ohm, la potencia disipada (en forma de calor por el **Efecto Joule**) puede expresarse también como:

$$P = I^2 \cdot R = \frac{\Delta V^2}{R}$$

La unidad de la potencia en el SI es el **watt** ($\text{W}$), donde $1\text{ W} = 1\text{ J/s}$.

---

## Fuerza Electromotriz (fem) y Fuentes de Energía

### Definición de Fuerza Electromotriz
La **fuerza electromotriz (fem)**, designada como $\varepsilon$, es la medida del trabajo o la energía por unidad de carga que realiza un dispositivo (generador, pila, batería) para elevar el potencial eléctrico de las cargas de un terminal de menor potencial a uno de mayor potencial.

$$\varepsilon = \frac{W}{q}$$

Aunque contiene la palabra "fuerza", la fem no representa una fuerza mecánica, sino una diferencia de potencial máxima medida en **volts** ($\text{V}$).

### Fuente Ideal vs. Fuente con Resistencia Interna
* **Fuente de fem Ideal:** Mantiene una diferencia de potencial constante entre sus terminales igual a $\varepsilon$, independientemente de la corriente $I$ que fluya por ella.
* **Fuente de fem Real:** Los materiales internos de la fuente ofrecen una cierta **resistencia interna** $r$. Al circular corriente, ocurre una caída de potencial interna igual a $I \cdot r$. Por lo tanto, la diferencia de potencial real entre las terminales de la fuente (voltaje terminal $V_{ab}$) es:

$$\Delta V = V_{ab} = \varepsilon - I \cdot r$$

Cuando el circuito se encuentra abierto ($I = 0$), el voltaje terminal iguala exactamente a la fuerza electromotriz ($\Delta V = \varepsilon$).

---

## Circuitos Eléctricos y Asociación de Resistores

### Definición de Circuito de Corriente Continua
Un circuito de corriente continua es un sistema cerrado de conductores por el cual circula una corriente eléctrica cuyo sentido de flujo no varía con el tiempo. El análisis de redes eléctricas complejas consiste en reducir conjuntos de resistores conectados a un único resistor con una **resistencia equivalente** ($R_{\text{eq}}$) que demande la misma corriente total ante la misma tensión aplicada.

### Asociación en Serie
Los resistores se conectan secuencialmente uno detrás de otro de modo que existe un único camino para la corriente.

>  **Características de la Asociación en Serie:**
> 1. **Intensidad de Corriente:** Es la misma a través de cada resistor:
>    $$I = I_1 = I_2 = \dots = I_n$$
> 2. **Diferencia de Potencial:** La tensión total suministrada es la suma de las caídas de tensión en cada resistor:
>    $$V = V_1 + V_2 + \dots + V_n$$
> 3. **Resistencia Equivalente:** Es la suma aritmética de cada una de las resistencias individuales:
>    $$R_{\text{eq}} = R_1 + R_2 + \dots + R_n$$
> * **Propiedad:** La resistencia equivalente de una asociación en serie siempre es **mayor** que cualquiera de las resistencias individuales del conjunto.

### Asociación en Paralelo
Los terminales de entrada de todos los resistores se conectan a un punto común, y los de salida a otro punto común, de modo que la corriente se bifurca en múltiples trayectorias.

>  **Características de la Asociación en Paralelo:**
> 1. **Diferencia de Potencial:** La tensión es la misma en todos los componentes:
>    $$\Delta V = \Delta V_1 = \Delta V_2 = \dots = \Delta V_n$$
> 2. **Intensidad de Corriente:** La corriente total de la línea es igual a la suma de las corrientes ramificadas:
>    $$I = I_1 + I_2 + \dots + I_n$$
> 3. **Resistencia Equivalente:** La recíproca de la resistencia equivalente es igual a la suma de las recíprocas de cada resistencia:
>    $$\frac{1}{R_{\text{eq}}} = \frac{1}{R_1} + \frac{1}{R_2} + \dots + \frac{1}{R_n}$$
> * **Propiedad:** La resistencia equivalente en paralelo siempre es **menor** que la menor de las resistencias individuales del conjunto.

### Asociación Mixta
Consiste en la combinación de agrupaciones en serie y paralelo dentro de un mismo circuito. Su resolución se realiza por etapas, simplificando progresivamente bloques puramente en serie o en paralelo hasta obtener la resistencia equivalente total.

---

## Leyes de Kirchhoff

Para el análisis de circuitos complejos de múltiples mallas y nodos que no pueden reducirse directamente por combinaciones de serie y paralelo, se emplean las dos **Leyes de Kirchhoff**:

### Conceptos Previos
* **Nodo (o nudo):** Punto de un circuito donde se conectan tres o más conductores.
* **Malla (o espira):** Cualquier trayectoria conductora cerrada dentro del circuito.

### Primera Ley (Ley de los Nodos)
Se fundamenta en el principio físico de la **conservación de la carga eléctrica** (la carga no puede crearse ni destruirse, ni acumularse en un nodo):

$$\sum I = 0 \quad \Rightarrow \quad \sum I_{\text{entran}} = \sum I_{\text{salen}}$$

La suma algebraica de todas las corrientes que concurren en un nodo es igual a cero.

### Segunda Ley (Ley de las Mallas)
Se fundamenta en el principio de la **conservación de la energía**: al recorrer una trayectoria cerrada completa (malla), el cambio neto en la energía potencial de una carga de prueba al regresar al punto de partida debe ser cero:

$$\sum V = 0$$

La suma algebraica de las diferencias de potencial eléctrico en cualquier malla cerrada de un circuito debe ser igual a cero.

### Convención de Signos
Para aplicar correctamente la ley de mallas, se debe elegir un sentido de recorrido arbitrario y seguir la siguiente convención:

* **Resistores:**
  * Si se atraviesa el resistor en el **mismo sentido** de la corriente asignada: $\Delta V = -I \cdot R$ (caída de potencial).
  * Si se atraviesa el resistor en el **sentido contrario** de la corriente asignada: $\Delta V = +I \cdot R$ (elevación de potencial).
* **Fuentes de fem ($\varepsilon$):**
  * Si se recorre la fuente de **negativo a positivo** (en dirección de la fem): $\Delta V = +\varepsilon$.
  * Si se recorre la fuente de **positivo a negativo** (en contra de la fem): $\Delta V = -\varepsilon$.

---

## Instrumentos de Medición Eléctrica

### Amperímetro
* **Función:** Mide la intensidad de corriente eléctrica que circula por una rama del circuito.
* **Conexión:** Se debe conectar en **serie** con el elemento cuya corriente se desea medir (para que la corriente pase a través de él).
* **Condición Ideal:** Su resistencia interna debe ser **cero** ($R_i \to 0$) para no alterar la corriente original del circuito.

### Voltímetro
* **Función:** Mide la diferencia de potencial (tensión) entre dos puntos del circuito.
* **Conexión:** Se debe conectar en **paralelo** con los puntos bajo análisis.
* **Condición Ideal:** Su resistencia interna debe tender a **infinito** ($R_i \to \infty$) para que no desvíe corriente del circuito principal.

### Óhmetro
* **Función:** Mide el valor de la resistencia eléctrica de un componente aislado.
* **Conexión:** Se conecta directamente a las terminales del resistor (este debe estar completamente desconectado de cualquier fuente de energía externa). Consiste internamente en un medidor analógico o digital, un resistor patrón y una fuente de fem interna en serie.

### Galvanómetro
* Es un instrumento de medición analógico altamente sensible diseñado para detectar y medir corrientes de muy baja intensidad. Constituye el elemento activo principal en la construcción de amperímetros, voltímetros y óhmetros analógicos clásicos de bobina móvil.

---

## Circuito RC

Un **circuito RC** es un circuito eléctrico compuesto por la combinación en serie de una resistencia $R$ y una capacitancia $C$ (las propiedades físicas de los capacitores se describen detalladamente en la sección de [[Unidad II#Capacitancia y Capacitores]]). En estos circuitos, la corriente eléctrica y la carga eléctrica varían en función del tiempo.

### Carga de un Capacitor
Al cerrar el interruptor conectando la fuente de fem $\varepsilon$, el capacitor comienza a acumular carga eléctrica en sus placas. Aplicando la Ley de Mallas de Kirchhoff al circuito:

$$\varepsilon - \frac{q}{C} - I \cdot R = 0 \quad \Rightarrow \quad \varepsilon - \frac{q}{C} = R \frac{dq}{dt}$$

Resolviendo esta ecuación diferencial con la condición inicial $q(0) = 0$, se obtienen las expresiones de carga $q(t)$ y corriente $i(t)$ en función del tiempo:

**Carga del capacitor:**
$$q(t) = C\varepsilon \left(1 - e^{-\frac{t}{RC}}\right) = Q_f \left(1 - e^{-\frac{t}{\tau}}\right)$$

**Corriente en el circuito:**
$$i(t) = \frac{\varepsilon}{R} e^{-\frac{t}{RC}} = I_0 e^{-\frac{t}{\tau}}$$

Donde:
* $Q_f = C\varepsilon$ es la carga final máxima del capacitor en estado estacionario.
* $I_0 = \frac{\varepsilon}{R}$ es la corriente inicial máxima en el instante $t = 0$.
* $\tau = RC$ es la **constante de tiempo** del circuito RC, medida en segundos ($\text{s}$). Representa el tiempo requerido para que el capacitor alcance aproximadamente el $63.2\%$ de su carga máxima total, o para que la corriente disminuya hasta el $36.8\%$ de su valor inicial.

### Descarga de un Capacitor
Si un capacitor inicialmente cargado con una carga $Q_0$ se desconecta de la fuente de alimentación y se cierra sobre una resistencia $R$, este comienza a liberar la energía almacenada. Aplicando la Ley de Mallas de Kirchhoff:

$$-\frac{q}{C} - I \cdot R = 0 \quad \Rightarrow \quad -\frac{q}{C} = R \frac{dq}{dt}$$

Resolviendo la ecuación diferencial se obtienen las expresiones para la descarga:

**Carga del capacitor:**
$$q(t) = Q_0 e^{-\frac{t}{RC}} = Q_0 e^{-\frac{t}{\tau}}$$

**Corriente en el circuito:**
$$i(t) = \frac{dq}{dt} = -\frac{Q_0}{RC} e^{-\frac{t}{RC}} = -I_0 e^{-\frac{t}{\tau}}$$

El signo negativo en la corriente indica que el flujo de portadores de carga durante el proceso de descarga se realiza en sentido opuesto al de carga del capacitor. Ambos decaen asintóticamente hacia cero.

---

## Fuerza Electromotriz de una Pila

Las pilas o baterías de acumuladores representan fuentes de fem autónomas portátiles. Generan energía potencial eléctrica mediante transformaciones y reacciones químicas internas electroquímicas de óxido-reducción (redox):
* **Ánodo (polo negativo):** Ocurre el proceso de oxidación (pérdida de electrones).
* **Cátodo (polo positivo):** Ocurre el proceso de reducción (ganancia de electrones).
* **Electrolito:** Solución conductora iónica que permite el libre transporte interno de los iones para cerrar el circuito químico. El trabajo requerido por el agente químico para desplazar los electrones internamente entre ánodo y cátodo define el potencial de la pila.

---

## Potencial de Contacto y Fuerzas Electromotrices Térmicas

* **Potencial de Contacto:** Es la diferencia de potencial eléctrico espontánea que se establece en la interfase de contacto físico entre dos conductores de naturaleza química o física distinta, incluso en ausencia de corrientes eléctricas aplicadas. Se produce debido a la diferencia en las funciones de trabajo y energías de Fermi de los metales, compensándose mutuamente en circuitos cerrados isotérmicos para no disipar energía neta espontánea.
* **Fuerzas Electromotrices Térmicas:** Cuando se mantiene una diferencia de temperatura entre las uniones de dos metales distintos en contacto, se induce una f.e.m. termodinámica neta observable. Este fenómeno físico (conocido como el **Efecto Seebeck**) permite convertir energía térmica directamente en energía eléctrica y es el principio fundamental de funcionamiento de los termopares empleados para sensores de temperatura industriales de alta precisión.
