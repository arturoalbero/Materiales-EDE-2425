# Introducción a la programación

En la asignatura de "Entornos de desarrollo" vamos a introducirnos en los conceptos fundamentales de los lenguajes de programación y la programación, haciendo énfasis en elementos comunes que nos permitirán comprender y programar en diversos lenguajes como C, C++, C#, Java y Python. Utilizaremos el entorno en línea [MyCompiler.io](https://www.mycompiler.io/es) para escribir, compilar e interpretar nuestro código, permitiéndonos explorar las características esenciales de cada lenguaje.

> **Actividad**
> Consulta los lenguajes de programación más populares en las siguientes fuentes:
> * [TIOBE index](https://www.tiobe.com/tiobe-index/)
> * [RedMonk ranking](https://redmonk.com/sogrady/2024/03/08/language-rankings-1-24/)

## Elementos Básicos de un Lenguaje de Programación

### Variables
Una **variable** es un espacio en la memoria de un programa donde podemos almacenar y manipular datos. Cada lenguaje de programación maneja las variables de manera diferente en cuanto a la declaración y el tipo de datos que almacenan. Estos tipos de datos pueden ser enteros, decimales, caracteres, cadenas, entre otros.

Por ejemplo, en C o C++ necesitamos declarar el tipo de la variable antes de usarla:

```c
int numero = 5;
char letra = 'A';
```

En lenguajes como Python, no es necesario declarar el tipo, ya que el lenguaje asigna el tipo automáticamente:

```python
numero = 5
letra = 'A'
```

### Tipos de Datos y Tipado

Los lenguajes de programación también difieren en la manera en que manejan los tipos de datos. Esto nos lleva a dos conceptos importantes:

- **Tipado estático vs. tipado dinámico**: En lenguajes como C, C++ y Java, el tipo de una variable debe ser declarado explícitamente, lo que se denomina **tipado estático**. En cambio, en Python, el tipo de una variable se asigna en tiempo de ejecución, lo que se llama **tipado dinámico**.
  
- **Tipado fuerte vs. tipado débil**: Un lenguaje con **tipado fuerte** (como Java o Python) restringe más las operaciones entre tipos diferentes, mientras que un lenguaje con **tipado débil** (como C) puede permitir ciertas conversiones automáticas entre tipos.

### Operadores

Los **operadores** permiten realizar operaciones sobre las variables, como sumar, restar, comparar o asignar valores. Los operadores básicos incluyen:

- **Aritméticos**: Suma (`+`), resta (`-`), multiplicación (`*`), división (`/`)
- **De asignación**: Igualdad (`=`), suma y asignación (`+=`), etc.
- **Relacionales**: Mayor que (`>`), menor que (`<`), igual a (`==`), etc.
- **Lógicos**: Y (`&&` o `and`), O (`||` o `or`), negación (`!` o `not`)

Ejemplo de uso de operadores en C++:

```cpp
int a = 10;
int b = 20;
int suma = a + b; // Operador aritmético
bool resultado = (a == b); // Operador relacional
```

### Entrada y Salida por Consola

La **entrada y salida de datos** es un aspecto fundamental en cualquier lenguaje de programación. Nos permite interactuar con el usuario o con otros sistemas mediante el uso de la consola.

- **Salida por consola**: Imprimir datos en la consola es común en todos los lenguajes. En C o C++, usamos `printf` o `cout` respectivamente, mientras que en Java usamos `System.out.println`, y en Python usamos `print`.
  
Ejemplos de salida en distintos lenguajes:

```c
// En C
printf("Hola Mundo\n");

// En C++
std::cout << "Hola Mundo" << std::endl;

// En Python
print("Hola Mundo")
```

- **Entrada por consola**: Para recibir datos del usuario, podemos usar funciones como `scanf` en C, `cin` en C++ o `input` en Python.

Ejemplo de entrada:

```c
// En C
int edad;
scanf("%d", &edad);

// En Python
edad = input("Introduce tu edad: ")
```


#### Ejemplos de Ejecución en MyCompiler.io

Utilizaremos [MyCompiler.io](https://www.mycompiler.io/es) para escribir y probar los ejemplos en los distintos lenguajes. Este entorno permite escribir código y ejecutarlo en diferentes lenguajes sin necesidad de instalar un entorno de desarrollo local. El compilador o intérprete asociado con cada lenguaje se encargará de ejecutar el código en la web.

> **Actividad**
>A continuación, te proponemos algunos ejercicios básicos que deberás implementar en los lenguajes que estamos trabajando (C, C++, C#, Java y Python). Estos ejercicios te permitirán familiarizarte con la sintaxis básica, las variables, los operadores y las entradas y salidas por consola:
>
> 1. **Imprimir un mensaje en consola**: Escribe un programa que imprima "Hola, Mundo" en consola.
>   
> 2. **Suma de dos números**: Escribe un programa que solicite al usuario dos números enteros, los sume e imprima el resultado.
>
> 3. **Área de un rectángulo**: Escribe un programa que solicite al usuario el ancho y la altura de un rectángulo e imprima su área.
>
> 4. **Conversión de temperatura**: Escribe un programa que convierta una temperatura de grados Celsius a Fahrenheit.
>
> 5. **Cálculo de edad**: Escribe un programa que solicite al usuario su año de nacimiento y calcule su edad actual.

Recuerda realizar cada uno de estos ejercicios en los lenguajes que estamos utilizando (C, C++, C#, Java y Python), y observa cómo cambian la sintaxis y las herramientas utilizadas en cada uno.


### Tabla de operadores

| **Tipo** | **Operador** | **Java** | **C#** | **C++** | **C** | **Python** |
|---|---|---|---|---|---|---|
| **Aritmético** | `+` (suma) | Igual | Igual | Igual | Igual | Igual |
| | `-` (resta) | Igual | Igual | Igual | Igual | Igual |
| | `*` (multiplicación) | Igual | Igual | Igual | Igual | Igual |
| | `/` (división) | Igual | Igual | Igual | Igual | Igual |
| | `%` (módulo) | Igual | Igual | Igual | Igual | Igual |
| | `++` (incremento) | Igual | Igual | Igual | Igual | no existe |
| | `--` (decremento) | Igual | Igual | Igual | Igual | no existe |
| | `//` (división entera) | no existe | no existe | no existe | no existe | Igual |
| | `**` (potencia) | no existe | no existe | no existe | no existe | Igual |
| | `+=` (asignación suma) | Igual | Igual | Igual | Igual | Igual |
| | `-=` (asignación resta) | Igual | Igual | Igual | Igual | Igual |
| | `*=` (asignación multiplicación) | Igual | Igual | Igual | Igual | Igual |
| | `/=` (asignación división) | Igual | Igual | Igual | Igual | Igual |
| | `%=` (asignación módulo) | Igual | Igual | Igual | Igual | Igual |
| **Lógico** | `&&` (AND lógico) | Igual | Igual | Igual | Igual | `and` |
| | `||` (OR lógico) | Igual | Igual | Igual | Igual | `or` |
| | `!` (NOT lógico) | Igual | Igual | Igual | Igual | Igual o `not` |
| | `==` (igualdad) | Igual | Igual | Igual | Igual | Igual |
| | `!=` (distinto) | Igual | Igual | Igual | Igual | Igual |

### Tabla con ejemplos de asignación para cada tipo de dato

| **Tipo de Dato** | **C** | **C++** | **Java** | **C#** | **Python** |
|---|---|---|---|---|---|
| **Enteros** | `int x = 10;` | `int x = 10;` | `int x = 10;` | `int x = 10;` | `x = 10` |
| **Float** | `float y = 5.5f;` | `float y = 5.5f;` | `float y = 5.5f;` | `float y = 5.5f;` | `y = 5.5` |
| **Double** | `double z = 3.14159;` | `double z = 3.14159;` | `double z = 3.14159;` | `double z = 3.14159;` | `z = 3.14159` |
| **Caracteres** | `char c = 'A';` | `char c = 'A';` | `char c = 'A';` | `char c = 'A';` | `c = 'A'` |
| **Cadenas de texto** | `char str[] = "Hola";` | `std::string str = "Hola";` | `String str = "Hola";` | `string str = "Hola";` | `str = "Hola"` |
| **Booleanos** | `_Bool b = 1;` | `bool b = true;` | `boolean b = true;` | `bool b = true;` | `b = True` |

### Explicación adicional:
* **Enteros**: Se utilizan valores enteros en todos los lenguajes con el mismo formato.
* **Float y Double**: En **C** y **C++**, el sufijo `f` se usa para `float`. Para `double`, no es necesario.
* **Caracteres**: Los caracteres se definen entre comillas simples en todos los lenguajes. En Python, los caracteres individuales se tratan como cadenas de texto de un solo carácter.
* **Cadenas de texto**: En **C**, se usan arreglos de caracteres o punteros. En los otros lenguajes, las cadenas son tipos de datos más complejos que permiten manipular texto directamente.
* **Booleanos**: En **C**, el tipo booleano se introdujo en C99 con `_Bool`, aunque se podía usar `int` en versiones anteriores. En los demás lenguajes, se usan tipos booleanos dedicados. En Python, `True` y `False` son las instancias booleanas.