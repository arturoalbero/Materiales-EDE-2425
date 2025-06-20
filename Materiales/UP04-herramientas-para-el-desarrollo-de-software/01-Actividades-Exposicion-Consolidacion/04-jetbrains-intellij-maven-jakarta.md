En IntelliJ tienes varias opciones para gestionar las dependencias de tus proyectos Java, como el gestor de dependencias propio de IntelliJ, **Maven** o **Gradle**. Aquí te doy una visión rápida de cada uno, con recomendaciones sobre cuál podría ser la mejor opción según tu caso.

## 1. **Gestor de dependencias de IntelliJ**

El gestor de dependencias integrado en IntelliJ se encarga de gestionar bibliotecas manualmente a través de configuraciones locales en el proyecto. Aunque puede ser útil para proyectos pequeños o sencillos, tiene limitaciones importantes:

### Ventajas del gestor de IntelliJ

- Fácil de usar para proyectos muy pequeños o para aquellos que no requieren muchas dependencias externas.
- Permite agregar librerías manualmente (en formato `.jar`) sin necesidad de un gestor externo.

### Desventajas del gestor de IntelliJ

- **No es escalable**: Si el proyecto crece y tiene muchas dependencias, manejar esto manualmente puede ser muy complicado y propenso a errores.
- **No maneja automáticamente las dependencias transitorias**: Si tu biblioteca necesita otras bibliotecas, tendrás que gestionarlas tú manualmente.
- **No es compatible con automatización o integración continua**: No se integra fácilmente con herramientas de automatización de construcción como Jenkins o CI/CD.
- **Menor soporte para plugins o configuraciones avanzadas**.

### ¿Cuándo usaremos el gestor de IntelliJ?

Usar el gestor de dependencias propio de IntelliJ solo es recomendable para proyectos **muy pequeños** o **prototipos** que no requieran integración continua, automatización, o un sistema de construcción más avanzado.

### Actividad 1

Crea un proyecto en Java usando el gestor de dependencias propio de IntelliJ y un programa que, al ejecutarlo, escriba por consola "Hola Mundo".

---
<div style="page-break-after: always;"></div>

## 2. **Maven**

**Maven** es un gestor de proyectos y dependencias ampliamente utilizado en proyectos Java. Define la estructura del proyecto y gestiona las dependencias a través de un archivo XML llamado `pom.xml`.

### Ventajas de Maven

- **Estandarización**: Tiene una estructura estándar de proyectos Java, lo que facilita la colaboración entre equipos.
- **Automatización de dependencias**: Puedes agregar dependencias fácilmente, y Maven descargará automáticamente las bibliotecas necesarias y sus dependencias transitorias desde repositorios centralizados.
- **Integración continua**: Está bien soportado en herramientas de integración continua (CI) como Jenkins, GitLab CI, GitHub Actions, etc.
- **Popularidad y soporte**: Hay una enorme comunidad y mucha documentación disponible.

### Desventajas de Maven

- **XML**: Algunos desarrolladores consideran que editar archivos `pom.xml` es tedioso y difícil de leer cuando el archivo crece.
- **Rendimiento**: Comparado con Gradle, Maven puede ser un poco más lento, especialmente en proyectos grandes.

### ¿Cuándo usaremos Maven?

**Maven** es una excelente opción si trabajas en **proyectos medianos o grandes** o si tu equipo ya está familiarizado con él. También es ideal para proyectos con equipos distribuidos, ya que su estructura estándar y amplio uso en la industria lo hacen fácil de adoptar.

### Configuración de un proyecto con Maven

1. **Crear un proyecto con Maven**:
   - Al crear un nuevo proyecto en IntelliJ, selecciona **Maven** como opción de proyecto.
   - IntelliJ generará automáticamente un archivo `pom.xml` donde podrás agregar tus dependencias.

2. **Agregar dependencias en Maven**:
   - Abre el archivo `pom.xml` y añade las dependencias dentro de la sección `<dependencies>`:

   ```xml
   <dependencies>
       <dependency>
           <groupId>junit</groupId>
           <artifactId>junit</artifactId>
           <version>4.13.1</version>
           <scope>test</scope>
       </dependency>
   </dependencies>
   ```

3. **Ejecutar Maven**:
   - Puedes ejecutar comandos de Maven directamente en IntelliJ desde el panel de Maven (en la barra lateral derecha).
   - Comandos comunes incluyen `clean`, `install`, y `package`.

### Actividad 2

Crea un proyecto en Java usando Maven y un programa que, al ejecutarlo, escriba por consola "Hola Mundo, vivo en Maven".

---
<div style="page-break-after: always;"></div>

## 3. **Gradle**

**Gradle** es un gestor de construcción más moderno y flexible que Maven. En lugar de usar XML, Gradle utiliza archivos de configuración en **Groovy** o **Kotlin** para definir dependencias y tareas, lo que lo hace más legible y potente.

### Ventajas de Gradle

- **Flexibilidad**: Gradle es más flexible que Maven, permitiendo configuraciones avanzadas sin tantas restricciones.
- **Rendimiento**: Gradle es generalmente más rápido que Maven debido a su sistema de ejecución incremental y su caché local.
- **Soporte para múltiples lenguajes**: Aunque es muy popular en proyectos Java, Gradle también es común en proyectos Android, Kotlin, y otros lenguajes como Scala o Groovy.
- **DSL legible**: Al usar un DSL en Groovy o Kotlin, los archivos de configuración (`build.gradle`) son más compactos y fáciles de leer que los archivos XML de Maven.

### Desventajasde Gradle

- **Curva de aprendizaje**: Aunque más potente, puede ser más difícil de aprender al principio si vienes de Maven, sobre todo si necesitas personalizar tareas específicas.
- **Menos estándar**: Aunque cada vez es más común, no todos los proyectos Java adoptan Gradle. Por lo tanto, puede no ser la mejor opción si tu equipo ya está familiarizado con Maven.

### ¿Cuándo usamos Gradle?

**Gradle** es ideal para **proyectos grandes**, especialmente si necesitas flexibilidad o si trabajas en proyectos **multilenguaje** o **Android**. También es una excelente opción si te importa el rendimiento y la eficiencia en la construcción.

### Configuración de un proyecto con Gradle

1. **Crear un proyecto con Gradle**:

   - Al crear un nuevo proyecto, selecciona **Gradle** como el sistema de construcción.
   - Se generará un archivo `build.gradle` que puedes usar para gestionar las dependencias.

2. **Agregar dependencias en Gradle**:
   - Abre el archivo `build.gradle` y agrega las dependencias en la sección `dependencies`:

   ```groovy
   dependencies {
       testImplementation 'junit:junit:4.13.1'
   }
   ```

3. **Ejecutar Gradle**:
   - Al igual que con Maven, puedes ejecutar tareas de Gradle directamente desde IntelliJ usando el panel de Gradle. Tareas comunes incluyen `build`, `test`, y `clean`.

---

### Actividad 3

Crea un proyecto en Java usando Gradle y un programa que, al ejecutarlo, escriba por consola "Hola Mundo, vivo en Gradle".

---

Durante el curso emplearemos Maven, por su mayor implantación en la actualidad.

