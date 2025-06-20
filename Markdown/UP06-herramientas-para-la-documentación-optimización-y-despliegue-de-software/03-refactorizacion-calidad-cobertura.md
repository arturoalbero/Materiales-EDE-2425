<style>
body{
    text-align: justify
}
</style>
# Refactorización y patrones de diseño

## 1. Refactorización de código

En ingeniería del software, la refactorización se refiere frecuentemente a una actualización del código que no afecta a su comportamiento, lo que también se conoce como limpieza del código. La refactorización se utiliza como parte del proceso de desarrollo de software: los desarrolladores a veces añaden nuevas funcionalidades y casos de prueba, y otras veces refactorizan su código para hacerlo más claro y robusto. En este caso, ejecutar las pruebas de nuevo puede demostrar que la refactorización no ha cambiado el comportamiento de la aplicación.

Por tanto, la refactorización es una parte del mantenimiento de software que no corrige ningún error ni añade ninguna funcionalidad nueva. El objetivo principal es mejorar la comprensión del código o cambiar su estructura para facilitar su mantenimiento futuro. A veces es difícil añadir nuevas funcionalidades a un programa con su estructura de código actual, por lo que un desarrollador puede refactorizarlo antes de añadir más código nuevo.

### 1.1. ¿Por qué refactorizar?

Hay muchas razones por las que deberíamos usar esta técnica:

- **Calidad**. Es la razón principal. La refactorización es una reflexión continua sobre nuestro código en un entorno donde no tenemos demasiado tiempo para mirar atrás. Un buen código es simple y está bien estructurado, y cualquiera puede leerlo y entenderlo sin formar parte del equipo de desarrollo. No deberíamos volver a esos programas escritos en una sola línea, donde la concisión era mejor que la legibilidad.

- **Eficiencia**. Mantener un buen diseño y un código estructurado es la forma más eficiente de desarrollar un programa. El esfuerzo que ponemos en evitar código duplicado y simplificar el diseño se recuperará cuando necesitemos hacer modificaciones posteriores, ya sea para corregir errores o para añadir nuevas funcionalidades.

- **Diseño evolutivo**. En lugar de un Gran Diseño inicial, a veces los requisitos no están claramente especificados al principio, por lo que debemos enfrentarnos al diseño gradualmente. Se pueden añadir nuevas funcionalidades mientras implementamos el proyecto, por lo que el diseño inicial puede volverse inútil. La refactorización nos permite hacer evolucionar el diseño a medida que nuevas funcionalidades se unen a las antiguas. Esto a menudo implica cambios importantes en la arquitectura del proyecto.

- **Evitar reescribir código**. En la mayoría de los casos, refactorizar es mejor que reescribir. No es fácil enfrentarse a un código que no es nuestro y que no sigue nuestros estándares, pero esto no es una buena razón para empezar desde cero. Especialmente en un entorno donde el ahorro de costes lo hace imposible. De todos modos, actualizar nuestro código no siempre es necesario. Debe haber una buena razón, y solo necesitamos hacer una actualización si hay un mal diseño que dificulte desarrollos futuros. Siempre que notemos que nuestro código es difícil de entender, o que hay código duplicado, entonces necesitamos refactorizarlo. A veces puede que necesitemos dar un paso atrás y replantearnos algunos aspectos, para poder avanzar de forma rápida y sencilla.

### 1.2. ¿Cuándo refactorizar?
Refactorizar el código no se debe a razones estéticas. Debemos prestar atención a algunas situaciones en las que es mejor parar y reorganizar nuestro código. Los elementos que nos avisan de que nuestro código está en problemas se conocen como Malos Olores. Un programador experimentado puede determinar que su programa empieza a "oler mal" cuando hay:

- **Identificadores ambiguos**. Pueden ser nombres de variables, clases o métodos. Necesitaremos renombrarlos para clarificar nuestro código. Por ejemplo, podemos renombrar una variable llamada `t` por otra llamada `waitTime`.

- **Código duplicado**. Esta es la principal razón para refactorizar nuestro código. Si detectamos el mismo fragmento de código en más de un lugar, necesitamos unificarlo.

- **Método largo**. Esta es una característica muy habitual de la programación estructurada, pero en programación orientada a objetos, cuanto más corto es un método, más fácil es usarlo. Así que podemos dividir el programa principal en subprogramas.

- **Clase grande**. Si una sola clase intenta resolver demasiados problemas, también puede tener demasiadas variables de instancia, lo que puede llevar a código duplicado.

- **Lista larga de parámetros**. No deberíamos pasar demasiados parámetros a nuestros métodos. Solo deberíamos usar los realmente necesarios para que el método complete su tarea. Aquellos métodos que reciben demasiados parámetros de entrada cambian su comportamiento muy a menudo y se vuelven muy difíciles de entender.

- **Envidia de funcionalidad (*feature envy*)**. Ocurre cuando un método usa más elementos de otra clase que de su propia clase. Este problema se suele resolver moviendo este método a la otra clase.

Por tanto, debemos tener en cuenta estos factores mientras implementamos el programa, para poder refactorizarlo y evitar estas situaciones. Veamos este ejemplo:

```java
public class NoRefactor
{
    public static void main(String[] args) 
    {
        int sum1 = 0, sum2 = 0, result = 0;
        int array1[] = {1,2,3,4}, array2[] = {5,6,7,8};

        for(int i = 0; i < array1.length; i++)
        {
            sum1 += array1[i];
        }
        result += sum1/array1.length;

        for(int i = 0; i < array2.length; i++)
        {
            sum2 += array2[i];
        }
        result += sum2/array2.length;

        System.out.println("The result is: " + result);
    }
}
```

Podemos encontrar fácilmente código duplicado en este ejemplo, así que podemos refactorizarlo así:

```java
public class Refactor 
{
    public static int calculateResult(int []array) 
    {
        int sum = 0;
        for(int i = 0; i < array.length; i++) 
        {
            sum += array[i];
        }
        return sum/array.length;
    }

    public static void main(String args) 
    {
        int array1[] = {1,2,3,4}, array2[] = {5,6,7,8};
        int result = 0;

        result = calculateResult(array1);
        result += calculateResult(array2);

        System.out.println("The result is: " + result);
    }
}
```

Ahora veamos este código:

```java
import java.io.BufferedReader;
import java.io.IOException;
import java.io.InputStreamReader;

public class LongMethod 
{
    public static void main(String args[])
    {
        int array[] = new int[10];
        BufferedReader input = new BufferedReader(
            new InputStreamReader(System.in));
        int result = 0;

        // Inicialización del array
        for(int i = 0; i < array.length; i++)
        {
            System.out.printf("Introduce valor para array[%d]", i);
            try 
            {
                array[i] = Integer.valueOf(input.readLine());
            } catch (IOException e) {
                err.println("Error: " + e.getMessage());
            }
        }

        // Suma del array
        System.out.println("Suma: ");
        for(int i = 0; i < array.length; i++)
        {
            result = result + array[i];
            System.out.print(array[i] + " " + 
                (i==array.length-1?" ":"+ "));
        }
        System.out.println("= " + result);
    }
}
```

El método `main` es demasiado grande, y podemos dividirlo en funciones:

```java
import java.io.BufferedReader;
import java.io.IOException;
import java.io.InputStreamReader;

public class NoLongMethod 
{
    public static int[] initialize()
    {
        int array[] = new int[10];
        
        BufferedReader input = new BufferedReader(
            new InputStreamReader(System.in));

        for(int i = 0; i < array.length; i++)
        {
            System.out.printf("Introduce valor para array[%d]", i);
            try 
            {
                array[i] = Integer.valueOf(input.readLine());
            } catch (IOException e) {
                err.println("Error: " + e.getMessage());
            }
        }

        return array;
    }

    public static void sumArray(int[] array)
    {
        int result = 0;

        System.out.println("Suma: ");

        // Suma del array
        for(int i = 0; i < array.length; i++)
        {
            result = result + array[i];
            System.out.print(array[i] + " " + 
                (i==array.length-1?" ":"+ "));
        }
        System.out.println("= " + result);
    }

    public static void main(String args[])
    {
        int[] array = initialize();
        sumArray(array);
    }
}
```

### 1.3. Refactorización en IntelliJ
En IntelliJ, podemos encontrar un menú principal Refactorizar con algunas opciones para refactorizar nuestro código. También podemos hacer clic derecho sobre cualquier elemento del código (variable, método, nombre de clase...) y elegir la opción Refactorizar. Con estas opciones podemos:

- **Refactorizar > Renombrar**: Renombrar variables, clases, métodos... y aplicar estos cambios a todo el código.
- **Refactorizar > Mover**: Mover clases/miembros de un paquete/clase a otro.
- **Refactorizar > Introducir constante**: Convertir un número o cadena literal en una constante.
- **Refactorizar > Introducir campo**: Transformar una variable local en un atributo privado de la clase.
- **Refactorizar > Extraer interfaz**: Extraer una interfaz de los métodos de una clase.
- **Refactorizar > Extraer superclase**: Extraer una superclase con métodos que pertenecerán a esta superclase.

[Más adelante en el documento](#4-herramientas-para-el-análisis-de-código-y-la-refactorización-en-intellij-community-edition) las trataremos con más detalle.



### 3.2 Conceptos clave de calidad del código

**Acoplamiento (Coupling)**:
- **Definición**: Grado de interdependencia entre módulos/clases.
- **Tipos**:
  - *Bajo acoplamiento* (deseable): Los cambios en un módulo afectan mínimamente a otros.
  - *Alto acoplamiento*: Cambios se propagan fácilmente, haciendo el sistema frágil.
- **Estrategias para reducirlo**:
  - Usar interfaces en lugar de implementaciones concretas
  - Aplicar el Principio de Inversión de Dependencias (DIP)
  - Limitar la visibilidad de clases/métodos (encapsulación)

**Cohesión**:
- Mide cuán relacionadas están las responsabilidades dentro de un módulo.
- *Alta cohesión* (ideal): Cada clase/método tiene una única responsabilidad clara.
- *Baja cohesión*: Las clases/métodos hacen demasiadas cosas no relacionadas.

**Fan-in/Fan-out**:
- **Fan-in**: Número de clases que dependen de una clase dada (alto fan-in sugiere utilidad general).
- **Fan-out**: Número de clases de las que depende una clase dada (alto fan-out sugiere complejidad).
- **Relación saludable**:
  - Alto fan-in + bajo fan-out = Diseño estable (clases base bien abstraídas)
  - Bajo fan-in + alto fan-out = Posible diseño frágil

**Deuda técnica**:
- Costo implícito en elegir soluciones rápidas pero subóptimas.
- La refactorización es el principal método para "pagar" esta deuda.

## 4. Herramientas para el análisis de código y la refactorización en IntelliJ Community Edition

IntelliJ provee al desarrollador de una serie de herramientas muy útiles para analizar el código y facilitar la refactorización. La mayoría de estas herramientas están disponibles en la versión Ultimate, que es muy poderosa pero de pago, pero la versión Community Editon, gratuita, incluye las más básicas, que no por ello son menos interesantes. A continuación, vamos a repasar algunas de estas herramientas:

### **4.1. Inspección Básica de Código** *(Sí incluido)*

- **Marcado en tiempo real** de:
  - Errores de sintaxis *(rojo)*.
  - Advertencias *(amarillo)*: variables sin usar, métodos largos, etc.
  - Sugerencias de optimización *(azul/verde)*.
- **Acción clave**: `Alt + Enter` sobre código subrayado para correcciones rápidas.

### **4.2. Refactorización Esencial** *(Sí incluido)*

| Operación                | Atajo           | Uso típico                     |
|--------------------------|-----------------|--------------------------------|
| Renombrar                | `Shift + F6`    | Cambiar nombres de clases/métodos/variables con actualización automática en todo el proyecto. |
| Extraer método           | `Ctrl + Alt + M`| Convertir fragmentos de código en métodos reutilizables. |
| Extraer variable/constante| `Ctrl + Alt + V/C` | Simplificar expresiones complejas. |
| Mover clase              | `F6`            | Reubicar archivos entre paquetes. |

### **4.3. Búsqueda de Problemas** *(Sí incluido, pero limitado)*

- **`Analyze > Inspect Code`**:
  - Detecta *code smells* básicos (código duplicado simple, métodos demasiado largos).
  - **Limitación**: No tiene detección avanzada de patrones complejos.

### 4.4 **Herramientas NO Incluidas en Community**

| Función                  | Alternativa Gratuita                          |
|--------------------------|-----------------------------------------------|
| Diagramas UML            | Usar [PlantUML](https://plantuml.com/) con plugin |
| Análisis de dependencias | Plugins como **SonarLint** o **Dependabot**   |
| Métricas avanzadas       | Plugins: **Statistic** (contar líneas/clases) |

Los comandos pueden variar entre Sistemas Operativos, pero en los menús están disponibles para consultar. Aparte, siempre se puede leer la documentación oficial.

***Fuentes:***
- Primera sección traducida y adaptada de [aquí](https://nachoiborraies.github.io/java/md/en/05f).
- [Jetbrains](https://www.jetbrains.com/es-es/).
- [IONOS.](https://www.ionos.es/digitalguide/paginas-web/desarrollo-web/que-es-la-refactorizacion/)
- [Artículo de GVA sobre refactorización en el que se basa la fuente inicial.](https://mestreacasa.gva.es/c/document_library/get_file?fname=WillyDev_Refactorizacion%5B1%5D.pdf&uuid=e8f9dc54-fe95-463e-a3b1-bc543d3fc9f9&groupId=4700530668)
- [Acoplamiento.](https://es.wikipedia.org/wiki/Acoplamiento_(inform%C3%A1tica))