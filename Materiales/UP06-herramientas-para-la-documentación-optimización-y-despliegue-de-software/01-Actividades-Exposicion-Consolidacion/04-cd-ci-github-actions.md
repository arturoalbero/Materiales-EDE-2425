# Implementación de CI/CD con GitHub Actions en IntelliJ y Maven**  


<!-- @import "[TOC]" {cmd="toc" depthFrom=1 depthTo=6 orderedList=false} -->

<!-- code_chunk_output -->

- [Implementación de CI/CD con GitHub Actions en IntelliJ y Maven**](#implementación-de-cicd-con-github-actions-en-intellij-y-maven)
  - [CI/CD: Integración y Entrega/Despliegue Continuos](#cicd-integración-y-entregadespliegue-continuos)
  - [Crear el Proyecto en IntelliJ con Maven](#crear-el-proyecto-en-intellij-con-maven)
  - [Agregar Código y Pruebas](#agregar-código-y-pruebas)
    - [Clase a probar (`Calculadora.java`)](#clase-a-probar-calculadorajava)
    - [Pruebas con JUnit (`CalculadoraTest.java`)](#pruebas-con-junit-calculadoratestjava)
  - [Configurar Git y Subir el Proyecto a GitHub](#configurar-git-y-subir-el-proyecto-a-github)
    - [Inicializar un repositorio Git](#inicializar-un-repositorio-git)
    - [Subir el código a GitHub](#subir-el-código-a-github)
  - [Configurar CI/CD con GitHub Actions](#configurar-cicd-con-github-actions)
    - [Crear un workflow en GitHub Actions](#crear-un-workflow-en-github-actions)

<!-- /code_chunk_output -->




## CI/CD: Integración y Entrega/Despliegue Continuos

**CI/CD** es una práctica fundamental en el desarrollo de software moderno que integra dos conceptos clave: la **Integración Continua (CI)** y la **Entrega Continua (CD)** o **Despliegue Continuo (CD)**. Su objetivo es automatizar y mejorar el proceso desde la creación del código hasta su implementación en producción, permitiendo ciclos de desarrollo más rápidos, eficientes y fiables.

La **Integración Continua (CI)** es la práctica de que los desarrolladores integren sus cambios de código en un repositorio compartido de forma frecuente, a menudo varias veces al día. Cada integración se verifica automáticamente mediante compilaciones y pruebas automatizadas para detectar errores de integración de manera temprana. Esto ayuda a mantener una base de código funcional y a reducir el "infierno de la integración" que ocurre cuando los equipos intentan combinar grandes volúmenes de código al final de un ciclo.

La **Entrega Continua (CD)** extiende la CI al automatizar el proceso de preparación del software para su lanzamiento. Esto significa que el código, una vez integrado y probado con éxito, está siempre en un estado desplegable. Aunque el software está listo para ser lanzado, la decisión de desplegarlo en producción se realiza manualmente.

El **Despliegue Continuo (CD)** va un paso más allá de la Entrega Continua, ya que automatiza también el despliegue del software en producción. Si el código pasa todas las fases de pruebas automatizadas, se despliega automáticamente, sin intervención humana. Esto permite entregas muy rápidas y frecuentes a los usuarios finales.

En esencia, CI/CD crea un *pipeline* automatizado que facilita la integración, prueba y entrega de software de manera constante, minimizando riesgos y acelerando el tiempo de llegada al mercado.

## Crear el Proyecto en IntelliJ con Maven
En este documento, configuraremos un flujo de trabajo de **CI/CD (Integración y Entrega Continua)** usando **GitHub Actions**. Se va a usar Java 17.

1. Abrir **IntelliJ IDEA** y seleccionar **New Project**.  
2. Elegir **Maven** como gestor de dependencias.  
3. En **GroupId**, escribir: `com.ejemplo` (puede cambiarse).  
4. En **ArtifactId**, escribir: `ci-cd-demo` (nombre del proyecto).  
5. Hacer clic en **Finish**.  

Una vez creado el proyecto, se verá una estructura similar a esta:  
```
ci-cd-demo
│── src
│   ├── main
│   │   └── java
│   │       └── com.ejemplo
│   │           └── Calculadora.java
│   ├── test
│   │   └── java
│   │       └── com.ejemplo
│   │           └── CalculadoraTest.java
│── pom.xml
│── .gitignore
```
---

## Agregar Código y Pruebas  

### Clase a probar (`Calculadora.java`)
En `src/main/java/com/ejemplo/Calculadora.java`:  

```java
package com.ejemplo;

public class Calculadora {
    public int sumar(int a, int b) {
        return a + b;
    }

    public int restar(int a, int b) {
        return a - b;
    }

    public int multiplicar(int a, int b) {
        return a * b;
    }

    public int dividir(int a, int b) {
        if (b == 0) {
            throw new ArithmeticException("No se puede dividir por cero");
        }
        return a / b;
    }
}
```

### Pruebas con JUnit (`CalculadoraTest.java`)  
En `src/test/java/com/ejemplo/CalculadoraTest.java`:  

```java
package com.ejemplo;

import org.junit.jupiter.api.Test;
import static org.junit.jupiter.api.Assertions.*;

class CalculadoraTest {

    private final Calculadora calculadora = new Calculadora();

    @Test
    void testSuma() {
        assertEquals(5, calculadora.sumar(2, 3));
    }

    @Test
    void testResta() {
        assertEquals(1, calculadora.restar(5, 4));
    }

    @Test
    void testMultiplicacion() {
        assertEquals(10, calculadora.multiplicar(2, 5));
    }

    @Test
    void testDivision() {
        assertEquals(2, calculadora.dividir(10, 5));
    }

    @Test
    void testDivisionPorCero() {
        assertThrows(ArithmeticException.class, () -> calculadora.dividir(10, 0));
    }
}
```

## Configurar Git y Subir el Proyecto a GitHub 

### Inicializar un repositorio Git 
1. Abrir **IntelliJ** y abrir la **terminal integrada** (`View > Tool Windows > Terminal`).  
2. Escribir los siguientes comandos:  
```sh
git init
git add .
git commit -m "Primer commit"
```

### Subir el código a GitHub  
1. Ir a [GitHub](https://github.com/) y crear un nuevo repositorio.  
2. Copiar el enlace del repositorio y ejecutar en la terminal de IntelliJ:  
```sh
git remote add origin <URL_DEL_REPOSITORIO>
git branch -M main
git push -u origin main
```
Ahora el código está en GitHub y listo para configurar GitHub Actions.  


## Configurar CI/CD con GitHub Actions  

### Crear un workflow en GitHub Actions  
1. En GitHub, ir a la pestaña **Actions**.  
2. Hacer clic en **New workflow** y seleccionar **Set up a workflow yourself**.  
3. Crear un archivo llamado `.github/workflows/ci.yml`.  
4. Agregar el siguiente contenido:  

```yaml
name: CI/CD Pipeline

on:
  push:
    branches:
      - main
  pull_request:
    branches:
      - main

jobs:
  build:
    runs-on: ubuntu-latest

    steps:
      - name: Clonar repositorio
        uses: actions/checkout@v4

      - name: Configurar JDK 17
        uses: actions/setup-java@v3
        with:
          distribution: 'temurin'
          java-version: '17'

      - name: Construir con Maven
        run: mvn clean package

      - name: Ejecutar pruebas unitarias
        run: mvn test
```
 
- Se ejecuta cuando hay un **push** o **pull request** en la rama `main`.  
- Usa una máquina virtual con **Ubuntu**.  
- Descarga el código y configura **Java 17**.  
- Ejecuta **Maven** para compilar (`mvn clean package`).  
- Ejecuta las pruebas con **JUnit** (`mvn test`).  

Después de agregar este archivo y hacer un commit, GitHub Actions ejecutará el workflow automáticamente en cada cambio.  

> **Actividad**
> Crea un workflow para probar alguno de los ejercicios que hiciste durante la unidad de programación 5
