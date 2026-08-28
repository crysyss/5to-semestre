---
aliases:
  - Potencial Eléctrico y Capacitancia
---
# Potencial Eléctrico y Capacitancia

## Índice General

- [[#Trabajo y Energía en Campos Eléctricos]]
    - [[#Fuerza Conservativa y Trabajo Eléctrico]]
    - [[#Energía Potencial Eléctrica]]
- [[#Potencial Eléctrico y Diferencia de Potencial]]
    - [[#Definición de Potencial Eléctrico]]
    - [[#Diferencia de Potencial y Movimiento de Cargas]]
    - [[#Superficies Equipotenciales]]
    - [[#Potencial debido a Distribuciones Continuas]]
    - [[#Relación entre Potencial y Campo Eléctrico]]
- [[#Capacitancia y Capacitores]]
    - [[#Rigidez Dieléctrica y Descarga de Corona]]
    - [[#Capacitancia Definición y Factores]]
    - [[#Capacitor de Placas Paralelas]]
    - [[#Dieléctricos en Capacitores]]
- [[#Circuitos con Capacitores]]
    - [[#Conexión en Serie]]
    - [[#Conexión en Paralelo]]
- [[#Energía Almacenada]]
    - [[#Energía en un Capacitor]]
    - [[#Densidad de Energía en un Campo Eléctrico]]
- [[#Dipolo Eléctrico]]
    - [[#Momento Dipolar Eléctrico]]
    - [[#Efecto de un Campo Externo Uniforme]]
    - [[#Polarización de Dieléctricos]]

---

## Trabajo y Energía en Campos Eléctricos

### Fuerza Conservativa y Trabajo Eléctrico
La fuerza eléctrica $\vec{F}$ ejercida por un campo sobre una carga de prueba es una **fuerza conservativa**:
* El trabajo realizado por la fuerza eléctrica sobre una trayectoria cerrada es cero ($\oint \vec{F} \cdot d\vec{r} = 0$).
* El trabajo depende únicamente de las posiciones inicial y final de la carga, no de la trayectoria recorrida.

El trabajo infinitesimal $dW$ realizado por la fuerza eléctrica al desplazar una carga en un diferencial $d\vec{r}$ es:
$$dW = \vec{F} \cdot d\vec{r}$$

Para mover una carga puntual $q$ entre los puntos $r_1$ y $r_2$ en el campo radial de una carga fija $Q$:
$$W_{1 \to 2} = \int_{r_1}^{r_2} K \frac{qQ}{r^2} dr = K q Q \left( \frac{1}{r_1} - \frac{1}{r_2} \right)$$

> 💡 **Signo del Trabajo:**
> * **Trabajo motor ($W > 0$):** El desplazamiento es espontáneo, en el sentido de la fuerza eléctrica.
> * **Trabajo resistente ($W < 0$):** El desplazamiento es contra la fuerza eléctrica, requiere un agente externo.

### Energía Potencial Eléctrica
Tomando como nivel de referencia cero el infinito ($r_2 \to \infty$, $U_\infty = 0$), la energía potencial eléctrica $U$ de un sistema formado por dos cargas puntuales $Q$ y $q$ separadas una distancia $r$ es:

$$U = K \frac{qQ}{r}$$

Relación entre trabajo y variación de energía potencial:
$$W_{1 \to 2} = U_1 - U_2 = -\Delta U$$

* **Atención:** En las fórmulas de energía potencial y trabajo, las cargas **deben ingresarse con sus respectivos signos ($+$ o $-$)**.

---

## Potencial Eléctrico y Diferencia de Potencial

### Definición de Potencial Eléctrico
El potencial eléctrico $V$ en un punto del espacio es una **magnitud escalar** que representa la energía potencial por unidad de carga de prueba positiva $q$:

$$V = \frac{U}{q}$$

Para una carga puntual $Q$ a una distancia $r$:
$$V = K \frac{Q}{r}$$

Unidad en el Sistema Internacional: **Volt (V)** $\rightarrow 1 \text{ V} = 1 \text{ J/C}$.

Para un conjunto de cargas puntuales, el potencial total es la **suma algebraica** (escalar) de los potenciales de cada carga:
$$V = \sum_{i} K \frac{Q_i}{r_i}$$

### Diferencia de Potencial y Movimiento de Cargas
La diferencia de potencial entre dos puntos $A$ y $B$ ($\Delta V = V_B - V_A$) representa el trabajo por unidad de carga realizado contra el campo.

El trabajo realizado por el campo eléctrico para desplazar una carga $q$ desde $A$ hasta $B$ es:
$$W_{A \to B} = q (V_A - V_B) = -q \Delta V$$

> 🧭 **Reglas para el movimiento espontáneo de cargas:**
> * **Cargas positivas ($+$):** Se desplazan espontáneamente de puntos de **mayor potencial a menor potencial** ($V_A > V_B$).
> * **Cargas negativas ($-$):** Se desplazan espontáneamente de puntos de **menor potencial a mayor potencial** ($V_A < V_B$).
> * **Recorrer una línea de campo:** En el sentido de las líneas de campo eléctrico, el potencial eléctrico **siempre disminuye**.

### Superficies Equipotenciales
Una superficie equipotencial es el lugar geométrico de todos los puntos que están al mismo potencial eléctrico.

* **Propiedad fundamental:** Las líneas de campo eléctrico son siempre **perpendiculares (normales)** a las superficies equipotenciales en cada punto.
* No se requiere trabajo para mover una carga a lo largo de una superficie equipotencial ($W = 0$ ya que $\Delta V = 0$).
* La superficie de cualquier conductor en equilibrio electrostático es una superficie equipotencial.

### Potencial debido a Distribuciones Continuas

1. **A partir de los elementos de carga $dq$:**
   $$V = K \int \frac{dq}{r}$$

2. **A partir del campo eléctrico conocido ($\vec{E}$):**
   $$V_B - V_A = -\int_{A}^{B} \vec{E} \cdot d\vec{s}$$

### Relación entre Potencial y Campo Eléctrico
El campo eléctrico es el gradiente negativo del potencial eléctrico:

$$\vec{E} = -\nabla V$$

Componentes rectangulares del campo eléctrico:

$$E_x = -\frac{\partial V}{\partial x}, \quad E_y = -\frac{\partial V}{\partial y}, \quad E_z = -\frac{\partial V}{\partial z}$$

---

## Capacitancia y Capacitores

### Rigidez Dieléctrica y Descarga de Corona
* **Rigidez Dieléctrica:** Magnitud máxima del campo eléctrico que puede soportar un material aislante antes de ionizarse y volverse conductor. Para el aire seco a 1 atm:
  $$E_{\text{máx}} \approx 3 \times 10^6 \text{ V/m} \quad (3 \text{ MN/C})$$
* **Poder de las Puntas (Descarga de Corona):** En la superficie de un conductor, la densidad de carga $\sigma$ y el campo $\vec{E}$ son mayores en las zonas de mayor curvatura (menor radio). En superficies puntiagudas, el campo puede superar la rigidez dieléctrica del aire produciendo fugas de carga visibles como destellos violeta.

### Capacitancia: Definición y Factores
La capacitancia $C$ es la propiedad de un dispositivo (capacitor) para almacenar carga eléctrica por unidad de diferencia de potencial:

$$C = \frac{Q}{V}$$

Unidad en el S.I.: **Faradio (F)** $\rightarrow 1 \text{ F} = 1 \text{ C/V}$.

> 💡 **Principio clave:** La capacitancia $C$ es **constante** para un conductor o capacitor dado; **NO depende** de la carga $Q$ ni del voltaje $V$. Depende únicamente de la geometría (forma, tamaño, separación) y de la naturaleza del medio (dieléctrico).

### Capacitor de Placas Paralelas
Dos placas conductoras de área $A$ separadas por una distancia $d$:

* Campo eléctrico interno: $E = \frac{\sigma}{\varepsilon_0} = \frac{Q}{\varepsilon_0 A}$
* Voltaje entre placas: $\Delta V = E d = \frac{Q d}{\varepsilon_0 A}$
* **Capacitancia en el vacío:**
  $$C_0 = \frac{\varepsilon_0 A}{d}$$

### Dieléctricos en Capacitores
Al introducir un material no conductor (dieléctrico) con constante dieléctrica $k$ ($k > 1$) llenando el espacio entre placas:

* Reducción del voltaje (si la carga $Q$ se mantiene constante):
  $$\Delta V = \frac{\Delta V_0}{k}$$
* **Aumento de la capacitancia:**
  $$C = k C_0$$

> 📌 **Ventajas de usar un dieléctrico:**
> 1. Aumenta la capacitancia ($C = k C_0$).
> 2. Incrementa el voltaje máximo de operación (mayor rigidez dieléctrica).
> 3. Brinda soporte mecánico a las placas, permitiendo aproximarlas sin que se toquen (reduce $d$).

---

## Circuitos con Capacitores

Deberás dejar una línea en blanco antes de cada tabla para asegurar su renderizado en Obsidian.

| Parámetro | Conexión en Serie | Conexión en Paralelo |
| :--- | :--- | :--- |
| **Esquema visual** | Conectados en la misma línea | Conectados entre los mismos nodos |
| **Carga ($Q$)** | Igual en cada capacitor: <br> $Q_{\text{eq}} = Q_1 = Q_2 = \dots$ | Se divide en cada rama: <br> $Q_{\text{eq}} = Q_1 + Q_2 + \dots$ |
| **Voltaje ($\Delta V$)** | Se divide entre capacitores: <br> $\Delta V_{\text{total}} = \Delta V_1 + \Delta V_2 + \dots$ | Igual en todos los capacitores: <br> $\Delta V_{\text{total}} = \Delta V_1 = \Delta V_2 = \dots$ |
| **Capacitancia Equivalente ($C_{\text{eq}}$)** | $$\frac{1}{C_{\text{eq}}} = \frac{1}{C_1} + \frac{1}{C_2} + \dots$$ | $$C_{\text{eq}} = C_1 + C_2 + \dots$$ |

---

## Energía Almacenada

### Energía en un Capacitor
El trabajo realizado para cargar un capacitor desde $q=0$ hasta $q=Q$ queda almacenado como energía potencial eléctrica $U$:

$$U = \frac{1}{2} \frac{Q^2}{C} = \frac{1}{2} C (\Delta V)^2 = \frac{1}{2} Q \Delta V$$

### Densidad de Energía en un Campo Eléctrico
La energía potencial por unidad de volumen ($u$) almacenada en el campo eléctrico entre las placas de un capacitor (o en cualquier región con campo $\vec{E}$ en el vacío) es:

$$u = \frac{U}{\text{Volumen}} = \frac{1}{2} \varepsilon_0 E^2$$

Unidades S.I.: **$\text{J/m}^3$**.

---

## Dipolo Eléctrico

Un dipolo eléctrico es un sistema formado por dos cargas de igual magnitud y signos opuestos ($+q$ y $-q$) separadas por una distancia pequeña.

### Momento Dipolar Eléctrico
Se define vectorialmente como:

$$\vec{p} = q \Delta \vec{r}$$

Donde:
* $\Delta \vec{r}$: Vector de posición relativa que apunta **desde la carga negativa hacia la carga positiva**.
* Magnitud: $p = q d$.
* Unidad S.I.: **Coulomb-metro ($\text{C}\cdot\text{m}$)**.

Para distribuciones discretas y continuas:
$$\vec{p} = \sum_{i} q_i \vec{r}_i = \int \vec{r} dq$$

### Efecto de un Campo Externo Uniforme $\vec{E}_0$

1. **Fuerza Neta ($\vec{F}_{\text{net}}$):**
   $$\vec{F}_{\text{net}} = (+q)\vec{E}_0 + (-q)\vec{E}_0 = 0$$
   *(El centro de masa del dipolo no se desplaza).*

2. **Torque o Momento de Par ($\vec{M}$ o $\vec{\tau}$):**
   $$\vec{M} = \vec{p} \times \vec{E}_0$$
   * Magnitud: $M = p E_0 \sin\theta$.
   * **Efecto:** El torque hace girar al dipolo hasta alinearlo en la misma dirección y sentido del campo eléctrico $\vec{E}_0$.

### Polarización de Dieléctricos
Al colocar un dieléctrico en un campo eléctrico externo $\vec{E}_0$:
* Los dipolos de los átomos o moléculas se reorientan alineándose con el campo.
* Aparece un campo inducido opuesto $\vec{E}_{\text{ind}}$ generado por las cargas polarizadas en las superficies del aislante.
* **Campo resultando en el interior del dieléctrico:**

$$\vec{E}_{\text{int}} = \vec{E}_0 - \vec{E}_{\text{ind}}$$

> 📉 **Efecto Neto:** El dieléctrico **reduce** la magnitud del campo eléctrico interno en un factor $k$:
> $$E_{\text{int}} = \frac{E_0}{k}$$
