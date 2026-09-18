# Formulario Fundamental de Física II

## Índice del Formulario

- [[#Constantes Universales y Unidades]]
- [[#1. Electrostática: Carga y Ley de Coulomb]]
- [[#2. Campo Eléctrico ($\vec{E}$)]]
- [[#3. Densidades de Carga y Distribuciones Continuas]]
- [[#4. Movimiento de Partículas Cargadas]]
- [[#5. Flujo Eléctrico y Ley de Gauss]]
- [[#6. Trabajo y Energía Potencial Eléctrica]]
- [[#7. Potencial Eléctrico ($V$)]]
- [[#8. Capacitancia y Capacitores]]
- [[#9. Combinación de Capacitores en Circuitos]]
- [[#10. Energía Almacenada en Capacitores y Campos]]
- [[#11. Dipolo Eléctrico]]

---

## Constantes Universales y Unidades

| Magnitud / Constante | Símbolo | Valor / Equivalencia S.I. |
| :--- | :---: | :--- |
| **Carga elemental** | $e$ | $1.6 \times 10^{-19} \text{ C}$ |
| **Constante de Coulomb** | $K$ | $K = \frac{1}{4\pi\varepsilon_0} \approx 9 \times 10^9 \text{ N}\cdot\text{m}^2/\text{C}^2$ |
| **Permeabilidad del vacío** | $\varepsilon_0$ | $8.85 \times 10^{-12} \text{ C}^2/(\text{N}\cdot\text{m}^2)$ |
| **Masa del electrón** | $m_e$ | $9.11 \times 10^{-31} \text{ kg}$ |
| **Masa del protón** | $m_p$ | $1.67 \times 10^{-27} \text{ kg}$ |
| **Voltio** | $\text{V}$ | $1 \text{ V} = 1 \text{ J/C}$ |
| **Faradio** | $\text{F}$ | $1 \text{ F} = 1 \text{ C/V}$ |

---

## 1. Electrostática: Carga y Ley de Coulomb

* **Cuantización de la carga:**
  $$q = \pm n e \quad (n = 1, 2, 3, \dots)$$

* **Contacto entre conductores idénticos:**
  $$q_1' = q_2' = \frac{q_1 + q_2}{2}$$

* **Ley de Coulomb (Fuerza puntual):**
  $$\vec{F} = K \frac{q_1 q_2}{r^2} \hat{e}_r$$

* **Superposición de fuerzas:**
  $$\vec{F}_{\text{net}} = \sum_{i} \vec{F}_i$$

---

## 2. Campo Eléctrico ($\vec{E}$)

* **Definición de campo eléctrico:**
  $$\vec{E} = \frac{\vec{F}}{q_0}$$

* **Campo de una carga puntual:**
  $$\vec{E} = K \frac{q}{r^2} \hat{e}_r$$

* **Superposición de campos:**
  $$\vec{E}_{\text{net}} = \sum_{i} \vec{E}_i$$

---

## 3. Densidades de Carga y Distribuciones Continuas

### Densidades de Carga

| Tipo de Distribución | Uniforme | No Uniforme | Unidades |
| :--- | :---: | :---: | :---: |
| **Lineal ($\lambda$)** | $\lambda = \frac{Q}{l}$ | $\lambda = \frac{dq}{dl}$ | $\text{C/m}$ |
| **Superficial ($\sigma$)** | $\sigma = \frac{Q}{A}$ | $\sigma = \frac{dq}{dA}$ | $\text{C/m}^2$ |
| **Volumétrica ($\rho$)** | $\rho = \frac{Q}{V}$ | $\rho = \frac{dq}{dV}$ | $\text{C/m}^3$ |

* **Campo continuo general:**
  $$\vec{E} = K \int \frac{dq}{r^2} \hat{r}$$

### Resultados Clásicos de Campo Eléctrico ($\vec{E}$)

* **Línea de carga finita (longitud $l$, a una distancia $a$ de un extremo):**
  $$E = K \frac{Q}{a(l + a)}$$

* **Anillo de carga (radio $a$, en el eje a una distancia $x$ del centro):**
  $$E_x = K \frac{x Q}{(x^2 + a^2)^{3/2}}$$

* **Disco cargado uniformemente (radio $R$, en el eje a una distancia $x$):**
  $$E = 2\pi K \sigma \left( 1 - \frac{x}{\sqrt{R^2 + x^2}} \right)$$

---

## 4. Movimiento de Partículas Cargadas

* **Aceleración en campo uniforme:**
  $$\vec{a} = \frac{q\vec{E}}{m}$$

* **Ecuaciones cinemáticas ($\vec{E}$ uniforme en $\hat{y}$):**
  $$v_x = v_{0x} = \text{cte}$$
  $$v_y = v_{0y} + a_y t$$
  $$y = y_0 + v_{0y} t + \frac{1}{2} a_y t^2$$

---

## 5. Flujo Eléctrico y Ley de Gauss

* **Flujo eléctrico uniforme en superficie plana:**
  $$\Phi_E = \vec{E} \cdot \vec{A} = E A \cos\theta$$

* **Flujo eléctrico en superficie general:**
  $$\Phi_E = \int \vec{E} \cdot d\vec{A}$$

* **Ley de Gauss (Superficie cerrada):**
  $$\Phi_E = \oint \vec{E} \cdot d\vec{A} = \frac{q_{\text{enc}}}{\varepsilon_0}$$

### Resultados Directos por Ley de Gauss

* **Esfera aislante sólida (radio $a$, carga $Q$):**
  * Exterior ($r \ge a$): $$E = K \frac{Q}{r^2}$$
  * Interior ($r < a$): $$E = K \frac{Q}{a^3} r$$

* **Línea infinita de carga (densidad $\lambda$):**
  $$E = \frac{\lambda}{2\pi \varepsilon_0 r} = \frac{2K\lambda}{r}$$

* **Plano infinito de carga (densidad $\sigma$):**
  $$E = \frac{\sigma}{2\varepsilon_0}$$

* **Superficie exterior de un conductor en equilibrio:**
  $$E = \frac{\sigma}{\varepsilon_0}$$

---

## 6. Trabajo y Energía Potencial Eléctrica

>  **Recordatorio crucial:** En todas las fórmulas de esta sección, las cargas $q$ y $Q$ **entran con sus respectivos signos ($+$ o $-$)**.

* **Trabajo de la fuerza eléctrica entre dos puntos:**
  $$W_{1 \to 2} = \int_{r_1}^{r_2} \vec{F} \cdot d\vec{r} = K q Q \left( \frac{1}{r_1} - \frac{1}{r_2} \right)$$

* **Energía potencial entre dos cargas puntuales:**
  $$U = K \frac{q Q}{r}$$

* **Energía potencial de un sistema discreto:**
  $$U_{\text{total}} = \sum_{i < j} K \frac{q_i q_j}{r_{ij}}$$

* **Relación trabajo y energía potencial:**
  $$W_{1 \to 2} = U_1 - U_2 = -\Delta U$$

---

## 7. Potencial Eléctrico ($V$)

* **Definición general:**
  $$V = \frac{U}{q_0}$$

* **Potencial de una carga puntual:**
  $$V = K \frac{Q}{r}$$

* **Potencial de múltiples cargas puntuales:**
  $$V = \sum_{i} K \frac{Q_i}{r_i}$$

* **Potencial de una distribución continua:**
  $$V = K \int \frac{dq}{r}$$

* **Diferencia de potencial a partir del campo $\vec{E}$:**
  $$\Delta V = V_B - V_A = -\int_{A}^{B} \vec{E} \cdot d\vec{s}$$

* **Trabajo del campo en función de la diferencia de potencial:**
  $$W_{A \to B} = q (V_A - V_B) = -q \Delta V$$

* **Obtención del campo $\vec{E}$ a partir del potencial $V$:**
  $$E_x = -\frac{\partial V}{\partial x}, \quad E_y = -\frac{\partial V}{\partial y}, \quad E_z = -\frac{\partial V}{\partial z}$$

---

## 8. Capacitancia y Capacitores

* **Definición general de capacitancia:**
  $$C = \frac{Q}{V}$$

* **Capacitor de placas paralelas (vacío):**
  $$C_0 = \frac{\varepsilon_0 A}{d}$$

* **Campo dentro de placas paralelas:**
  $$E = \frac{\sigma}{\varepsilon_0} = \frac{Q}{\varepsilon_0 A} = \frac{V}{d}$$

* **Capacitor con dieléctrico ($k > 1$):**
  $$C = k C_0 = \frac{k \varepsilon_0 A}{d}$$
  $$V = \frac{V_0}{k} \quad (Q \text{ constante})$$
  $$E_{\text{int}} = \frac{E_0}{k} = E_0 - E_{\text{ind}}$$

---

## 9. Combinación de Capacitores en Circuitos

| Propiedad                            |                  Conexión en Serie                   |        Conexión en Paralelo         |
| :----------------------------------- | :--------------------------------------------------: | :---------------------------------: |
| **Carga ($Q$)**                      |         $Q_{\text{eq}} = Q_1 = Q_2 = \dots$          | $Q_{\text{eq}} = Q_1 + Q_2 + \dots$ |
| **Voltaje ($V$)**                    |         $V_{\text{eq}} = V_1 + V_2 + \dots$          | $V_{\text{eq}} = V_1 = V_2 = \dots$ |
| **Capacitancia Equivalente**         | $$\frac{1}{C_{\text{eq}}} = \sum_{i} \frac{1}{C_i}$$ |  $$C_{\text{eq}} = \sum_{i} C_i$$   |
| **Dos capacitores (fórmula rápida)** |    $$C_{\text{eq}} = \frac{C_1 C_2}{C_1 + C_2}$$     |    $$C_{\text{eq}} = C_1 + C_2$$    |

---

## 10. Energía Almacenada en Capacitores y Campos

* **Energía almacenada en un capacitor ($U$):**
  $$U = \frac{1}{2} \frac{Q^2}{C} = \frac{1}{2} C V^2 = \frac{1}{2} Q V$$

* **Densidad de energía eléctrica ($u$ en $\text{J/m}^3$):**
  $$u = \frac{1}{2} \varepsilon_0 E^2 \quad (\text{en el vacío})$$
  $$u = \frac{1}{2} k \varepsilon_0 E^2 \quad (\text{en un dieléctrico})$$

---

## 11. Dipolo Eléctrico

* **Momento dipolar eléctrico ($\vec{p}$):**
  $$\vec{p} = q \Delta \vec{r} \quad (\text{apunta de } -q \text{ a } +q)$$
  $$\text{Magnitud: } p = q d$$

* **Torque sobre un dipolo en campo externo uniform $\vec{E}_0$:**
  $$\vec{\tau} = \vec{p} \times \vec{E}_0 \implies \tau = p E_0 \sin\theta$$

* **Fuerza neta en campo uniforme:**
  $$\vec{F}_{\text{net}} = 0$$

* **Energía potencial de un dipolo en campo $\vec{E}_0$:**
  $$U = -\vec{p} \cdot \vec{E}_0 = -p E_0 \cos\theta$$
