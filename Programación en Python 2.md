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
