## **Ejercicio 1: Análisis de bucles `for` en Java**

Analiza el comportamiento de cada uno de los siguientes fragmentos de código en Java.

### **1.1**

```java
for(;;) {}
```

**Resultado:**
Este es un **bucle infinito**.
No tiene condición de salida, así que se ejecuta indefinidamente. Es equivalente a:

```java
while(true) {}
```

---

### **1.2**

```java
int i = 0;
for(; i < 10; i++) {
    System.out.println(i); 
}
```

**Resultado esperado:**
 Imprime los valores del 0 al 9, **10 veces en total**.
**Nota:** El comentario original decía “11 veces”, pero eso es incorrecto.

**Salida esperada:**

```
0
1
2
3
4
5
6
7
8
9
```

---

### **1.3**

```java
int k = 0;
for(; k < 10;) {
    System.out.println(k); 
}
```

**Resultado:**
Esto sería un **bucle infinito si no se modifica `k` dentro del bucle**.
Como está, `k` nunca cambia, y `k < 10` siempre será verdadero.

Para evitar el bucle infinito, debería incluir una instrucción como `k++` dentro del bucle:

```java
int k = 0;
for(; k < 10;) {
    System.out.println(k); 
    k++;
}
```

---

### **1.4**

```java
final int l = 0;
for(; l > 10; l++) {
    System.out.println(l);
}
```

**Resultado:**
**Error de compilación.**
No se puede modificar una variable `final`, ya que es constante.
El uso de `l++` en el bucle intenta modificar una variable inmutable.

**Corrección:** Si `l` es final, no puede ser usado como variable de control en un bucle que lo modifica.

---

## **Ejercicio 2: ¿Qué se muestra en pantalla?**

### Código:

```java
for(int a = 0, b = 0; a < 7; a++, b += 2) {
    System.out.println("a vale: " + a + " y b vale: " + b);
}
```

### Análisis:

En cada iteración:

* `a` empieza en 0 y aumenta de 1 en 1.
* `b` empieza en 0 y aumenta de 2 en 2.
* Se imprime el valor actual de `a` y `b`.

### Tabla de iteraciones:

| Iteración | a | b  | Salida en pantalla     |
| --------- | - | -- | ---------------------- |
| 1         | 0 | 0  | a vale: 0 y b vale: 0  |
| 2         | 1 | 2  | a vale: 1 y b vale: 2  |
| 3         | 2 | 4  | a vale: 2 y b vale: 4  |
| 4         | 3 | 6  | a vale: 3 y b vale: 6  |
| 5         | 4 | 8  | a vale: 4 y b vale: 8  |
| 6         | 5 | 10 | a vale: 5 y b vale: 10 |
| 7         | 6 | 12 | a vale: 6 y b vale: 12 |

**Fin del bucle** cuando `a == 7`, ya que `7 < 7` es falso.

**Corrección importante:**
El análisis original incluye una **iteración 8 y 9 incorrectas**, que no ocurren.

**Salida final del programa:**

```
a vale: 0 y b vale: 0
a vale: 1 y b vale: 2
a vale: 2 y b vale: 4
a vale: 3 y b vale: 6
a vale: 4 y b vale: 8
a vale: 5 y b vale: 10
a vale: 6 y b vale: 12
```

---

## **Ejercicio 1: Evaluación de operaciones con operadores compuestos**

### Código:

```java
int a = 20, b = 10, c = 5, e = 10, f = 4;

a += 1;
b -= 1;
e *= 2;
f /= 2;
c += 2 + c;
```

### Análisis paso a paso:

| Variable | Operación    | Resultado | Explicación                                       |
| -------- | ------------ | --------- | ------------------------------------------------- |
| `a`      | `a += 1`     | `21`      | Suma 1 a `a`: `20 + 1 = 21`                       |
| `b`      | `b -= 1`     | `9`       | Resta 1 a `b`: `10 - 1 = 9`                       |
| `e`      | `e *= 2`     | `20`      | Multiplica `e` por 2: `10 * 2 = 20`               |
| `f`      | `f /= 2`     | `2`       | Divide `f` entre 2 (división entera): `4 / 2 = 2` |
| `c`      | `c += 2 + c` | `12`      | `c = c + 2 + c → 5 + 2 + 5 = 12`                  |

### Resultado final:

```java
a = 21
b = 9
c = 12
e = 20
f = 2
```

---

## **Ejercicio 2: Cálculo paso a paso de la variable `n`**

### Código:

```java
int n = 1, a = 3, b = 4;

a = b + n++;
n *= 3;
n = n + a + b * a;
```

### Análisis paso a paso:

1. **Inicialización:**

   ```java
   n = 1;
   a = 3;
   b = 4;
   ```

2. **Primera operación:**

   ```java
   a = b + n++;
   ```

   * `n++` devuelve 1, y luego incrementa `n` a 2.
   * `a = 4 + 1 = 5`

3. **Segunda operación:**

   ```java
   n *= 3;
   ```

   * `n = 2 * 3 = 6`

4. **Tercera operación:**

   ```java
   n = n + a + b * a;
   ```

   * `b * a = 4 * 5 = 20`
   * `n = 6 + 5 + 20 = 31`

### Resultado final:

```java
n = 31
```

# Actividad: Análisis de Bucles y Expresiones en Java

## **Ejercicio 1**

### Enunciado:

¿Cuántas veces se ejecuta el cuerpo del siguiente bucle?

```java
int i = 0;
while (true) {
    i++;
    if (i < 10)
        continue;
    i++;
    if (i == 10)
        break;
}
```

### Análisis:

1. `i` se incrementa en cada iteración (`i++`).
2. Si `i < 10`, se ejecuta `continue`, lo cual **salta el resto del bucle** y vuelve al inicio.
3. Por lo tanto, **nunca se alcanza la segunda instrucción `i++` mientras `i < 10`**.
4. Una vez que `i == 10`, se omite el `continue`, y se ejecuta `i++`, haciendo que `i == 11`.
5. La condición `if (i == 10)` ya no se cumple nunca más.
6. El `break` **jamás se ejecuta**, y el bucle sigue indefinidamente.

### Conclusión:

**El bucle es infinito. Nunca se rompe.**

---

## **Ejercicio 2**

### Enunciado:

Indica cuál será el resultado de ejecutar el siguiente programa Java:

```java
public class Prueba {
    public static void main(String[] args) {
        for (int i = 0; i < 100; i++) {
            if (i == 74) break;
            if (i % 9 != 0) continue;
            System.out.println(i);
        }

        int i = 0;
        while (true) {
            i++;
            int j = i * 27;
            if (j == 1269) break;
            if (i % 10 != 0) continue;
            System.out.println(i);
        }
    }
}
```

### Análisis:

#### Primera parte: Bucle `for`

* Itera desde `i = 0` hasta `i < 100`.
* Se imprimen solo los valores que:

  * No hacen que el bucle se rompa (`i != 74`).
  * Sean múltiplos de 9 (`i % 9 == 0`).

**Valores impresos:**

```
0
9
18
27
36
45
54
63
72
```

#### Segunda parte: Bucle `while`

* `i` se incrementa en cada iteración.
* `j = i * 27`.
* El bucle termina cuando `j == 1269` → `i == 47`.
* Se imprimen solo los valores de `i` que son múltiplos de 10 antes de llegar a 47.

**Valores impresos:**

```
10
20
30
40
```

### Conclusión:

**Salida total del programa:**

```
0
9
18
27
36
45
54
63
72
10
20
30
40
```

---

# Actividad: Arrays y Operaciones Básicas en Java

---

## **Ejercicio 3**

### Enunciado:

Diseñar el algoritmo e implementar un programa para:

* Crear un vector de 10 elementos de tipo numérico entero y de nombre `vector`.
* Rellenar el vector con los 10 primeros números impares.
* Mostrar el contenido del vector en pantalla.

### Análisis:

* Los 10 primeros números impares son: `1, 3, 5, 7, 9, 11, 13, 15, 17, 19`.
* Usamos un bucle para rellenar el vector de forma progresiva.

### Ejemplo de código:

```java
int[] vector = new int[10];
int valor = 1;

for (int i = 0; i < vector.length; i++) {
    vector[i] = valor;
    valor += 2;
}

for (int i = 0; i < vector.length; i++) {
    System.out.println(vector[i]);
}
```

---

## **Ejercicio 4**

### Enunciado:

Crea un programa que pida diez números reales por teclado, los almacene en un array y luego muestre todos sus valores.

### Análisis:

* Se utiliza un array `double[]` de tamaño 10.
* Se usan bucles `for` para entrada y salida de datos.

### Ejemplo de código:

```java
Scanner sc = new Scanner(System.in);
double[] numeros = new double[10];

for (int i = 0; i < numeros.length; i++) {
    System.out.print("Introduce un número: ");
    numeros[i] = sc.nextDouble();
}

for (int i = 0; i < numeros.length; i++) {
    System.out.println("Valor " + i + ": " + numeros[i]);
}
```

---

## **Ejercicio 5**

### Enunciado:

Crea un programa que pida diez números reales por teclado, los almacene en un array, y luego muestre la **suma** de todos los valores.

### Análisis:

* Similar al ejercicio anterior, pero se acumula la suma en una variable `double`.

### Ejemplo de código:

```java
Scanner sc = new Scanner(System.in);
double[] numeros = new double[10];
double suma = 0;

for (int i = 0; i < numeros.length; i++) {
    System.out.print("Introduce un número: ");
    numeros[i] = sc.nextDouble();
    suma += numeros[i];
}

System.out.println("Suma total: " + suma);
```

---

## **Ejercicio 6**

### Enunciado:

Crea un programa que pida diez números reales por teclado, los almacene en un array, y luego lo recorra para averiguar el **máximo y mínimo**, mostrándolos por pantalla.

### Análisis:

* Se inicializan `max` y `min` con el primer valor del array y se comparan en cada iteración.

### Ejemplo de código:

```java
Scanner sc = new Scanner(System.in);
double[] numeros = new double[10];

for (int i = 0; i < numeros.length; i++) {
    System.out.print("Introduce un número: ");
    numeros[i] = sc.nextDouble();
}

double max = numeros[0];
double min = numeros[0];

for (int i = 1; i < numeros.length; i++) {
    if (numeros[i] > max) max = numeros[i];
    if (numeros[i] < min) min = numeros[i];
}

System.out.println("Máximo: " + max);
System.out.println("Mínimo: " + min);
```

---

## **Ejercicio 7**

### Enunciado:

Crea un programa que pida veinte números enteros por teclado, los almacene en un array y luego muestre por separado la **suma de todos los valores positivos y negativos** (el 0 se considera positivo).

### Análisis:

* Usar dos variables acumuladoras: `sumaPositivos` y `sumaNegativos`.

### Ejemplo de código:

```java
Scanner sc = new Scanner(System.in);
int[] numeros = new int[20];
int sumaPositivos = 0, sumaNegativos = 0;

for (int i = 0; i < numeros.length; i++) {
    System.out.print("Introduce un número entero: ");
    numeros[i] = sc.nextInt();

    if (numeros[i] >= 0)
        sumaPositivos += numeros[i];
    else
        sumaNegativos += numeros[i];
}

System.out.println("Suma de positivos: " + sumaPositivos);
System.out.println("Suma de negativos: " + sumaNegativos);
```

---

## **Ejercicio 8**

### Enunciado:

Crea un programa que pida veinte números reales por teclado, los almacene en un array y luego lo recorra para **calcular y mostrar la media**.

### Análisis:

* Se acumula la suma de los valores y se divide entre 20.

### Ejemplo de código:

```java
Scanner sc = new Scanner(System.in);
double[] numeros = new double[20];
double suma = 0;

for (int i = 0; i < numeros.length; i++) {
    System.out.print("Introduce un número: ");
    numeros[i] = sc.nextDouble();
    suma += numeros[i];
}

double media = suma / numeros.length;
System.out.println("Media: " + media);
```

---

## **Ejercicio 9**

### Enunciado:

Crea un programa que pida dos valores enteros `N` y `M`, luego cree un array de tamaño `N`, escriba el valor `M` en **todas sus posiciones** y lo muestre por pantalla.

### Ejemplo de código:

```java
Scanner sc = new Scanner(System.in);
System.out.print("Introduce N (tamaño del array): ");
int N = sc.nextInt();
System.out.print("Introduce M (valor a asignar): ");
int M = sc.nextInt();

int[] vector = new int[N];
for (int i = 0; i < N; i++) {
    vector[i] = M;
}

for (int i = 0; i < N; i++) {
    System.out.println("Posición " + i + ": " + vector[i]);
}
```

---

## **Ejercicio 10**

### Enunciado:

Crea un programa que pida dos valores enteros `P` y `Q`, luego cree un array que contenga **todos los valores desde P hasta Q**, y lo muestre por pantalla.

### Análisis:

* La cantidad de elementos del array es `Q - P + 1`.
* Se rellenan las posiciones con `P`, `P+1`, ..., hasta `Q`.

### Ejemplo de código:

```java
Scanner sc = new Scanner(System.in);
System.out.print("Introduce P: ");
int P = sc.nextInt();
System.out.print("Introduce Q: ");
int Q = sc.nextInt();

int[] vector = new int[Q - P + 1];

for (int i = 0; i < vector.length; i++) {
    vector[i] = P + i;
}

for (int i = 0; i < vector.length; i++) {
    System.out.println("Valor " + i + ": " + vector[i]);
}
```


---

## **Ejercicio 1: Cálculo del Factorial**

### Enunciado:

Se ha realizado la siguiente clase para calcular el factorial de un número introducido por teclado. Tras ejecutarlo varias veces, los resultados no son correctos. Encuentra el error o errores y explica por qué.

### Código original:

```java
import java.util.Scanner;

public class Error1 {
   public static void main(String[] args) {
      double factorial;
      int num;
      Scanner teclado = new Scanner(System.in);
      System.out.print("Introduce un número: ");
      num = teclado.nextInt();
      factorial = 1;
      for (int i = num; i > 0; i--) {
         factorial = factorial * i;
      }
      System.out.println("El factorial de " + num + " es: " + factorial);
   }
}
```

### Análisis del error:

* El código **funciona correctamente para valores positivos** de `num`.
* Pero si se introduce `0`, el resultado debería ser `1` (por definición matemática), y el bucle **no se ejecuta**. Aun así, `factorial` ya está en `1`, por lo que **en realidad está bien implementado.**
* **No hay errores lógicos ni de compilación.** El comentario que sugiere usar `i >= 0` en el `for`:

  ```java
  for (int i = num; i >= 0; i--)
  ```

  provocaría un **resultado incorrecto**, ya que incluiría el producto por 0, y todo factorial sería 0.

### Conclusión:

**El código es correcto.** Si se introducen resultados incorrectos es posible que el error sea conceptual (esperar valores negativos o no controlar la entrada). Se puede mejorar agregando una validación:

### Mejora propuesta:

```java
if (num < 0) {
    System.out.println("No se puede calcular el factorial de un número negativo.");
} else {
    // mismo cálculo
}
```

---

## **Ejercicio 2: Cálculo de suma de sueldos y conteo de sueldos mayores a 1000**

### Enunciado:

Dado un conjunto de 10 sueldos introducidos por teclado, se desea mostrar su suma total y cuántos de ellos son mayores de 1000€. Los resultados no son correctos. Detecta y corrige los errores.

### Código original:

```java
import java.util.Scanner;

public class Error2 {
   public static void main(String[] args) {
      int sueldo, suma, mayor_1000;
      Scanner teclado = new Scanner(System.in);
      suma = 0;
      mayor_1000 = 0;

      for (int i = 1; i <= 10; i++) {
         System.out.print("Escribe un sueldo: ");
         sueldo = teclado.nextInt();
         if (sueldo > 1000) {
            mayor_1000--;
         }
         suma = suma + sueldo;
      }

      System.out.println("Mayores de 1000 hay: " + mayor_1000);
      System.out.println("la suma es de: " + suma);
   }
}
```

### Errores detectados:

1. **`mayor_1000--` está mal**: se está restando en lugar de sumar.

   * Debe ser `mayor_1000++`.

2. El comentario sugería que el bucle tenía:

   ```java
   for (int i = 1; i < 10; i--)  // Incorrecto
   ```

   Pero el código actual usa `i++` y `i <= 10`, lo cual es **correcto**.

### Corrección:

```java
if (sueldo > 1000) {
    mayor_1000++;  // Corrección aquí
}
```

### Resultado corregido:

```java
System.out.println("Mayores de 1000 hay: " + mayor_1000);
System.out.println("La suma es de: " + suma);
```

---

## **Ejercicio 3: Media de números introducidos hasta número negativo**

### Enunciado:

Se desea calcular la media de los números introducidos hasta que el usuario ingrese un número negativo. Los resultados obtenidos no son correctos.

### Código original:

```java
import java.util.Scanner;

public class Error3 {
   public static void main(String[] args) {
      int num, suma, elementos;
      float media;
      Scanner teclado = new Scanner(System.in);
      System.out.print("Introduzca un número: ");
      num = teclado.nextInt();
      suma = 0;
      elementos = 0;

      while (num > 0) {
         suma += num;
         elementos++;
         System.out.print("Introduzca otro número: ");
         num = teclado.nextInt();
      }

      if (elementos == 0) {
         System.out.println("Imposible hacer la media");
      } else {
         media = (float) suma / elementos;
         System.out.println("La media es de: " + media);
      }
   }
}
```

### Errores comentados en el código (comentarios antiguos):

* Comentarios como:

  ```java
  suma = 1;
  elementos = 1;
  suma += elementos;
  media = (float)elementos / suma;
  ```

  Estos eran **errores previos** y están **corregidos correctamente** en el código actual.

### Verificación:

* `suma += num` está bien.
* `elementos++` está bien.
* El cálculo de la media también es correcto:

  ```java
  media = (float) suma / elementos;
  ```

### Conclusión:

**El código actual es correcto.**
El problema inicial probablemente estaba en usar mal `suma` y `elementos`. Es importante asegurarse de que la lógica del bucle y las condiciones estén implementadas como en la versión corregida.
