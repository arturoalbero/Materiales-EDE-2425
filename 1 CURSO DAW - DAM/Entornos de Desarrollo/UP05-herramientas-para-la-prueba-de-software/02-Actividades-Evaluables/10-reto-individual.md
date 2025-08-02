# Reto individual

## Ejercicio 1: Pruebas de software

> **Actividad**
> Diseña un plan de pruebas para el programa que diseñaste en el reto de la unidad 4, acorde al diagrama de la unidad 3, para ello:
- Diseña el plan de pruebas general
- Diseña los casos de uso. Implementa JUNIT
- Diseña pruebas de integración. Implementa Mockito
- Diseña pruebas de aceptación. Implementa Cucumber

## Ejercicio 2: Uso del debugger

Dado el siguiente código y usando el Debugger de IntelliJ:

```java
public class EjercicioDebug {
    public static void main(String[] args) {
        int[] n = {3, 7, 2, 9, 5};
        int r = 0;
        for (int i = 0; i < n.length; i++) {
            r += procesaNumero(n[i]); // Colocar breakpoint con condición: n[i] > 5
        }
        System.out.println("Resultado: " + r);
        muestraInfoExtra(n);
    }
    static int procesaNumero(int x) {
        int y = 0;
        if (x % 2 == 0) {
            y = x * 2;
        } else {
            y = x * 3;
        }
        System.out.println("Procesando: " + x);
        System.out.println("Temporal: " + y);
        System.out.println("-----");
        return y;
    }
   
    static void muestraInfoExtra(int[] arr) {
        int s = 0;
        for (int i = 0; i < arr.length; i++) {
            s += arr[i];
        }
        for (int i = 0; i < arr.length; i++) {
            if (arr[i] % 2 == 0) {
                System.out.println(arr[i] + " es par");
            } else {
                System.out.println(arr[i] + " es impar");
            }
        }
        System.out.println("Suma total: " + s);
    }
}
```

Coloca un punto de ruptura en la línea indicada con la condición establecida y realiza las siguientes pruebas:
-	En el primer punto de ruptura, ejecuta un step over y continúa hasta la siguiente ruptura.
-	La segunda vez que pare, ejecuta un step into y ejecuta step over 3 veces. Después ejecuta step out.

Presenta los resultados en forma de memoria, con capturas de pantalla de cada paso.

## Rubrica

| | ÍTEM | Criterio Evaluación | PESO |
|---|---|---|---
| 1| Diseño del plan de pruebas | 3a | 2
| 1| Pruebas de unidad| 3b, 3f, 3g | 1
| 1| Pruebas de integración| 3i | 1
| 1| Pruebas de aceptación | 3b, 3f, 3g | 1
| 1| Otras pruebas| 3a | 1
| 2| Uso del Debugger de intelliJ | 3c, 3d | 2
| 2| Presentación de la memoria | 3h | 2 |

Se debe entregar un enlace al repositorio y una memoria explicando el proceso punto por punto