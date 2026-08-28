---
aliases:
  - Fuerzas y Campos Eléctricos
---
# Fuerzas y Campos Eléctricos

## Índice General

- [[#Conceptos Básicos de Electrostática]]
    - [[#Carga Eléctrica]]
    - [[#Conductores y Aislantes]]
    - [[#Cuantización de la Carga]]
    - [[#Conservación de la Carga]]
    - [[#Métodos de Electrización]]
- [[#Ley de Coulomb]]
    - [[#Formulación Matemática]]
    - [[#Principio de Superposición de Fuerzas]]
- [[#Campo Eléctrico]]
    - [[#Definición y Campo de una Carga Puntual]]
    - [[#Líneas de Campo Eléctrico]]
- [[#Distribuciones Continuas de Carga]]
    - [[#Densidades de Carga]]
    - [[#Fórmula General del Campo Continuo]]
    - [[#Modelos Clásicos de Distribución]]
        - [[#Línea Cargada Finita]]
        - [[#Anillo Uniforme de Carga]]
        - [[#Disco Cargado Uniformemente]]
- [[#Movimiento de Partículas Cargadas]]
    - [[#Aceleración en Campo Uniforme]]
    - [[#Tipos de Trayectorias]]
- [[#Flujo Eléctrico]]
    - [[#Concepto y Caso Uniforme]]
    - [[#Caso General e Integral]]
    - [[#Flujo en Superficies Cerradas]]
- [[#Ley de Gauss]]
    - [[#Enunciado Fundamental]]
    - [[#Requisitos de una Superficie Gaussiana]]
    - [[#Aplicaciones de la Ley de Gauss]]
        - [[#Simetría Esférica Esfera Aislante]]
        - [[#Simetría Cilíndrica Línea Infinita]]
        - [[#Simetría Plana Plano Infinito]]
- [[#Conductores en Equilibrio Electrostático]]
    - [[#Propiedades Fundamentales]]
    - [[#Demostraciones con Ley de Gauss]]

---

## Conceptos Básicos de Electrostática

### Carga Eléctrica
La carga eléctrica es una propiedad intrínseca de la materia. Reside en los átomos que la constituyen:
* **Protones:** Carga positiva ($+$), ubicados en el núcleo atómico.
* **Electrones:** Carga negativa ($-$), orbitando alrededor del núcleo.

>[!IMPORTANT]  **Regla de oro de las interacciones:** Cargas de signos iguales se repelen, y cargas de signos opuestos se atraen.

### Conductores y Aislantes
La facilidad con la que las cargas se mueven en un material determina su clasificación:

* **Conductores:** Poseen electrones libres que no están fuertemente ligados a los átomos y pueden moverse con facilidad por todo el material (ej. metales).
* **Aislantes:** No poseen electrones libres; todos sus electrones están ligados a los átomos y no pueden desplazarse libremente (ej. plástico, madera).

### Cuantización de la Carga
La carga eléctrica no es continua, sino que existe en múltiplos enteros de una cantidad elemental mínima, que corresponde al valor absoluto de la carga del electrón o del protón.

La carga elemental en el S.I. se mide en **Coulombs (C)**:
$$e = 1.6 \times 10^{-19} \text{ C}$$

La ecuación de cuantización es:
$$q = \pm n e$$

Donde:
* $q$: Carga del cuerpo.
* $n$: Número entero ($n = 1, 2, 3, \dots$).
* $e$: Cantidad elemental de carga ($1.6 \times 10^{-19} \text{ C}$).

### Conservación de la Carga
>  **Principio:** La carga eléctrica total de un sistema aislado se mantiene constante (se conserva). No se crea ni se destruye, solo se transfiere entre cuerpos.

### Métodos de Electrización

1. **Por Frotamiento:** Al frotar dos cuerpos neutros, se arrancan electrones de uno y se transfieren al otro. Uno queda con carga positiva y el otro con carga negativa de igual magnitud.
2. **Por Contacto:** Al aproximar y tocar un cuerpo cargado a uno neutro, se transfieren electrones. Ambos terminan con cargas del mismo signo.
   
    **Nota Importante:** Si dos cuerpos conductores son **idénticos** y se ponen en contacto, la carga final se distribuye equitativamente entre ambos:
   $$q_1' = q_2' = \frac{q_1 + q_2}{2}$$

3. **Por Inducción:** Se aproxima un cuerpo cargado (inductor) a un conductor neutro (inducido) sin tocarlo, provocando una separación de cargas. Al conectar el inducido a tierra (un sumidero/fuente infinito de electrones), este gana o pierde electrones. Al desconectar la tierra y retirar el inductor, el cuerpo queda cargado con signo opuesto al inductor.

---

## Ley de Coulomb

Describe la fuerza de atracción o repulsión electrostática entre dos cargas puntuales en reposo.

### Formulación Matemática

$$\vec{F} = K \frac{q_1 q_2}{r^2} \hat{e}_r$$

Donde:
* $\vec{F}$: Vector fuerza electrostática.
* $q_1, q_2$: Magnitudes de las cargas eléctricas (C).
* $r$: Distancia de separación entre las cargas (m).
* $\hat{e}_r$: Vector unitario en la dirección de la línea que une las cargas.
* $K$: Constante eléctrica del vacío:
  $$K = \frac{1}{4\pi\varepsilon_0} \approx 9 \times 10^9 \text{ N}\cdot\text{m}^2/\text{C}^2$$
* $\varepsilon_0$: Permeabilidad del espacio libre (vacío):
  $$\varepsilon_0 = 8.85 \times 10^{-12} \text{ C}^2/(\text{N}\cdot\text{m}^2)$$

### Principio de Superposición de Fuerzas
Cuando hay múltiples cargas interactuando, la fuerza neta sobre una carga de interés es la **suma vectorial** de las fuerzas individuales ejercidas por cada una de las otras cargas por separado:

$$\vec{F}_{\text{total}} = \vec{F}_1 + \vec{F}_2 + \dots + \vec{F}_n = \sum_{i} \vec{F}_i$$

---

## Campo Eléctrico

El campo eléctrico ($\vec{E}$) es una perturbación que una carga eléctrica genera en el espacio que la rodea. Se define como la fuerza eléctrica experimentada por una carga de prueba positiva por unidad de carga:

$$\vec{E} = \frac{\vec{F}}{q_0}$$

La unidad en el S.I. es el **Newton por Coulomb (N/C)**.

### Definición y Campo de una Carga Puntual

$$\vec{E} = K \frac{q}{r^2} \hat{e}_r$$

Donde:
* $q$: Carga generadora del campo.
* $r$: Distancia desde la carga al punto donde se evalúa el campo.
* $\hat{e}_r$: Vector unitario que apunta radialmente hacia afuera desde la carga generadora.

>  **Sentido de $\vec{E}$:** El campo eléctrico apunta radialmente **hacia afuera** de las cargas positivas ($+$) y radialmente **hacia adentro** de las cargas negativas ($-$).

### Líneas de Campo Eléctrico
Son una herramienta visual y teórica para representar el campo eléctrico. Tienen las siguientes propiedades:

* Son tangentes a la dirección del campo eléctrico en cada punto del espacio.
* El número de líneas por unidad de área perpendicular es proporcional a la intensidad de $\vec{E}$.
* Salen de cargas positivas y entran a cargas negativas.
* El número de líneas que salen/entran es proporcional a la magnitud de la carga.
* **¡Crucial!** Las líneas de campo **nunca** pueden cruzarse ni tocarse entre sí.

---

## Distribuciones Continuas de Carga

Cuando las fuentes de campo están formadas por una cantidad inmensa de cargas muy próximas, se modelan como un continuo de carga mediante densidades.

### Densidades de Carga


| Tipo de Distribución | Símbolo | Definición (Uniforme) | Definición (No Uniforme) | Unidades S.I. |
| :--- | :---: | :---: | :---: | :---: |
| **Lineal** (barra, hilo) | $\lambda$ | $\lambda = \frac{Q}{l}$ | $\lambda = \frac{dq}{dl}$ | $\text{C/m}$ |
| **Superficial** (placa, disco) | $\sigma$ | $\sigma = \frac{Q}{A}$ | $\sigma = \frac{dq}{dA}$ | $\text{C/m}^2$ |
| **Volumétrica** (esfera) | $\rho$ | $\rho = \frac{Q}{V}$ | $\rho = \frac{dq}{dV}$ | $\text{C/m}^3$ |

### Fórmula General del Campo Continuo
Para calcular el campo total, se divide la distribución en elementos diferenciales de carga $dq$ y se integra sobre todo el cuerpo:

$$\vec{E} = K \int \frac{dq}{r^2} \hat{r}$$

### Modelos Clásicos de Distribución

#### 1. Línea Cargada Finita
Barra de longitud $l$, carga total $Q$ (densidad $\lambda = Q/l$), evaluada en un punto $P$ sobre su eje a una distancia $a$ de uno de sus extremos:

$$\vec{E} = -K \frac{Q}{a(l + a)} \hat{i}$$

*(Dirigido en sentido opuesto a la barra si la carga es positiva)*.

#### 2. Anillo Uniforme de Carga
Anillo de radio $a$, carga total $Q$, evaluado en un punto $P$ a lo largo de su eje central a una distancia $x$ de su centro:

$$\vec{E_x} = K \frac{x Q}{(x^2 + a^2)^{3/2}}\hat{i}$$

>  **Nota:** En el centro del anillo ($x = 0$), el campo eléctrico es nulo ($E = 0$) por razones de simetría.

#### 3. Disco Cargado Uniformemente
Disco de radio $R$, densidad superficial de carga $\sigma$, evaluado en un punto $P$ sobre su eje central a una distancia $x$:

$$E = 2\pi K \sigma \left( 1 - \frac{x}{\sqrt{R^2 + x^2}} \right)$$

---

## Movimiento de Partículas Cargadas

Cuando una partícula de masa $m$ y carga $q$ se coloca en un campo eléctrico $\vec{E}$, experimenta una fuerza eléctrica. Como esta fuerza suele ser mucho mayor que la gravitatoria, esta última se desprecia.

### Aceleración en Campo Uniforme
Aplicando la segunda ley de Newton ($\vec{F}_R = m\vec{a}$):

$$q\vec{E} = m\vec{a} \implies \vec{a} = \frac{q\vec{E}}{m}$$

* **Si la carga es positiva ($+$):** La aceleración tiene la misma dirección y sentido que $\vec{E}$.
* **Si la carga es negativa ($-$)**: La aceleración tiene la misma dirección pero sentido opuesto a $\vec{E}$.

### Tipos de Trayectorias
* **Trayectoria Rectilínea:** Ocurre cuando la partícula parte del reposo o su velocidad inicial $\vec{v}_0$ es paralela a $\vec{E}$.
* **Trayectoria Parabólica:** Ocurre cuando la velocidad inicial $\vec{v}_0$ es perpendicular a $\vec{E}$ (análogo al movimiento de proyectiles en un campo gravitatorio).

---

## Flujo Eléctrico ($\Phi_E$)

El flujo eléctrico mide la cantidad de líneas de campo eléctrico que atraviesan una superficie determinada.

### Concepto y Caso Uniforme
Para un campo eléctrico uniforme que atraviesa una superficie plana de área $A$:

$$\Phi_E = \vec{E} \cdot \vec{A} = E A \cos\theta$$

Donde:
* $\theta$: Ángulo entre la dirección de $\vec{E}$ y el vector normal unitario $\hat{n}$ de la superficie (perpendicular al plano).
* Magnitud de flujo máxima: $\Phi_E = EA$ (cuando $\vec{E}$ es perpendicular a la superficie, es decir, paralelo a $\hat{n}$, $\theta = 0^{\circ}$).
* Flujo nulo: $\Phi_E = 0$ (cuando $\vec{E}$ es paralelo a la superficie, es decir, perpendicular a $\hat{n}$, $\theta = 90^{\circ}$).

Unidades en el S.I.: **$\text{N}\cdot\text{m}^2/\text{C}$**.

### Caso General e Integral
Si el campo varía en la superficie o la superficie es curva, dividimos el área en diferenciales de área $d\vec{A}$:

$$\Phi_E = \int \vec{E} \cdot d\vec{A}$$

### Flujo en Superficies Cerradas
Por convención, el vector unitario normal $\hat{n}$ siempre apunta **hacia afuera** de la superficie cerrada:
* **Líneas salientes:** Producen flujo positivo ($\Phi_E > 0$).
* **Líneas entrantes:** Producen flujo negativo ($\Phi_E < 0$).

El flujo neto a través de una superficie cerrada se representa con una integral cerrada:

$$\Phi_E = \oint \vec{E} \cdot d\vec{A}$$

---

## Ley de Gauss

La Ley de Gauss es una de las ecuaciones de Maxwell fundamentales del electromagnetismo. Relaciona el flujo eléctrico neto a través de cualquier superficie cerrada con la carga neta encerrada por dicha superficie.

### Enunciado Fundamental

$$\Phi_E = \oint \vec{E} \cdot d\vec{A} = \frac{q_{\text{in}}}{\varepsilon_0}$$

Donde:
* $q_{\text{in}}$: Carga neta encerrada dentro de la superficie cerrada (superficie gaussiana).
* $\varepsilon_0$: Permeabilidad del vacío.

### Requisitos de una Superficie Gaussiana
Para poder despejar fácilmente el campo eléctrico de la integral ($\oint E dA = E \oint dA = EA$), la superficie elegida debe tener alta simetría y cumplir:
1. El valor de la magnitud del campo $|\vec{E}|$ debe ser constante sobre toda la superficie.
2. El vector $\vec{E}$ y el diferencial de área $d\vec{A}$ deben ser paralelos entre sí ($\vec{E} \cdot d\vec{A} = E dA$) o perpendiculares entre sí ($\vec{E} \cdot d\vec{A} = 0$).

### Aplicaciones de la Ley de Gauss

#### A. Simetría Esférica (Esfera Aislante)
Esfera aislante de radio $a$ con carga total $Q$ distribuida uniformemente con densidad $\rho$:

* **Fuera de la esfera ($r > a$):**
  Elegimos una superficie gaussiana esférica de radio $r$.
  $$E(4\pi r^2) = \frac{Q}{\varepsilon_0} \implies E = K \frac{Q}{r^2}$$
  *(Se comporta exactamente como una carga puntual concentrada en el origen).*

* **Dentro de la esfera ($r < a$):**
  La carga encerrada es proporcional al volumen interior: $q_{\text{in}} = \rho V_{\text{in}} = Q \frac{r^3}{a^3}$.
  $$E(4\pi r^2) = \frac{Q \frac{r^3}{a^3}}{\varepsilon_0} \implies E = K \frac{Q}{a^3} r$$
  *(El campo eléctrico crece de manera lineal con la distancia $r$ desde el centro).*

#### B. Simetría Cilíndrica (Línea Infinita de Carga)
Línea infinitamente larga con densidad de carga lineal constante $\lambda$.
Elegimos un cilindro gaussiano coaxial de radio $r$ y longitud $l$. El flujo solo atraviesa el área lateral del cilindro ($A = 2\pi r l$):

$$E(2\pi r l) = \frac{\lambda l}{\varepsilon_0} \implies E = \frac{\lambda}{2\pi \varepsilon_0 r} = 2K \frac{\lambda}{r}$$

#### C. Simetría Plana (Plano Infinito de Carga)
Plano infinito con densidad superficial de carga uniforme $\sigma$.
Elegimos un cilindro gaussiano que atraviesa el plano de manera perpendicular. El flujo solo sale por las dos tapas extremas del cilindro, cada una de área $A$:

$$2 E A = \frac{\sigma A}{\varepsilon_0} \implies E = \frac{\sigma}{2\varepsilon_0}$$

*(El campo eléctrico de un plano infinito es **uniforme**, es decir, independiente de la distancia al plano).*

---

## Conductores en Equilibrio Electrostático

Un conductor está en equilibrio electrostático cuando no hay un movimiento neto de cargas en su interior. Esto da lugar a 4 propiedades fundamentales muy importantes para exámenes teóricos:

### Propiedades Fundamentales

1. **El campo eléctrico en el interior de un conductor es nulo ($\vec{E}_{\text{int}} = 0$):**
   * *Explicación física:* Si aplicamos un campo externo $\vec{E}_{\text{ext}}$, los electrones libres se mueven rápidamente hacia un extremo acumulando carga. Esto genera un campo interno opuesto $\vec{E}_{\text{int}}$ que crece hasta cancelar exactamente al campo externo.
2. **Cualquier exceso de carga reside enteramente en la superficie del conductor:**
   * *Demostración:* Si tomamos una superficie gaussiana justo debajo de la superficie del conductor, como $E = 0$ en el interior, el flujo es cero ($\Phi_E = 0$). Por la Ley de Gauss, la carga encerrada debe ser nula ($q_{\text{in}} = 0$). Por lo tanto, el exceso de carga solo puede estar afuera, en la superficie exterior.
3. **El campo eléctrico justo fuera de la superficie del conductor es perpendicular a ella y tiene magnitud:**
   * $$E = \frac{\sigma}{\varepsilon_0}$$
   * *Demostración:* Al usar un pequeño cilindro gaussiano en la superficie del conductor, la base interior tiene $E = 0$ y la pared lateral es paralela a las líneas de campo ($E_{\text{lateral}} = 0$). El flujo neto es solo a través de la tapa exterior ($EA$).
     $$E A = \frac{\sigma A}{\varepsilon_0} \implies E = \frac{\sigma}{\varepsilon_0}$$
4. **En conductores de forma irregular, la carga se acumula en las puntas:**
   * La densidad superficial de carga $\sigma$ es máxima en los puntos donde el radio de curvatura es menor. Por lo tanto, el campo eléctrico externo es extremadamente intenso cerca de las puntas de un conductor irregular (efecto punta o de corona).
