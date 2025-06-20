<style> body{
    text-align: justify;
    }
    p{
        text-indent: 2rem;
    } 
</style>

# **Tutorial: Desarrollo Basado en Pruebas (TDD) con Cucumber, IntelliJ y Maven**  

En este tutorial, aprenderás a utilizar **Cucumber** en **IntelliJ IDEA** con **Maven** para desarrollar una aplicación siguiendo el enfoque **TDD (Desarrollo Basado en Pruebas)**.  

Siguiendo este método, primero escribiremos las pruebas en **lenguaje natural (Gherkin)**, luego implementaremos la lógica en Java para hacer que las pruebas pasen.  

---

## **1. Crear el Proyecto en IntelliJ con Maven**  

1. Abre **IntelliJ IDEA** y selecciona **New Project**.  
2. Elige **Maven** como gestor de dependencias.  
3. En **GroupId**, escribe: `com.ejemplo`.  
4. En **ArtifactId**, escribe: `calculadora-cucumber`.  
5. Haz clic en **Finish**.  

El proyecto tendrá esta estructura inicial:  
```
calculadora-cucumber
│── src
│   ├── main
│   │   └── java
│   │       └── com.ejemplo
│   │           └── Calculadora.java
│   ├── test
│   │   ├── java
│   │   │   └── com.ejemplo
│   │   │       ├── RunCucumberTest.java
│   │   │       ├── StepDefinitions.java
│   │   └── resources
│   │       └── features
│   │           └── calculadora.feature
│── pom.xml
│── .gitignore
```

---

## **2. Agregar Dependencias de Cucumber**  

Edita el archivo `pom.xml` y agrega las siguientes dependencias para **Cucumber y JUnit**:  

```xml
<dependencies>
    <!-- Cucumber Core -->
    <dependency>
        <groupId>io.cucumber</groupId>
        <artifactId>cucumber-java</artifactId>
        <version>7.14.0</version>
    </dependency>

    <!-- Cucumber JUnit -->
    <dependency>
        <groupId>io.cucumber</groupId>
        <artifactId>cucumber-junit</artifactId>
        <version>7.14.0</version>
        <scope>test</scope>
    </dependency>

    <!-- JUnit 5 -->
    <dependency>
        <groupId>org.junit.jupiter</groupId>
        <artifactId>junit-jupiter</artifactId>
        <version>5.9.2</version>
        <scope>test</scope>
    </dependency>

    <!-- Plugin para ejecutar pruebas -->
    <dependency>
        <groupId>org.apache.maven.plugins</groupId>
        <artifactId>maven-surefire-plugin</artifactId>
        <version>3.0.0-M7</version>
    </dependency>
</dependencies>
```

Ejecuta en la terminal de IntelliJ:  
```sh
mvn clean install
```
para descargar las dependencias.

---

## **3. Escribir Escenarios de Prueba en Gherkin**  

Creamos el archivo `src/test/resources/features/calculadora.feature` con los escenarios en **Gherkin**:  

```gherkin
Feature: Calculadora
  Como usuario, quiero realizar operaciones matemáticas básicas
  para obtener resultados correctos.

  Scenario: Sumar dos números
    Given que tengo una calculadora
    When sumo 2 y 3
    Then el resultado debe ser 5

  Scenario: Restar dos números
    Given que tengo una calculadora
    When resto 5 y 2
    Then el resultado debe ser 3
```

**Explicación:**  
- `Given` establece el estado inicial.  
- `When` define la acción.  
- `Then` verifica el resultado esperado.  

---

## **4. Implementar la Clase `Calculadora.java`**  

Creamos la clase en `src/main/java/com/ejemplo/Calculadora.java`:  

```java
package com.ejemplo;

public class Calculadora {
    public int sumar(int a, int b) {
        return a + b;
    }

    public int restar(int a, int b) {
        return a - b;
    }
}
```

---

## **5. Implementar los Step Definitions**  

Creamos la clase `StepDefinitions.java` en `src/test/java/com/ejemplo/StepDefinitions.java`:  

```java
package com.ejemplo;

import io.cucumber.java.en.Given;
import io.cucumber.java.en.When;
import io.cucumber.java.en.Then;
import static org.junit.jupiter.api.Assertions.*;

public class StepDefinitions {
    private Calculadora calculadora;
    private int resultado;

    @Given("que tengo una calculadora")
    public void queTengoUnaCalculadora() {
        calculadora = new Calculadora();
    }

    @When("sumo {int} y {int}")
    public void sumo(int a, int b) {
        resultado = calculadora.sumar(a, b);
    }

    @When("resto {int} y {int}")
    public void resto(int a, int b) {
        resultado = calculadora.restar(a, b);
    }

    @Then("el resultado debe ser {int}")
    public void elResultadoDebeSer(int esperado) {
        assertEquals(esperado, resultado);
    }
}
```

---

## **6. Configurar el Runner de Pruebas**  

Creamos la clase `RunCucumberTest.java` en `src/test/java/com/ejemplo/RunCucumberTest.java`:  

```java
package com.ejemplo;

import org.junit.platform.suite.api.*;

@Suite
@IncludeEngines("cucumber")
@SelectClasspathResource("features")
@ConfigurationParameter(key = "cucumber.glue", value = "com.ejemplo")
public class RunCucumberTest {
}
```

---

## **7. Ejecutar las Pruebas con Maven**  

Para ejecutar las pruebas, usa el siguiente comando en la terminal:  

```sh
mvn test
```

Si todo está configurado correctamente, deberías ver un resultado similar a este:  

```
[INFO] Running com.ejemplo.RunCucumberTest
Feature: Calculadora

  Scenario: Sumar dos números
    Given que tengo una calculadora
    When sumo 2 y 3
    Then el resultado debe ser 5

  Scenario: Restar dos números
    Given que tengo una calculadora
    When resto 5 y 2
    Then el resultado debe ser 3

[INFO] Tests run: 2, Failures: 0, Errors: 0, Skipped: 0
```

Esto indica que las pruebas han pasado correctamente.  

---

## **8. Añadir CI/CD con GitHub Actions (Opcional)**  

Si deseas integrar **GitHub Actions** para ejecutar pruebas en cada cambio de código, crea el archivo `.github/workflows/test.yml`:  

```yaml
name: Run Cucumber Tests

on:
  push:
    branches:
      - main
  pull_request:
    branches:
      - main

jobs:
  test:
    runs-on: ubuntu-latest

    steps:
      - name: Clonar repositorio
        uses: actions/checkout@v4

      - name: Configurar JDK 17
        uses: actions/setup-java@v3
        with:
          distribution: 'temurin'
          java-version: '17'

      - name: Construir y ejecutar pruebas
        run: mvn clean test
```

Con esto, GitHub ejecutará automáticamente las pruebas en cada push.  

## Herramientas CASE

Las **herramientas CASE** (**Computer-Aided Software Engineering**) son programas diseñados para asistir en el desarrollo de software, especialmente en las etapas de análisis, diseño, implementación, prueba y mantenimiento. Ayudan a automatizar y estandarizar muchas de las tareas repetitivas y complejas del ciclo de vida del software, lo que mejora la eficiencia y la calidad del desarrollo.

En el contexto de los alumnos que usan **Java**, **IntelliJ IDEA**, **Maven**, **Mockito**, **Cucumber**, **GitHub Actions**, y que están familiarizados con **Office 365** y **Visual Paradigm Online**, las herramientas CASE pueden clasificarse de acuerdo a las fases del ciclo de vida del desarrollo de software en las que se utilizan.

### **Clasificación de las Herramientas CASE**

#### **1. Herramientas CASE para el Análisis y Diseño**
Estas herramientas ayudan a modelar y visualizar los requisitos y el diseño del software antes de comenzar a programar.

- **Visual Paradigm Online**: Ya lo conocen los alumnos. Esta herramienta se utiliza para crear diagramas UML (como diagramas de clases, secuencias, casos de uso, etc.) que ayudan a planificar la estructura del software antes de codificar.
- **Lucidchart / Microsoft Visio**: Herramientas de diagramación que pueden ser útiles para representar visualmente el diseño del sistema y sus componentes.

Estas herramientas permiten a los alumnos crear diagramas estructurados, que son fundamentales en el desarrollo orientado a objetos (como lo que hacen con Java) y el trabajo en equipo, ya que facilitan la comunicación sobre la arquitectura del software.

#### **2. Herramientas CASE para la Implementación**
Son herramientas que ayudan a escribir el código, realizar pruebas y gestionar el control de versiones.

- **IntelliJ IDEA**: Es el **IDE** principal que los alumnos usan para escribir el código Java. Aunque no es estrictamente una herramienta CASE, IntelliJ ayuda a realizar tareas automatizadas como la refactorización del código, la navegación entre clases y la integración de herramientas de pruebas.
- **Maven**: Es el sistema de gestión de dependencias que facilita la construcción y gestión del proyecto. Permite automatizar tareas como la compilación del código y la ejecución de pruebas.
- **JUnit, Mockito, Cucumber**: Son herramientas de prueba que permiten a los alumnos escribir pruebas unitarias (JUnit), simular dependencias en pruebas (Mockito) y realizar pruebas basadas en comportamiento (Cucumber).
- **GitHub Actions**: Esta herramienta automatiza los flujos de trabajo de CI/CD, permitiendo que las pruebas y despliegues se realicen automáticamente con cada cambio de código, lo que mejora la productividad y la calidad del software.

#### **3. Herramientas CASE para la Prueba**
Estas herramientas permiten crear, ejecutar y gestionar pruebas de software.

- **JUnit y Mockito**: Son fundamentales para el desarrollo basado en pruebas (TDD). **JUnit** permite crear pruebas unitarias, mientras que **Mockito** se usa para simular objetos y controlar el entorno de pruebas, facilitando la escritura de pruebas más efectivas.
- **Cucumber**: Permite escribir pruebas en lenguaje natural, lo que facilita la comunicación entre desarrolladores y otros stakeholders (como los clientes) en proyectos ágiles.

#### **4. Herramientas CASE para el Mantenimiento**
Estas herramientas son útiles para gestionar el mantenimiento y la evolución del software después de que se ha implementado.

- **Visual Paradigm Online**: Aunque también se usa para el diseño, Visual Paradigm también permite gestionar versiones y realizar ingeniería inversa, lo que facilita la actualización de los diagramas conforme evoluciona el software.

---

### **Beneficios de las Herramientas CASE en el Contexto Actual**

1. **Automatización y Estandarización**: Herramientas como **Maven** y **GitHub Actions** automatizan la construcción y las pruebas del software, lo que reduce errores manuales y mejora la eficiencia.
2. **Mejora en la Comunicación y el Diseño**: **Visual Paradigm Online** y otras herramientas de diagramación permiten que los alumnos visualicen el diseño y compartan ideas de manera clara y estructurada.
3. **Desarrollo Basado en Comportamiento (BDD)**: El uso de **Cucumber** permite que los alumnos sigan un enfoque de desarrollo basado en pruebas desde el principio, escribiendo pruebas que describen el comportamiento del sistema de manera comprensible.
4. **Pruebas Automatizadas**: Con **JUnit** y **Mockito**, los alumnos pueden realizar pruebas de unidades de manera automática, lo que les ayuda a encontrar errores temprano y garantiza la calidad del código.

---

### **Conclusión**

Las herramientas CASE proporcionan un conjunto de recursos que mejoran la eficiencia y la calidad del desarrollo de software. En el contexto de los alumnos que usan **Java**, **Maven**, **Cucumber**, **GitHub Actions**, y herramientas de **diseño** como **Visual Paradigm Online**, estas herramientas les permiten automatizar tareas, mejorar la colaboración y realizar un desarrollo más estructurado y orientado a pruebas.

## Cucumber

Cucumber permite escribir pruebas en lenguaje natural **Gherkin** y ejecutarlas en Java. Vamos a expandir nuestro proyecto con Cucumber. Para ello, debemos agregar las dependencias pertinentes al archivo `pom.xml`:

```xml
<dependency>
    <groupId>io.cucumber</groupId>
    <artifactId>cucumber-java</artifactId>
    <version>7.15.0</version>
</dependency>
<dependency>
    <groupId>io.cucumber</groupId>
    <artifactId>cucumber-junit</artifactId>
    <version>7.15.0</version>
    <scope>test</scope>
</dependency>
```
Esta vez, al sincronizar el proyecto, IntelliJ nos propondrá instalar el plugin de cucumber (y cualquier otro que piense oportuno, sus motivos nos dará).
**Si usas Gradle**, en `build.gradle`:

Para trabajar con cucumber, necesitamos añadir un apartado de recursos a la parte de testeo del proyecto. Añadimos un directorio haciendo click derecho en /src/test y nos dará la opción de añadir una carpeta etiquetada como resources. Dentro de ella, añadimos una carpeta features. En `src/test/resources/features/`, creamos un archivo `calculadora.feature`:

```gherkin
Feature: Sumar números
  Scenario: Sumar dos valores
    Given tengo dos números 5 y 3
    When los sumo
    Then el resultado debe ser 8
```

A continuación, debemos crear las clases de pasos que necesita cucumber para realizar sus pruebas. Dentro de test/java, creamos el paquete steps. En `src/test/java/steps/`, creamos `CalculadoraSteps.java`:

```java
package steps;

public class CalculadoraSteps {
    private int numeroA;
    private int numeroB;
    private int resultado;

    @Given("tengo dos números {int} y {int}")
    public void tengoDosNumeros(int a, int b) {
        this.numeroA = a;
        this.numeroB = b;
    }

    @When("los sumo")
    public void losSumo() {
        resultado = numeroA + numeroB;
    }

    @Then("el resultado debe ser {int}")
    public void elResultadoDebeSer(int esperado) {
        assertEquals(esperado, resultado);
    }
}
```
Resolvemos los errores de importación con las herramientas de IntelliJ y procedemos a crear la clase de ejecución. En `src/test/java/`, creamos `RunCucumberTest.java`:

```java
import org.junit.platform.suite.api.ConfigurationParameter;
import org.junit.platform.suite.api.IncludeEngines;
import org.junit.platform.suite.api.SelectClasspathResource;
import org.junit.platform.suite.api.Suite;

import static io.cucumber.junit.platform.engine.Constants.PLUGIN_PROPERTY_NAME;

@Suite
@IncludeEngines("cucumber")
@SelectClasspathResource("features")
@ConfigurationParameter(key = PLUGIN_PROPERTY_NAME, value = "pretty")
public class RunCucumberTest {
}
```


### **5. Ejecutar la prueba**

1. Haz clic derecho en `RunCucumberTest.java` y selecciona **Run 'RunCucumberTest'**.
2. Deberías ver una salida indicando que el escenario se ejecutó correctamente.

### **Principales anotaciones de Cucumber:**

| Anotación   | Descripción |
|------------|------------|
| `@Given`   | Define el contexto inicial. |
| `@When`    | Describe la acción que ocurre. |
| `@Then`    | Verifica el resultado esperado. |

