# Formulario de Física II - Unidad III: Circuitos de Corriente Continua

## Índice del Formulario

- [[#Unidades y Equivalencias S.I.]]
- [[#1. Corriente Eléctrica e Intensidad]]
- [[#2. Densidad de Corriente y Velocidad de Arrastre]]
- [[#3. Resistencia, Conductividad y Resistividad]]
- [[#4. Variación de la Resistividad con la Temperatura]]
- [[#5. Ley de Ohm y Potencia Eléctrica]]
- [[#6. Fuerza Electromotriz (fem) y Voltaje Terminal]]
- [[#7. Asociación de Resistores]]
- [[#8. Leyes de Kirchhoff]]
- [[#9. Circuitos RC (Carga y Descarga de un Capacitor)]]

---

## Unidades y Equivalencias S.I.

| Magnitud | Símbolo | Unidad S.I. | Equivalencia / Relación |
| :--- | :---: | :---: | :--- |
| **Intensidad de corriente** | $I$ | Ampere ($\text{A}$) | $1 \text{ A} = 1 \text{ C/s}$ |
| **Densidad de corriente** | $J$ | — | $\text{A/m}^2$ |
| **Resistencia eléctrica** | $R$ | Ohm ($\Omega$) | $1\ \Omega = 1 \text{ V/A}$ |
| **Resistividad** | $\rho$ | — | $\Omega \cdot \text{m}$ |
| **Conductividad** | $\sigma$ | — | $(\Omega \cdot \text{m})^{-1}$ |
| **Potencia eléctrica** | $P$ | Watt ($\text{W}$) | $1 \text{ W} = 1 \text{ J/s} = 1 \text{ V}\cdot\text{A}$ |
| **Constante de tiempo RC** | $\tau$ | Segundo ($\text{s}$) | $1 \text{ s} = 1\ \Omega \cdot \text{F}$ |

---

## 1. Corriente Eléctrica e Intensidad

* **Corriente promedio e instantánea:**
  $$I_{\text{prom}} = \frac{\Delta Q}{\Delta t} \qquad I = \frac{dQ}{dt}$$
  * $dQ$: Diferencial de carga neta transportada (en $\text{C}$).
  * $dt$: Diferencial de tiempo (en $\text{s}$).

* **Submúltiplos del Ampere:**
  * Miliampere: $1\text{ mA} = 10^{-3}\text{ A}$
  * Microampere: $1\ \mu\text{A} = 10^{-6}\text{ A}$
  * Nanoampere: $1\text{ nA} = 10^{-9}\text{ A}$
  * Picoampere: $1\text{ pA} = 10^{-12}\text{ A}$

---

## 2. Densidad de Corriente y Velocidad de Arrastre

* **Densidad de corriente escalar (uniforme):**
  $$J = \frac{I}{A}$$
  * $A$: Área transversal de la sección del conductor (en $\text{m}^2$).

* **Densidad de corriente y velocidad de arrastre:**
  $$J = n q v_d \qquad \vec{J} = n q \vec{v}_d$$
  * $n$: Número de portadores de carga móviles por unidad de volumen ($\text{m}^{-3}$).
  * $q$: Carga eléctrica de cada portador individual ($\text{C}$). Para electrones, $q = -e \approx -1.6 \times 10^{-19}\text{ C}$.
  * $v_d$: Velocidad de arrastre o deriva ($\text{m/s}$).

---

## 3. Resistencia, Conductividad y Resistividad

* **Resistividad en función del campo y la densidad de corriente:**
  $$\rho = \frac{1}{\sigma} = \frac{E}{J}$$
  * $E$: Magnitud del campo eléctrico interno (en $\text{V/m}$).
  * $J$: Densidad de corriente ($\text{A/m}^2$).

* **Resistencia de un conductor cilíndrico uniforme:**
  $$R = \rho \frac{l}{A}$$
  * $l$: Longitud del conductor (en $\text{m}$).
  * $A$: Área de sección transversal ($\text{m}^2$).

* **Definición fundamental de la resistencia (Relación d.d.p y corriente):**
  $$R = \frac{\Delta V}{I}$$

---

## 4. Variación de la Resistividad con la Temperatura

* **Resistividad dependiente de la temperatura:**
  $$\rho(T) = \rho_0 [1 + \alpha (T - T_0)]$$
  * $\rho_0$: Resistividad a la temperatura de referencia $T_0$ ($\Omega \cdot \text{m}$).
  * $\alpha$: Coeficiente térmico de resistividad del material ($^\circ\text{C}^{-1}$ o $\text{K}^{-1}$).
  * $T$: Temperatura de trabajo, y $T_0$ la temperatura de referencia (usualmente $0\ ^\circ\text{C}$ o $20\ ^\circ\text{C}$).

* **Resistencia dependiente de la temperatura:**
  $$R(T) = R_0 [1 + \alpha (T - T_0)]$$
  * $R_0$: Resistencia del conductor a la temperatura de referencia $T_0$ ($\Omega$).

---

## 5. Ley de Ohm y Potencia Eléctrica

* **Ley de Ohm (Formulaciones vectorial y macroscópica):**
  $$\vec{E} = \rho \vec{J} \qquad \Delta V = I \cdot R$$

* **Potencia eléctrica general:**
  $$P = I \cdot \Delta V$$

* **Potencia disipada en un resistor puro (Efecto Joule):**
  $$P = I^2 \cdot R = \frac{\Delta V^2}{R}$$

---

## 6. Fuerza Electromotriz (fem) y Voltaje Terminal

* **Definición de fem ($\varepsilon$):**
  $$\varepsilon = \frac{W}{q}$$
  * $W$: Trabajo realizado por la fuente para transportar una carga $q$ (en $\text{J}$).

* **Voltaje terminal real de una fuente (con resistencia interna $r$):**
  $$\Delta V = \varepsilon - I \cdot r$$
  * $r$: Resistencia interna de la fuente (en $\Omega$).
  * En circuito abierto ($I = 0$): $\Delta V = \varepsilon$.
  * En cortocircuito ideal ($\Delta V = 0$): $I_{\text{cc}} = \frac{\varepsilon}{r}$.

---

## 7. Asociación de Resistores

### Conexión en Serie
* **Corriente única:**
  $$I = I_1 = I_2 = \dots = I_n$$
* **Caída de tensión total:**
  $$V = V_1 + V_2 + \dots + V_n$$
* **Resistencia equivalente en serie:**
  $$R_{\text{eq}} = \sum_{i=1}^{n} R_i = R_1 + R_2 + \dots + R_n$$

### Conexión en Paralelo
* **Tensión común:**
  $$\Delta V = \Delta V_1 = \Delta V_2 = \dots = \Delta V_n$$
* **Corriente de bifurcación:**
  $$I = I_1 + I_2 + \dots + I_n$$
* **Resistencia equivalente en paralelo:**
  $$\frac{1}{R_{\text{eq}}} = \sum_{i=1}^{n} \frac{1}{R_i} = \frac{1}{R_1} + \frac{1}{R_2} + \dots + \frac{1}{R_n}$$
  * Para solo dos resistores en paralelo:
    $$R_{\text{eq}} = \frac{R_1 \cdot R_2}{R_1 + R_2}$$

---

## 8. Leyes de Kirchhoff

* **Primera Ley (Ley de los Nodos):**
  $$\sum I = 0 \qquad \Rightarrow \qquad \sum I_{\text{entran}} = \sum I_{\text{salen}}$$

* **Segunda Ley (Ley de las Mallas):**
  $$\sum V = 0 \qquad \Rightarrow \qquad \sum \Delta V_i = 0$$

* **Reglas de Signo para la Malla:**
  * Cruzar un resistor $R$ a favor de la corriente: $\Delta V = -I \cdot R$
  * Cruzar un resistor $R$ en contra de la corriente: $\Delta V = +I \cdot R$
  * Cruzar una fem de $-$ a $+$: $\Delta V = +\varepsilon$
  * Cruzar una fem de $+$ a $-$: $\Delta V = -\varepsilon$

---

## 9. Circuitos RC (Carga y Descarga de un Capacitor)

*(Para fundamentos teóricos de capacitancia $C$, consultar [[Unidad II#Capacitancia y Capacitores]])*

* **Ecuación diferencial de carga (Malla de Kirchhoff):**
  $$\varepsilon - \frac{q}{C} - R \frac{dq}{dt} = 0$$

* **Constante de tiempo del circuito RC:**
  $$\tau = R \cdot C$$

### Proceso de Carga
* **Carga en función del tiempo $q(t)$:**
  $$q(t) = C\varepsilon \left(1 - e^{-\frac{t}{RC}}\right) = Q_f \left(1 - e^{-\frac{t}{\tau}}\right)$$
  * $Q_f = C\varepsilon$: Carga máxima final (cuando $t \to \infty$).

* **Corriente en función del tiempo $i(t)$:**
  $$i(t) = \frac{\varepsilon}{R} e^{-\frac{t}{RC}} = I_0 e^{-\frac{t}{\tau}}$$
  * $I_0 = \frac{\varepsilon}{R}$: Corriente inicial máxima (cuando $t = 0$).

### Proceso de Descarga
* **Carga en función del tiempo $q(t)$:**
  $$q(t) = Q_0 e^{-\frac{t}{RC}} = Q_0 e^{-\frac{t}{\tau}}$$
  * $Q_0$: Carga inicial acumulada en el capacitor.

* **Corriente en función del tiempo $i(t)$:**
  $$i(t) = -\frac{Q_0}{RC} e^{-\frac{t}{RC}} = -I_0 e^{-\frac{t}{\tau}}$$
  * El signo negativo indica que la corriente de descarga circula en sentido contrario a la de carga.
