# Formulario de Física II - Unidad VI: Circuitos de Corriente Alterna

## Índice del Formulario

- [[#Constantes y Unidades del S.I.]]
- [[#1. Valores de la Señal Senoidal]]
- [[#2. Resistores en C.A.]]
- [[#3. Inductores en C.A.]]
- [[#4. Capacitores en C.A.]]
- [[#5. Circuito RLC en Serie]]
- [[#6. Impedancia y Desfase]]
- [[#7. Potencia en C.A.]]
- [[#8. Factor de Potencia]]
- [[#9. Resonancia]]
- [[#10. Transformadores]]
- [[#Tabla Resumen de Fórmulas Clave]]

---

## Constantes y Unidades del S.I.

| Magnitud | Símbolo | Unidad S.I. | Equivalencia / Valor |
| :--- | :---: | :---: | :--- |
| **Frecuencia** | $f$ | Hertz ($\text{Hz}$) | $1\ \text{Hz} = 1\ \text{ciclo/s}$ |
| **Frecuencia angular** | $\omega$ | Radián por segundo ($\text{rad/s}$) | $\omega = 2\pi f$ |
| **Resistencia** | $R$ | Ohmio ($\Omega$) | — |
| **Inductancia** | $L$ | Henry ($\text{H}$) | — |
| **Capacitancia** | $C$ | Faradio ($\text{F}$) | — |
| **Reactancia inductiva** | $X_L$ | Ohmio ($\Omega$) | $X_L = \omega L$ |
| **Reactancia capacitiva** | $X_C$ | Ohmio ($\Omega$) | $X_C = \dfrac{1}{\omega C}$ |
| **Impedancia** | $Z$ | Ohmio ($\Omega$) | $Z = \sqrt{R^2+(X_L-X_C)^2}$ |
| **Potencia activa** | $P$ | Watt ($\text{W}$) | — |
| **Potencia reactiva** | $Q$ | Volt-ampere reactivo ($\text{VAR}$) | — |
| **Potencia aparente** | $S$ | Volt-ampere ($\text{VA}$) | — |

---

## 1. Valores de la Señal Senoidal

* **Voltaje instantáneo:**
  $$v(t) = V_{\max}\operatorname{sen}(\omega t) = V_{\max}\operatorname{sen}(2\pi f t)$$

* **Corriente instantánea:**
  $$i(t) = I_{\max}\operatorname{sen}(\omega t) = I_{\max}\operatorname{sen}(2\pi f t)$$

* **Frecuencia angular:**
  $$\omega = 2\pi f = \frac{2\pi}{T}$$

* **Valor eficaz o rms:**
  $$V_{\text{ef}} = \frac{V_{\max}}{\sqrt{2}} = 0{,}707\,V_{\max}$$
  $$I_{\text{ef}} = \frac{I_{\max}}{\sqrt{2}} = 0{,}707\,I_{\max}$$

* **Valor medio en medio ciclo:**
  $$V_{\text{med}} = \frac{2}{\pi}V_{\max} = 0{,}637\,V_{\max}$$
  $$I_{\text{med}} = \frac{2}{\pi}I_{\max} = 0{,}637\,I_{\max}$$

* **Valor pico a pico:**
  $$V_{pp} = 2V_{\max} \qquad I_{pp} = 2I_{\max}$$

> [!note] Relación entre valores
> El valor eficaz es el que produce el mismo efecto térmico que una corriente continua del mismo valor. Los valores indicados en la red eléctrica son eficaces.

---

## 2. Resistores en C.A.

* **Ley de Ohm instantánea:**
  $$v_R(t) = i(t)R$$

* **Amplitud máxima:**
  $$V_R = I_{\max}R$$

* **Desfase:** voltaje y corriente están **en fase** ($\varphi = 0°$).

* **Potencia media disipada:**
  $$P = V_{\text{ef}}I_{\text{ef}} = I_{\text{ef}}^2R = \frac{V_{\text{ef}}^2}{R}$$

---

## 3. Inductores en C.A.

* **Fuerza electromotriz autoinducida:**
  $$\varepsilon = -L\frac{di}{dt}$$

* **Reactancia inductiva:**
  $$X_L = \omega L = 2\pi f L$$

* **Voltaje máximo:**
  $$V_L = I_{\max}X_L$$

* **Voltaje instantáneo:**
  $$v_L(t) = I_{\max}X_L\operatorname{sen}(2\pi f t + 90°)$$

* **Desfase:** el voltaje **adelanta $90°$** a la corriente.

* **Energía almacenada:**
  $$U_L = \frac{1}{2}LI^2$$

> [!tip] Dependencia
> $X_L$ aumenta con la frecuencia y con la inductancia. En corriente continua ($f=0$), la bobina ideal se comporta como un cortocircuito.

---

## 4. Capacitores en C.A.

* **Carga y corriente:**
  $$q = Cv_C \qquad i(t) = \frac{dq}{dt}$$

* **Reactancia capacitiva:**
  $$X_C = \frac{1}{\omega C} = \frac{1}{2\pi f C}$$

* **Voltaje máximo:**
  $$V_C = I_{\max}X_C$$

* **Voltaje instantáneo:**
  $$v_C(t) = I_{\max}X_C\operatorname{sen}(2\pi f t - 90°)$$

* **Desfase:** el voltaje **atrasa $90°$** a la corriente.

* **Energía almacenada:**
  $$U_C = \frac{1}{2}CV^2$$

> [!tip] Dependencia
> $X_C$ disminuye al aumentar la frecuencia o la capacitancia. En corriente continua ($f=0$), el capacitor ideal se comporta como un circuito abierto.

---

## 5. Circuito RLC en Serie

* **Voltaje total (suma fasorial):**
  $$V = \sqrt{V_R^2 + (V_L - V_C)^2}$$

* **Sustituyendo $V_R=IR$, $V_L=IX_L$, $V_C=IX_C$:**
  $$V = I\sqrt{R^2 + (X_L - X_C)^2}$$

* **Corriente instantánea:**
  $$i(t) = I_{\max}\operatorname{sen}(\omega t - \varphi)$$

* **Condición de resonancia:**
  $$X_L = X_C$$

---

## 6. Impedancia y Desfase

* **Impedancia:**
  $$\boxed{Z = \sqrt{R^2 + (X_L - X_C)^2}}$$

* **Ley de Ohm en C.A.:**
  $$\boxed{V = IZ}$$

* **Ángulo de desfase:**
  $$\boxed{\tan\varphi = \frac{X_L - X_C}{R} = \frac{2\pi f L - \dfrac{1}{2\pi f C}}{R}}$$

* **Ángulo:**
  $$\varphi = \arctan\left(\frac{X_L - X_C}{R}\right)$$

> [!important] Signo del desfase
> * $X_L > X_C$ → circuito **inductivo** → $\varphi > 0$ → la corriente se atrasa.
> * $X_C > X_L$ → circuito **capacitivo** → $\varphi < 0$ → la corriente se adelanta.
> * $X_L = X_C$ → **resonancia** → $\varphi = 0$ → voltaje y corriente en fase.

---

## 7. Potencia en C.A.

* **Potencia instantánea:**
  $$p(t) = v(t)i(t)$$

* **Potencia activa o media:**
  $$\boxed{P = V_{\text{ef}}I_{\text{ef}}\cos\varphi = \frac{1}{2}V_{\max}I_{\max}\cos\varphi}$$

* **Potencia reactiva:**
  $$\boxed{Q = V_{\text{ef}}I_{\text{ef}}\operatorname{sen}\varphi}$$

* **Potencia aparente:**
  $$\boxed{S = V_{\text{ef}}I_{\text{ef}}}$$

* **Relación entre potencias:**
  $$\boxed{S^2 = P^2 + Q^2} \qquad S = \sqrt{P^2 + Q^2}$$

* **Unidades:**
  * $P$ en **watts** ($\text{W}$).
  * $Q$ en **volt-ampere reactivo** ($\text{VAR}$).
  * $S$ en **volt-ampere** ($\text{VA}$).

---

## 8. Factor de Potencia

* **Definición:**
  $$\boxed{fp = \frac{P}{S} = \cos\varphi}$$

* **Valores posibles:**
  $$0 \le fp \le 1$$

* **Valor ideal:**
  $$fp = 1 \quad \Longleftrightarrow \quad \varphi = 0° \quad \Longleftrightarrow \quad \text{carga resistiva pura}$$

* **Pérdidas por efecto Joule:**
  $$P_{\text{pérdidas}} = I^2R$$

* **Caída de tensión:**
  $$\Delta V = IR$$

> [!warning] Bajo factor de potencia
> Un $fp$ bajo aumenta la corriente necesaria para una misma potencia activa, lo que incrementa las pérdidas, las caídas de tensión y la sobrecarga de generadores, transformadores y líneas.

---

## 9. Resonancia

* **Condición:**
  $$X_L = X_C \quad \Longrightarrow \quad 2\pi f L = \frac{1}{2\pi f C}$$

* **Frecuencia de resonancia:**
  $$\boxed{f_0 = \frac{1}{2\pi\sqrt{LC}}}$$

* **Frecuencia angular de resonancia:**
  $$\boxed{\omega_0 = \frac{1}{\sqrt{LC}}}$$

* **En resonancia:**
  $$Z = R \qquad I_{\max} = \frac{V_{\max}}{R} \qquad \varphi = 0 \qquad fp = 1$$

---

## 10. Transformadores

* **Relación de fuerzas electromotrices:**
  $$\boxed{\frac{\varepsilon_1}{\varepsilon_2} = \frac{N_1}{N_2}}$$

* **Relación de voltajes:**
  $$\boxed{\frac{V_2}{V_1} = \frac{N_2}{N_1}}$$

* **Conservación de la potencia (transformador ideal):**
  $$\boxed{V_1I_1 = V_2I_2}$$

* **Transformador elevador:** $N_2 > N_1$ → $V_2 > V_1$.
* **Transformador reductor:** $N_2 < N_1$ → $V_2 < V_1$.

> [!note] Relación inversa
> Si el voltaje aumenta, la corriente disminuye en la misma proporción, de modo que la potencia se mantiene constante en un transformador ideal.

---

## Tabla Resumen de Fórmulas Clave

| Fórmula | Expresión |
| :--- | :--- |
| **Voltaje instantáneo** | $v(t)=V_{\max}\operatorname{sen}(2\pi f t)$ |
| **Corriente instantánea** | $i(t)=I_{\max}\operatorname{sen}(2\pi f t)$ |
| **Valor eficaz** | $V_{\text{ef}}=\dfrac{V_{\max}}{\sqrt{2}}$ |
| **Valor medio** | $V_{\text{med}}=\dfrac{2}{\pi}V_{\max}$ |
| **Reactancia inductiva** | $X_L=2\pi f L$ |
| **Reactancia capacitiva** | $X_C=\dfrac{1}{2\pi f C}$ |
| **Impedancia RLC serie** | $Z=\sqrt{R^2+(X_L-X_C)^2}$ |
| **Ley de Ohm en C.A.** | $V=IZ$ |
| **Ángulo de desfase** | $\tan\varphi=\dfrac{X_L-X_C}{R}$ |
| **Potencia activa** | $P=V_{\text{ef}}I_{\text{ef}}\cos\varphi$ |
| **Potencia reactiva** | $Q=V_{\text{ef}}I_{\text{ef}}\operatorname{sen}\varphi$ |
| **Potencia aparente** | $S=V_{\text{ef}}I_{\text{ef}}$ |
| **Factor de potencia** | $fp=\cos\varphi=\dfrac{P}{S}$ |
| **Frecuencia de resonancia** | $f_0=\dfrac{1}{2\pi\sqrt{LC}}$ |
| **Transformador ideal** | $\dfrac{V_2}{V_1}=\dfrac{N_2}{N_1}$ |
| **Potencia en transformador** | $V_1I_1=V_2I_2$ |

---

## Enlaces

- [[Unidad VI]] — Resumen completo de la unidad
- [[Unidad V]] — Inducción electromagnética e inductancia
- [[Unidad IV]] — Magnetismo
- [[Unidad III]] — Corriente eléctrica y circuitos de corriente continua
- [[Formulario Unidad IV]]
