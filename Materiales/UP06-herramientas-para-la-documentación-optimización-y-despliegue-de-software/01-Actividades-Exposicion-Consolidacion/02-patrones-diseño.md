# Patrones de diseño

## Patrones de diseño
Existen algunas técnicas útiles que podemos aplicar cuando necesitamos refactorizar nuestro código: los patrones de diseño. Son soluciones repetibles para un problema en el diseño de software.

Las principales ventajas de usar patrones de diseño son:

- Constituyen un amplio catálogo de soluciones a problemas.
- Estandarizan cómo resolver algunos problemas dados.
- Simplifican el aprendizaje de buenas prácticas de programación.
- Proporcionan un vocabulario común entre desarrolladores.
- Evitan reinventar la rueda.

### Tipos de patrones de diseño
Según su propósito, podemos dividir los patrones de diseño en estas categorías:

- **Patrones creacionales**: Encapsulan la lógica de la instanciación de objetos, ocultando los detalles concretos de cada objeto. Así, podemos trabajar solo con abstracciones.
- **Patrones estructurales**: Nos ayudan a definir cómo se componen los objetos.
- **Patrones de comportamiento**: Nos ayudan a definir cómo interactúan los objetos entre sí.

### Patrón Factory (Fábrica)
El patrón Factory es uno de los patrones más usados en Java. Es un patrón creacional que proporciona una de las mejores formas de crear objetos. Usar este patrón nos permite crear objetos sin mostrar la lógica de creación al usuario. Solo usamos una interfaz común.

Por ejemplo, volvamos al ejemplo de Figuras de documentos anteriores. Teníamos una interfaz `Shape` que era implementada por algunas clases, como `Circle`, `Square` o `Rectangle`. Cada vez que queríamos crear un objeto, teníamos que llamar a un constructor concreto:

```java
Shape myShape = new Circle(3);
...
Shape myShape2 = new Square(5);
...
myShape.draw();
...
```

Por tanto, el desarrollador debe conocer el nombre de cada clase que implementa la interfaz `Shape`. Pero si usamos el patrón Factory, podemos encapsular todas las formas posibles de crear una figura, de modo que solo necesitemos especificar qué figura necesitamos, y el patrón proporcionará una instancia de la figura concreta.

El primer paso es definir la fábrica de figuras. Esto normalmente consiste en crear una nueva clase con un método estático que se encarga de crear los objetos de una clase o jerarquía de clases dada. En nuestro caso, definimos un método estático para crear subtipos de `Shape`:

```java
public class ShapeFactory 
{
    public static Shape getShape(ShapeType type, float param1, float param2)
    {
        if(type == ShapeType.CIRCLE){
            return new Circle(param1);            
        } else if(type == ShapeType.RECTANGLE){
            return new Rectangle(param1,param2);
        } else if(type == ShapeType.SQUARE){
            return new Square(param1);
        }

        return null;
    }
}
```

De este modo, si queremos crear una instancia de cualquier figura, solo necesitamos llamar a esta fábrica con el nombre de la figura que queremos crear y sus parámetros:

```java
Shape shape1 = ShapeFactory.getShape(ShapeType.CIRCLE,3, 0);
shape1.draw();
System.out.println(shape1.calculateArea());
```

Respecto a `ShapeType`, es solo un enum donde podemos especificar todos los subtipos que queremos manejar:

```java
public enum ShapeType { CIRCLE, SQUARE, RECTANGLE }
```

Desde el punto de vista del desarrollador, solo hay una clase (o interfaz, en este caso), que es "Shape", y no necesita saber nada sobre el resto de clases implementadoras. Este patrón de diseño es realmente útil cuando hay una jerarquía de clases compleja con un patrón de instanciación común (parámetros similares), o un gran conjunto de clases que son muy similares e implementan la misma interfaz padre o clase abstracta, como podemos ver en el siguiente ejemplo.

Tenemos una empresa que vende algunos productos. Debemos aplicar el IVA general a algunos productos, y un IVA reducido a otros. Así que empezamos definiendo una clase abstracta llamada `Invoice` con dos subclases para representar estos dos tipos de IVA.

```java
public abstract class Invoice 
{
    private int id;
    private double amount;

    public int getId() 
    {
        return id;
    }

    public void setId(int id)
    {
        this.id = id;
    }

    public double getAmount() 
    {
        return amount;
    }

    public void setAmount(double amount) 	
    {
        this.amount = amount;
    }

    public abstract double getAmountVAT();
}
```

Estas son las subclases:

```java
public class InvoiceVAT extends Invoice
{
    @Override
    public double getAmountVAT() 
    {
        return getAmount()*1.21;
    }
}

public class InvoiceVATReduced extends Invoice
{
    @Override
    public double getAmountVAT()
    {
        return getAmount()*1.10;
    }
}
```

De este modo, podemos definir un enum `InvoiceType` para identificar los tipos de enum:

```java
public enum InvoiceType { NORMAL, REDUCED }
```

Y también una clase `InvoiceFactory` para crear uno de los tipos de factura dependiendo de los parámetros:

```java
public class InvoiceFactory 
{
    public static Invoice getInvoice(InvoiceType type)
    {
        if (type == InvoiceType.NORMAL)
        {
            return new InvoiceVAT();
        } else if (type == InvoiceType.REDUCED) {
            return new InvoiceVATReduced();
        } else {
            return null;
        }
    }
}
```

Finalmente, podemos usar esta fábrica para crear las facturas:

```java
Invoice myInvoice = FactoryInvoice.getInvoice(InvoiceType.NORMAL);
Invoice myInvoiceRed = FactoryInvoice.getInvoice(InvoiceType.REDUCED);

myInvoice.setId(1);
myInvoice.setAmount(1000);

myInvoiceRed.setId(2);
myInvoiceRed.setAmount(500);

System.out.println(myInvoice.getAmountVAT());
System.out.println(myInvoiceRed.getAmountVAT());
```

> **Actividad:**
>
> Crea un nuevo proyecto llamado Facturas con los paquetes `facturas.tipos` para los tipos de factura, y `facturas.principal` con la clase principal. Implementa las clases del ejemplo de facturas anterior, y añade un nuevo tipo de factura con un IVA superreducido (4%).

### Patrón Singleton

Cuando trabajamos la programación orientada a objetos y, concretamente, los métodos y atributos estáticos, vimos cómo implementar este patrón de diseño. Es un buen momento para repasarlo.

Este patrón también es un patrón creacional que nos permite gestionar solo un único objeto de una clase dada. Se usa comúnmente en clases que almacenan parámetros de configuración para una aplicación dada, de modo que solo debe haber un objeto de este tipo para toda la aplicación, y este objeto debe compartirse entre todos los componentes de la aplicación.

El patrón Singleton consiste en tener una instancia estática de la propia clase, que se devolverá cada vez que pidamos una nueva instancia desde cualquier parte del código. También habrá un constructor privado que se llamará solo una vez para crear el atributo estático la primera vez que se necesite.

Por ejemplo, si tenemos una clase para contar el número total de facturas:

```java
public class InvoiceCounter
{
    private int counter;

    public void increaseCounter()
    {
        counter++;
    }

    public int getCounter()
    {
        return counter;
    }
}
```

Podemos añadir un atributo (privado) estático que apunte a la misma clase:

```java
private static InvoiceCounter myCounter;
```

Y un constructor privado:

```java
private InvoiceCounter()
{
    this.counter = 0;
}
```

Para tener una instancia de esta clase, necesitamos añadir un método público y estático, como `getInstance` o, en este caso, `getCounter`:

```java
public static InvoiceCounter getInvoiceCounter()
{
    if(myCounter == null)
    {
        myCounter = new InvoiceCounter();
    }
    return myCounter;
}
```

Entonces, solo habrá una única instancia de este objeto en el sistema. Si queremos usarlo para tratar algunas facturas, podemos hacerlo así:

```java
public static void main(String[] args) 
{
    InvoiceCounter counter = InvoiceCounter.getCounter();
    Invoice myInvoice = 
        InvoiceFactory.getInvoice(InvoiceType.NORMAL);
    Invoice myInvoiceRed = 
        InvoiceFactory.getInvoice(InvoiceType.REDUCED);

    counter.increaseCounter();
    myInvoice.setId(counter.getCounter());
    myInvoice.setAmount(1000);

    counter.increaseCounter();
    myInvoiceRed.setId(counter.getCounter());
    myInvoiceRed.setAmount(500);

    System.out.println(myInvoice.getAmountVAT());
    System.out.println(myInvoiceRed.getAmountVAT());
}
```

>**Actividad:**:
>
>Añade la clase `InvoiceCounter` al proyecto Facturas iniciado en la actividad anterior. Realiza los cambios apropiados para aumentar automáticamente el contador de facturas tan pronto como instanciemos una nueva factura desde `InvoiceFactory`, para que no necesitemos aumentarlo manualmente desde el método principal, como hicimos en el ejemplo anterior.

Aunque el patrón singleton es muy útil para almacenar datos globales y de configuración, no está exento de problemas:

- **Dificultad para el testeo y el mantenimiento:** La naturaleza global de la instancia puede complicar las pruebas unitarias, ya que introduce un acoplamiento fuerte. El acoplamiento ocurre cuando un módulo o clase es altamente dependiente de otro, es decir, necesita conocer detalles específicos de la implementación del otro para funcionar y, por lo tanto, es más complejo de mantener.
- **Problemas de concurrencia:** En entornos multihilo, puede haber problemas si no se maneja adecuadamente el acceso a la instancia. Esto se soluciona con los mecanismos propios de la programación concurrente, pero añaden complejidad a la ejecución del programa.

> **Actividad**
>
>La clase `Biblioteca` contiene diez estanterías, numeradas del 1 al 10. Añade este atributo a la clase `Estanteria`. Solo existe una biblioteca. La biblioteca permite hacer las siguientes cosas:
>
>- Añadir libros nuevos. Se añaden a la primera estantería disponible. Devuelve falso si la biblioteca está llena.
>- Añadir libros nuevos a estanterías concretas. Devuelve falso si la estantería no tiene hueco.
>- Eliminar un libro. Se le pasa el isbn del libro y, si está, devuelve verdadero y lo elimina. Si no está, devuelve falso.
>- Cambiar un libro de estantería. Se le pasa el isbn del libro y el número de la estantería. Devuelve verdadero si se puede cambiar o si ya estuviera en la estantería. Devuelve falso si la estantería nueva está llena o si el libro no existe en la biblioteca.
>- Mejora el método anterior con un enum que indique lo que ha pasado en cada caso.
>- Intercambia dos libros de estantería. Recibe como parámetro el isbn de los dos libros y devuelve verdadero si el cambio es posible y falso si no lo es (por ejemplo, porque un libro no existe en la librería).
>- Un método que, dado el isbn o el título de un libro, te devuelva la estantería en la que se encuentra.
>- Un método que te devuelva el libro con más páginas.
>- Un método que te devuelva la primera estantería con más libros.
>- Un método que te devuelva la primera estantería con más páginas.
>- Cambia el main para que realice las siguientes acciones:
>   - Primero consigue el acceso a la biblioteca.
>   - Después te pide introducir todos los libros secuencialmente.
>   - Después te pide eliminar 5 libros. Detecta si hay algún problema.
>   - Después te pide introducir 5 libros en distintas estanterías. Detecta si hay algún problema.
>   - Después te pide cambiar 4 libros de estantería. Detecta si hay algún problema.
>   - Después te pide intercambiar libros 2 veces. Detecta si hay algún problema.
>   - Muestra la biblioteca entera en formato csv.
>   - Finalmente, muestra el libro con más páginas y en qué estantería se encuentra; muestra la estantería con más libros y también la estantería con más páginas.

### Pruebas unitarias con singleton

Para ejecutar pruebas unitarias con singleton, debemos "trampear" el singleton. Una técnica sencilla es crear un método para restablecer la instancia, para así poder controlar de forma precisa qué datos tiene la instancia en cada momento. Este método es tan sencillo como lo que sigue:

```java
public static void resetInstancia() {
        instancia = null;
    }
```
> **Actividad**
> Crea un conjunto de pruebas unitarias para todos los métodos de la clase `Biblioteca`.




