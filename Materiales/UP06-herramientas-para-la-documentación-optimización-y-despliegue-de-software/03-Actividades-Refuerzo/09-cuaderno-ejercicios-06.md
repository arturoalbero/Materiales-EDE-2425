# Cuaderno de ejercicios UP06

## Ejercicio 1

Realiza de la mano de un agente de Inteligencia Artificial, como ChatGPT o Gemini, un diseño de CD/CI para alguna de tus prácticas. Documenta el proceso en una memoria.

## Ejercicio 2

Emplea la inteligencia artificial para conseguir preguntas de tipo test de esta unidad. Genera 5 de cada documento. Recuerda que tienes el prompt en el cuaderno de la unidad 2.

## Ejercicio 3

Refactoriza el siguiente código:

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
Haz la refactorización manual y luego hazla empleando las herramientas específicas de IntelliJ (Refactor -> Rename y Refactor->Extract Method)