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

**Operadores Booleanos:** and, or, not no funcionan con objetos de numpy, para este tipo de elementos hay que utilizar:
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
