# Comandos Base
## de Definición
```sql
CREATE DATABASE --Se utiliza para crear una nueva base de datos vacia
DROP DATABASE --Se utiliza para eliminar completamente una base de datos existente
CREATE TABLE --Se utliza para crear una nueva tabla, donde la infromación se almacena realmente
ALTER TABLE --Se utiliza para modificar una tabla existente
DROP TABLE --Se utiliza para eliminar por completo una tabla existente
ALTER COLUMN --Se utiliza para modificar una columna ya existente
DROP COLUMN --Se utiliza para eliminar por completo una columna existente
USE --Se utliza para seleccionar alguna BD
ADD --Se utiliza para añadir algo 
```
## de Manipulación
```sql
SELECT --Se utiliza cuando quieres leer (o seleccionar) tus datos
INSERT --Se utliza cuando quieres añadir (o insertar) nuevos datos
UPDATE --Se utiliza cuando quieres cambiar (o actualizar) datos existentes
DELETE --Se utliza cuando quieres eliminar (o borrar) datos existentes
REPLACE --Se utiliza cuando quieres añadir o cambiar (o reemplazar) datos nuevos o ya existentes
TRUNCATE --Se utiliza cuando quieres vaciar (o borrar) todos los datos de la plantilla/ reiniciar
```

**EJEMPLO**
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

INSERT INTO Personas (Nombre, Apellido, Edad) --Insertamos dentro de la tabla indicada y los valores a ingresar
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
