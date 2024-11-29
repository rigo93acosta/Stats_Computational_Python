# Tabla de COntenido
- [Programación dinámica](#programación-dinámica)
    - [Optimzación Fibonnaci](#optimización-de-fibonacci)
        - [Optimización Especial](#optimización-especial)
        - [Código](#código)
    

# Programación dinámica

**Programación dinámica:** Se escogió para esconder a patrocinadores gubernamentales el hecho que en realidad estaba haciendo Matemáticas. La frase Programación Dinámica es algo que ningún congresista puede oponerse. **Richard Bellman**

**Programación dinámica:**
- Subsestructura Óptima: Una solución global óptima se puede encontrar al combinar soluciones óptimas de subproblemas locales.
- Problemas empalmados: Una solución óptima que involucra resolver el mismo problema en varias ocasiones.

**Memoization:**
- La memorización es una técnica para guardar cómputos previos y evitar realizarlos nuevamente.
- Normalmente se utiliza un diccionario, donde las consultas se pueden hacer en O(1).
- Intercambia tiempo por espacio.

> Ventaja de consulta de los Sets y Dict de O(1).

## Optimización de Fibonacci

$$F_n = F_{n-1} + F_{n-2} \quad \forall~n > 2$$

![Fibonacci](images/Fibonnaci.png)

Pero el algoritmo recursivo es ineficiente, debido a que crece de manera exponencial el tiempo de cómputo.

> **Hint:** Para medir tiempo de ejecución desde consola (Mi sistema operativo es Pop!_OS):
>```shell
>time python src/programacion_dinamica-1.py
>```
Aprovechando el tiempo de consulta de los diccionarios optimizamos el tiempo de ejecución para calcular un número $n$ de Fibonacci.

>**Hint:** Para aumentar el tamaño de recursión y no sea un límite, añadimos la siguiente línea de código:
>```python
>sys.setrecursionlimit(10002)
>```

> Sitio Web para observar como funciona ambos algoritmos: [Dynamic Programming (Fibonacci)](https://www.cs.usfca.edu/~galles/visualization/DPFib.html)

### Optimización Especial
```python
from functools import lru_cache

@lru_cache(maxsize=None)
def fib(n):
    if n < 2:
        return n
    return fib(n-1) + fib(n-2)
```
### Código 
[**File**: programacion_dinamica-1.py](src/programacion_dinamica-1.py)
```python
import sys

def fibonacci_recursivo(n):
    if n == 0 or n == 1:
        return 1

    return fibonacci_recursivo(n - 1) + fibonacci_recursivo(n - 2)


def fibonacci_dinamico(n, memo = {}):
    if n == 0 or n == 1:
        return 1

    try:
        return memo[n]
    except KeyError:
        resultado = fibonacci_dinamico(n - 1, memo) + fibonacci_dinamico(n - 2, memo)
        memo[n] = resultado

        return resultado

if __name__ == '__main__':
    sys.setrecursionlimit(10002)
    n = int(input('Escoge un numero: '))
    resultado = fibonacci_dinamico(n)
    print(resultado)
```

