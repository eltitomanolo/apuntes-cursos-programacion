
# **GESTION DE DATOS BÁSICO** (DATACAMP)

-----
## INTRODUCCIÓN A SQL
-----
### TEMA 1: Seleccionando columnas
(Buen sitio en español para consultas: https://diego.com.es/certificacion-php en sección Databases
o en su repositorio github https://github.com/diegotham/certificacion-php/tree/master/7-Databases)
**SQL** = Structured Query Lenguage: es el lenguaje nativo para acceder a las bases de datos relacionales.

Una base de datos relacional es un conjunto de tablas en las que cada una representa un tipo de entidad.
Cada fila (record) contiene información de una única entidad, y cada columna representa un atributo. Una consulta o query es una petición de datos a la base de datos.

Aunque es opcional, los comandos se escriben en mayúsculas, se les llama keywords. Igualmente opcional es poner punto y coma al final de la consulta:
```SQL
# es más fácil de leer si traducimos SELECT como "devuelve"

SELECT name FROM people;  #devuelve una columna

SELECT name, birthdate    #devuelve varias columnas
FROM people;

SELECT *                  #devuelve todas las columnas
FROM people;

SELECT *                  #devuelve 10 resultados
FROM people
LIMIT 10;

SELECT DISTINCT language  #devuelve valores distintos, que no estén duplicados
FROM films;

SELECT COUNT(*)           #devuelve el número de registros en una tabla completa
FROM people;

SELECT COUNT(birthdate)   #devuelve el número de registros válidos en una columna de una tabla
FROM people;

SELECT COUNT(DISTINCT birthdate)  #devuelve el úmero de registros válidos y distintos
FROM people;
```

### TEMA 2: Filtrando filas
En SQL, la keyword WHERE permite hacer filtrados por texto o por valores numéricos en una tabla:
``` SQL
# = equal
# <> not equal (no utilizar != )
# < less than
# > greater than
# <= less than or equal to
# >= greater than or equal to

SELECT title
FROM films
WHERE title = 'Metropolis';  # ojo: comillas simples cuando se utilicen textos

SELECT title
FROM films
WHERE release_year < 2000;

SELECT name, birthdate
FROM people
WHERE birthdate = '1974-11-11'  # ojo: la fecha va en formato ISO

SELECT COUNT(*)   # devuelve cuántos elementos hay en la tabla que cumplen con las condiciones indicadas 
FROM films
WHERE language = 'Hindi';

SELECT title      # para estrechar la búsqueda condiciones utilizamos AND
FROM films
WHERE release_year > 1994
AND release_year < 2000;  # un AND para cada condición
AND language = 'Spanish'

SELECT title    # para ampliar la búsqueda condiciones utilizamos OR
FROM films
WHERE release_year = 1994
OR release_year = 2000;

SELECT title    # se pueden combinar los OR y los AND, OJO porque hay reglas de precedencia
FROM films
WHERE (release_year >= 1990 AND release_year < 2000)
AND (certification = 'PG' OR certification = 'R');

SELECT title  #utilizando la palabra BETWEEN podemos acortarlo. los extremos son inclusivos
FROM films
WHERE release_year BETWEEN 1994 AND 2000;

SELECT name   #cuando hay muchos OR se puede emplear WHERE "campo" IN para hecerlo más legible
FROM kids
WHERE age IN (2, 4, 6, 8, 10);  #operación OR entre todos los valores

SELECT COUNT(*)   # busca valores nulos o que faltan (no aplica a los valores inválidos)
FROM people
WHERE birthdate IS NULL;  # NOT NULL bara buscar los que no son nulos

SELECT name   # busca valores que cumplan una determinada pauta
FROM companies
WHERE name LIKE 'Data%';  # NOT LIKE para seleccionar los que no cumplen la pauta
                          # el comodín % implica: cero, uno o varios caracteres iguales
                          # el comodín _ implica: un solo carácter
                          
```
### TEMA 3: Funciones agregadas
Las funciones agregadas realizan un cálculo sobre un conjunto de valores y devuelve un solo valor. Con la excepción de COUNT(*), las funciones de agregado ignoran los valores NULL. Las funciones de agregado se suelen usar con la cláusula GROUP BY de la instrucción SELECT.
El nombre de la columna queda con el nombre de la función agregada utilizada y el resultado es un único valor. Para cambiar el nomre de la columna se podría utilizar un alias mediante AS.

En SQL podemos hacer operaciones de cálculo directamente en el nombre de una columna mediante SELECT <operación>. En <operación> podría estar incluida una función agregada.

SQL asume que si divides un entero por un entero es que quieres que devuelva un entero, ojo porque se pueden cometer errores como:
SELECT 45 / 10 * 100.0; #devuelve 400 erróneamente
cuando veamos la posibilidad de tener decimales en la división hay que meter por lo menos un flotante
SELECT 45 * 100.0 / 10; #devuelve 45.0

```SQL

# AVG: calcula la media de los valores de la columna budget
# MAX: devuelve el valor máximo de la columna
# SUM: devuelve el sumatorio de todos los valores de la columna
# MIN: devuelve el valor mínimo de la columna
SELECT AVG(budget)  
FROM films;

SELECT MAX(budget) AS max_budget,   # se pueden asignar alias a algunos cálculos
       MAX(duration) AS max_duration
FROM films;

SELECT AVG(duration)/60.0 AS avg_duration_hours   # se pueden realizar operaciones
FROM films

SELECT (4 * 3); #devuelve el resultado de la operación básica
SELECT (4.0 / 3.0) AS result;   ##devuelve el resultado de la operación básica y lo asigna a una variable
```

### TEMA 4: Ordenando y agrupando

La ordenación **ORDER BY** por defecto es ascendente, para invertir el orden añadiremos **DESC** al final.
```SQL
SELECT title
FROM films
ORDER BY release_year DESC;  # añadida la palabra clave DESC para invertir el orden

SELECT birthdate, name    # ordenar por varias columnas
FROM people
ORDER BY birthdate, name;   #primero ordenaría por birthdate y después por name
```

La agrupación **GROUP BY** es utilizada con funciones agregadas como COUNT() o MAX(). Es lógico, porque al unirse varias filas en una, en la columna siguiente solo se pueden poner datos que provengan de todas esas filas agrupadas en una.
Hay que seguir este orden:

-SELECT

-FROM

-GROUP BY

-ORDER BY

Se retornará un error si intentas poner en SELECT un campo que no está en GROUP BY sin utilizarlo para hacer algún cálculo para toda la agrupación.
```SQL
SELECT sex, count(*)   # vamos a seleccionar un columna y la vamos a contar
FROM employees
GROUP BY sex; # agrupando por el valor de una columna

SELECT release_year, MAX(budget)    # introducimos la función agregada max
FROM films
GROUP BY release_year

SELECT release_year, country, MAX(budget) #si aquí hay 2 columnas y una tercera con una función agregada
FROM films
GROUP BY release_year, country    #aquí deben estar las 2 primeras columnas
```

En SQL, **las funciones agregadas no pueden utilizarse dentro de la claúsula WHERE**. Si queremos realizar un filtrado en base al resultado de una función agregada necesitaremos utilizar la claúsula **HAVING**.

```SQL
SELECT release_year
FROM films
GROUP BY release_year
HAVING COUNT(title) > 10;   # muestra solo los años en los que hay más de 10 títulos
```

Ejemplos didácticos todo junto:
```SQL
SELECT release_year, AVG(budget) AS avg_budget, AVG(gross) AS avg_gross   #ponemos alias a las columnas que queremos mostrar
FROM films    # la base de datos
WHERE release_year > 1990   # restringimos la búsqueda
GROUP BY release_year   # agrupamos la salida
HAVING AVG(budget) > 60000000   # restringimos la salida
ORDER BY AVG(gross) DESC    # ordenamos la salida

SELECT country, AVG(budget) as avg_budget, AVG (gross) as avg_gross   #las columnas que queremos mostrar
FROM films    # la base de datos
GROUP BY country    # group by country
HAVING COUNT(title) > 10    #where the country has more than 10 titles
ORDER BY country    # order by country
LIMIT 5   #limit to only show 5 results
```
Para consultar varias tablas relaccionadas entre si:
```SQL
SELECT title, imdb_score
FROM films
JOIN reviews
ON films.id = reviews.film_id   # indica cuál es el vínculo entre las tablas (campo clave)
WHERE title = 'To Kill a Mockingbird';
```

-----
## UNIENDO DATOS EN SQL
-----
### TEMA 1: Introducción a las uniones interiores: INNER JOIN  (se toman todos las columnas de las tablas aunque solo se muestran las deseadas)
Las uniones interiores combinan registros que están en ambas tablas.
Con INNER JOIN construimos una tabla temporal con los datos de dos tablas que son comunes en dos columnas de dichas tablas.

![INNER JOIN](https://user-images.githubusercontent.com/32695362/118518037-0b442900-b738-11eb-9089-68196032dd7e.png) .

Es una práctica común crear alias para cada tabla acortando el nombre y poniendo solo la inicial.(en todos los ejercicios se sigue esteprotocolo.

```SQL
# En ocasiones el orden lógico para escribir código es:
SELECT c.code AS country_code, name, year, inflation_rate   -- 3. Select fields with aliases
FROM countries AS c
  INNER JOIN economies AS e   #  -- 1. Join to economies (alias e)
    ON c.code = e.code;   #     -- 2. Match on code
    
# ejemplo de varias uniones consecutivas entre varias tablas:
SELECT *
FROM left_table
  INNER JOIN right_table
    ON left_table.id = right_table.id	# el campo left.table.id se mantiene como nexo común
  INNER JOIN another_table
    ON left_table.id = another_table.id;	## el campo left.table.id se mantiene como nexo común
    
# ejemplo de varias uniones consecutivas, una unión se hace sobre el resultado de la otra     
SELECT c.code, name, region, e.year, fertility_rate, unemployment_rate
  FROM countries AS c
  INNER JOIN populations AS p
    ON c.code = p.country_code	# c.code de la primera tabla es el nexo común
  INNER JOIN  economies AS e
    ON c.code = e.code;    ## c.code es el nexo común
```
Cuando unimos tablas que tienen un campo con idéntico nombre podemos utilizar **USING(campo_comun)** en lugar de ON:
```SQL
SELECT c.code AS country_code, name, year, inflation_rate
FROM countries AS c
  INNER JOIN economies AS e
    USING(code)     # elcampo común va entre paréntesis  
```
**Autouniones**: Self-ish joins, just in CASE, unimos una tabla con ella misma para obtener campos emparejados como si fuera un torneo de futbol en el que tienen que jugar todos contra todos, si no queremos jugar contra nosotros mismos hay que incluir una claúsula AND que meta una exclusión tipo <> para eviarlo
```SQL
SELECT p1.country_code, p1.size AS size2010, p2.size AS size2015  # hay que poner alias porque sino saldrían 2 colunmas con el mismo texto
FROM populations AS p1                                            # y eso es algo que no permite, lógicamente, SQL.
  INNER JOIN populations AS p2
    ON p1.country_code = p2.country_code
    
SELECT p1.country_code,
       p1.size AS size2010, 
       p2.size AS size2015,
       ((p2.size - p1.size)/p1.size * 100.0) AS growth_perc # 1. calculate growth_perc
FROM populations AS p1  
  INNER JOIN populations AS p2  #-- 3. autounión (alias as p2)
    ON p1.country_code = p2.country_code
        AND p1.year = p2.year - 5;   #cálculo para seleccionar un año en la primera y cinco años menos en la segunda
```
**CASE WHEN THEN ELSE END** se utiliza dentro de SELECT para crear una columna personalizada que se agrega a la tabla temporal resultante, pudiendo mostrar etiquetas o resultados en función del valor de otra columna.

Si queremos que la tabla no sea temporal, es decir que se mantenga para futuras consultas hay que utilizar **INTO**.

```SQL
SELECT name, continent, code, surface_area,
   CASE WHEN surface_area > 2000000 THEN 'large'
        WHEN surface_area > 350000 THEN 'medium'
        ELSE 'small' END
        AS geosize_group  #le asignamos un alias a la colunma que se va a crear y añadir al final
FROM countries

SELECT name, continent, code, surface_area,
    CASE WHEN surface_area > 2000000 THEN 'large'
       WHEN surface_area > 350000    THEN 'medium'
       ELSE 'small' END
       AS geosize_group # alias de la nueva columna
INTO countries_plus # creamos una nueva tabla que nos puede servir para la siguiente consulta
FROM countries;

SELECT country_code, size,
  CASE WHEN size > 50000000 THEN 'large'
       WHEN size > 1000000  THEN 'medium'
       ELSE 'small' END
       AS popsize_group
INTO pop_plus       
FROM populations
WHERE year = 2015;  # <-- el punto y coma indica el final de la primera consulta y el inicio de la segunda consulta sobre la primera
SELECT name, continent, geosize_group, popsize_group 
FROM countries_plus AS c
  INNER JOIN pop_plus AS p  # la tabla pop_plus fuecreada en la consulta anterior con INTO pop_plus
    ON c.code = p.country_code
ORDER BY geosize_group;

```

### TEMA 2: Uniones exteriores: LEFT y RIGHT JOINS (igual que el anterior, se toman todas las columnas de las tablas aunque solo se muestran las deseadas)
Buena explicación en español:  https://diego.com.es/principales-tipos-de-joins-en-sql .
Las uniones exteriores combinan todos los registros de una tabla con todos los que coincidan en el campo clave de otra. cuando no coincida con ninguno se pone NULL.

**LEFT JOIN**: Coge la tabla completa de la izquierda y le agrega las columnas de la tabla de la derecha que tengan el mismo campo clave, poniendo NULL en los registros no tengan pareja. Si en la tabla de la derecha hay varios registros que coincide con el mismo campo clave los añade todos repitiendo los valores de la tabla de la izquierda.

![left_join](https://user-images.githubusercontent.com/32695362/118516046-404f7c00-b736-11eb-98e7-1d03f8806241.png)
![LEFT JOIN 2](https://user-images.githubusercontent.com/32695362/118516693-d7b4cf00-b736-11eb-9da8-19f3c1c63148.png)

**RIGHT JOIN**: Igual que el anterior pero hacia la derecha. No se utiliza mucho porque en realidad se consigue lo mismo cambiando el orden en que se cogen las tablas.

```SQL
SELECT c.name AS country, local_name, l.name AS language, percent
FROM countries AS c  # From left table (alias as c)
  LEFT JOIN languages AS l  #  Join to right table (alias as l)
    ON c.code = l.code    #   campos que deben ser iguales
ORDER BY c.name DESC;
```
**FULL JOIN***: Coje todos los registros de las tablas derecha e izquierda y los une cuando tengan igual campo clave, rellenandocon NULL donde no haya coincidencia.

![FULL JOIN](https://user-images.githubusercontent.com/32695362/118520231-30399b80-b73a-11eb-9319-2979f9922e82.png).

```SQL
SELECT countries.name, code, languages.name AS language
FROM languages
  FULL JOIN countries
    USING (code)    #-- 5. Match on code
WHERE countries.name LIKE 'V%' OR countries.name IS NULL  # Where countries.name starts with V or is null
ORDER BY countries.name;
```

**CROSS JOIN**: Toma todas las combinaciones posibles de dos tablas.

![cross join](https://user-images.githubusercontent.com/32695362/118522108-ff5a6600-b73b-11eb-962e-1e7ca8bbf799.png)

```SQL
SELECT c.name AS city, l.name AS language
FROM cities AS c        
  CROSS JOIN languages AS l
```

### TEMA 3: Teoría de conjuntos (a diferencia de los tema 1 y 2 anteriores, solo se toman algunas columnas de las tablas).
Con estas instrucciones se van a crear tablas con los registros similares de dos tablas, es decir, mismos campos y del mismo tipo. la unión se realiza sin campo clave de unión. Es similar a operaciones con conjuntos. Con estas sentencias de conjuntos se apilan/juntan registros de dos tablas pero no se hacen búsquedas como ocurre con JOIN.

![conjuntos](https://user-images.githubusercontent.com/32695362/118522792-c242a380-b73c-11eb-8922-1aaf41b66282.png).

En el diagrama anterior,cáda conjunto representa una tabla de datos.

**UNION** todos los registros pero no duplica los comunes.

**UNION ALL** todos los registros repitiendo los comunes.

**INTERSECT** solo los registros que están en ambas tablas.

**EXCEPT**  los registros de la primera tabla excepto los que también están en la segunda.

```SQL
SELECT country_code
  FROM cities
	UNION   # 	-- Set theory clause
SELECT code   #  este campo debe ser similar al primero country_code, es decir, texto, número ....
  FROM currencies
ORDER by country_code;


SELECT code, year
  FROM economies
  INTERSECT  # 	-- Set theory clause
SELECT country_code, year  #  estos campos deben ser similares a los primeros code y year
  FROM populations
ORDER BY code, year;
```
**SEMI JOINS Y ANTI JOINS** (volvemos a estudiar uniones, como las que realizan INNER JOIN, SELF JOIN,LEFT JOIN, RIGHT JOIN, FULL JOIN Y CROSS JOIN y que agregaban columnas a la tabla izquierda original).
Ahora se va a utilizar la tabla de la derecha para decidir qué registros mantener en la tabla de la izquierda. (es como utilizar WHERE pero dependiendo de los valores de otra tabla. Son consultas anidadas para restringir búsquedas)
**SEMI JOINS:** elije registros de 
**SEMI JOINS Y ANTI JOINS**

```SQL
SELECT name
  FROM languages
WHERE code IN   # SEMI JOIN
  (Select code
   FROM countries
   WHERE region = 'Middle East')
ORDER BY name;

SELECT code, name
  FROM countries
  WHERE continent = 'Oceania' # varias condiciones unidas con AND
  	AND code NOT IN   # ANTI JOIN
  	(SELECT code
  	 FROM currencies);
```

### TEMA 4: Subconsultas (consultas anidadas) dentro de WHERE, SELECT y FROM.

La subconsultas sirven para reducir o establecer el subconjunto de datos donde se realizarán las búsquedas, se suelen incrustar entre paréntesis después de comprobar previamente de manera independiente que funcionan. Se pueden anidar varias unas dentro de otras.

Lo más común es que las subconsultas se encuentren dentro de las claúsulas **WHERE**.

```SQL
SELECT *
  FROM populations
WHERE life_expectancy > 1.15* 
  (SELECT AVG(life_expectancy)	#<-Subconsulta introducida como una condición más en la claúsula WHERE de la línea anterior
      FROM populations
      WHERE year = 2015)
AND year = 2015;

SELECT name, country_code, urbanarea_pop
  FROM cities
WHERE name IN
  (SELECT capital	#<-Subconsulta introducida como una condición más en la claúsula WHERE de la línea anterior
   FROM countries)
ORDER BY urbanarea_pop DESC;
   
```

Lo segundo más común es realizar subconsultas en **SELECT**, no hay que olvidar que hay que darle un alias que será la cabecera de la columna de datos resultante.
```SQL
SELECT countries.name AS country,
  (SELECT COUNT(*)	#<-Subconsulta introducida como una selección más en la claúsula SELECT de la línea anterior
   FROM cities
   WHERE countries.code = cities.country_code) AS cities_num	# hay que darle un alias AS
FROM countries
ORDER BY cities_num DESC, country
LIMIT 9;

```

Por último también se pueden ralizar subconsultas dentro de **FROM** y así establecer el grupo de datos sobre el que se realiza la consulta.
```SQL
SELECT local_name, subquery.lang_num
  FROM countries,
  	(SELECT code, COUNT(name) AS lang_num 	# subconsulta agregada a la claúsula FROM de la línea anterior
  	 FROM languages
  	 GROUP BY code) AS subquery	# alias
  WHERE subquery.code = countries.code
ORDER BY lang_num DESC;
```


