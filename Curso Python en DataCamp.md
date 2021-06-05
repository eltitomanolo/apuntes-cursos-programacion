# CURSO PYTHON EN DATACAMP  

---
## TEMA 1
```PYTHON
print()   #imprime en el terminal
type() # devuelve el tipo de dato pasado como argumento (int,float, bool, str...)
str() #convierte números en cadenas
int() #convierte números y cadenas a entero
float() #convierte números y cadenas a flotante
bool()  #convierte números a booleano (True False)

```
---
## TEMA 2

El primer elemento de una lista tiene índice 0.

```PYTHON
lista = [a, b, c, d, e, f] # una lista da un solo nombre a una coleccion de valores
lista = [a, 1, 'casa']  #puede contener diferentes tipos de datos
listas = [['casa', 1],['barco',14]]  #puede contener otras listas
x = [["a", "b", "c"], # otra forma más visual de listas de listas
     ["d", "e", "f"],
     ["g", "h", "i"]]
type(lista) # devolvería que es un tipo de datos list
lista[1] # devuelve al segundo elemento de una lista.
lista[-1] # devuelve al último elemento de una lista (índice negativo significa que empezamos por el final, no hay -0)
lista[2:5] # devuelve un rango, el primer índice está incluido y el último índice no
lista[:5] # si se omite algún índice devuelve todos los elementos de ese sentido
lista[3] = 'p' # cambia un elemento de una lista
lista[0:2]= ['h', 'g'] # cambia varios elementos de un rango
lista2 = lista + ['h', 'g']  #el operador + añade elementos a una lista
del(lista[3])     #elimina un elemento de una lista OJO: los siguientes elementos cambian el índice
```
El nombre de la lista es la posición de memoria donde se empieza a guardar una lista, por lo que si se asigna a otra variable mediante "=" entonces ambas apuntan a la misma posición de memoria, por lo que si se varía el valor de algún elemento, éste varía en ambas listas.

file:///home/manuel/Escritorio/copia%20de%20listas.png![image](https://user-images.githubusercontent.com/32695362/120519634-215a1680-c3d3-11eb-82f7-6a29d5a68bfc.png)

Para copiar/duplicar una lista hay que utilizar y=list(x)
file:///home/manuel/Escritorio/listas2.png![image](https://user-images.githubusercontent.com/32695362/120519899-76962800-c3d3-11eb-90c1-cee173f5eea8.png)

nota: el separador ; se utiliza para poner varios comandos en una sola línea.



---
## TEMA 3 Funciones y Paquetes.

Una función es un código reutilizable que realiza una sola tarea y se le puede introducir argumentos de entrada. Todas las funciones utilizadas hasta ahora son *Funciones Integradas* en Python.

**help(funcion)** muestra la ayuda de una función python. Cuando un argumento se muestra entre corchetes indica que es opcional. Cuando un argumento se muestra igualado a algún valor indica que éste es por defecto.

**?max** idem del anterior

Todas las variables en Python son **Objetos**, que a su vez tienen sus propios **métodos** según su tipo (int, float, boolean, listas...). Los métodos son funciones que pertenecen a los objetos, dependiendo del tipo de objeto habrá disponible unos determinados método.

```PYTHON
max(lista)     #devuelve el máximo valor de una lista de valores
round (n, p)     #redondea el número n con número de decimales después de la coma p. Si se omite p se redondea al entero más cercano
help(funcion)       #muestra la ayuda de una función python.
?max      #idem del anterior
len(list)      #devuelve elnúmero de elementos de una lista
sorted(list)   #ordena los valores según los argumentos
lista.index('a')    # llamamos al método index del objeto lista del tipo "list" y que devuelve el número de orden de un elemento de una lista
```
**Métodos con string**: (help(str) nos muestra toda la información y atributos del objeto del tipo str)
```PYTHON
texto= "manolo"
texto.upper()  #Pone todas las letras en mayúsculas
texto.count("o")    #cuenta las letras o
```

**Métodos con list**:

```PYTHON
areas = [11.25, 18.0, 20.0, 10.75, 9.50]
areas.index(20.0)        #devuelve el número de índice donde se encuentra el valor introducido como parámetro
areas.count(9.50)        #devuelve la cantidad de coincidencias con el argumento en la lista
areas.append(24.5)       #añade elemento al final
areas.remove(15.45)      #quita el primer elemento que coincida
areas.reverse()          #invierte el orden de los elementos
```

Un **Paquete** es un directorio donse se encuentran **módulos** que son scripts de python que definen funciones, métodos y tipos que resuelven problemas particulares. Para poder utilizar un paquete primero debe instalarse en el sistema utilizando **pip** (pip3 install numpy) y después indicar en tu script que quieres utilizarlo

Un paquete importante es *Numpy*, destinado a operar con matrices.

```PYTHON
import numpy   #importa todo el paquete
numpy.array([1,2,3]) crea un array,

import numpy as np  #importa todo el paquete y le asigna un alias   RECOMENDADO
np.array([1,2,3])   #crea un array utilizando el alias del paquete

from numpy import array  #importamos solo una función del paquete.
array([1,2,3])           #crea un array utilizando solo el nombre de lafunción del paquete. ESTO ES CONFUSO

from scipy.linalg import inv as my_inv  #importamos las función inv(), y le damos el nombre my_inv, del subpaquete linalg que se encuentra dentro del paquete scipy
```


---
## TEMA 4  

**NumPy** (Numeric Python) Es un paquete para python esencial para la Ciencia de Datos. La listas no son eficientes y es difícil operar con ellas. NumPy tiene un tipo nuevo "array" con métodos especializados para realizar todo tipo de operaciones con este tipo nuevo.
Los arrays deben contener valores de un solo tipo, matriz de int, matriz de booleanos...etc, si no es así los convierte todos al mismo tipo de la mejor manera posible para que sea homogénea,por ejemplo si tiene int y bool, los convierte todos a int, porque no se podría de manera inversa.  
Supongamos que tenemos una matriz bmi con flotantes:  
bmi[1]		-> devuelve el elemento de índice 1 (el segundo)  
bmi >23		-> devuelve un array booleano que indica qué elementos son mayores de 23.  
bmi[bmi >23]-> devuelve una matriz solo con los elementos mayores de 23.  
```Python
baseball = [180, 215, 210, 210, 188, 176, 209, 200] # lista que necesitamos convertir en matriz
import numpy as np  # Import the numpy package as np
np_baseball = np.array(baseball) # las matrices se crean a partir de listas
np_baseball*5  #multiplica todos los elementos por 5
np_height_in[100:111] # devuelve una matriz con los elementos del subconjunto con índices desde el 100 al 110 (parecido a las listas)
```  
Para construir una matriz de varias dimensiones:
```Python
mi_matriz = np.array([[1],[2]],[[3],[4]]) #construimos una matriz 2x2
mi_matriz.shape # método que muestra la dimensión de la matriz
mi_matriz[2][3]	# selecciona elemento 3 de la fila 2
mi_matriz[2,3]	# idéntica a la anterior
mi_matriz[:,1] # devuelve un subconjunto de mi_matriz con todas las filas (:) y la última columna( aunque se podía haber puesto un intervalo n:m)
mi_matriz_2D [fila_inicio:fila_final , columna_inicio:columna_final] # devuelve un subconjuto de la matriz_2D 
```
Para analizar datos tenemos algunos métodos en np:
```Python
np.mean(array)      #la media de los valores de la matriz introducida como argumento
np.median(array)    #la media de los valores de la matriz introducida como argumento
np.corrcoef(array)  #busca correlacion de los datos
np.std(array)       #desviación standard
np.sum()
np.sort()
np.random.normal(distribution_mean, distributio_desvatio_standard, number of samples)

gk_heights = np_heights[np_positions == 'GK']     #devuelve un array donde los índices sean 'GK'
other_heights = np_heights[np_positions != 'GK']  #devuelve un array donde los índices NO sean 'GK'

```


INTERESANTE:  
Orden prelación de los operadores matemáticos:  
https://www.aprendeprogramando.es/cursos-online/python/operadores-aritmeticos/operadores-aritmeticos  

Información en Español librería NumPy:  
https://aprendeconalf.es/docencia/python/manual/numpy/  

