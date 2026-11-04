---
aliases:
  - Inducción Electromagnética
  - Inducción
  - Ley de Faraday
  - Inductancia
---
# Inducción Electromagnética

## Índice General

- [[#Inducción Electromagnética]]
    - [[#Introducción]]
- [[#Flujo Magnético]]
    - [[#Definición]]
    - [[#Propiedades del Flujo Magnético]]
- [[#Experimentos de Inducción]]
    - [[#Experimentos de Faraday y Henry]]
    - [[#Corriente y Fem Inducidas]]
- [[#Ley de Faraday]]
    - [[#Enunciado]]
    - [[#Bobina con N Espiras]]
- [[#Dirección de la Fem Inducida]]
- [[#Ley de Lenz]]
    - [[#Sentido de las Corrientes Inducidas]]
    - [[#Conservación de la Energía]]
- [[#Autoinducción e Inductancia]]
    - [[#Fem Autoinducida]]
    - [[#Inductancia de una Bobina]]
    - [[#Unidad de Inductancia]]
- [[#Circuito RL]]
    - [[#Comportamiento del Inductor]]
    - [[#Conexión de la Fuente]]
    - [[#Desconexión de la Fuente]]
    - [[#Constante de Tiempo]]
- [[#Energía en un Campo Magnético]]
- [[#Ejemplos Resueltos]]
- [[#Bibliografía]]

---

## Inducción Electromagnética

### Introducción
Las corrientes eléctricas producen efectos magnéticos: toda corriente eléctrica genera un campo magnético. Surge entonces una pregunta natural: **¿puede un fenómeno magnético producir también un fenómeno eléctrico?**

En 1831, **Michael Faraday** descubrió que los efectos eléctricos producidos por un fenómeno magnético aparecen como consecuencia de la **variación temporal de los campos magnéticos**. Es decir, no basta con tener un campo magnético: se necesita que el **flujo magnético cambie** con el tiempo.

Este descubrimiento dio origen a la **inducción electromagnética**, base del funcionamiento de generadores, transformadores, motores eléctricos y muchos otros dispositivos.

> [!important] Idea central
> Un flujo magnético variable a través de un circuito induce una fuerza electromotriz (fem) y, si el circuito está cerrado, una corriente inducida.

---

## Flujo Magnético

### Definición
El **flujo magnético** $\Phi_B$ es una medida del número de líneas de campo magnético que atraviesan una superficie. Se define de manera análoga al flujo eléctrico estudiado en [[Unidad I]].

Para una superficie dividida en elementos de área $d\vec{A}$, el flujo a través de un elemento es:

$$d\Phi_B = \vec{B}\cdot d\vec{A} = B\cos\theta\,dA$$

El flujo magnético total a través de la superficie es:

$$\boxed{\Phi_B = \int \vec{B}\cdot d\vec{A} = \int B\cos\theta\,dA}$$

donde $\theta$ es el ángulo entre el campo magnético $\vec{B}$ y el vector normal al área $d\vec{A}$.

Si el campo magnético es **uniforme** y la superficie es **plana**, la expresión se simplifica:

$$\boxed{\Phi_B = BA\cos\theta}$$

**Unidad del flujo magnético:**

$$\boxed{1\ \text{Wb} = 1\ \text{T}\cdot\text{m}^2 = 1\ \text{N}\cdot\text{m/A}}$$

La unidad se llama **weber** ($\text{Wb}$).

### Propiedades del Flujo Magnético

- El flujo magnético a través de una **superficie cerrada** cualquiera es siempre **cero**:
  $$\oint \vec{B}\cdot d\vec{A} = 0$$
  Esto es consecuencia de la inexistencia de monopolos magnéticos.

- Debido a lo anterior, el flujo a través de una **superficie abierta** no depende de la forma de la superficie, sino **solo de la curva que la limita**.

- El flujo es una **cantidad escalar**, pero puede ser positivo o negativo según la orientación relativa de $\vec{B}$ y $d\vec{A}$.

> [!note] Relación con la Unidad IV
> La expresión del flujo magnético es formalmente igual a la del flujo eléctrico. La diferencia fundamental es que las líneas de campo magnético son cerradas, por lo que el flujo neto a través de una superficie cerrada siempre se anula.

---

## Experimentos de Inducción

### Experimentos de Faraday y Henry
Durante la década de 1830, **Michael Faraday** en Inglaterra y **Joseph Henry** en Estados Unidos realizaron experimentos pioneros sobre la fem inducida por medios magnéticos.

**Experimento 1: imán inmóvil cerca de una bobina**

- Una bobina está conectada a un galvanómetro.
- Cuando el imán está inmóvil, el medidor **no indica corriente**.
- Esto es esperable, pues no hay fuente de fem en el circuito.

**Experimento 2: imán en movimiento**

- Cuando el imán se acerca o se aleja de la bobina, el medidor indica corriente.
- La corriente aparece **solo mientras el imán está en movimiento**.
- Si el imán permanece fijo y es la bobina la que se mueve, también se detecta corriente durante el movimiento.

**Experimento 3: dos bobinas**

- Se sustituye el imán por una segunda bobina conectada a una batería.
- Si ambas bobinas están fijas, no hay corriente en la primera bobina.
- Si una bobina se mueve respecto a la otra, aparece corriente, pero **solo mientras hay movimiento relativo**.

**Experimento 4: corriente variable en una bobina cercana**

- Ambas bobinas permanecen inmóviles y se varía la corriente en la segunda, abriendo y cerrando un interruptor o cambiando la resistencia.
- Se observa un pulso momentáneo de corriente en el primer circuito.
- La corriente inducida aparece **solo mientras cambia la corriente** en el segundo circuito.

> [!important] Conclusión experimental
> Lo que produce la fem inducida no es el campo magnético en sí, sino su **variación temporal**. Si el flujo magnético no cambia, no hay fem inducida.

### Corriente y Fem Inducidas
La corriente que aparece en un circuito debido a un campo magnético variable se llama **corriente inducida**. La fuerza electromotriz necesaria para generarla se llama **fem inducida**.

> [!note] Fem y corriente inducidas
> Una fem inducida puede existir incluso si el circuito está abierto; en ese caso no circula corriente, pero sigue habiendo una diferencia de potencial inducida.

---

## Ley de Faraday

### Enunciado
Los resultados de los experimentos de Faraday se resumen en la **ley de Faraday de la inducción**:

> [!important] Ley de Faraday
> La fem inducida en una espira cerrada es igual al **negativo de la tasa de cambio del flujo magnético** a través de la espira.

$$\boxed{\varepsilon = -\frac{d\Phi_B}{dt}}$$

El signo negativo expresa la **ley de Lenz**: la fem inducida se opone al cambio que la produce.

### Bobina con N Espiras
Si se tiene una bobina con $N$ espiras idénticas y el flujo varía a la misma tasa a través de cada espira, la tasa total de cambio es $N$ veces mayor que para una sola espira. La fem total es:

$$\boxed{\varepsilon = -N\frac{d\Phi_B}{dt}}$$

donde $\Phi_B$ es el flujo a través de **cada espira**.

> [!tip] Interpretación
> Para aumentar la fem inducida se puede aumentar el número de espiras, aumentar la intensidad del campo magnético, aumentar el área de la espira o hacer más rápida la variación del flujo.

---

## Dirección de la Fem Inducida

La dirección de una fem o corriente inducida se determina con la ley de Faraday y con reglas sencillas para los signos. El procedimiento es:

1. **Definir una dirección positiva** para el vector de área $\vec{A}$.
2. A partir de las direcciones de $\vec{A}$ y del campo magnético $\vec{B}$, determinar el **signo del flujo** $\Phi_B$ y su tasa de cambio $d\Phi_B/dt$.
3. Determinar el signo de la fem o corriente inducida:
   - Si el flujo es **creciente**, $d\Phi_B/dt > 0$ y la fem inducida es **negativa**.
   - Si el flujo es **decreciente**, $d\Phi_B/dt < 0$ y la fem inducida es **positiva**.

> [!warning] Regla práctica
> El signo negativo de la ley de Faraday no es un simple detalle matemático: indica que la corriente inducida siempre se opone al cambio del flujo magnético.

---

## Ley de Lenz

### Sentido de las Corrientes Inducidas
La ley de Faraday, a través de su signo negativo, establece una diferencia entre las corrientes inducidas por un aumento del flujo y las producidas por una disminución. La **ley de Lenz** explica el sentido de circulación de esas corrientes:

> [!important] Ley de Lenz
> La polaridad de la fem inducida es tal que tiende a producir una corriente que crea un flujo magnético que **se opone al cambio** en el flujo magnético a través del área encerrada por el circuito.

Esto significa que la corriente inducida tiende a **mantener el flujo magnético original**, oponiéndose a que aumente o disminuya.

**Ejemplos:**

- Si el polo norte de un imán se **acerca** a una espira, la corriente inducida circula de modo que la cara enfrentada al imán sea también **Norte**. Así se produce una repulsión que se opone al acercamiento.
- Si el polo norte del imán se **aleja**, la corriente inducida genera un polo **Sur** en la cara enfrentada, atrayendo al imán y oponiéndose a la separación.

Solo mientras exista movimiento relativo entre la espira y el imán persistirán las corrientes inducidas. Si se detiene el acercamiento o la separación, las corrientes cesan y la fuerza magnética desaparece.

### Conservación de la Energía
La ley de Lenz es una consecuencia de la **conservación de la energía**.

- Producir una corriente eléctrica requiere un consumo de energía.
- En la inducción electromagnética, el trabajo realizado **contra las fuerzas magnéticas** que aparecen entre la espira y el imán es el que suministra la energía necesaria para mantener la corriente inducida.
- Si no hay desplazamiento, el trabajo es nulo, no se transfiere energía al sistema y no pueden aparecer corrientes inducidas.
- Si las corrientes inducidas no se opusieran a la acción magnética del imán, no habría trabajo exterior ni cesión de energía al sistema.

> [!note] Idea clave
> La naturaleza se opone al cambio: la corriente inducida siempre actúa de manera que se necesita realizar trabajo para mantener el fenómeno de inducción.

---

## Autoinducción e Inductancia

### Fem Autoinducida
Cuando la corriente en un circuito varía, el campo magnético que ella misma produce también varía. Ese campo variable atraviesa la espira del propio circuito y genera una **fem inducida** que se opone al cambio de corriente.

Este fenómeno se llama **autoinducción**, y la fem resultante se llama **fem autoinducida** o **fuerza contraelectromotriz**.

Como el flujo es proporcional al campo magnético y este es proporcional a la corriente, la fem autoinducida es proporcional a la **rapidez de cambio de la corriente**:

$$\varepsilon = -L\frac{di}{dt}$$

donde $L$ es la **inductancia** de la espira o bobina.

### Inductancia de una Bobina
Para una bobina con $N$ espiras, la inductancia se define como:

$$\boxed{L = \frac{N\Phi_B}{i}}$$

donde $\Phi_B$ es el flujo magnético a través de cada espira e $i$ es la corriente que circula por la bobina.

La inductancia es una medida de la **oposición a un cambio en la corriente**. Es análoga a la resistencia, que es una medida de la oposición al paso de la corriente:

$$\text{Resistencia: } R = \frac{V}{i} \qquad \text{Inductancia: } L = \frac{N\Phi_B}{i}$$

La inductancia depende de la **geometría** del inductor y de las propiedades magnéticas del medio.

### Unidad de Inductancia
La unidad del SI para la inductancia es el **henry** ($\text{H}$):

$$\boxed{1\ \text{H} = 1\ \text{V}\cdot\text{s/A}}$$

> [!note] Origen del nombre
> La unidad se llama henry en honor a Joseph Henry, quien descubrió la inducción electromagnética de forma independiente a Faraday.

---

## Circuito RL

### Comportamiento del Inductor
Un **inductor** es un elemento con una gran inductancia. Su función principal en un circuito es **oponerse a los cambios bruscos de corriente**.

- Si el voltaje de la batería se incrementa para aumentar la corriente, el inductor se opone y el aumento no es instantáneo.
- Si se reduce el voltaje, el inductor produce una reducción lenta de la corriente en lugar de una caída inmediata.
- En general, el inductor hace que el circuito sea **lento en reaccionar** a los cambios de voltaje.

> [!tip] Regla intuitiva
> El inductor intenta mantener la corriente igual a como estaba antes del cambio.

### Conexión de la Fuente
Se considera un circuito serie formado por una fuente de corriente continua, una resistencia $R$ y un inductor $L$. Al cerrar el interruptor, la regla de mallas de Kirchhoff establece:

$$\varepsilon - iR - L\frac{di}{dt} = 0$$

La solución de esta ecuación diferencial, con $i(0)=0$, es:

$$\boxed{i(t) = \frac{\varepsilon}{R}\left(1 - e^{-t/\tau}\right)}$$

donde:

$$\boxed{\tau = \frac{L}{R}}$$

es la **constante de tiempo** del circuito RL.

La corriente no salta instantáneamente de cero a su valor máximo, sino que aumenta de forma **exponencial** hasta alcanzar el valor de equilibrio:

$$I_{\max} = \frac{\varepsilon}{R}$$

### Desconexión de la Fuente
Cuando se anula la fuente de tensión y quedan conectados solo la resistencia y el inductor, la regla de Kirchhoff queda:

$$iR + L\frac{di}{dt} = 0$$

La solución, con corriente inicial $I_0$, es:

$$\boxed{i(t) = I_0\,e^{-t/\tau}}$$

donde:

$$I_0 = \frac{\varepsilon}{R}$$

La corriente disminuye de forma **exponencial** desde su valor máximo.

### Constante de Tiempo
La constante de tiempo $\tau = L/R$ indica la rapidez con que el circuito responde a los cambios:

- Al conectar la fuente, en un tiempo $t=\tau$ la corriente alcanza el **$63{,}2\%$** de su valor máximo.
- Al desconectar la fuente, en un tiempo $t=\tau$ la corriente disminuye un **$63{,}2\%$** de su valor máximo, es decir, queda el $36{,}8\%$.

> [!note] Comparación con el circuito RC
> El circuito RL es análogo al circuito RC estudiado en [[Unidad II]]: en ambos casos la corriente o el voltaje varían exponencialmente con una constante de tiempo característica.

---

## Energía en un Campo Magnético

Una fuente de tensión en un circuito RL proporciona más energía que un circuito sin inductor. Parte de esa energía se disipa en la resistencia y el resto se almacena en el **campo magnético** del inductor.

Multiplicando la ecuación de Kirchhoff por la corriente:

$$\varepsilon i - i^2R - Li\frac{di}{dt} = 0$$

Reordenando:

$$\varepsilon i = i^2R + \frac{d}{dt}\left(\frac{1}{2}Li^2\right)$$

donde:

- $\varepsilon i$ es la **potencia suministrada** por la batería.
- $i^2R$ es la potencia **disipada** en la resistencia.
- $\dfrac{d}{dt}\left(\dfrac{1}{2}Li^2\right)$ es la rapidez con que se **almacena energía** en el inductor.

Integrando, la energía almacenada en el campo magnético de un inductor es:

$$\boxed{U_L = \frac{1}{2}Li^2}$$

> [!important] Resultado
> La energía almacenada en un inductor depende de su inductancia y del cuadrado de la corriente que lo atraviesa. Es análoga a la energía almacenada en un capacitor, $U_C = \frac{1}{2}CV^2$.

---

## Ejemplos Resueltos

### Ejemplo 1: Fem inducida en una bobina
Una bobina de $200$ espiras tiene un flujo magnético que cambia de $0{,}50\ \text{Wb}$ a $0{,}10\ \text{Wb}$ en $0{,}20\ \text{s}$. Calcule la fem inducida.

$$\varepsilon = -N\frac{\Delta\Phi_B}{\Delta t} = -(200)\frac{0{,}10 - 0{,}50}{0{,}20}$$

$$\varepsilon = -(200)\frac{-0{,}40}{0{,}20} = 400\ \text{V}$$

La fem inducida es de $400\ \text{V}$.

### Ejemplo 2: Circuito RL
Un circuito RL tiene $\varepsilon = 12\ \text{V}$, $R = 6\ \Omega$ y $L = 0{,}50\ \text{H}$. Calcule la constante de tiempo, la corriente máxima y la corriente en $t=\tau$.

**Constante de tiempo:**

$$\tau = \frac{L}{R} = \frac{0{,}50}{6} = 0{,}0833\ \text{s}$$

**Corriente máxima:**

$$I_{\max} = \frac{\varepsilon}{R} = \frac{12}{6} = 2\ \text{A}$$

**Corriente en $t=\tau$:**

$$i(\tau) = I_{\max}(1 - e^{-1}) = 2(1 - 0{,}368) = 1{,}26\ \text{A}$$

### Ejemplo 3: Energía almacenada
Para el inductor del ejemplo anterior, cuando la corriente alcanza $2\ \text{A}$, la energía almacenada es:

$$U_L = \frac{1}{2}Li^2 = \frac{1}{2}(0{,}50)(2)^2 = 1\ \text{J}$$

### Ejemplo 4: Inductancia de un solenoide ideal
Un solenoide tiene $N=1000$ vueltas, longitud $l=0{,}50\ \text{m}$ y área transversal $A=2{,}0\times10^{-4}\ \text{m}^2$. Su inductancia es:

$$L = \frac{\mu_0N^2A}{l} = \frac{(4\pi\times10^{-7})(1000)^2(2{,}0\times10^{-4})}{0{,}50}$$

$$L \approx 5{,}0\times10^{-4}\ \text{H} = 0{,}50\ \text{mH}$$

---

## Bibliografía

- Sears, F., Zemansky, M., Young, H., & Freedman, R. (2009). *Física universitaria con física moderna* (12 ed., Vol. 2). Ciudad de México: Pearson.
- Serway, R., & Jewett, J. (2015). *Física para ciencias e ingeniería* (9 ed., Vol. 2). México D. F.: Cengage Learning.
- Tipler, P. A., & Mosca, G. (2004). *Física para ciencias e ingeniería* (5 ed., Vol. 2). Nueva York: W. H. Freeman & Company.
- Bueche, F. (2001). *Física* (9 ed.). Ciudad de México: McGraw-Hill.

---

## Enlaces

- [[Unidad IV]] — Magnetismo
- [[Unidad VI]] — Circuitos de corriente alterna
- [[Unidad II]] — Potencial eléctrico y capacitancia
- [[Material de Lectura Unidad V.pdf]] — Material de lectura original
- [[Formulario Unidad V]]
