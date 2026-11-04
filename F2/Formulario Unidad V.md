# Formulario de Física II - Unidad V: Inducción Electromagnética

## Índice del Formulario

- [[#Constantes y Unidades del S.I.]]
- [[#1. Flujo Magnético]]
- [[#2. Ley de Faraday]]
- [[#3. Ley de Lenz]]
- [[#4. Autoinducción e Inductancia]]
- [[#5. Circuito RL]]
- [[#6. Energía en un Campo Magnético]]
- [[#7. Inductancia de un Solenoide]]
- [[#Tabla Resumen de Fórmulas Clave]]

---

## Constantes y Unidades del S.I.

| Magnitud | Símbolo | Unidad S.I. | Equivalencia / Valor |
| :--- | :---: | :---: | :--- |
| **Flujo magnético** | $\Phi_B$ | Weber ($\text{Wb}$) | $1\ \text{Wb} = 1\ \text{T}\cdot\text{m}^2$ |
| **Fem inducida** | $\varepsilon$ | Voltio ($\text{V}$) | $1\ \text{V} = 1\ \text{Wb/s}$ |
| **Inductancia** | $L$ | Henry ($\text{H}$) | $1\ \text{H} = 1\ \text{V}\cdot\text{s/A}$ |
| **Resistencia** | $R$ | Ohmio ($\Omega$) | — |
| **Corriente** | $i$ | Ampere ($\text{A}$) | — |
| **Tiempo** | $t$ | Segundo ($\text{s}$) | — |
| **Constante de tiempo** | $\tau$ | Segundo ($\text{s}$) | $\tau = L/R$ |
| **Permeabilidad del vacío** | $\mu_0$ | $\text{T}\cdot\text{m/A}$ | $4\pi\times10^{-7}$ |
| **Energía almacenada** | $U_L$ | Joule ($\text{J}$) | — |

---

## 1. Flujo Magnético

* **Flujo a través de un elemento de área:**
  $$d\Phi_B = \vec{B}\cdot d\vec{A} = B\cos\theta\,dA$$

* **Flujo magnético total:**
  $$\boxed{\Phi_B = \int \vec{B}\cdot d\vec{A} = \int B\cos\theta\,dA}$$

* **Campo uniforme sobre superficie plana:**
  $$\boxed{\Phi_B = BA\cos\theta}$$

* **Unidad:**
  $$1\ \text{Wb} = 1\ \text{T}\cdot\text{m}^2 = 1\ \text{N}\cdot\text{m/A}$$

* **Superficie cerrada:**
  $$\boxed{\oint \vec{B}\cdot d\vec{A} = 0}$$

> [!important] Propiedad clave
> El flujo magnético a través de una superficie cerrada es siempre cero. Por eso, el flujo a través de una superficie abierta depende solo de la curva que la limita, no de la forma de la superficie.

---

## 2. Ley de Faraday

* **Fem inducida en una espira:**
  $$\boxed{\varepsilon = -\frac{d\Phi_B}{dt}}$$

* **Fem inducida en una bobina de $N$ espiras:**
  $$\boxed{\varepsilon = -N\frac{d\Phi_B}{dt}}$$

* **Forma con intervalo finito:**
  $$\varepsilon = -N\frac{\Delta\Phi_B}{\Delta t}$$

> [!important] Significado
> La fem inducida es igual al negativo de la tasa de cambio del flujo magnético. El signo negativo representa la oposición al cambio (ley de Lenz).

---

## 3. Ley de Lenz

* **Enunciado:** la polaridad de la fem inducida es tal que tiende a producir una corriente que crea un flujo magnético que **se opone al cambio** en el flujo magnético.

* **Regla práctica:**
  * Si el flujo **aumenta**, la corriente inducida crea un campo que se opone al aumento.
  * Si el flujo **disminuye**, la corriente inducida crea un campo que se opone a la disminución.

* **Consecuencia energética:** para mantener la corriente inducida es necesario realizar trabajo contra las fuerzas magnéticas. La ley de Lenz es una manifestación de la conservación de la energía.

---

## 4. Autoinducción e Inductancia

* **Fem autoinducida:**
  $$\boxed{\varepsilon = -L\frac{di}{dt}}$$

* **Definición de inductancia para una bobina de $N$ espiras:**
  $$\boxed{L = \frac{N\Phi_B}{i}}$$

* **Unidad:**
  $$1\ \text{H} = 1\ \text{V}\cdot\text{s/A}$$

* **Interpretación:** la inductancia es una medida de la oposición a un cambio en la corriente.
  $$R = \frac{V}{i} \qquad \longleftrightarrow \qquad L = \frac{N\Phi_B}{i}$$

> [!note] Dependencia
> La inductancia depende de la geometría del inductor y de las propiedades magnéticas del medio.

---

## 5. Circuito RL

### Conexión de la fuente

* **Ecuación de Kirchhoff:**
  $$\varepsilon - iR - L\frac{di}{dt} = 0$$

* **Corriente en función del tiempo (con $i(0)=0$):**
  $$\boxed{i(t) = \frac{\varepsilon}{R}\left(1 - e^{-t/\tau}\right)}$$

* **Corriente máxima:**
  $$I_{\max} = \frac{\varepsilon}{R}$$

### Desconexión de la fuente

* **Ecuación de Kirchhoff:**
  $$iR + L\frac{di}{dt} = 0$$

* **Corriente en función del tiempo:**
  $$\boxed{i(t) = I_0\,e^{-t/\tau}}$$

* **Corriente inicial:**
  $$I_0 = \frac{\varepsilon}{R}$$

### Constante de tiempo

$$\boxed{\tau = \frac{L}{R}}$$

* Al conectar la fuente, en $t=\tau$ la corriente alcanza el **$63{,}2\%$** de su valor máximo.
* Al desconectar la fuente, en $t=\tau$ la corriente queda en el **$36{,}8\%$** de su valor inicial.

---

## 6. Energía en un Campo Magnético

* **Potencia suministrada por la fuente:**
  $$P = \varepsilon i$$

* **Balance de potencia:**
  $$\varepsilon i = i^2R + \frac{d}{dt}\left(\frac{1}{2}Li^2\right)$$

* **Energía almacenada en el inductor:**
  $$\boxed{U_L = \frac{1}{2}Li^2}$$

> [!important] Analogía
> La energía del inductor es análoga a la del capacitor:
> $$U_L = \frac{1}{2}Li^2 \qquad \longleftrightarrow \qquad U_C = \frac{1}{2}CV^2$$

---

## 7. Inductancia de un Solenoide

Para un solenoide ideal de $N$ vueltas, longitud $l$ y área transversal $A$:

$$\boxed{L = \frac{\mu_0N^2A}{l}}$$

* $\mu_0 = 4\pi\times10^{-7}\ \text{T}\cdot\text{m/A}$.
* La inductancia aumenta con el cuadrado del número de vueltas y con el área, y disminuye al aumentar la longitud.

---

## Tabla Resumen de Fórmulas Clave

| Fórmula | Expresión |
| :--- | :--- |
| **Flujo magnético** | $\Phi_B = \int \vec{B}\cdot d\vec{A}$ |
| **Flujo uniforme** | $\Phi_B = BA\cos\theta$ |
| **Flujo en superficie cerrada** | $\oint \vec{B}\cdot d\vec{A} = 0$ |
| **Ley de Faraday (una espira)** | $\varepsilon = -\dfrac{d\Phi_B}{dt}$ |
| **Ley de Faraday ($N$ espiras)** | $\varepsilon = -N\dfrac{d\Phi_B}{dt}$ |
| **Fem autoinducida** | $\varepsilon = -L\dfrac{di}{dt}$ |
| **Inductancia** | $L = \dfrac{N\Phi_B}{i}$ |
| **Constante de tiempo RL** | $\tau = \dfrac{L}{R}$ |
| **Carga del inductor** | $i(t) = \dfrac{\varepsilon}{R}\left(1 - e^{-t/\tau}\right)$ |
| **Descarga del inductor** | $i(t) = I_0\,e^{-t/\tau}$ |
| **Corriente máxima** | $I_{\max} = \dfrac{\varepsilon}{R}$ |
| **Energía del inductor** | $U_L = \dfrac{1}{2}Li^2$ |
| **Inductancia de solenoide** | $L = \dfrac{\mu_0N^2A}{l}$ |

---

## Enlaces

- [[Unidad V]] — Resumen completo de la unidad
- [[Unidad IV]] — Magnetismo
- [[Unidad VI]] — Circuitos de corriente alterna
- [[Unidad II]] — Potencial eléctrico y capacitancia
- [[Material de Lectura Unidad V.pdf]] — Material de lectura original
- [[Formulario Unidad IV]]
