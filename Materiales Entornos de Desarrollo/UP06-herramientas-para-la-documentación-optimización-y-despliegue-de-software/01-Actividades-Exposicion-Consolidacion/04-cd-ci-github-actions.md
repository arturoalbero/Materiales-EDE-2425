# **Tutorial: Implementación de CI/CD con GitHub Actions en IntelliJ y Maven**  

En este tutorial, configuraremos un flujo de trabajo de **CI/CD (Integración y Entrega Continua)** usando **GitHub Actions**. Se cubrirá la automatización de compilación, pruebas y despliegue de una aplicación Java en **GitHub Pages**.  

El alumnado trabajará en **IntelliJ IDEA** con **Maven** y aplicará los conocimientos previos de **GitHub Pages**. No es necesario conocimiento sobre servidores externos.  

---

## **1. Crear el Proyecto en IntelliJ con Maven**  

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

## **2. Agregar Código y Pruebas**  

### **Clase a probar (`Calculadora.java`)**  
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

### **Pruebas con JUnit (`CalculadoraTest.java`)**  
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
---

## **3. Configurar Git y Subir el Proyecto a GitHub**  

### **Inicializar un repositorio Git**  
1. Abrir **IntelliJ** y abrir la **terminal integrada** (`View > Tool Windows > Terminal`).  
2. Escribir los siguientes comandos:  
```sh
git init
git add .
git commit -m "Primer commit"
```

### **Subir el código a GitHub**  
1. Ir a [GitHub](https://github.com/) y crear un nuevo repositorio.  
2. Copiar el enlace del repositorio y ejecutar en la terminal de IntelliJ:  
```sh
git remote add origin <URL_DEL_REPOSITORIO>
git branch -M main
git push -u origin main
```
Ahora el código está en GitHub y listo para configurar GitHub Actions.  

---

## **4. Configurar CI/CD con GitHub Actions**  

### **Crear un workflow en GitHub Actions**  
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

### **Explicación del workflow**  
- Se ejecuta cuando hay un **push** o **pull request** en la rama `main`.  
- Usa una máquina virtual con **Ubuntu**.  
- Descarga el código y configura **Java 17**.  
- Ejecuta **Maven** para compilar (`mvn clean package`).  
- Ejecuta las pruebas con **JUnit** (`mvn test`).  

Después de agregar este archivo y hacer un commit, GitHub Actions ejecutará el workflow automáticamente en cada cambio.  

---

## **5. Desplegar en GitHub Pages**  

Dado que GitHub Pages solo soporta archivos estáticos, se generará un archivo **HTML con JavaScript** que muestre los resultados de la calculadora.  

### **Crear un archivo HTML en `src/main/resources/index.html`**  
```html
<!DOCTYPE html>
<html lang="es">
<head>
    <meta charset="UTF-8">
    <title>Calculadora</title>
    <script>
        function calcular() {
            var a = parseInt(document.getElementById("num1").value);
            var b = parseInt(document.getElementById("num2").value);
            document.getElementById("resultado").innerText = "Suma: " + (a + b);
        }
    </script>
</head>
<body>
    <h1>Calculadora</h1>
    <input type="number" id="num1">
    <input type="number" id="num2">
    <button onclick="calcular()">Calcular</button>
    <p id="resultado"></p>
</body>
</html>
```

### **Modificar el workflow para desplegar en GitHub Pages**  
```yaml
  deploy:
    needs: build
    runs-on: ubuntu-latest

    steps:
      - name: Clonar repositorio
        uses: actions/checkout@v4

      - name: Copiar archivos estáticos
        run: cp -r src/main/resources/ public/

      - name: Subir artefactos a GitHub Pages
        uses: actions/upload-pages-artifact@v2
        with:
          path: public

      - name: Desplegar en GitHub Pages
        uses: actions/deploy-pages@v2
```
Después de hacer un commit con este cambio, el proyecto se desplegará en **GitHub Pages** automáticamente.  

---

## **6. Verificar el Despliegue**  
1. Ir a **Settings > Pages** en el repositorio de GitHub.  
2. En **Branch**, seleccionar `github-pages` y hacer clic en **Save**.  
3. Acceder a la URL generada (`https://usuario.github.io/repositorio`).  

GitHub Pages solo soporta archivos estáticos (HTML, CSS, JavaScript), por lo que no puede ejecutar directamente código Java en el backend. Sin embargo, hay dos formas de integrar la calculadora en una página web:  

1. **Generar una API REST en Java** con Spring Boot y desplegarla en otro servicio (como Heroku o Render).  
2. **Compilar el código Java a WebAssembly (WASM)** con herramientas como TeaVM o CheerpJ, lo cual permite ejecutarlo en el navegador sin servidor.  

Dado que el alumnado no tiene experiencia en servidores externos, la opción más accesible es convertir el código Java en WebAssembly para que funcione directamente en GitHub Pages.  

---

# **Ejecutar Código Java en GitHub Pages con WebAssembly (TeaVM)**  

**TeaVM** es una herramienta que transpila código Java a JavaScript, permitiendo su ejecución en el navegador sin necesidad de servidores.  

### **1. Agregar TeaVM al Proyecto**  
En el archivo `pom.xml`, agregar la siguiente dependencia:  

```xml
<dependencies>
    <dependency>
        <groupId>org.teavm</groupId>
        <artifactId>teavm-jso</artifactId>
        <version>0.8.1</version>
    </dependency>
</dependencies>
```

Luego, agregar el plugin de TeaVM para compilar Java a JavaScript:  

```xml
<build>
    <plugins>
        <plugin>
            <groupId>org.teavm</groupId>
            <artifactId>teavm-maven-plugin</artifactId>
            <version>0.8.1</version>
            <executions>
                <execution>
                    <goals>
                        <goal>compile</goal>
                    </goals>
                </execution>
            </executions>
            <configuration>
                <targetDirectory>${project.build.directory}/web</targetDirectory>
                <targetType>javascript</targetType>
                <mainClass>com.ejemplo.CalculadoraWeb</mainClass>
            </configuration>
        </plugin>
    </plugins>
</build>
```

---

### **2. Crear la Interfaz Web con Java y TeaVM**  
En `src/main/java/com/ejemplo/CalculadoraWeb.java`:  

```java
package com.ejemplo;

import org.teavm.jso.browser.Window;
import org.teavm.jso.dom.html.HTMLDocument;
import org.teavm.jso.dom.html.HTMLInputElement;
import org.teavm.jso.dom.html.HTMLParagraphElement;

public class CalculadoraWeb {
    public static void main(String[] args) {
        HTMLDocument document = Window.current().getDocument();

        HTMLInputElement num1 = (HTMLInputElement) document.getElementById("num1");
        HTMLInputElement num2 = (HTMLInputElement) document.getElementById("num2");
        HTMLParagraphElement resultado = (HTMLParagraphElement) document.getElementById("resultado");

        document.getElementById("calcular").addEventListener("click", evt -> {
            int a = Integer.parseInt(num1.getValue());
            int b = Integer.parseInt(num2.getValue());
            Calculadora calc = new Calculadora();
            resultado.setTextContent("Suma: " + calc.sumar(a, b));
        });
    }
}
```

---

### **3. Crear el HTML para GitHub Pages**  
En `src/main/resources/index.html`:  

```html
<!DOCTYPE html>
<html lang="es">
<head>
    <meta charset="UTF-8">
    <title>Calculadora Java</title>
</head>
<body>
    <h1>Calculadora en Java con TeaVM</h1>
    <input type="number" id="num1">
    <input type="number" id="num2">
    <button id="calcular">Calcular</button>
    <p id="resultado"></p>

    <script src="teavm/teavm.js"></script>
</body>
</html>
```

---

### **4. Modificar el Workflow para Generar JavaScript**  
Modificar el archivo `.github/workflows/ci.yml` para incluir la compilación con TeaVM:  

```yaml
  deploy:
    needs: build
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
        run: mvn clean package teavm:compile

      - name: Mover archivos generados
        run: |
          mkdir public
          cp -r src/main/resources/* public/
          cp -r target/web/* public/

      - name: Subir artefactos a GitHub Pages
        uses: actions/upload-pages-artifact@v2
        with:
          path: public

      - name: Desplegar en GitHub Pages
        uses: actions/deploy-pages@v2
```

---

### **5. Probar la Calculadora en GitHub Pages**  
Después de hacer un commit, GitHub Pages desplegará la aplicación.  

1. Ir a **Settings > Pages** en GitHub.  
2. Seleccionar `github-pages` como rama.  
3. Acceder a la URL generada:  
   ```
   https://usuario.github.io/repositorio
   ```
4. Ingresar dos números y hacer clic en "Calcular".  

El código Java ahora se ejecuta en el navegador como JavaScript gracias a TeaVM.  
