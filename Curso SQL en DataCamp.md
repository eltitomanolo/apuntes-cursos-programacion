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

```




