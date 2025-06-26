# Documentación. Doxygen

No importa cuán bueno sea el software... si la documentación no es lo suficientemente buena, la gente no lo usará. Y, si tiene que usarse, a menos que la documentación sea adecuada, no se utilizará correctamente.  

Para tener una buena documentación, debemos tener en cuenta los siguientes tipos de documentación, de modo que podamos elegir la más adecuada según su propósito final.  

## Tipos de documentación

Según el uso que se le dará a la documentación, esta puede ser:  

- **Tutoriales**  
  - Orientados al aprendizaje  
  - Permiten a los usuarios comenzar a usar el software  
  - Son como una lección  
  - **Analogía:** enseñar a un niño a cocinar  

- **Guías prácticas (How-to guides)**  
  - Orientadas a resultados  
  - Muestran cómo resolver un problema o necesidad concreta  
  - Son una lista de pasos o etapas  
  - **Analogía:** una receta de un libro de cocina  

- **Explicaciones**  
  - Orientadas a la comprensión  
  - Explican algo y ofrecen contexto  
  - **Analogía:** un artículo sobre la historia social de la gastronomía  

- **Referencia**  
  - Orientada a la información  
  - Describe cómo se ha construido algo  
  - Es exacta y completa  
  - **Analogía:** una entrada en una enciclopedia  

En lo que respecta a productos de software, los tipos más comunes de documentación son:  

- **Manuales de usuario**, para enseñar al usuario final cómo utilizar la aplicación.  
- **Proceso de software**, un documento que contiene todos los diagramas e informes de las etapas de análisis y diseño de la aplicación, para que se pueda ver cómo ha sido concebida.  
- **Referencia de API (Interfaz de Programación de Aplicaciones)**, una referencia completa con todos los componentes incluidos en la aplicación, especialmente clases, métodos públicos y elementos. Este último tipo de documentación es particularmente útil para el equipo de desarrollo, ya que facilita el mantenimiento y las futuras actualizaciones del producto.  

Para crear un manual de usuario, podemos usar cualquier editor de texto disponible y redactar un documento completo que explique cómo usar cada componente de la aplicación. Alternativamente, también podemos crear un manual de usuario en línea, de modo que los usuarios puedan acceder a un sitio web y buscar el contenido que les interese.

[*fuente*](https://nachoiborraies.github.io/java/md/en/09a)

> **Actividad:** 
> Busca un ejemplo real de cada tipo de documentación.

A la hora de programar, disponemos de varias herramientas para generar documentación, como javadoc o Doxygen.
## 3. Javadoc

Javadoc es una herramienta oficial de Java que se utiliza para generar documentación API en formato HTML directamente desde el código fuente. Esta documentación se basa en comentarios especiales que se escriben en el código, justo antes de las clases, métodos y otros elementos, y proporciona una manera fácil de crear y mantener documentación legible y coherente para los desarrolladores.

Javadoc utiliza comentarios específicos que comienzan con `/**` y terminan con `*/`, lo que los distingue de los comentarios regulares en Java (`//` y `/*` ... `*/`). Los comentarios Javadoc incluyen etiquetas especiales:

- `@author`: Especifica quién escribió la clase.
- `@version`: Es la versión actual de la clase, útil para llevar control de cambios.
- `@since`: Indica la fecha o versión en la que la clase fue introducida o modificada.
- `@param` para describir parámetros.
- `@return` para describir el valor de retorno.
- `@throws` para excepciones (si las hay).

```java
/**
 * Clase que representa una cuenta bancaria simple con operaciones 
 * básicas como depósito, retiro y consulta de saldo.
 * 
 * Esta clase es utilizada para gestionar cuentas bancarias individuales
 * en una aplicación de banca.
 * 
 * 
 * @author Juan Pérez
 * @version 1.0
 * @since 2024-10-24
 */
public class CuentaBancaria {

    private double saldo;

    /**
     * Constructor para crear una cuenta bancaria con un saldo inicial.
     * 
     * @param saldoInicial El saldo inicial de la cuenta.
     */
    public CuentaBancaria(double saldoInicial) {
        this.saldo = saldoInicial;
    }

    /**
     * Método para depositar dinero en la cuenta bancaria.
     * 
     * @param monto El monto a depositar.
     */
    public void depositar(double monto) {
        this.saldo += monto;
    }

    /**
     * Método para retirar dinero de la cuenta bancaria.
     * 
     * @param monto El monto a retirar.
     * @throws IllegalArgumentException si el monto es mayor que el saldo.
     */
    public void retirar(double monto) {
        if (monto > saldo) {
            throw new IllegalArgumentException("Fondos insuficientes");
        }
        this.saldo -= monto;
    }

    /**
     * Método que devuelve el saldo actual de la cuenta.
     * 
     * @return El saldo actual de la cuenta.
     */
    public double consultarSaldo() {
        return this.saldo;
    }
}
```
> **Actividad**
> Crea documentación javadoc para el siguiente código, trabajado en la unidad de programación 4. Organiza el proyecto en paquetes para que tenga sentido.
>

```java
// Martillo.java
public class Martillo {
    protected float longitud;
    protected String marca;
    protected CabezaDeMartillo cabeza; // Composición: Martillo "tiene" una CabezaDeMartillo

    public Martillo() {
        this.cabeza = new CabezaDeMartillo(); // La CabezaDeMartillo se crea con el Martillo
    }

    public void martillar() {
        // Implementación del método martillar
    }
}

// MartilloElectrico.java
public class MartilloElectrico extends Martillo { // Herencia: MartilloElectrico "es un" Martillo
    private float bateria;

    public float getBateria() {
        return bateria;
    }

    public void setBateria(float bateria) {
        this.bateria = bateria;
    }

    public int tiempoRestante() {
        // Cálculo y retorno del tiempo restante de la batería
        return 0; // Placeholder
    }
}

// Trabajador.java
public class Trabajador {
    private String nombre;
    private Martillo martillo; // Agregación: Trabajador "usa un" Martillo

    public Trabajador(String nombre, Martillo martillo) { // El Martillo se pasa al constructor
        this.nombre = nombre;
        this.martillo = martillo;
    }

    public String getNombre() {
        return nombre;
    }

    public void setNombre(String nombre) {
        this.nombre = nombre;
    }

    public Martillo getMartillo() {
        return martillo;
    }

    public void setMartillo(Martillo martillo) {
        this.martillo = martillo;
    }

    public void trabajar() {
        // Implementación del método trabajar
    }
}

// CabezaDeMartillo.java
public class CabezaDeMartillo {
    private String material;

    public CabezaDeMartillo() {
        // Constructor por defecto
    }

    public CabezaDeMartillo(String material) {
        this.material = material;
    }

    public String getMaterial() {
        return material;
    }

    public void setMaterial(String material) {
        this.material = material;
    }
}
```

IntelliJ ofrece herramientas para generar tanto la documentación como la página web resultante de manera más o menos automatizada. Cuando colocas comentarios especiales de javadoc encima de un método, al pulsar intro después de `/**`, aparecerán los parámetros relevantes, así como el cierre del comentario. Una vez documentado el proyecto, seguimos los siguientes pasos en IntelliJ:

1. **Selecciona tu clase o paquete** en el explorador de proyectos, el que contiene el código que quieres documentar.
2. Ve a **Tools** → **Generate JavaDoc** (Herramientas → Generar JavaDoc).

3. Se abre una ventana donde puedes especificar opciones como:
   - El **directorio de salida** donde se guarda la documentación generada (generalmente un directorio como `docs` o `javadoc`).
   - Los **filtros** para elegir si quieres generar la documentación para todo el proyecto, solo algunas clases, etc.
   - La posibilidad de inclusión de **fuentes** o **archivos relacionados** en la documentación.

4. Haz clic en **OK**. IntelliJ ejecutará el proceso de generación de Javadoc.

Una vez completada la generación, se puede encontrar la documentación en el directorio especificado, normalmente en formato HTML. Busca el archivo `index.html`.

La documentación es especialmente importante cuando se trabaja en equipo o en proyectos grandes, pero es peligrosa si no se mantiene con regularidad, ya que los compiladores avisan de errores en el código, pero normalmente no en la documentación. Puedes emplear modelos de generación de texto a través de Inteligencia Artificial, como *Chatgpt*, para generar documentación de tus clases, aunque el resultado no siempre será adecuado. Sin embargo, sí puede ayudarte a la hora de comprobar que la clase hace, efectivamente, lo que la documentación dice que hace la clase y corregir errores menores y de formato.

> **Actividad**
> Genera la documentación del proyecto anterior como si fuera una web con las herramientas de IntelliJ.

> **Actividad:** Entra en esta [**página web**](https://nachoiborraies.github.io/java/md/en/09c) y aprende a usar Doxygen. Genera un documento del programa anterior.