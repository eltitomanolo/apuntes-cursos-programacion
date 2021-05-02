# CURSO PYTHON EN DATACAMP  

---
## TEMA 1 

---
## TEMA 2  

---
## TEMA 3  

---
## TEMA 4  

**NumPy** (Numeric Python) Es un paquete para python esencial para la Ciencia de Datos. La listas no son eficientes y es difícil operar con ellas. NumPy tiene un tipo nuevo "array" con métodos especializados para realizar todo tipo de operaciones con este tipo nuevo.
Los arrays deben contener valores de un solo tipo, matriz de int, matriz de booleanos...etc, si no es así los convierte todos al mismo tipo de la mejor manera posible para que sea homogénea,por ejemplo si tiene int y bool, los convierte todos a int, porque no se podría de manera inversa.  
Supongamos que tenemos una matriz bmi con flotantes:  
bmi[1]		-> devuelve el elemento de índice 1 (el segundo)  
bmi >23		-> devuelve un array booleano que indica qué elementos son mayores de 23.  
bmi[bmi >23]-> devuelve una matriz solo con los elementos mayores de 23.  
```Python
# lista que necesitamos convertir en matriz
baseball = [180, 215, 210, 210, 188, 176, 209, 200]

# Import the numpy package as np
import numpy as np

# las matrices se crean a partir de listas
np_baseball = np.array(baseball)
```  
construir una matriz de varias dimensiones:
```Python
mi_matriz = np.array([[1],[2]],[[3],[4]]) #construimos una matriz 2x2
mi_matriz.shape # muestra dimensión de la matriz

mi_matriz[2][3]	# selecciona elemento 3 de la fila 2
mi_matriz[2,3]	# idéntica a la anterior
```


INTERESANTE:  
Orden prelación de los operadores matemáticos:  
https://www.aprendeprogramando.es/cursos-online/python/operadores-aritmeticos/operadores-aritmeticos  

Información en Español librería NumPy:  
https://aprendeconalf.es/docencia/python/manual/numpy/  
