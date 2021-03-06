# CURSO PROGRAMACIÓN EN PYTHON BÁSICO  (DATACAMP)

---
## PYTHON INTERMEDIO
---
### TEMA 1 Basic plots with Matplotlib

Matplotlib es un paquete para visualización de datos, utilizamos el subpaquete pyplot que se importa como plt. Normalmente grafica datos que le pasamos como listas o como arrays.

Ejemplos de gráficos y su código en su página oficial: https://matplotlib.org/stable/gallery/index.html.

Ejemplos, descripción yusos de cada tipo de gráfico: https://doc.arcgis.com/es/insights/latest/create/scatter-plot.htm



```PYTHON
# Scatter plot (gráfico de dispersión)
plt.scatter(x = gdp_cap, y = life_exp, s = np.array(pop) * 2, c = col, alpha = 0.8)

plt.xscale('log')   # escala logaritmica en el eje x
plt.xlabel('GDP per Capita [in USD]')   # etiquetas ejes
plt.ylabel('Life Expectancy [in years]')
plt.title('World Development in 2007')    # título
plt.xticks([1000,10000,100000], ['1k','10k','100k'])  # renombrado de los valores del eje x

plt.text(1550, 71, 'India') # texto añadido dentro de la gráfica
plt.text(5700, 80, 'China')

plt.grid(True)  # activar rejilla

plt.show()  # mostrar gráfica

```

### TEMA 2 Diccionarios y Pandas
 Un diccionario almacena pares llave:valor, se declaran entre llaves {}, cuando se solicita una llave mediante corchetes [] devuelve el valor. Tanto las llaves como los valores pueden ser de cualquier tipo, pero las llaves deben ser inmutables (no se podría utilizar una lista porque se podría cambiar los elementos que la componen). Los valores a su vez pueden ser otros diccionarios.
 
 En un diccionario las llaves deben ser únicas e inmutables , aunque pueden añadirse llaves diferentes en cualquier momento. 
 
Aunque parecen los mismo y se acceden a los elementos de manera similar, una lista es una secuencia de datos a los que accedemos mediante un índice numérico dentro de un rango, sin embargo un diccionario es una secuencia de datos a los que accedemos mediante llaves inmutables. **Si el orden de los elementos importa, y queremos hacer subconjuntos de manera fácil utilizamos listas, si el orden no importa y queremos hacer búsquedas rápidas de un único elemento utilizaremos un diccionario.**
 
 ```PYTHON
europe = {'spain':'madrid', 'france':'paris', 'germany':'berlin', 'norway':'oslo' }  # Definition of dictionary

print(europe.keys())  # imprimimos todas las llaves del diccionario
print(europe['norway']) # imprimimos el valor que da la llave 'norway'
europe['cataluña'] = 'barcelona' # añadimos un par llave:valor al diccionario europe (si existe previamente actualiza el valor)
'cataluña' in europe  # devuelve True si la llave está en el diccionario europe
del(europe['cataluña'])   # borra un par llave:valor del diccionario

europe = { 'spain': { 'capital':'madrid', 'population':46.77 }, # Dictionary of dictionaries
           'france': { 'capital':'paris', 'population':66.03 },
           'germany': { 'capital':'berlin', 'population':80.62 },
           'norway': { 'capital':'oslo', 'population':5.084 } }
           
print(europe['france']['capital'])  # Print out the capital of France

data = { 'capital':'rome', 'population':59.83   } # Create sub-dictionary data
europe['italy'] = data  # Add data to europe under key 'italy'

 ```
 Cuando tenemos tablas con diferentes tipos de datos a NumPy le cuesta trabajo manejarlos con arrays, es mejor hacerlo con Pandas que está construido en base a NumPy, y es una herramienta de manipulación de datos de alo nivel.
 
 A una tabla se asignará a un ** Objeto Dataframe**, y las filas representan observaciones únicas y las columnas las variables, además la primera columna y la primera fila llevan asociadas etiquetas. Podemos crear un Dataframe a partir de un diccionario
 
### TEMA 3 Logic, Control Flow and Filtering
**Operadores de compararación:** Siempre devuelven tipos booleanos True y False. En caso de que los elementos a comparar sean cadenas los comparadores mayor y menos indicarán el orden alfabético.  
```python
< #Strictly less than  
<= #Less than or equal  
> #Strictly greater than  
>= #Greater than or equal  
== #Equal  
!= #Not equal

# recordatorio:
bmi = np.array([ 21.852, 20.975, 21.75 , 24.747, 21.441]) #creamos un objeto numpy
bmi > 23  # devuelve: ([False, False, False, True, False], dtype=bool)
bmi[bmi > 23] #devuelve array([ 24.747])
```

**Operadores Booleanos:** :warning: and, or, not no funcionan con objetos de numpy, para este tipo de elementos hay que utilizar:
**logical_and()
logical_or()
logical_not()**
```python
x = 12 # variable de ejemplo
x > 5 and x < 15  # es correcto en una expresión normal con variables

bmi = np.array([ 21.852, 20.975, 21.75 , 24.747, 21.441]) #creamos un objeto numpy
bmi > 21 and bmi < 22 # :warning: es INCORRECTO CON OBJETOS NUMPY
np.logical_and(bmi > 21, bmi < 22)  #devuelve: array([True, False, True, False, True], dtype=bool)
bmi[np.logical_and(bmi > 21, bmi < 22)] # devuelve: array([21.852, 21.75, 21.441])

```

**Sentencias Condicionales:** cambian el flujo de un programa dependiendo del valor de una o varias expresiones. Importante poner dos puntos al final de cada expresión condicional e indentar los códigos a ejecutar:
```python
z = 3
if z % 2 == 0 :  # importante poner dos puntos tras cada condición y tabular las siguientes expresiones con tab o 4 espacios
    print("z is divisible by 2") # False
elif z % 3 == 0 :
    print("z is divisible by 3") # True
else :
    print("z is neither divisible by 2 nor by 3")

# devuelve:  z is divisible by 3
```
**Filtrado de datos en Pandas** podemos utilizar operadores de comparación y operadores booleanos para hacer una subselección de datos en un DataFrame de Pandas.
```python
tenemos el dataFrame: 
    country  capital   area  population
BR  Brazil   Brasilia  8.516 200.40
RU  Russia   Moscow    17.100 143.50
IN  India    New Delhi 3.286 1252.00
CH  China    Beijing   9.597 1357.00
SA  South_Africa Pretoria 1.221 52.988

import pandas as pd
brics = pd.read_csv("path/to/brics.csv", index_col = 0) #importamos el dataFrame de un csv

brics["area"] #devuelve una  serie con la columna area # podíamos haber utilizado brics.loc[:,"area"] ó brics.iloc[:,2]
brics["area"] > 8 #devuelve una serie con los mayores de 8
brics[brics["area"] > 8] #creamos un subDataFrame (doble corchete convierte la serie en DataFrame)

np.logical_and(brics["area"] > 8, brics["area"] < 10) # inclusión de varias condiciones unidas por operadores booleanos.

```
### TEMA 4 Loops
**Bucles con While**: hay que asegurarse de que la condición de salida de bucle se va a conseguir en algún momento

```python
#Bucle básico:
x = 1
while x < 4 :
    print(x)
    x = x + 1
    
#Bucle While combinado con condicionales if elif :
offset = -6

# Code the while loop
while offset != 0 :
    print("correcting...")
    if offset > 0 :
      offset = offset -1
    else : 
      offset = offset +1    
    print(offset)
    
```
**Bucles For sobre listas:** Utilizando **enumerate(lista)** genera dos valores en cada iteración: el índice del valor y el valor en sí.
```python
#Bucle básico:
fam = [1.73, 1.68, 1.71, 1.89]
for height in fam : 
    print(height)
   
# areas list
areas = [11.25, 18.0, 20.0, 10.75, 9.50]
# Change for loop to use enumerate() and update print()
for index, a in enumerate(areas) :      #utilizamos enumerate para obtener pares tipo: índice del valor y propio valor
    print('room ' + str(index) + ': ' +str(a))
    
# areas list
areas = [11.25, 18.0, 20.0, 10.75, 9.50]
# Code the for loop
for index, area in enumerate(areas, 1) : # el "1" indica que índice empezará desde el 1 y no desde el 0
    print("room " + str(index) + ": " + str(area))
    
# house list of lists
house = [["hallway", 11.25],  #interacionamos con listas de listas
         ["kitchen", 18.0], 
         ["living room", 20.0], 
         ["bedroom", 10.75], 
         ["bathroom", 9.50]]
         
# Build a for loop from scratch -----for index, area in enumerate(areas, 1) :
for index, room in enumerate(house):
    print('the '+ house[index][0] +' is '+ str(house[index][1]) + ' sqm')

```
**Bucles For sobre Diccionarios:** Nota: los diccionarios no están ordenados, por definición, por lo que cuando iteractuamos sobre ellos nos podremos encontrar los resultados en cualquier orden.
```python
# Definition of dictionary
europe = {'spain':'madrid', 'france':'paris', 'germany':'berlin',
          'norway':'oslo', 'italy':'rome', 'poland':'warsaw', 'austria':'vienna' }    
# Iterate over europe
for key, value in europe.items(): # hay que utilizar el método: .items()
    print( 'the capital of ' + key + ' is ' + value)

```

**Bucles For sobre Numpy arrays:** Nota:
```python
# Import numpy as np
import numpy as np
# For loop over np_height (array con alturas)
for x in np_height:
    print(str(x) + ' inches')

# For loop over np_baseball (array con alturas y pesos )
for y in np.nditer(np_baseball):
    print (str(y))

```
**Bucles For sobre Pandas dataframes:** Nota:
```python
# Import cars data
import pandas as pd
cars = pd.read_csv('cars.csv', index_col = 0)

# Iterate over rows of cars
for lab, row in cars.iterrows():  # vamos a iterar sobre las filas con .iterrows(), utilizando la etiqueta de fila "lab" y los datos "row"
    print(lab)
    print(row) #genera una serie Panda, 
    print(str(row['cars_per_cap']) # si queremos acceder al valor de una columna debemos utilizar el nombre de la columna entre corchetes
    
# Bucle Para añadir una columna COUNTRY en mayúsculas (este método espoco eficiente)
for lab, row in cars.iterrows():
    cars.loc[lab, 'COUNTRY'] = row['country'].upper()
    
# para hacer lo mismo de manera más eficiente usaremos .apply(str.upper) y **así no necesitamos un bucle for**.
cars['COUNTRY'] = cars['country'].apply(str.upper)
```

### TEMA 5 Hackear estadísticas
**Números aleatorios:** Nota: se puede resolver un problema de manera analítica, creando una ecuación, o de manera Hacker resolviéndolo 1000 veces para datos aleatorios y ver qué pasa.
Numpy tiene un **subpaquete llamado "random"** que tiene las funciones seed() y rand() para generar datos aleatorios:
np.random.rand() genera un dato seuso-aleatorio entre 0 y 1. Si lo introducimos sin semilla Python la elige de manera aleatoria, pero si le metemos el parámetro semilla con np.random.seed(semilla) generará una serie concreta de números en función de ésta. (se utiliza para que otras personas puedan reproducir tu análisis).

```python
import numpy as np
np.random.rand()      # Pseudo-random flotantes de 0.0 a 1.0

np.random.seed(123)   # Introducimos una semilla para que los números aleatorios se generen en secuancias idénticas para asegurar reproductividad. 
np.random.rand()      # inicio de la secuencia pseudo aleatoria idéntica a partir de la semilla anterior.


```
