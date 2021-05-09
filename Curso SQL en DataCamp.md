# CURSO SQL EN DATACAMP.

## TEMA 1: Seleccionando columnas

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

## TEMA 2: Filtrando filas
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

SELECT title    # se pueden conbinar los OR y los AND, OJO porque hay reglas de precedenica
FROM films
WHERE (release_year >= 1990 AND release_year < 2000)
AND (certification = 'PG' OR certification = 'R');

SELECT title  #utilizando la palabra BETWEEN podemos acortarlo. los extremos son inclusivos
FROM films
WHERE release_year
BETWEEN 1994 AND 2000;

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
## TEMA 3: Funciones agregadas
En SQL las funciones agregadas realizan cálculos con los datos y generan una tabla con el nombre de la función y el resultado.
SQL asume que si divides un entero por un entero es que quieres que devuelva un entero, ojo porque se pueden cometer errores como:
SELECT 45 / 10 * 100.0; #devuelve 400 erróneamente
cuando seamos la posibilidad de tener decimales en la división hay que meter por lo menos un flotante
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

## TEMA 4: Ordenando y agrupando

La ordenación **ORDER BY** por defecto es ascendente, para invertir el orden añadiremos **DESC** al final.
```SQL
SELECT title
FROM films
ORDER BY release_year DESC;  # añadida la palabra clave DESC para invertir el orden

SELECT birthdate, name    # ordenar por varias columnas
FROM people
ORDER BY birthdate, name;   #primero ordenaría por birthdate y después por name
```

La agrupación **GROUP BY** es utilizada con funciones agregadas COUNT() or MAX(). Cuidado porque GROUP BY siempre va después de FROM. Y a su vez ORDER BY va siempre después de GROUP BY
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

En SQL, **las funciones agregadas no pueden utilizarse con la claúsula WHERE**. Si queremos realizar un filtrado en base al resultado de una función agregada necesitaremos utilizar la claúsula **HAVING**.
```SQL
SELECT release_year
FROM films
GROUP BY release_year
HAVING COUNT(title) > 10;   # muestra solo los años en los que hay más de 10 títulos
```

Ejemplos didácticos todo junto:
```SQL
SELECT release_year, AVG(budget) AS avg_budget, AVG(gross) AS avg_gross   #las columnas que queremos mostrar
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

