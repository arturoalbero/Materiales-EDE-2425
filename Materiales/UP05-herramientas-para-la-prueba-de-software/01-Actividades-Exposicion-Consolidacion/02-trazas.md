<style> body{
    text-align: justify;
    }
    p{
        text-indent: 2rem;
    } 
</style>
# La traza de un programa

## Definición de Traza de un programa

La traza de un programa es un registro detallado de la ejecución de un programa, que muestra los valores de las variables, los resultados de las operaciones y el flujo de control en cada paso. En ella implementamos las técnicas de depuración de caja blanca de manera holística.

Es una herramienta útil para depurar y entender cómo funciona un programa, especialmente cuando se busca identificar errores o comportamientos inesperados.

### Tabla de seguimiento de variables

Una de las técnicas más efectivas es crear una tabla donde se registren los valores de las variables en cada paso del algoritmo. Supongamos el siguiente algoritmo en lenguaje natural:

1. Iniciar con `a = 5` y `b = 3`.
2. Sumar `a` y `b`, guardar el resultado en `c`.
3. Multiplicar `c` por 2, guardar el resultado en `d`.
4. Mostrar el valor de `d`.

Dado el anterior algoritmo, realizamos la siguiente tabla donde hacemos un seguimiento del valor de las variables.

| Paso | Operación                     | a  | b  | c  | d  |
|------|-------------------------------|----|----|----|----|
| 1    | Iniciar `a = 5`, `b = 3`       | 5  | 3  | -  | -  |
| 2    | `c = a + b` (5 + 3)            | 5  | 3  | 8  | -  |
| 3    | `d = c * 2` (8 * 2)            | 5  | 3  | 8  | 16 |
| 4    | Mostrar `d`                    | 5  | 3  | 8  | 16 |

Usando Entornos de Desarrollo Integrado, esta información la podemos consultar a través del depurador (debugger). Podemos sustituir la tabla por anotaciones (con la misma información) si el problema es simple, para reducir la aparatosidad. Las anotaciones son otra forma de expresar la traza.

Además del valor de las variables, también podemos evaluar el camino que se toma en los nodos de decisión mediante el uso de tablas de verdad.

## Ejemplo de aplicación

Vamos a crear un **ejemplo sencillo** que combine un algoritmo, su traza y una tabla de verdad para evaluar el camino que se toma en los nodos de decisión y el número de veces que se repite un bucle. Supongamos el siguiente algoritmo:

```plaintext
1. Iniciar con \( x = 2 \) y \( y = 3 \).
2. Si \( x > y \), mostrar "x es mayor que y".
3. Si \( x < y \), mostrar "x es menor que y" y repetir el siguiente paso 2 veces:
   - Incrementar \( x \) en 1.
4. Mostrar el valor final de \( x \).
```

Realizamos la traza siguiendo paso a paso el algoritmo y anotar los valores de las variables y las decisiones tomadas.

```plaintext
1. **Paso 1**: \( x = 2 \), \( y = 3 \).
2. **Paso 2**: Evaluar \( x > y \):
   - \( 2 > 3 \) es **Falso**, no se ejecuta esta condición.
3. **Paso 3**: Evaluar \( x < y \):
   - \( 2 < 3 \) es **Verdadero**, se muestra "x es menor que y".
   - Se entra en el bucle que se repite 2 veces:
     - **Primera iteración**:
       - Incrementar \( x \) en 1: \( x = 3 \).
     - **Segunda iteración**:
       - Incrementar \( x \) en 1: \( x = 4 \).
4. **Paso 4**: Mostrar el valor final de \( x \), que es **4**.
```

A continuación, creamos una tabla de verdad para las condiciones \( x > y \) y \( x < y \), y vemos qué camino se toma en cada caso.

| \( x \) | \( y \) | \( x > y \) | \( x < y \) | Camino tomado                     |
|---------|---------|-------------|-------------|-----------------------------------|
|   2     |   3     |    Falso    |   Verdadero | Mostrar "x es menor que y", bucle |
|   3     |   3     |    Falso    |   Falso     | No se cumple ninguna condición    |
|   4     |   3     |   Verdadero |   Falso     | Mostrar "x es mayor que y"        |

Podemos emplear las trazas para cualquier algoritmo que diseñemos y nos serán especialmente útiles para detectar errores o comportamientos anómalos.

> **Actividad:** Realiza un algoritmo que, dada una fecha de entrada, determine si es válida y, en caso de que sea válida, qué signo del zodiaco tendría un bebé nacido ese día. Para calcular si es válida una fecha, debes tener en cuenta los números de día y mes introducidos, contemplando si se trata de un año bisiesto o no.
> Un año es bisiesto si es divisible entre 4, con las excepciones de los años que son divisibles entre 100, que solo serán bisiestos si también son divisibles entre 400 (1900 no es biesto, pero 2000 y 2004 sí lo son).
> Las fechas para determinar el signo del zodiaco son las siguientes:
>
>1. **Aries**: 21 marzo - 19 abril.
>2. **Tauro**: 20 abril - 20 mayo.
>3. **Géminis**: 21 mayo - 20 junio.
>4. **Cáncer**: 21 junio - 22 julio.
>5. **Leo**: 23 julio - 22 agosto.
>6. **Virgo**: 23 agosto - 22 septiembre.
>7. **Libra**: 23 septiembre - 22 octubre.
>8. **Escorpio**: 23 octubre - 21 noviembre.
>9. **Sagitario**: 22 noviembre - 21 diciembre.
>10. **Capricornio**: 22 diciembre - 19 enero.
>11. **Acuario**: 20 enero - 18 febrero.
>12. **Piscis**: 19 febrero - 20 marzo.
>
> Calcula las trazas para los valores 29 de febrero de 2000, 29 de febrero de 1999, 31 de abril de 2024, 7 de abril de 1787, 1 de enero de 1900 y 13 de marzo de 2032.
