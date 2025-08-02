# Modelización de Clases y Objetos

Continuando con la Programación Orientada a Objetos, una vez comprendida la estructura de una **clase** y un **objeto**, el siguiente paso fundamental es cómo los modelamos para que representen eficazmente el mundo real o el problema que queremos resolver. La **modelización** es el proceso de identificar las clases y objetos necesarios, definir sus atributos y comportamientos, y establecer las relaciones entre ellos, aún sin introducir la herencia.

<!-- @import "[TOC]" {cmd="toc" depthFrom=1 depthTo=6 orderedList=false} -->

<!-- code_chunk_output -->

- [Modelización de Clases y Objetos](#modelización-de-clases-y-objetos)
  - [Identificación de Clases y Objetos](#identificación-de-clases-y-objetos)
      - [¿Cómo identificamos clases?](#cómo-identificamos-clases)
    - [Definición de Atributos y Métodos](#definición-de-atributos-y-métodos)

<!-- /code_chunk_output -->



## Identificación de Clases y Objetos

El primer paso en la modelización es identificar las entidades clave en el dominio del problema. El dominio del problema se establece en el documento de Especificación de Requerimientos del Sistema (IEEE 830) o en documentos similares. Generalmente, las **clases** corresponden a sustantivos o conceptos abstractos importantes. Es muy similar al diagrama Entidad-Relación que se trabaja en bases de datos, pero en el diagrama de clases UML también modelizamos las acciones que realiza cada elemento.

  * **Clase:** Representa una categoría o un "plano" general para un conjunto de objetos que comparten características y comportamientos comunes.

      * **Ejemplos:** `Coche`, `Libro`, `Cliente`, `Factura`, `Producto`.

  * **Objeto (Instancia):** Es una ocurrencia concreta de una clase, con valores específicos para sus atributos.

      * **Ejemplos:** Un objeto `Coche` con color "rojo", marca "Ford", modelo "Fiesta". Un objeto `Libro` con título "Cien años de soledad" y autor "Gabriel García Márquez".

#### ¿Cómo identificamos clases?

1.  **Sustantivos:** Los sustantivos en la descripción del problema suelen ser buenos candidatos para clases.
2.  **Entidades tangibles:** Personas, lugares, cosas.
3.  **Conceptos abstractos:** Eventos, transacciones, roles.

### Definición de Atributos y Métodos

Una vez identificadas las clases, debemos determinar qué información almacenará cada objeto (sus **atributos**) y qué acciones podrá realizar (sus **métodos**).

  * **Atributos:** Son las propiedades o características que describen el estado de un objeto. Cada objeto de la misma clase tendrá los mismos atributos, pero con valores potencialmente diferentes.

      * **Ejemplo para la clase `Coche`:** `matricula` (string), `modelo` (string), `color` (string), `velocidadActual` (number).

  * **Métodos:** Representan las operaciones o comportamientos que un objeto puede llevar a cabo o que se pueden realizar sobre él. Los métodos suelen ser verbos o frases verbales.

      * **Ejemplo para la clase `Coche`:** `arrancar()` (void), `acelerar(incremento: number)` (void), `frenar()` (void), `obtenerVelocidad()` (number).

> **Actividad**
> Extrae y modela a partir del siguiente enunciado las posibles clases:
>
> Se nos pide un sistema para gestionar la entrega de diplomas de un instituto. Los diplomas se entregan a alumnos, identificados por su nombre y NIA, que cursan asignaturas, que se identifican por el nombre de la asignatura, su código y su curso académico. En un diploma se recoge la información básica sobre la asignatura y el alumno, añadiendo además una calificación. Un alumno puede matricularse en una asignatura y también darse de baja. Una asignatura puede ser modificada. Un diploma puede expedirse. 

