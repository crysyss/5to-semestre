# Formulario de Física II - Unidad IV: Magnetismo

## Índice del Formulario

- [[#Constantes y Unidades del S.I.]]
- [[#1. Campo Magnético y Líneas de Campo]]
- [[#2. Fuerza Magnética sobre una Carga en Movimiento]]
- [[#3. Ecuación de Lorentz]]
- [[#4. Flujo Magnético]]
- [[#5. Movimiento de Partículas Cargadas]]
- [[#6. Fuerza Magnética sobre una Corriente]]
- [[#7. Ley de Biot-Savart]]
- [[#8. Casos Particulares de Fuentes Magnéticas]]
- [[#9. Fuerza entre Dos Conductores Paralelos]]
- [[#10. Ley de Ampere]]

---

## Constantes y Unidades del S.I.

| Magnitud | Símbolo | Unidad S.I. | Equivalencia / Valor |
| :--- | :---: | :---: | :--- |
| **Inducción magnética** | $B$ | Tesla ($\text{T}$) | $1\ \text{T} = 1\ \text{N/(A·m)} = 1\ \text{N·s/(C·m)}$ |
| **Flujo magnético** | $\Phi_B$ | Weber ($\text{Wb}$) | $1\ \text{Wb} = 1\ \text{T}·\text{m}^2 = 1\ \text{N}·\text{m/A}$ |
| **Permeabilidad del espacio libre** | $\mu_0$ | — | $4\pi \times 10^{-7}\ \text{T}·\text{m/A}$ |
| **Densidad de flujo magnético** | — | Gauss ($\text{G}$) | $1\ \text{G} = 10^{-4}\ \text{T}$ |

---

## 1. Campo Magnético y Líneas de Campo

* **Dirección del campo magnético:** Aquella en la que tiende a apuntar el polo norte de la aguja de una brújula.
* **Reglas de representación de líneas de campo:**
  * La línea que pasa por un punto es **tangente** al vector $\vec{B}$ en ese punto.
  * El **número de líneas por unidad de área** es proporcional a la **intensidad** del campo.
* **Sentido de las líneas:** Siempre **salen del polo norte** y **entran al polo sur**, formando **espiras cerradas**.

>  **Convenciones de dibujo (3D):**
> * $\odot$ (punto) → vector dirigido **hacia fuera** del plano (como la cabeza de una flecha que viene hacia usted).
> * $\otimes$ (cruz) → vector dirigido **hacia dentro** del plano (como las puntas de una flecha que se aleja).

* **Propiedades:**
  * Líneas cerca entre sí → campo **grande**; líneas separadas → campo **pequeño**.
  * Las líneas de campo **nunca se cruzan**.
  * Líneas rectas, paralelas e igualmente espaciadas → campo **uniforme**.

* **Campo magnético de la Tierra:**
  * $B_{\text{Tierra}} \approx 10^{-4}\ \text{T} = 1\ \text{G}$
  * **Declinación magnética** $\Delta = \theta_{\text{norte verdadero}} - \theta_{\text{norte magnético}}$ (ángulo entre norte magnético y geográfico).
  * **Ángulo de inclinación** $\alpha$: ángulo entre $\vec{B}$ terrestre y la horizontal.

---

## 2. Fuerza Magnética sobre una Carga en Movimiento

* **Magnitud (4.1):**
  $$F = |q|\, v_\perp B \sin\emptyset$$
  * $|q|$: magnitud de la carga; $v_\perp$: componente de $\vec{v}$ perpendicular a $\vec{B}$.
  * $\emptyset$: ángulo entre $\vec{v}$ y $\vec{B}$.

* **Vectorial (4.2):**
  $$\vec{F} = q\,\vec{v} \times \vec{B}$$
  * $\vec{F}$ es **perpendicular** a $\vec{v}$ y a $\vec{B}$ (regla del producto cruz).

* **Cuatro características:**
  1. $F \propto |q|$
  2. $F \propto B$
  3. Depende de la velocidad: una carga **en reposo no experimenta fuerza magnética**.
  4. $\vec{F} \perp \vec{B}$ y $\vec{F} \perp \vec{v}$.

* **Reglas de la mano derecha:**
  * **Regla a)** Dedos en $\vec{v}$, $\vec{B}$ saliendo de la palma → $\vec{F}$ en la dirección del **pulgar**.
  * **Regla b)** $\vec{v}$ en el **pulgar**, $\vec{B}$ en los **dedos** → $\vec{F}$ en la dirección de la **palma**.
  * Para carga **negativa**, invertir el sentido.

---

## 3. Ecuación de Lorentz

* **Fuerza total sobre una carga con campos $\vec{E}$ y $\vec{B}$ presentes (4.3):**
  $$\vec{F} = q\left(\vec{E} + \vec{v} \times \vec{B}\right)$$

---

## 4. Flujo Magnético

* **Flujo a través de un elemento de área (4.4):**
  $$d\Phi_B = B_\perp\,dA = B\cos\emptyset\,dA = \vec{B} \cdot d\vec{A}$$

* **Flujo magnético total (4.5):**
  $$\Phi_B = \int B_\perp\,dA = \int B\cos\emptyset\,dA = \int \vec{B} \cdot d\vec{A}$$

* **Caso de campo uniforme sobre superficie plana (4.6):**
  $$\Phi_B = B A \cos\emptyset$$

* **Flujo a través de una superficie cerrada (4.7):**
  $$\oint \vec{B} \cdot d\vec{A} = 0$$
  * El flujo magnético total a través de una superficie cerrada es **siempre cero** (no existen monopolos magnéticos).

---

## 5. Movimiento de Partículas Cargadas

* **Fuerza magnética vs. fuerza centrípeta (4.8):**
  $$|q|\,vB = m\frac{v^2}{R}$$

* **Radio de la trayectoria circular (4.9):**
  $$R = \frac{mv}{|q|B}$$

* **Rapidez angular (4.10):**
  $$\omega = \frac{v}{R} = \frac{|q|B}{m}$$

* **Frecuencia del ciclotrón:**
  $$f = \frac{\omega}{2\pi} = \frac{|q|B}{2\pi m}$$
  * $f$ es **independiente del radio** $R$ de la trayectoria.

* **Movimiento helicoidal:** Si $\vec{v}$ no es perpendicular a $\vec{B}$, el movimiento es una **hélice**:
  * $v_\parallel$ (paralela a $\vec{B}$) = constante, la partícula avanza en línea recta.
  * $v_\perp$ (perpendicular a $\vec{B}$) = constante, genera la circunferencia de radio $R = \dfrac{mv_\perp}{|q|B}$.

* **Trabajo de la fuerza magnética:**
  $$W = \int \vec{F} \cdot d\vec{s} = 0$$
  * La fuerza magnética **nunca realiza trabajo** (es perpendicular al desplazamiento en todo momento).

---

## 6. Fuerza Magnética sobre una Corriente

* **Fuerza sobre un segmento recto de alambre (4.11):**
  $$\vec{F}_B = (q\vec{v}_D \times \vec{B})\,nAL$$

* **Fuerza sobre un conductor en campo uniforme (4.12):**
  $$\vec{F}_B = I\,\vec{L} \times \vec{B}$$
  * $\vec{L}$ apunta en la dirección de la corriente $I$, con magnitud $L$ (longitud del segmento).

* **Fuerza sobre un elemento infinitesimal (4.13):**
  $$d\vec{F}_B = I\,d\vec{s} \times \vec{B}$$

* **Fuerza total sobre un alambre de forma arbitraria (4.14):**
  $$\vec{F}_B = I \int_a^b d\vec{s} \times \vec{B}$$

>  **Resultantes generales:**
> * La fuerza sobre un conductor curvo es igual a la de un conductor recto que une los mismos puntos extremos (misma corriente).
> * La fuerza neta sobre **cualquier espira cerrada** en un campo uniforme es **cero**: $\vec{F}_1 + \vec{F}_2 = \vec{0}$.

---

## 7. Ley de Biot-Savart

* **Ley de Biot-Savart — elemento de corriente (4.15):**
  $$d\vec{B} = \frac{\mu_0}{4\pi}\frac{I\,d\vec{s} \times \hat{r}}{r^2}$$
  * $\hat{r}$: vector unitario desde $d\vec{s}$ hacia el punto $P$.
  * $d\vec{B} \perp d\vec{s}$ y $d\vec{B} \perp \hat{r}$.

* **Permeabilidad del espacio libre (4.16):**
  $$\mu_0 = 4\pi \times 10^{-7}\ \text{T}·\text{m/A}$$

* **Campo magnético total (integración) (4.17):**
  $$\vec{B} = \frac{\mu_0 I}{4\pi} \int \frac{d\vec{s} \times \hat{r}}{r^2}$$

---

## 8. Casos Particulares de Fuentes Magnéticas

* **Alambre recto de longitud finita, punto a distancia $a$ (4.18):**
  $$B = \frac{\mu_0 I}{4\pi a}\left(\cos\emptyset_1 - \cos\emptyset_2\right)$$

* **Alambre recto largo (infinito) (4.19):**
  $$B = \frac{\mu_0 I}{2\pi a}$$

* **Arco circular de radio $a$ y ángulo $\emptyset$ (4.20):**
  $$B = \frac{\mu_0 I \emptyset}{4\pi a}$$

* **Espira circular de radio $a$ en un punto axial a distancia $x$ del centro (4.24):**
  $$B_x = \frac{\mu_0 I a^2}{2(a^2+x^2)^{3/2}}$$
  * En el centro ($x = 0$): $B = \dfrac{\mu_0 I}{2a}$
  * Muy lejos ($x \gg a$): $B \approx \dfrac{\mu_0 I a^2}{2x^3}$

---

## 9. Fuerza entre Dos Conductores Paralelos

* **Fuerza sobre un tramo de longitud $L$ (4.21):**
  $$F_1 = I_1 L B_2 = \frac{\mu_0 I_1 I_2 L}{2\pi a}$$

* **Fuerza por unidad de longitud (4.22):**
  $$\frac{F_1}{L} = \frac{\mu_0 I_1 I_2}{2\pi a}$$
  * $a$: distancia entre los alambres paralelos.

>  **Sentido de la fuerza:**
> * Corrientes en **misma dirección** → los alambres se **atraen**.
> * Corrientes en **direcciones opuestas** → los alambres se **repelen**.

* **Definición del Ampere (S.I.):**
  $$1\ \text{A} \iff \frac{F_1}{L} = 2\times 10^{-7}\ \text{N/m} \quad \text{con } I_1 = I_2,\ a = 1\ \text{m}$$

* **Definición del Coulomb:**
  $$1\ \text{C} = 1\ \text{A} \times 1\ \text{s}$$

---

## 10. Ley de Ampere

* **Enunciado (4.23):**
  $$\oint \vec{B} \cdot d\vec{s} = \mu_0 I$$
  * $I$: corriente total que pasa a través de cualquier superficie limitada por la trayectoria cerrada.
  * Solo es útil para configuraciones de **alta simetría** (análogo a la Ley de Gauss).

* **Espira rectangular cerca de un alambre largo (ejemplo 4.6):**
  $$\Phi_B = \frac{\mu_0 I b}{2\pi}\ln\left(1 + \frac{a}{c}\right)$$
  * $a$: ancho de la espira; $b$: lado largo; $c$: distancia del alambre al lado más cercano.

---

## Tabla Resumen de Fórmulas Clave

| Fórmula | Expresión | Etiqueta |
| :--- | :--- | :---: |
| **Fuerza magnética** | $\vec{F} = q\vec{v} \times \vec{B}$ | 4.2 |
| **Ecuación de Lorentz** | $\vec{F} = q(\vec{E} + \vec{v} \times \vec{B})$ | 4.3 |
| **Flujo magnético** | $\Phi_B = BA\cos\emptyset$ | 4.6 |
| **Flujo en superficie cerrada** | $\oint \vec{B} \cdot d\vec{A} = 0$ | 4.7 |
| **Radio de órbita circular** | $R = \dfrac{mv}{\|q\|B}$ | 4.9 |
| **Rapidez angular** | $\omega = \dfrac{\|q\|B}{m}$ | 4.10 |
| **Frecuencia del ciclotrón** | $f = \dfrac{\|q\|B}{2\pi m}$ | — |
| **Fuerza sobre conductor** | $\vec{F}_B = I\vec{L} \times \vec{B}$ | 4.12 |
| **Biot-Savart (elemento)** | $d\vec{B} = \dfrac{\mu_0}{4\pi}\dfrac{I\,d\vec{s} \times \hat{r}}{r^2}$ | 4.15 |
| **Alambre infinito** | $B = \dfrac{\mu_0 I}{2\pi a}$ | 4.19 |
| **Fuerza entre paralelos (por longitud)** | $\dfrac{F_1}{L} = \dfrac{\mu_0 I_1 I_2}{2\pi a}$ | 4.22 |
| **Ley de Ampère** | $\oint \vec{B} \cdot d\vec{s} = \mu_0 I$ | 4.23 |
| **Espira circular (punto axial)** | $B_x = \dfrac{\mu_0 I a^2}{2(a^2 + x^2)^{3/2}}$ | 4.24 |

---

## Enlaces

* [[Unidad IV]] — Resumen completo de la unidad
* [[Unidad III]] — Corriente eléctrica (base para la fuerza sobre corrientes)
* [[Formulario Unidades I y II]]
