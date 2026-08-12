## Índice General

- [[#Propósitos Generales, filosofía, ventajas y particularidades.]]
    - [[#Lema de los creadores:]]
    - [[#Motivaciones de su diseño:]]
    - [[#Tecnologia Java: Entorno de desarrollo]]
    - [[#Ediciones de Java]]
- [[#Lenguaje Java]]
    - [[#Conceptos básicos]]
    - [[#Modificadores de acceso y no-acceso]]
        - [[#Modificadores de acceso]]
        - [[#Modificadores de No-Acceso]]
            - [[#+static (De Clase)]]
            - [[#+ final (Inmutable)]]
            - [[#+abstract (Incompleto) blueprints]]
    - [[#Clases Wrapper]]
        - [[#La Analogía de la Caja]]
        - [[#Tabla de Primitivos y sus Wrappers]]
        - [[#Autoboxing y Unboxing]]
        - [[#Ventajas Adicionales de Usar Wrappers]]
    - [[#Clases abstractas]]
        - [[#El Propósito Clave: Forzar un Contrato]]
        - [[#Reglas y Características Fundamentales]]
    - [[#Interfaces]]
        - [[#El Propósito Clave: Polimorfismo sin Herencia]]
        - [[#Reglas y Características Fundamentales]]
        - [[#Interfaces vs clases abstractas]]
    - [[#Herencia]]
        - [[#El Propósito Clave: Reutilización y Jerarquía]]
        - [[#super: Llamando al Padre]]
        - [[#Sobreescritura (@Override) vs Sobrecarga]]
        - [[#Reglas y Características Fundamentales]]
    - [[#Genéricos (Generics)]]
        - [[#La Analogía del Molde Universal]]
        - [[#Clases Genéricas]]
        - [[#Métodos Genéricos]]
        - [[#Wildcards]]
    - [[#Iterable e Iterator]]
        - [[#El Propósito Clave: el for-each]]
        - [[#Implementando Iterable]]
    - [[#Excepciones]]
        - [[#Jerarquía de Excepciones]]
        - [[#Checked vs Unchecked]]
        - [[#try-catch-finally]]
        - [[#try-with-resources]]
        - [[#Excepciones Personalizadas]]
    - [[#Hilos (Thread)]]
        - [[#Creando un Hilo]]
        - [[#El Problema de la Concurrencia]]
        - [[#synchronized]]
    - [[#String Pool y Pools de Wrappers]]
        - [[#String Pool]]
        - [[#Integer Cache]]

# Propósitos Generales, filosofía, ventajas y particularidades.

### Lema de los creadores:

##### "_Write it once, run everywere_"

De forma resumida, esto se debe a que el programador solo escribe el código una vez, y la JVM se encarga de hacer la traducción final para cada sistema operativo específico. Por eso, el mismo archivo de bytecode funciona en cualquier lugar que tenga una JVM instalada.

---

### Motivaciones de su diseño:

- Simple, orientado a objetos y familiar
- Robusto y seguro
- De arquitectura neutral y portable
- De buen rendimiento
- Interpretado, multihilo y dinámico

---

![[20251018112326.png]]

---

### Tecnologia Java: Entorno de desarrollo

##### La tecnología Java incluye una serie de herramientas para crear aplicaciones completas:

- Un compilador (javac)
- Un intérprete (java)
- Un generador de documentación (javadoc)
- Un conjunto de librerias (La API de java)
- La Máquina Virtual de Java (JVM)
- Un depurador (jdb)
- Un empaquetador (jar)

---

### Ediciones de Java

- **Java SE (Standard Edition):** aplicaciones cliente desktop.
- **Jakarta EE (Enterprise Edition):** aplicaciones para servidores.
- **Java ME (Micro Edition):** aplicaciones para dispositivos móviles.
- **Java FX:** desarrollo de aplicaciones gráficas para Internet, para escritorio y para móviles.

---

![[20251018113518.png]]

![[20251018113612.png]]

![[20251018113722.png]]

![[20251018171407.png]]

---

---

# Lenguaje Java

## Conceptos básicos

- **Clase:** se puede decir que es la definición de las características de cierto tipo de objeto del mundo real. Por ejemplo, Persona es una clase. Auto es una clase. En un programa Java es una estructura sintáctica que permite definir datos y operaciones (es una implementación de TAD). Se puede ver como una plantilla de datos.
    
- **Objeto:** es una instancia “viva” de cierta clase. "Persona es la clase y Juan Perez es una instancia de la clase Persona".
    
- **Atributos:** (características del objeto) o datos miembros.
    
- **Métodos:** (qué puedo hacer o que puede hacer el objeto).
    

---

## Modificadores de acceso y no-acceso

## Modificadores de acceso

Estos modificadores definen "quién" puede acceder a una clase, atributo o método. Son fundamentales para el **encapsulamiento**, uno de los pilares de la Programación Orientada a Objetos.

- **`public` (Público):** Totalmente accesible. Cualquiera puede acceder desde cualquier lugar (dentro o fuera del paquete).
    
    - **Clases:** Se puede acceder desde cualquier otro paquete.
    - **Atributos/Métodos:** Se puede acceder desde cualquier clase.
- **`protected` (Protegido):** Accesible dentro del mismo paquete y también por clases hijas (subclases), incluso si están en paquetes diferentes.
    
    - **Atributos/Métodos:** Solo clases del mismo paquete o sus subclases pueden acceder.
- **(default) o (package-private):** Si no escribes ningún modificador, es `default`. Solo es accesible para clases que están en el **mismo paquete**.
    
    - **Clases:** Solo visible para otras clases del mismo paquete.
    - **Atributos/Métodos:** Solo accesible desde clases del mismo paquete.
- **`private` (Privado):** El más restrictivo. Solo se puede acceder desde **dentro de la misma clase**. Es como tu diario personal, nadie más puede verlo.
    
    - **Atributos/Métodos:** Solo el código de la propia clase puede acceder. No se puede usar en clases (solo en clases anidadas).

|**Modificador**|**Misma Clase**|**Mismo Paquete**|**Subclase (Otro Paquete)**|**Otro Paquete**|
|---|---|---|---|---|
|`public`|✅|✅|✅|✅|
|`protected`|✅|✅|✅|❌|
|`(default)`|✅|✅|❌|❌|
|`private`|✅|❌|❌|❌|

## Modificadores de No-Acceso

Estos definen otras características, como el comportamiento, la herencia o la pertenencia.

##### `static` (De Clase)

El modificador **`static`** indica que un miembro (atributo o método) **pertenece a la clase en sí, no a una instancia u objeto individual**.

- **Atributo `static` (Variable de clase):** Hay una única copia de esta variable compartida por todos los objetos de esa clase. Si un objeto la cambia, todos los demás objetos verán ese cambio. Es ideal para contadores o constantes compartidas.

```java
class Coche {
    public static int contadorDeCoches = 0; // Se comparte entre todos los coches.
    public Coche() {
        contadorDeCoches++;
    }
}
Coche c1 = new Coche();
Coche c2 = new Coche();
System.out.println(Coche.contadorDeCoches); // Imprime 2. Se accede via la clase.
```

- **Método `static`:** Se puede llamar sin crear un objeto de la clase. Son comunes en clases de utilidad. No pueden acceder a atributos o métodos que **no** sean `static`, porque no están asociados a ningún objeto en particular.

```java
// La clase Math está llena de métodos static
double raiz = Math.sqrt(25); // No necesitas hacer: new Math()
```

##### + `final` (Inmutable)

La palabra **`final`** significa que algo **no puede ser modificado** después de su inicialización. Su comportamiento depende de dónde se use.

- **Variable `final`:** Se convierte en una **constante**. Debe ser inicializada una sola vez (en su declaración o en el constructor) y su valor no puede cambiar.

```java
final double PI = 3.14159;
// PI = 3.14; // ¡Error de compilación!
```

- **Método `final`:** **No puede ser sobreescrito** por una subclase. Se usa para garantizar que el comportamiento de un método no sea alterado por la herencia.

```java
class Padre {
    public final void mensaje() {
        System.out.println("Este es un mensaje final.");
    }
}
class Hijo extends Padre {
    // public void mensaje() { } // ¡Error de compilación!
}
```

**Clase `final`:** **No puede ser heredada**. Ninguna otra clase puede extenderla. Clases como `String` en Java son `final` por seguridad y rendimiento.

```java
final class ClaseInmutable { }
// class OtraClase extends ClaseInmutable { } // ¡Error de compilación!
```

##### +`abstract` (Incompleto) blueprints

El modificador **`abstract`** se usa para crear clases y métodos que están "incompletos", dejando su implementación a las clases hijas. Es clave para la **abstracción**.

- **Clase `abstract`:** Es una clase "plantilla" que **no puede ser instanciada** (no puedes hacer `new` de ella). Sirve como base para otras clases. Puede tener tanto métodos abstractos como métodos concretos (con implementación).

```java
abstract class Figura {
    // Método concreto
    public void mostrarInfo() {
        System.out.println("Soy una figura.");
    }
    // Método abstracto (sin cuerpo)
    public abstract double calcularArea();
}
```

- **Método `abstract`:** Es un método declarado pero **sin cuerpo** (sin `{}`). Obliga a cualquier subclase **no abstracta** a proporcionar una implementación para ese método. Solo pueden existir dentro de una clase abstracta.

```java
class Circulo extends Figura {
    private double radio;
    // Obligado a implementar el método abstracto
    @Override
    public double calcularArea() {
        return Math.PI * radio * radio;
    }
}
```

---

## Algunas cuestiones de Java

- Todos los métodos son virtuales (modificables en las clases hijas) excepto cuando se coloca el modificador “final”.
- Solo existe Herencia simple (en C++ hay herencia múltiple). (Una clase puede tener un solo “padre”).
- Cualquier clase en Java siempre es hija de la clase Object ( esta clase tiene algunas funcionalidades ya definidas).
- Los constructores no se heredan.

---

## Clases Wrapper

En Java, una **clase wrapper** (o clase envoltorio) es una clase que "envuelve" o contiene un valor de un tipo de dato primitivo (`int`, `char`, `double`, etc.) para que pueda ser tratado como un objeto.

**El Problema Principal que Resuelven**

Java tiene dos categorías de tipos de datos:

1. **Tipos Primitivos:** Son datos simples y muy eficientes (`int`, `boolean`, `double`, etc.). No son objetos.
2. **Objetos:** Son instancias de clases, más complejos y con métodos asociados.

El problema es que muchas de las estructuras de datos más importantes de Java, como las **Colecciones** (`ArrayList`, `HashMap`, etc.), están diseñadas para trabajar **exclusivamente con objetos**.

Por ejemplo, no puedes hacer esto: `ArrayList<int> miLista = new ArrayList<>();` ESTO DA ERROR.

Aquí es donde las clases wrapper son esenciales. Envuelves el `int` en su clase wrapper `Integer` y ya puedes usarlo: `ArrayList<Integer> miLista = new ArrayList<>();` ESTO ES CORRECTO.

### La Analogía de la Caja

Imagina que un dato primitivo, como el número `5`, es una simple canica.

- Un `ArrayList` es un sistema de transporte muy sofisticado que **solo acepta cajas**, no canicas sueltas.
- Una **clase wrapper** (como `Integer`) es la **caja** donde metes la canica.

Una vez que la canica (`5`) está dentro de su caja (`Integer`), el sistema de transporte (`ArrayList`) puede manejarla sin problemas.

### Tabla de Primitivos y sus Wrappers

##### Cada tipo primitivo en Java tiene su correspondiente clase wrapper:

|Tipo Primitivo|Clase Wrapper|
|:--|:--|
|`int`|`Integer`|
|`double`|`Double`|
|`char`|`Character`|
|`boolean`|`Boolean`|
|`long`|`Long`|
|`float`|`Float`|
|`short`|`Short`|
|`byte`|`Byte`|

### Autoboxing y Unboxing

En las versiones modernas de Java, no necesitas "envolver" y "desenvolver" los primitivos manualmente. Java lo hace automáticamente por ti.

- **Autoboxing:** Convierte automáticamente un primitivo en su objeto wrapper.
- **Unboxing:** Convierte automáticamente un objeto wrapper de vuelta a su primitivo.

```java
ArrayList<Integer> numeros = new ArrayList<>();

// Autoboxing: Java convierte el primitivo 100 en un objeto Integer por ti
numeros.add(100); 

// Unboxing: Java convierte el objeto Integer de la lista en un primitivo int
int miNumero = numeros.get(0); 

System.out.println(miNumero); // Imprime 100
```

### Ventajas Adicionales de Usar Wrappers

1. **Pueden ser nulos (`null`):** Un objeto puede no tener valor (`null`), lo que es útil para representar la ausencia de un dato. Un primitivo no puede ser nulo.

```java
Integer numeroDeHijos = null; // Válido, representa que no sabemos el dato.
// int otroNumero = null;    // ¡Error de compilación!
```

2. **Ofrecen métodos útiles:** Las clases wrapper tienen métodos estáticos muy prácticos para hacer conversiones y otras operaciones.

```java
String texto = "123";
int numero = Integer.parseInt(texto); // Convierte un String a un int.
```

---

## Clases abstractas

Una **clase abstracta** es una clase que no se puede instanciar directamente (no puedes crear un objeto de ella con `new`). Su propósito es servir como una **clase base (superclase)** para otras clases.

Las clases abstractas son generalmente demasiado generales para crear objetos reales y solo especifican los atributos y comportamientos que sus subclases tienen en común.

Piensa en el concepto "Figura". Puedes dibujar un círculo o un rectángulo, pero no puedes dibujar una "Figura" genérica. "Figura" es un concepto abstracto, mientras que "Círculo" y "Rectángulo" son objetos concretos. En Java, `Figura` sería la clase abstracta.

###### El Propósito Clave: Forzar un Contrato

El objetivo principal de una clase abstracta es **forzar a todas sus subclases a tener ciertos métodos**. Esto se logra a través de los **métodos abstractos**.

Un **método abstracto** es un método que se declara sin implementación (sin cuerpo, solo la firma seguida de un punto y coma).

> [!info] Definición Rápida
> 
> - **Declaración de clase abstracta:** Se usa la palabra clave `abstract` antes de `class`.
> - **Declaración de método abstracto:** Se usa `abstract` antes del tipo de retorno del método.
> 
> ```java
> // Clase abstracta "Figura"
> ```
>
public abstract class Figura {
>
> // Método concreto (con implementación) public void mostrarNombre() { System.out.println("Soy una figura."); }
> 
> // Método abstracto (sin implementación) // Obliga a todas las subclases a definir cómo se calcula su área. public abstract double calcularArea(); }
> 
> ```
> Al heredar de `Figura`, una subclase como `Circulo` está **obligada por contrato** a proporcionar una implementación para el método `calcularArea()`. Si no lo hace, el compilador dará un error.
> ```

### Reglas y Características Fundamentales

- **No se pueden crear objetos:** No puedes hacer `new Figura();`. Esto generará un error de compilación. Las clases abstractas están incompletas por definición.

- **Pueden tener métodos concretos:** Como viste con `mostrarNombre()`, una clase abstracta puede tener métodos completamente funcionales que las subclases heredan y pueden usar directamente.

- **Pueden tener constructores y atributos:** Aunque no se pueden instanciar, las clases abstractas tienen constructores. Estos son llamados por los constructores de las subclases (usando `super()`) para inicializar los atributos heredados.

- **Obligación de implementación:** Cualquier clase que herede de una clase abstracta debe implementar **todos** los métodos abstractos de la superclase. La única excepción es si la subclase también se declara como `abstract`.

- **El poder del Polimorfismo:** Las clases abstractas son cruciales para el polimorfismo. Puedes crear un arreglo de referencias de tipo `Figura` y llenarlo con objetos de sus subclases concretas (`Circulo`, `Rectangulo`, etc.). Luego, al invocar el método `calcularArea()` en cada elemento, Java sabrá automáticamente qué versión del método llamar (la del círculo, la del rectángulo, etc.).


---

## Interfaces

Una **interfaz** es una construcción sintáctica que define un conjunto de métodos abstractos. En su forma más pura, una interfaz especifica **qué** puede hacer una clase, pero no dice absolutamente nada sobre **cómo** lo hace.

Piensa en una interfaz como el **panel de botones de un control remoto**. El panel define las acciones disponibles (`encender()`, `subirVolumen()`, `cambiarCanal()`), pero no contiene los circuitos internos. Cualquier dispositivo (un televisor, un equipo de sonido) que quiera ser controlado por ese remoto debe implementar la lógica interna para cada uno de esos botones.

### El Propósito Clave: Polimorfismo sin Herencia

El superpoder de las interfaces es que permiten el polimorfismo entre clases que **no están relacionadas por herencia**. Una clase en Java solo puede heredar de **una** superclase, pero puede **implementar múltiples** interfaces.

Esto resuelve un problema de diseño crucial: ¿Qué pasa si quieres que un `Empleado` y una `Factura` sean procesados por el mismo sistema de pagos? Un `Empleado` no "es un tipo de" `Factura`, por lo que la herencia no tiene sentido. Sin embargo, ambos "pueden ser pagados". Esa capacidad, "ser pagable", es el contrato que una interfaz puede definir.

### Reglas y Características Fundamentales

- **Declaración:** Se usa la palabra clave `interface`.
    
- **Atributos:** Todas las variables declaradas en una interfaz son implícitamente `public`, `static` y `final`. Es decir, son **constantes** que pertenecen a la interfaz.
    
- **Implementación:** Una clase no `extends` una interfaz, la **`implements`** (implementa).
    
- **El Contrato:** Si una clase `implements` una interfaz, está **obligada** a proporcionar una implementación para **todos** los métodos abstractos definidos en esa interfaz. Si no lo hace, la clase debe declararse como `abstract`.
    

Java 8 introdujo dos grandes cambios que hicieron las interfaces mucho más flexibles:

- **Métodos `default`:** Permiten añadir un método a una interfaz con una implementación por defecto. Las clases que implementan la interfaz heredan este método automáticamente, pero pueden sobreescribirlo si necesitan un comportamiento diferente. Esto es útil para añadir nueva funcionalidad a interfaces existentes sin romper el código de las clases que ya la implementan.
    
- **Métodos `static`:** Permiten definir métodos de utilidad que pertenecen a la interfaz misma y no a las clases que la implementan.
    

### Interfaces vs clases abstractas

|**Característica**|**Clase Abstracta**|**Interfaz**|
|---|---|---|
|**Propósito**|Definir la **identidad** de un objeto (relación "es un").|Definir una **capacidad** de un objeto (relación "puede hacer").|
|**Herencia**|Una clase solo puede **heredar de una** clase abstracta.|Una clase puede **implementar múltiples** interfaces.|
|**Atributos**|Puede tener cualquier tipo de atributo (`static`, `final`, de instancia).|Solo puede tener constantes (`public static final`).|
|**Métodos**|Puede tener métodos `abstract` y **concretos** (con cuerpo).|Principalmente métodos `abstract`. (Con `default` y `static` desde Java 8).|
|**Constructores**|**Tiene** constructores (para ser llamados por las subclases).|**No tiene** constructores.|

##### Cuándo usar cuál:

- Usa una **clase abstracta** cuando quieres compartir código y estado (`atributos`) entre clases estrechamente relacionadas.
    
- Usa una **interfaz** cuando quieres definir un contrato de comportamiento que puede ser implementado por clases de jerarquías dispares.
    

---

## Herencia

La **herencia** es el mecanismo por el cual una clase (subclase o clase hija) adquiere los atributos y métodos de otra clase (superclase o clase padre). Se declara con la palabra clave `extends`.

Piensa en una jerarquía biológica: `Animal` es la superclase. `Perro` y `Gato` son subclases que **heredan** características comunes de `Animal` (como `comer()` o `dormir()`), pero cada una añade o modifica su propio comportamiento (`ladrar()`, `maullar()`).

```java
class Animal {
    protected String nombre;
    
    public Animal(String nombre) {
        this.nombre = nombre;
    }
    
    public void comer() {
        System.out.println(nombre + " está comiendo.");
    }
}

class Perro extends Animal {
    public Perro(String nombre) {
        super(nombre); // Llama al constructor de Animal
    }
    
    public void ladrar() {
        System.out.println(nombre + " dice: ¡Guau!");
    }
}
```

###### El Propósito Clave: Reutilización y Jerarquía

La herencia modela una relación **"es un"** (`Perro` **es un** `Animal`). Su objetivo principal es evitar la duplicación de código: en lugar de reescribir `comer()` en cada clase de animal, se escribe una sola vez en `Animal` y todas las subclases la heredan automáticamente.

### super: Llamando al Padre

La palabra clave **`super`** se usa dentro de una subclase para referirse a su superclase directa.

- **`super(...)`:** Llama al constructor de la superclase. Debe ser la **primera línea** del constructor de la subclase (si se usa explícitamente).
- **`super.metodo()`:** Llama a la versión del método definida en la superclase, útil cuando la subclase la ha sobreescrito pero aún necesita el comportamiento original.

```java
class Perro extends Animal {
    public Perro(String nombre) {
        super(nombre);
    }
    
    @Override
    public void comer() {
        super.comer(); // Ejecuta el comer() de Animal primero
        System.out.println("...y mueve la cola mientras come.");
    }
}
```

> [!info] Constructor por defecto Si el constructor de la subclase no llama explícitamente a `super(...)`, Java inserta automáticamente una llamada a `super()` (sin argumentos) como primera instrucción. Si la superclase no tiene un constructor vacío, esto provoca un error de compilación.

### Sobreescritura (@Override) vs Sobrecarga

Son dos conceptos que suelen confundirse:

- **Sobreescritura (Overriding):** Una subclase redefine un método **heredado**, con la misma firma (nombre, parámetros y tipo de retorno compatible). Se usa la anotación `@Override` como buena práctica (el compilador avisa si no coincide exactamente con un método del padre).
- **Sobrecarga (Overloading):** Varios métodos con el **mismo nombre** pero **distinta firma** (diferente cantidad o tipo de parámetros), dentro de la misma clase. No tiene relación directa con la herencia.

```java
class Calculadora {
    // Sobrecarga: mismo nombre, distintos parámetros
    public int sumar(int a, int b) { return a + b; }
    public double sumar(double a, double b) { return a + b; }
}
```

### Reglas y Características Fundamentales

- **Herencia simple:** Como se vio en [[#Algunas cuestiones de Java]], una clase solo puede extender **una** superclase.
- **Todas las clases heredan de `Object`:** implícitamente, aunque no se escriba `extends Object`.
- **`final` bloquea la herencia:** una clase o método `final` no puede ser extendido/sobreescrito ([[#+ final (Inmutable)]]).
- **Constructores no se heredan:** cada clase debe definir los suyos, aunque puede reutilizar los del padre vía `super(...)`.
- **Los miembros `private` no se heredan (no son visibles) para la subclase**, aunque técnicamente existan en el objeto.

---

## Genéricos (Generics)

Los **genéricos** permiten que clases, interfaces y métodos operen sobre un **tipo de dato parametrizado**, definido en el momento de su uso, en lugar de fijarlo de antemano. Se escriben entre `<>` (diamond operator).

### La Analogía del Molde Universal

Imagina una caja de embalaje genérica: la misma caja (la clase) puede fabricarse para transportar libros, ropa o electrónica, pero **una vez fabricada para libros, solo transporta libros**. Los genéricos son ese molde: `ArrayList<T>` es el molde, y `ArrayList<String>` o `ArrayList<Integer>` son las cajas ya especializadas.

### Clases Genéricas

Se declara un **parámetro de tipo** (por convención, una letra mayúscula como `T`, `E`, `K`, `V`) entre `<>` junto al nombre de la clase.

```java
class Caja<T> {
    private T contenido;
    
    public void guardar(T contenido) {
        this.contenido = contenido;
    }
    
    public T obtener() {
        return contenido;
    }
}

Caja<String> cajaDeTexto = new Caja<>();
cajaDeTexto.guardar("Hola");
String texto = cajaDeTexto.obtener(); // No hace falta castear
```

> [!info] Convenciones comunes de nombres
> 
> - `T` – Type (tipo genérico)
> - `E` – Element (usado en colecciones)
> - `K`, `V` – Key, Value (usado en mapas, ej. `HashMap<K,V>`)

### Métodos Genéricos

Un método puede ser genérico **aunque su clase no lo sea**. El parámetro de tipo se declara antes del tipo de retorno.

```java
public <T> void imprimirElemento(T elemento) {
    System.out.println("Elemento: " + elemento);
}
```

### Wildcards

El comodín **`?`** representa un tipo desconocido, útil cuando se trabaja con métodos que aceptan colecciones de cualquier tipo genérico.

- **`? extends T`:** acepta `T` o cualquier subclase de `T` (límite superior). Se usa cuando solo se **lee** de la estructura.
- **`? super T`:** acepta `T` o cualquier superclase de `T` (límite inferior). Se usa cuando solo se **escribe** en la estructura.

> [!info] Ventaja principal de los genéricos Aportan **seguridad de tipos en tiempo de compilación**: si intentas insertar un `String` en un `ArrayList<Integer>`, el compilador lo rechaza antes de ejecutar el programa, evitando errores de casteo (`ClassCastException`) en tiempo de ejecución.

---

## Iterable e Iterator

**`Iterable`** es una interfaz que, al ser implementada por una clase, permite que sus objetos sean recorridos con el bucle **for-each**. Casi todas las colecciones de Java (`ArrayList`, `HashSet`, etc.) implementan `Iterable`.

### El Propósito Clave: el for-each

Cuando una clase implementa `Iterable<T>`, obliga a definir el método `iterator()`, que devuelve un objeto `Iterator<T>`. Ese objeto sabe cómo recorrer la colección elemento por elemento, sin exponer su estructura interna (un `ArrayList` y un `HashSet` se recorren "por dentro" de forma distinta, pero ambos se usan igual desde afuera).

```java
ArrayList<String> nombres = new ArrayList<>();
nombres.add("Ana");
nombres.add("Luis");

// El for-each funciona porque ArrayList implementa Iterable
for (String nombre : nombres) {
    System.out.println(nombre);
}
```

El `Iterator<T>` expone tres métodos clave:

- **`hasNext()`:** devuelve `true` si quedan elementos por recorrer.
- **`next()`:** devuelve el siguiente elemento y avanza el cursor.
- **`remove()`:** elimina de forma segura el último elemento devuelto por `next()` (a diferencia de borrar directamente de la colección mientras se recorre, lo cual lanza `ConcurrentModificationException`).

```java
Iterator<String> it = nombres.iterator();
while (it.hasNext()) {
    String nombre = it.next();
    if (nombre.equals("Luis")) {
        it.remove(); // Forma segura de eliminar durante el recorrido
    }
}
```

### Implementando Iterable

Una clase propia puede hacerse recorrible con `for-each` implementando `Iterable<T>`:

```java
class ColeccionDeNombres implements Iterable<String> {
    private String[] nombres = {"Ana", "Luis", "Marta"};
    
    @Override
    public Iterator<String> iterator() {
        return new Iterator<String>() {
            private int indice = 0;
            
            @Override
            public boolean hasNext() {
                return indice < nombres.length;
            }
            
            @Override
            public String next() {
                return nombres[indice++];
            }
        };
    }
}
```

---

## Excepciones

Una **excepción** es un evento que interrumpe el flujo normal de ejecución del programa, generalmente causado por un error (dividir entre cero, acceder a un índice inexistente, un archivo que no existe, etc.). Java maneja las excepciones como **objetos**.

### Jerarquía de Excepciones

Todas las excepciones descienden de la clase `Throwable`, que se divide en dos grandes ramas:

- **`Error`:** problemas graves del entorno de ejecución (memoria agotada, fallo de la JVM) que normalmente **no** se manejan en el código de la aplicación.
- **`Exception`:** problemas que **sí** puede y debe manejar el programador.

```
Throwable
 ├── Error (ej: OutOfMemoryError)
 └── Exception
      ├── RuntimeException (unchecked)
      │    ├── NullPointerException
      │    ├── ArrayIndexOutOfBoundsException
      │    └── ArithmeticException
      └── (checked, ej: IOException)
```

### Checked vs Unchecked

- **Checked (verificadas):** el compilador **obliga** a manejarlas, ya sea con `try-catch` o declarándolas con `throws` en la firma del método. Ejemplo: `IOException`, `SQLException`. Representan condiciones externas previsibles (un archivo puede no existir).
- **Unchecked (no verificadas):** subclases de `RuntimeException`. El compilador **no obliga** a manejarlas. Suelen representar errores de programación (un `NullPointerException` normalmente indica un bug, no una condición esperada).

### try-catch-finally

```java
try {
    int resultado = 10 / 0; // Lanza ArithmeticException
} catch (ArithmeticException e) {
    System.out.println("Error: " + e.getMessage());
} finally {
    System.out.println("Esto se ejecuta siempre, haya error o no.");
}
```

- **`try`:** bloque donde puede ocurrir el error.
- **`catch`:** captura y maneja un tipo específico de excepción (se pueden encadenar varios `catch` para distintos tipos).
- **`finally`:** se ejecuta **siempre**, ocurra o no una excepción; ideal para liberar recursos (cerrar archivos, conexiones, etc.).

> [!info] Orden de los catch Los bloques `catch` de excepciones más específicas deben ir **antes** que los de excepciones más generales (ej: `ArithmeticException` antes que `Exception`), o el compilador dará error, ya que el `catch` general capturaría todo primero.

### try-with-resources

Simplifica el cierre de recursos (`AutoCloseable`, como archivos o conexiones) sin necesidad de un `finally` explícito. El recurso se cierra automáticamente al salir del bloque.

```java
try (FileReader lector = new FileReader("archivo.txt")) {
    // usar el recurso
} catch (IOException e) {
    System.out.println("No se pudo leer el archivo.");
}
// lector.close() se llama automáticamente aquí
```

### Excepciones Personalizadas

Se puede crear una excepción propia extendiendo `Exception` (checked) o `RuntimeException` (unchecked), útil para representar errores específicos del dominio de la aplicación.

```java
class SaldoInsuficienteException extends Exception {
    public SaldoInsuficienteException(String mensaje) {
        super(mensaje);
    }
}

class CuentaBancaria {
    private double saldo;
    
    public void retirar(double monto) throws SaldoInsuficienteException {
        if (monto > saldo) {
            throw new SaldoInsuficienteException("Saldo insuficiente para retirar " + monto);
        }
        saldo -= monto;
    }
}
```

---

## Hilos (Thread)

Un **hilo (`Thread`)** es una unidad de ejecución independiente dentro de un programa. Java es multihilo por diseño (como se menciona en [[#Motivaciones de su diseño:]]), lo que permite ejecutar varias tareas de forma concurrente dentro del mismo proceso.

### Creando un Hilo

Hay dos formas principales:

1. **Extender la clase `Thread`** y sobreescribir su método `run()`.

```java
class MiHilo extends Thread {
    @Override
    public void run() {
        System.out.println("Hilo ejecutándose: " + Thread.currentThread().getName());
    }
}

MiHilo hilo = new MiHilo();
hilo.start(); // NO se llama run() directamente
```

2. **Implementar la interfaz `Runnable`** (opción preferida, ya que Java solo permite herencia simple y así la clase queda libre para extender otra).

```java
class MiTarea implements Runnable {
    @Override
    public void run() {
        System.out.println("Tarea ejecutándose en un hilo.");
    }
}

Thread hilo = new Thread(new MiTarea());
hilo.start();
```

> [!info] start() vs run() Llamar a `run()` directamente **no crea un hilo nuevo**: simplemente ejecuta el método como código normal en el hilo actual. Solo `start()` le pide a la JVM que cree un hilo nuevo del sistema operativo y ejecute `run()` dentro de él.

### El Problema de la Concurrencia

Cuando **varios hilos acceden y modifican el mismo dato compartido** al mismo tiempo, pueden producirse resultados inconsistentes o impredecibles (condición de carrera o _race condition_), porque las operaciones de cada hilo pueden intercalarse de forma no controlada.

### synchronized

El modificador **`synchronized`** garantiza que **solo un hilo a la vez** pueda ejecutar un bloque de código o método sobre un mismo objeto, evitando condiciones de carrera.

```java
class Contador {
    private int valor = 0;
    
    public synchronized void incrementar() {
        valor++; // Solo un hilo a la vez puede ejecutar esta línea sobre el mismo objeto
    }
}
```

- **Método `synchronized`:** bloquea el objeto (`this`) completo mientras se ejecuta.
- **Bloque `synchronized(objeto)`:** permite sincronizar solo una parte del código, usando un objeto específico como "candado", lo cual suele ser más eficiente.

---

## String Pool y Pools de Wrappers

Java optimiza la memoria reutilizando objetos inmutables comunes mediante **pools (piscinas) de objetos**, en lugar de crear una instancia nueva cada vez que el valor ya existe.

### String Pool

El **String Pool** (o _String Constant Pool_) es una zona especial de memoria donde Java almacena literales de tipo `String`. Cuando se crea un `String` con comillas dobles (un literal), Java primero revisa si ya existe uno igual en el pool: si existe, reutiliza esa misma referencia; si no, lo crea y lo agrega al pool.

```java
String a = "Hola";
String b = "Hola";
System.out.println(a == b); // true -> misma referencia, ambos apuntan al pool

String c = new String("Hola");
System.out.println(a == c); // false -> new fuerza la creación de un objeto nuevo, fuera del pool
System.out.println(a.equals(c)); // true -> el contenido sí es igual
```

> [!info] == vs equals() `==` compara **referencias** (si es el mismo objeto en memoria). `equals()` compara **contenido**. Con `String`, esta distinción es crítica precisamente por la existencia del pool: dos literales iguales suelen compartir referencia, pero un `String` creado con `new` nunca la comparte automáticamente.

### Integer Cache

Java aplica una optimización similar con las [[#Clases Wrapper]] de tipos enteros pequeños. La clase `Integer` (y también `Short`, `Byte`, `Long`, `Character`) mantiene una **caché** de objetos ya creados para el rango de valores entre **-128 y 127**.

```java
Integer x = 100;
Integer y = 100;
System.out.println(x == y); // true -> ambos están dentro del rango cacheado (-128 a 127)

Integer m = 200;
Integer n = 200;
System.out.println(m == n); // false -> fuera del rango cacheado, son objetos distintos
```

Esto ocurre gracias al **autoboxing** ([[#Autoboxing y Unboxing]]): al escribir `Integer x = 100;`, Java internamente llama a `Integer.valueOf(100)`, y este método es el que consulta la caché antes de decidir si crea un objeto nuevo o reutiliza uno existente.

> [!info] Buena práctica Para comparar el **valor** de dos wrappers (`Integer`, `Long`, etc.), siempre se debe usar `.equals()` en lugar de `==`, ya que depender del rango cacheado es una fuente común de bugs sutiles.