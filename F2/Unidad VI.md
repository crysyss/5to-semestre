---
aliases:
  - Corriente Alterna
  - Circuitos de Corriente Alterna
  - CA
---
# Circuitos de Corriente Alterna

## Índice General

- [[#Circuitos de Corriente Alterna]]
    - [[#Introducción]]
- [[#Sistema Eléctrico de Corriente Alterna]]
    - [[#Generación, Transporte y Distribución]]
    - [[#Ventajas de la C.A. frente a la C.C.]]
    - [[#Utilización de la Corriente Continua]]
- [[#Generación de Tensiones Alternas]]
    - [[#Alternadores]]
    - [[#Fasores]]
    - [[#Valores Instantáneo, Máximo, Medio y Eficaz]]
    - [[#Ecuaciones de la Señal Senoidal]]
- [[#Circuitos RLC en Corriente Alterna]]
    - [[#Resistores en C.A.]]
    - [[#Inductores o Bobinas en C.A.]]
    - [[#Condensadores o Capacitores en C.A.]]
    - [[#Circuitos RLC en Serie]]
    - [[#Impedancia y Ángulo de Desfase]]
- [[#Potencia en Circuitos de Corriente Alterna]]
    - [[#Potencia Instantánea y Media]]
    - [[#Potencia Activa, Reactiva y Aparente]]
    - [[#Triángulo de Potencia]]
    - [[#Factor de Potencia]]
    - [[#Efectos de un Bajo Factor de Potencia]]
- [[#Resonancia en Circuitos de Corriente Alterna]]
- [[#Transformadores]]
    - [[#Partes de un Transformador]]
    - [[#Relaciones del Transformador Ideal]]
- [[#Ejemplos Resueltos]]
- [[#Bibliografía]]

---

## Circuitos de Corriente Alterna

### Introducción
En la [[Unidad III]] se estudiaron los circuitos alimentados por fuentes de **corriente continua (c.c.)**, en los que el voltaje se mantiene constante en el tiempo. En esta unidad se analizan los circuitos alimentados por fuentes de **corriente alterna (c.a.)**, en los cuales tanto el voltaje como la intensidad de corriente **varían continuamente** y cambian de sentido periódicamente.

La forma de onda más común en c.a. es la **senoidal**. Por ello, el estudio se centra en señales del tipo:

$$v(t) = V_{\max}\operatorname{sen}(2\pi f t)$$

$$i(t) = I_{\max}\operatorname{sen}(2\pi f t)$$

donde $V_{\max}$ e $I_{\max}$ son las amplitudes máximas y $f$ es la frecuencia de la señal.

> [!note] Idea central
> En corriente alterna los elementos del circuito ya no se comportan igual que en corriente continua: la **resistencia** disipa energía, mientras que la **bobina** y el **capacitor** almacenan energía y producen **desfases** entre el voltaje y la corriente.

---

## Sistema Eléctrico de Corriente Alterna

### Generación, Transporte y Distribución
Un sistema eléctrico de c.a. está formado por tres subsistemas:

1. **Generación:** centrales hidroeléctricas, termoeléctricas, nucleares, eólicas y fotovoltaicas producen la energía eléctrica.
2. **Transmisión:** líneas de alta tensión transportan la energía desde las centrales hasta los centros de consumo. El voltaje se eleva mediante **transformadores elevadores**.
3. **Distribución:** en las ciudades, el voltaje se reduce mediante **transformadores reductores** y llega a los usuarios por líneas de media y baja tensión.

> [!important] Papel del transformador
> La posibilidad de **elevar y reducir el voltaje** con transformadores es la razón principal por la que se usa corriente alterna en la transmisión de energía. En corriente continua los transformadores no funcionan.

### Ventajas de la C.A. frente a la C.C.
- Generadores y motores **más baratos, eficientes y simples**.
- Posibilidad de **transformar la tensión** de forma sencilla y económica.
- Transporte de grandes cantidades de energía a **largas distancias** con menor sección de conductores, gracias a la alta tensión.
- Posibilidad de emplear **motores de inducción** muy simples y robustos.
- Reducción de fenómenos indeseables como la magnetización de las máquinas y las polarizaciones o corrosiones electrolíticas.

### Utilización de la Corriente Continua
Aunque la c.a. domina la generación y el transporte, la c.c. sigue utilizándose en:

- Sistemas eléctricos aislados de baja tensión, como automóviles.
- Equipos de comunicación.
- Sistemas de protección y control que deben permanecer operativos.
- Sistemas de protección contra incendios e iluminación de emergencia.
- Acumuladores, que se cargan mediante alternadores.

---

## Generación de Tensiones Alternas

### Alternadores
La producción industrial de energía eléctrica se realiza en **alternadores**. En ellos:

- Las bobinas del **inducido** permanecen fijas, montadas en el estator.
- Los **polos magnéticos** que producen el campo giran solidarios al rotor.
- El rotor está unido por un eje a una turbina hidráulica, de gas o de vapor.

La **frecuencia** de la onda de voltaje inducida depende de:

- El **número de pares de polos** del rotor.
- La **velocidad angular** con que gira el rotor.

$$f = (\text{número de pares de polos}) \times (\text{vueltas por segundo})$$

### Fasores
Una señal senoidal puede representarse mediante un **fasor**: un vector giratorio cuya proyección sobre un eje describe la onda senoidal.

- La **longitud** del fasor representa la amplitud máxima.
- El **ángulo** del fasor representa la fase de la señal.
- Una rotación completa del fasor, $360°$, corresponde a un ciclo completo de la onda.

Esta representación permite sumar voltajes y corrientes alternas como **vectores**, lo que simplifica el análisis de los circuitos RLC.

### Valores Instantáneo, Máximo, Medio y Eficaz

| Valor | Símbolo | Descripción |
| :--- | :---: | :--- |
| **Instantáneo** | $v(t)$, $i(t)$ | Valor de la magnitud en un instante dado. |
| **Máximo o pico** | $V_{\max}$, $I_{\max}$ | Mayor amplitud que alcanza la señal. |
| **Pico a pico** | $V_{pp}$, $I_{pp}$ | Diferencia entre el pico positivo y el negativo: $V_{pp}=2V_{\max}$. |
| **Medio** | $V_{\text{med}}$, $I_{\text{med}}$ | Valor promedio en medio ciclo: $\frac{2}{\pi}$ de la amplitud. |
| **Eficaz o rms** | $V_{\text{ef}}$, $I_{\text{ef}}$ | Valor constante que produce el mismo efecto térmico que la c.a. |

El **valor eficaz** o **cuadrático medio (rms)** de una corriente variable se define como el valor de una corriente constante que desarrolla la misma cantidad de calor, en el mismo tiempo y en la misma resistencia. Por eso también se lo llama **valor eficaz**.

> [!important] Dato práctico
> Cuando se indica un valor de tensión o corriente alterna —por ejemplo, $220\ \text{V}$— normalmente se trata del **valor eficaz**, no del valor máximo.

### Ecuaciones de la Señal Senoidal

**Voltaje instantáneo:**

$$v(t) = V_{\max}\operatorname{sen}(\omega t) = V_{\max}\operatorname{sen}(2\pi f t)$$

**Corriente instantánea:**

$$i(t) = I_{\max}\operatorname{sen}(\omega t) = I_{\max}\operatorname{sen}(2\pi f t)$$

**Valor eficaz de la corriente:**

$$\boxed{I_{\text{ef}} = \frac{I_{\max}}{\sqrt{2}} = 0{,}707\,I_{\max}}$$

**Valor eficaz del voltaje:**

$$\boxed{V_{\text{ef}} = \frac{V_{\max}}{\sqrt{2}} = 0{,}707\,V_{\max}}$$

**Valor medio en medio ciclo:**

$$\boxed{I_{\text{med}} = \frac{2}{\pi}I_{\max} = 0{,}637\,I_{\max}}$$

> [!warning] Cuidado con el valor medio
> El valor medio de una señal senoidal **sobre un ciclo completo** es cero, porque la mitad positiva y la mitad negativa se cancelan. El valor $0{,}637\,I_{\max}$ corresponde al promedio del **valor absoluto** o de medio ciclo.

---

## Circuitos RLC en Corriente Alterna

### Resistores en C.A.
En un circuito **resistivo puro**, la corriente y el voltaje están **en fase**: alcanzan sus máximos y ceros al mismo tiempo.

$$v_R(t) = i(t)R = I_{\max}R\operatorname{sen}(2\pi f t)$$

$$V_R = I_{\max}R$$

- No existe desfase entre $v_R$ e $i$.
- El resistor disipa energía en forma de calor.
- Se cumple la ley de Ohm instantánea: $v_R = iR$.

### Inductores o Bobinas en C.A.
Una corriente variable en una bobina produce un campo magnético variable que **autoinduce** una fuerza electromotriz que se opone a la variación de la corriente:

$$\varepsilon = -L\frac{di}{dt}$$

Esta oposición se llama **reactancia inductiva** $X_L$:

$$\boxed{X_L = \omega L = 2\pi f L}$$

Su unidad es el **ohmio** ($\Omega$). La reactancia inductiva:

- Es **directamente proporcional** a la frecuencia $f$.
- Es **directamente proporcional** a la inductancia $L$.
- Aumenta al aumentar la frecuencia o la inductancia.

En una bobina ideal, el voltaje **se adelanta $90°$** respecto a la corriente (la corriente se atrasa $90°$):

$$v_L(t) = I_{\max}X_L\operatorname{sen}(2\pi f t + 90°)$$

$$\boxed{V_L = I_{\max}X_L}$$

La bobina no disipa energía: la almacena en su campo magnético.

### Condensadores o Capacitores en C.A.
Un capacitor almacena carga eléctrica y se opone al aumento del voltaje. Esta oposición se llama **reactancia capacitiva** $X_C$:

$$\boxed{X_C = \frac{1}{\omega C} = \frac{1}{2\pi f C}}$$

Su unidad es el **ohmio** ($\Omega$). La reactancia capacitiva:

- Es **inversamente proporcional** a la frecuencia $f$.
- Es **inversamente proporcional** a la capacitancia $C$.
- Disminuye al aumentar la frecuencia o la capacitancia.

En un capacitor ideal, el voltaje **se atrasa $90°$** respecto a la corriente (la corriente se adelanta $90°$):

$$v_C(t) = I_{\max}X_C\operatorname{sen}(2\pi f t - 90°)$$

$$\boxed{V_C = I_{\max}X_C}$$

La relación entre carga, capacitancia y voltaje es:

$$q = Cv_C \qquad i(t) = \frac{dq}{dt}$$

El capacitor no disipa energía: la almacena en su campo eléctrico.

> [!tip] Resumen de desfases
> - **Resistor:** voltaje y corriente **en fase** ($0°$).
> - **Bobina:** el voltaje **adelanta** $90°$ a la corriente.
> - **Capacitor:** el voltaje **atrasa** $90°$ a la corriente.

### Circuitos RLC en Serie
En un circuito **RLC en serie**, los tres elementos son recorridos por la **misma corriente instantánea**. El voltaje total es la **suma vectorial** de los voltajes individuales:

$$\vec{V} = \vec{V}_R + \vec{V}_L + \vec{V}_C$$

Como $\vec{V}_L$ y $\vec{V}_C$ están sobre la misma línea pero en sentidos opuestos, se restan. El fasor resultante $\vec{V}_L - \vec{V}_C$ es perpendicular a $\vec{V}_R$, por lo que se aplica el teorema de Pitágoras:

$$V = \sqrt{V_R^2 + (V_L - V_C)^2}$$

Sustituyendo $V_R = IR$, $V_L = IX_L$ y $V_C = IX_C$:

$$V = I\sqrt{R^2 + (X_L - X_C)^2}$$

### Impedancia y Ángulo de Desfase
La **impedancia** $Z$ es la oposición total al paso de la corriente alterna. Combina la resistencia real y las reactancias:

$$\boxed{Z = \sqrt{R^2 + (X_L - X_C)^2}}$$

La ley de Ohm para corriente alterna se escribe:

$$\boxed{V = IZ}$$

El **ángulo de desfase** $\varphi$ entre el voltaje total y la corriente es:

$$\boxed{\tan\varphi = \frac{X_L - X_C}{R} = \frac{2\pi f L - \dfrac{1}{2\pi f C}}{R}}$$

$$\varphi = \arctan\left(\frac{X_L - X_C}{R}\right)$$

Si el voltaje de la fuente es $v(t)=V_{\max}\operatorname{sen}(\omega t)$, la corriente es:

$$i(t) = I_{\max}\operatorname{sen}(\omega t - \varphi)$$

> [!important] Interpretación del signo de $\varphi$
> - Si $X_L > X_C$: el circuito es **inductivo**, $\varphi > 0$ y la corriente **se atrasa** respecto al voltaje.
> - Si $X_C > X_L$: el circuito es **capacitivo**, $\varphi < 0$ y la corriente **se adelanta** respecto al voltaje.
> - Si $X_L = X_C$: el circuito está en **resonancia**, $\varphi = 0$ y la corriente está en fase con el voltaje.

---

## Potencia en Circuitos de Corriente Alterna

### Potencia Instantánea y Media
La potencia instantánea entregada a un dispositivo es el producto del voltaje instantáneo por la corriente instantánea:

$$p(t) = v(t)\,i(t) = V_{\max}I_{\max}\operatorname{sen}(\omega t)\operatorname{sen}(\omega t - \varphi)$$

La **potencia media** o **activa** se obtiene promediando $p(t)$ sobre un ciclo:

$$\boxed{P = V_{\text{ef}}I_{\text{ef}}\cos\varphi = \frac{1}{2}V_{\max}I_{\max}\cos\varphi}$$

El factor $\cos\varphi$ se llama **factor de potencia**.

### Potencia Activa, Reactiva y Aparente

| Potencia | Símbolo | Expresión | Unidad | Descripción |
| :--- | :---: | :--- | :---: | :--- |
| **Activa o media** | $P$ | $V_{\text{ef}}I_{\text{ef}}\cos\varphi$ | Watt (W) | Potencia realmente consumida o transformada en trabajo útil. |
| **Reactiva** | $Q$ | $V_{\text{ef}}I_{\text{ef}}\operatorname{sen}\varphi$ | Volt-ampere reactivo (VAR) | Potencia intercambiada por bobinas y capacitores. |
| **Aparente o total** | $S$ | $V_{\text{ef}}I_{\text{ef}}$ | Volt-ampere (VA) | Suma vectorial de $P$ y $Q$. |

La relación entre las tres potencias es:

$$\boxed{S = \sqrt{P^2 + Q^2}}$$

### Triángulo de Potencia
Las potencias activa, reactiva y aparente se representan geométricamente como los lados de un **triángulo rectángulo**:

- Cateto horizontal: $P$ (potencia activa).
- Cateto vertical: $Q$ (potencia reactiva).
- Hipotenusa: $S$ (potencia aparente).
- Ángulo entre $P$ y $S$: $\varphi$ (ángulo de desfase).

### Factor de Potencia
Se define el **factor de potencia** $fp$ como la relación entre la potencia activa y la potencia aparente:

$$\boxed{fp = \frac{P}{S} = \cos\varphi}$$

Es una magnitud **adimensional** y coincide con el coseno del ángulo de desfase entre la corriente y la tensión.

- El factor de potencia toma valores entre **0 y 1**.
- El valor **ideal es 1**, lo que corresponde a una carga **resistiva pura** ($P=S$).
- Un factor de potencia menor que 1 indica que parte de la energía se intercambia de forma reactiva y no se transforma en trabajo útil.

El instrumento que mide el factor de potencia es el **cosímetro**.

### Efectos de un Bajo Factor de Potencia
Un factor de potencia bajo produce efectos indeseables:

1. **Aumento de pérdidas** en las redes de transmisión y distribución, debido al aumento de la corriente: $P_{\text{pérdidas}} = I^2R$.
2. **Aumento de las caídas de tensión** en las redes: $\Delta V = IR$.
3. **Sobrecarga de equipos y líneas** del sistema eléctrico: generadores, transformadores y líneas de transmisión y distribución.

> [!tip] Corrección del factor de potencia
> En la práctica, el factor de potencia se corrige conectando **capacitores** en paralelo con las cargas inductivas, de modo que la potencia reactiva del capacitor compense la de las bobinas.

---

## Resonancia en Circuitos de Corriente Alterna

La **resonancia** ocurre en un circuito RLC serie cuando las reactancias inductiva y capacitiva se igualan y, por lo tanto, se cancelan:

$$X_L = X_C$$

$$2\pi f L = \frac{1}{2\pi f C}$$

Despejando la frecuencia:

$$\boxed{f_0 = \frac{1}{2\pi\sqrt{LC}}}$$

También se puede expresar como frecuencia angular:

$$\boxed{\omega_0 = \frac{1}{\sqrt{LC}}}$$

En resonancia:

- La impedancia es **mínima** e igual a $R$: $Z=R$.
- La corriente es **máxima**: $I_{\max}=V_{\max}/R$.
- El ángulo de desfase es **cero**: $\varphi=0$.
- El voltaje y la corriente están **en fase**.
- El factor de potencia es **1**.

> [!example] Aplicación
> Un circuito serie RLC puede usarse como **circuito de sintonización** en un receptor de radio: la amplitud de la corriente es máxima cuando la frecuencia de la señal recibida coincide con la frecuencia de resonancia del circuito.

---

## Transformadores

### Partes de un Transformador
Un transformador está formado por:

- **Núcleo magnético:** construido con chapas de hierro laminadas. Constituye el camino para las líneas de campo magnético.
- **Arrollamientos o bobinas:** de cobre o aluminio, por los que circulan las corrientes. Hay un arrollamiento **primario** y uno **secundario**.
- **Tanque o cuba:** contiene la parte activa (núcleo y bobinas).
- **Aceite aislante y refrigerante:** retira el calor producido en las bobinas y lo transporta hacia el exterior.

### Relaciones del Transformador Ideal
En un transformador ideal se desprecian las pérdidas en los arrollamientos y en el núcleo. Se cumplen las siguientes relaciones:

**Relación de fuerzas electromotrices:**

$$\boxed{\frac{\varepsilon_1}{\varepsilon_2} = \frac{N_1}{N_2}}$$

**Relación de voltajes:**

$$\boxed{\frac{V_2}{V_1} = \frac{N_2}{N_1}}$$

**Conservación de la potencia (transformador ideal):**

$$\boxed{V_1I_1 = V_2I_2}$$

donde $N_1$ y $N_2$ son los números de vueltas de los arrollamientos primario y secundario.

- Si $N_2 > N_1$, el transformador es **elevador** de tensión.
- Si $N_2 < N_1$, el transformador es **reductor** de tensión.
- Si el voltaje aumenta, la corriente disminuye en la misma proporción, de modo que la potencia se conserva.

> [!note] Transformadores reales
> En un transformador real existen pérdidas por efecto Joule en los arrollamientos y pérdidas en el núcleo por histéresis y corrientes parásitas. Por eso su rendimiento es menor que 1, aunque en los transformadores de potencia suele ser muy alto.

---

## Ejemplos Resueltos

### Ejemplo 1: Impedancia de un circuito RLC serie
Un circuito serie tiene $R=30\ \Omega$, $L=0{,}20\ \text{H}$ y $C=50\ \mu\text{F}$, conectado a una fuente de $120\ \text{V}_{\text{ef}}$ y $60\ \text{Hz}$. Calcule $X_L$, $X_C$, $Z$, la corriente eficaz y el factor de potencia.

**Reactancias:**

$$\omega = 2\pi(60) = 376{,}99\ \text{rad/s}$$

$$X_L = \omega L = (376{,}99)(0{,}20) = 75{,}40\ \Omega$$

$$X_C = \frac{1}{\omega C} = \frac{1}{(376{,}99)(50\times10^{-6})} = 53{,}05\ \Omega$$

**Impedancia:**

$$Z = \sqrt{30^2 + (75{,}40 - 53{,}05)^2} = \sqrt{900 + 499{,}5} = 37{,}41\ \Omega$$

**Corriente eficaz:**

$$I_{\text{ef}} = \frac{V_{\text{ef}}}{Z} = \frac{120}{37{,}41} = 3{,}21\ \text{A}$$

**Ángulo de desfase y factor de potencia:**

$$\varphi = \arctan\left(\frac{75{,}40 - 53{,}05}{30}\right) = \arctan(0{,}745) = 36{,}7°$$

$$fp = \cos(36{,}7°) = 0{,}802$$

El circuito es **inductivo**: la corriente se atrasa respecto al voltaje.

### Ejemplo 2: Transformador ideal
Un transformador tiene $N_1=500$ vueltas y $N_2=50$ vueltas. Si el primario se conecta a $2400\ \text{V}$ y el secundario entrega $20\ \text{A}$, calcule el voltaje secundario y la corriente primaria.

$$V_2 = V_1\frac{N_2}{N_1} = 2400\cdot\frac{50}{500} = 240\ \text{V}$$

$$I_1 = \frac{V_2I_2}{V_1} = \frac{(240)(20)}{2400} = 2\ \text{A}$$

Es un transformador **reductor** de tensión.

### Ejemplo 3: Frecuencia de resonancia
Un circuito RLC serie tiene $L=10\ \text{mH}$ y $C=10\ \mu\text{F}$. Determine su frecuencia de resonancia.

$$f_0 = \frac{1}{2\pi\sqrt{LC}} = \frac{1}{2\pi\sqrt{(10\times10^{-3})(10\times10^{-6})}}$$

$$f_0 = \frac{1}{2\pi\sqrt{1\times10^{-7}}} = \frac{1}{2\pi(3{,}162\times10^{-4})} = 503{,}3\ \text{Hz}$$

---

## Bibliografía

- Young, H. D., & Freedman, R. A. (2009). *Física universitaria con física moderna* (Vol. II). México: Addison Wesley.
- Serway, R. A., & Jewett, J. W. (2009). *Física para ciencias e ingeniería con física moderna* (Vol. II). México: Cengage Learning.
- Halliday, D., Resnick, R., & Krane, K. S. (2007). *Física* (Vol. II). México: Editorial Patria.

---

## Enlaces

- [[Unidad III]] — Corriente eléctrica y circuitos de corriente continua
- [[Unidad IV]] — Magnetismo
- [[Unidad V]] — Inducción electromagnética e inductancia
- [[Formulario Unidad VI]]
