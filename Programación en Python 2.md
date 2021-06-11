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
 
