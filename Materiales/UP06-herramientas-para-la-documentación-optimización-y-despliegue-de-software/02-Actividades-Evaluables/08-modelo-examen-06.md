# MODELO DE EXAMEN (TEST)

# Ejercicio: Refactoriza este código

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
## Rubrica

| | ÍTEM | Criterio Evaluación | PESO |
|---|---|---|---
| | Test | TODOS | 6
| | Refactorización: Variables| 4a | 1
| | Refactorización: Métodos| 4a | 2
| | Refactorización: Claridad| 4a | 1
