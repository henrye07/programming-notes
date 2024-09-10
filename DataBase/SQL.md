# Comandos Base
## de Definición (DDL- Data Definition Language)
```sql
CREATE DATABASE --Se utiliza para crear una nueva base de datos vacia
DROP DATABASE --Se utiliza para eliminar completamente una base de datos existente
CREATE TABLE --Se utliza para crear una nueva tabla, donde la infromación se almacena realmente
ALTER TABLE --Se utiliza para modificar una tabla existente
DROP TABLE --Se utiliza para eliminar por completo una tabla existente
ALTER COLUMN --Se utiliza para modificar una columna ya existente
DROP COLUMN --Se utiliza para eliminar por completo una columna existente
```
## de Manipulación (DML- Data Manipulation Language)
```sql
SELECT --Se utiliza cuando quieres leer (o seleccionar) tus datos
INSERT --Se utliza cuando quieres añadir (o insertar) nuevos datos
UPDATE --Se utiliza cuando quieres cambiar (o actualizar) datos existentes
DELETE --Se utliza cuando quieres eliminar (o borrar) datos existentes
REPLACE --Se utiliza cuando quieres añadir o cambiar (o reemplazar) datos nuevos o ya existentes
TRUNCATE --Se utiliza cuando quieres vaciar (o borrar) todos los datos de la plantilla/ reiniciar
```
## Adicionales
```sql
USE --Se utliza para seleccionar alguna BD
ADD --Se utiliza para añadir algo 
INNER JOIN --Selecciona los elementos contenidos entre las tablas segun la condicion que se pida. Interseccion entre*
```
## Constraints
Los constraints o resticciones de SQL se utlizan para especificar reglas para los datos de una tabla. Se utilizan para limitar el tipo de datos que pueden insertarse en una tabla, lo que asegura la precision, consistencia y confiabilidad.
```sql
NOT NULL --Asegura que una columna no pueda contenener valores null
UNIQUE --Asegura que todos los valores de la columna sean diferentes
PRIMARY KEY --Identifica a una fila de una tabla. Es una combinacion de NOT NULL y UNIQUE
FOREIGN KEY --Previene acciones que romperian la realcion con otra tabla
CHECK --Asegura que los valores de una columna cumplan cierta condicion
DEFAULT --Setea un valor por defecto a la columna, si no es especificado en el INSERT
CREATE INDEX --Usado para crear y recuperar datos de manera rapida
```
### **FOREIGN KEY**
```sql
CREATE TABLE Orders(
	OrderId INT NOT NULL PRIMARY KEY,
	OrderNumber INT NOT NULL,
	PersonId INT FOREIGN KEY REFERENCES Persons(PersonId) --De esta manera se le referencia la tabla y el campo con el cual se va a relacionar, esta debe ser una clave primaria
)
```
### CHECK
```sql
CREATE TABLE Orders(
	Id INT NOT NULL PRIMARY KEY,
	LastName VARCHAR(255) NOT NULL,
	FirstName VARCHAR(255),
	Age INT CHECK (Age>=18) --Asegurarse que el valor ingresado sea mayor o igual a 18
)
```
## WHERE
```sql
WHERE campo AND --Hacer varias condiciones
			OR 
			NOT
			IN('A..','B..') --Para buscar igualdad en un conjunto de valores
			BETWEEN --Para buscar valores entre 2 limites
			LIKE --Permite buscar por patrolenes determinados.
				 --'A%' (Personas que comiencen con A).
			
```

## ORDER BY
```sql
ORDER BY [COLUMN,...] ASC --Por Defecto
					  DESC
--Se pueden combinar 
ORDER BY [COLUMN,COLUMN2 DESC] 
```
## FUNCIONES DE AGREGACION
Devuelve un unico resultado
```sql
COUNT --Devuelve el numero total de filas seleccionadas por la consulta
MIN -- Devuelve el valor minimo del campo que especifiquemos
MAX -- Devuelve el valor maximo del campo que especifiquemos
SUM -- Suma los valores del campo que especifiquemos. Solo se puede utilizar en columnas numericas
AVG --Devuelve el valor promedio del campo que especifiquemos. Solo se puede utilizar en columnas numericas
```
**EJEMPLO**
```sql
SELECT COUNT(Id) FROM Persons
--1985
```
## **EJEMPLO**
```sql
-- DEFINICION -----------------------

CREATE DATABASE Nombre; --Creara la base de datos Nombre
USE Nombre; --Ingresamos a la BD Nombre
DROP DATABASE Nombre; --Eliminara la BD Nombre

CREATE TABLE Personas(
	-- Nombre del campo | Tipo ,de dato | otros parametros o campos -> PRIMARY KEY
	Id INT IDENTITY(1,1) PRIMARY KEY,  
	Nombre VARCHAR(50) NOT NULL,
	Apellido VARCHAR(50) NOT NULL
); --Creara una tabla llamada Personas con los campos descritos dentro

--Añadir nuevos campos
ALTER TABLE Personas
ADD Edad INT NOT NULL 
--Borrar Campos existentes
ALTER TABLE Personas
DROP COLUMN Edad  

```

```sql
-- MANIPULACIÓN -----------------------

INSERT INTO Personas (Nombre, Apellido, Edad) --Insertamos dentro de la tabla indicada e indicamos los valores a ingresar/orden
VALUES ('Ruben','Rueda',26) --Le asignamos los valores

UPDATE Personas --Ingresamos a la tabla escrita para actualizar algunos valores
SET Nombre = 'Juan', --SET permite asignar los valores a los campos
	Apellido = 'Rodriguez',
	Edas = 23
WHERE Id = 1 --WHERE es un filtro para decirle en que lugar se va a actualizar

DELETE FROM Personas --Eliminara de la tabla escrita algun valor o todos si no se especifica el ID
WHERE Id = 1

TRUNCATE TABLE Personas --Reiniciara la tabla

SELECT * FROM Personas --Selecionamos la todos los datos de cierta tabla
SELECT Id,Nombre FROM Personas --Si deseamos traer solo algunos campos
SELECT Id, Nombre + ' ' + Apellido AS Descripcion FROM Personas --Concatenación en peticion con el alias Descripcion
WHERE Id = 1
```

```sql
--Para insertar un alias de una tabla podemos hacer lo siguiente
SELECT * FROM Users u  --Despues del nombre le asignamos el alias, en este caso u
INNER JOIN Users_Roles ur --Alias ur
ON u.Id = ur.IdUser --Una vez dados los alias, podemos usarlos en los demas comandos para acciones posteriores

--Tambien es posible anidar JOINS
INNER JOUN Roles r
ON ur.IdRole = r.Id
```

