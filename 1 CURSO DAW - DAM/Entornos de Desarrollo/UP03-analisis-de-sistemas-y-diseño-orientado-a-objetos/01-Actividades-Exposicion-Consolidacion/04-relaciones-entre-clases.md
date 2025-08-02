# Relaciones entre clases


<!-- @import "[TOC]" {cmd="toc" depthFrom=1 depthTo=6 orderedList=false} -->

<!-- code_chunk_output -->

- [Relaciones entre clases](#relaciones-entre-clases)
  - [Relaciones de Herencia](#relaciones-de-herencia)
  - [Relaciones de componente](#relaciones-de-componente)
  - [Otras relaciones](#otras-relaciones)

<!-- /code_chunk_output -->



## Relaciones de Herencia

A través de los diagramas UML podemos expresar las relaciones entre las clases de múltiples maneras, mediante líneas que las unen. A su vez, también podemos especificar cardinalidades, como en los diagramas Entidad-Relación empleados en base de datos, para cuantificar los detalles de las relaciones, e incluso nombrar a dichas relaciones (generalmente con un verbo). Representamos las cardinalidades con 0, 1, muchos (representado a veces con `*` o una letra) o números fijos. Las clases se pueden relacionar entre ellas de las siguientes maneras:

- **Herencia:** "es un" (relación jerárquica). Una clase deriva de otra. La clase base se denomina a veces clase padre y la clase derivda clase hija. En algunos casos, la clase padre es una clase abstracta. Esto significa que la clase abstracta no puede ser instanciada, pero las derivadas (mientras no sean abstractas a su vez) sí. Las clases abstractas, a la hora de ser programadas, pueden tener métodos abstractos, que son métodos sin definir (se definen en las clases derivadas). Más adelante veremos que hay herencia simple y múltiple, así como otros tipos de herencia. 

![alt text](images/image-10.png)

<details>
<summary><b>Haz click aquí para ver el código plantuml</b></summary>

```plantuml
@startuml
class Persona{}
class Profesor{}
Persona<|--Profesor
@enduml
```
</details>

![alt text](images/image-11.png)

<details>
<summary><b>Haz click aquí para ver el código plantuml</b>
</summary>

```plantuml
@startuml
abstract class SerVivo{}
class Perro{}
class Persona{}
SerVivo <|--Persona
SerVivo <|--Perro
@enduml
```
</details>

## Relaciones de componente

- **Componente:** "tiene un". Una clase contiene como atributo un objeto (o varios) de otra.
- **Composición:** De tipo *componente*. En este caso, el atributo es dependiente de la clase principal.

![alt text](images/image-12.png)

<details>
<summary>
<b>Haz click aquí para ver el código plantuml</b>
</summary>

```plantuml
@startuml
class Persona{}
class Brazo{}
Persona "1" *-- "2" Brazo : tiene
@enduml
```

</details>

*Una persona tiene dos brazos. Los brazos no pueden existir sin la persona.*

- **Agregación:** De tipo *componente*. En este caso, el atributo no es dependiente de la clase principal y puede existir por separado.

![alt text](images/image-13.png)

<details>
<summary><b>Haz click aquí para ver el código plantuml</b></summary>

```plantuml
@startuml
class Persona{}
class Motocicleta{}
Persona "1" o-- "muchas" Motocicleta : Posee
@enduml
```
</details>

*Una persona posee muchas motocicletas. Cada motocicleta puede existir sin la persona.*

- **Asociación:** "colabora con". Dos clases pueden trabajar en colaboración. La colaboración puede ser simétrica o asimétrica (señalamos la dirección con una flecha). Aunque no es exactamente el mismo concepto, la asociación se puede usar de forma alternativa a la agregación y la composición. De hecho, muchas veces, el resultado al programarla será el mismo.

![alt text](images/image-14.png)

<details>
<summary><b>Haz click aquí para ver el código plantuml</b></summary>

```plantuml
@startuml
class Alumno{}
class Profesor{}
Profesor -- Alumno : Enseña >
@enduml
```

</details>


## Otras relaciones

Además de esas relaciones básicas, existen otras un poco más avanzadas.

- **Dependencia:** "usa". En este tipo de relación, se dice que una clase usa a otra. Este uso puede ser mediante clases que contengan otras clases o mediante la implementación de interfaces dentro de una clase. Se representa como la herencia, pero con línea discontinua. A efectos de programación, una interfaz y una clase abstracta son muy similares. En ambos casos, no permiten instancias de ellas, sino de clases derivadas o que las usen. En Java, las interfaces vienen a compensar las limitaciones que tiene el hecho de que no exista la herencia múltiple.

![alt text](images/image-15.png)

<details><summary><b>Haz clik aquí para verl el código plantuml</b></summary>

```plantuml
@startuml
skinparam classAttributeIconSize 0
interface PuedeMoverse{
    + mover() : void
}
class Persona{
    - nombre : string
    - edad : number
}
class Motocicleta{
    - cilindrada : string
    - matricula : string
}
Persona ..|> PuedeMoverse
Motocicleta ..|>PuedeMoverse
@enduml
```

</details>

Un uso muy habitual de las interfaces es el de agrupar instancias que semánticamente son cosas distintas, pero que todas pueden realizar la misma acción. De esta forma, les podemos pedir a todas ellas con un mensaje que realicen dicha acción, aunque sean cosas tan dispares como una puerta o un plazo de entrega (en ambos casos, se podrían cerrar).

- **Pertenencia al mismo paquete:** En caso de que queramos especificar también los paquetes, podemos encapsular las clases en formas geométricas para verlo claro, de la siguiente manera:

![alt text](images/image-16.png)

<details>
<summary><b>Haz click aquí para ver el código plantuml
</b></summary>

```plantuml
@startuml

package animales{
    abstract class Animal{}
    package mamiferos{
        class Perro{}
        class Gato{}
    }
    package aves{
        class Periquito{}
        class Loro{}
    }
}
package vehiculos{
    class Motocicleta{}
    class Coche{}
    class CocheElectrico{}
    class Avion{}
}
package utilidades{
    interface PuedeVolar{}
}
Perro --|> Animal
Gato --|> Animal
Periquito --|> Animal
Loro --|> Animal
CocheElectrico --|> Coche
Periquito ..|> PuedeVolar
Loro ..|> PuedeVolar
Avion ..|> PuedeVolar

@enduml
```
</details>

Como se puede observar, puede haber paquetes dentro de paquetes y las clases de un paquete pueden relacionarse con clases de otros paquetes. Los paquetes tienen una relación más de conveniencia a la hora de programar que semántica. 

> **Actividad**
> Explica el siguiente diagrama:

![alt text](images/image-17.png)

<details>
<summary><b>Haz click aquí para ver el código plantuml
</b></summary>

```plantuml
@startuml
skinparam classAttributeIconSize 0
package animales{
class Persona{
    + hablar()
}
class Perro{
    + ladrar()
}
}
package utilidades{
class Aspiración{
    - descripción : string
}
abstract class SerVivo{
    # edad : number
    # nombre : string
    # respirar() : void
}
package caracteristicas{
class Extremidad{
    - peso : number
}
interface Respira{}
}
}

SerVivo "1" *-- "*" Extremidad : tiene
SerVivo ..|> Respira
Persona --|> SerVivo
Perro --|> SerVivo
Persona "1" *-- "*" Aspiración
Persona "1" o-- "1" Perro : tiene
@enduml
```
</details>

> **Actividad** 
>Crea un diagrama de la siguiente explicación
>
>La vida es dura, pero la vida de cada persona tiene un grado de dureza diferente, que clasificamos con un número. Las personas asismo tienen algo que las identifica, su propio nombre. Pueden elegir varias profesiones, como carpintero o influencer. Los carpinteros usan la madera para construir muebles. Los influencer usan las mesas, que son muebles, para poner sus ordenadores. Una persona puede tener varios muebles. Las sillas también son muebles.