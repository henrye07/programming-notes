# Install
Para instalar este paquete debemos ir a NutGet Package Manager, existen 2 maneras: Consola e Intefaz.

Es necesario instalar los paquete de:

	-Microsoft.EntityFrameworkCore.Tools
	-microsoft.entityframeworkcore.sqlserver

## Console - Package Manager Console
Selecionamos la opcion de Package Manager Console en Tools > NutGet Package Managert.

Cargara una consola en la parte inferior donde es necesario digitar el codigo para instalar este paquete

```console
Install-Package Microsoft.EntityFrameworkCore.Tools
Install-Package Microsoft.EntityFrameworkCore.SqlServer
```

## Interfaz - Manage NutGet Package for Solutions

Selecionamos la opcion de Manage NutGet Package for Solutions en Tools > NutGet Package Managert.

Buscamos los paquetes e instalamos.


# Database First
Cuando usamos la metodologia Database First, debemos tener los datos de la base para que se cargue:

```c#
'Server=[localdb]\mssqllocaldb;Database=Blogging;Trusted_Connection=True;'
 //Server se le asigna el nommbre del servidor
 //Seguido por un \ vendrá el nombre de la BD
 //Tambien se le asigna la contraseña si este tiene y se le puede añadir opciones adicionales
```

```c#
//Entonces en la consola del Package Manager Console, se debe ingresar este codigo para conectar a la base de datos y cargar sus modelos de manera automatica
Scaffold-DbContext "Server=.\SQLEXPRESS;Database=Northwind;Trusted_Connection=True;" Microsoft.EntityFrameworkCore.SqlServer -OutputDir Models -ContextDir Context -Context NortwindContext -ContextNamespace [New.Namespace es el nombre para el context de la bd]
```

# CODE FIRST
Se deben crear los modelos como si se estuviera creando una clase normal, simplemente que sin funciones. Solo se debe declarar las variables y el tipo.
Una buena practica es crear la carpeta de va a contener los modelos.

## Ejemplo
Para este ejemplo crearemos una clase para que contenga el ID y evitar repetir mucho codigo
```c#

namespace CodeFirst.Models
{
    public class EntidadBase
    {
        public int Id { get; set; }
    }
}

namespace CodeFirst.Models
{
    public class Deposito : EntidadBase
    {
        public string Descripcion { get; set; }
        //public Domicilio Domicilio { get; set; }
        public List<Producto> Productos { get; set; }

    }
}

namespace CodeFirst.Models
{
    public class Sucursal : EntidadBase
    {
        public string Nombre { get; set; }
        public string Cuit { get; set; }
        public List<Deposito> Depositos { get; set; }
    }
}
```
Para poder especificar, migrar y crear la base de datos debemos crear un contexto que sera el encarga de darle a la base de datos todas las peticiones que se le esten generando desde los modelos.
**MODELOS -> CONTEXTO -> DB**

## CONTEXT
Una buena practica es crear una carpeta para solo este modulo.
Es necesario de ciertas librerias para llamar algunas funciones y clases como:
DbSet -> Se encargara de agregar el modelo/ Inicializarlo
```c#
using Microsoft.EntityFrameworkCore; //Conteine a DbSet, DbContext
namespace CodeFirst.Context
{
    public class CodeFirstDBContext : DbContext
    {
        //Acoplamos el modelo de clases al DbContext de EF
        public DbSet<Producto> Productos { get; set; }
        public DbSet<Marca> Marca { get; set; }
        public DbSet<Deposito> Depositos { get; set; }
        public DbSet<Sucursal> Sucursales { get; set; }

        protected override void OnConfiguring(DbContextOptionsBuilder optionsBuilder)
        {
        //Conectamos con nuestra base SQL Server usando un string de conexión
            optionsBuilder.UseSqlServer("Server=DESKTOP-2O4OU10\\SQLEXPRESS;Initial Catalog=EFCodeFirst;Integrated Security=true;"); //Integrated Security=true Permite que se cree sin proveer un User y Password
            base.OnConfiguring(optionsBuilder); 
        }
    }
}
```
Las migraciones permiten que el contexto se cree en la DB.
Esto se debe hacer a traves de la consola de Package Manager Console

```console
add-migration [FirstMigration] //Esto solo crea la migracion
update-database //Con este comando se efectuaran los cambios en la DB
```

Las migraciones tienen 2 metodos: 
	- Up: Es donde se crean todo lo relacionado a las tablas
	- Down: Dondes se puede revertir esas migraciones

### Data Annotetions
```c#
using System.ComponentModel.DataAnnotations;
namespace CodeFirst.Models
{
    public class Producto : EntidadBase
    {
        public int Id { get; set; }
        public int Codigo { get; set; }

        [MaxLength(50)] //DataAnnotesion permite añadir atributos
        [Required]
        public string Descripcion { get; set; }
        public int Peso { get; set; }
        public DateTime FechaElaboracion { get; set; }
        public Marca Marca { get; set; }
    }
}
```

Si vas a realizar cambios en algunas tablas, para que estas se actualicen en la BD se debe crear una nueva migracion y actualizacion de la DB

# GET STARTED
Para comenzar con entity una vez se tiene los modelos y el contexto creado, simplemente debemos inicializar el contexto que contiene la base de datos con los modelos para empezar a realizar las request.

```c#
using New.Namespace;

var context = new NortwindContext(); //Este es el nombre con el que se creo el contexto
```
Para entrar en algun modelo simplemente debemos llamarlo por su nombre, es decir:

**READ**
```c#
var customers = context.Customers; //Aqui cargaran todos los datos de Customers
```
Si deseamos filtrar la salida de nuestros datos, lo podemos hacer a traves de la función ***Select***
```c#
var customers = context.Customers.Select(selector => 
										 new {IdCustomer = selector.CustomerId,
										 NameCustomer=selector.CustomerName}); 
//Ademas de hacer el filtrado se le esta cambiando el nombre a las columnas, es decir para acceder a esos datos es necesario por el nombre que se le asigno anteriormente
```
Podemos usar la funcion ***Any*** para conocer si un objeto se encuentra teniendo en cuenta una condicion.
```c#
string idCustomer = Console.ReadLine();
bool anyCustomer = context.Customers.Any(x=> x.CustomerId == idCustomer.ToUpper()); //Nos devolvera True o Flase segun si existe el elemento solicitado
```
Para traer los datos de ese elemento si es unico:
```c#
var customer = context.Customers.FirstOrDefault(c=> c.CustomerId==idCustomer);
```
Para incluir los datos de otra tabla, debemos adicionar la opcion de ***Include*** antes de hacer el filtrado.
```c#
var customer = context.Customers.Include(i=>i.Orders).FirstOrDefault(c=> c.CustomerId==idCustomer);
```
**CREATE**
Para crear un nuevo objeto debemos inicializarlo desde el modelo, es decir:
```c#
using New.Namespace.Models;

var newCostumer = new Customer(){
	CustomerId="ELON",
	CompanyName="ELON MUSK",
	Orders= new List<Order>()
};

newCustomer.Orders.Add(new Order(){
	CustomerId = NewCustomer.CustomerId  || "ELON",
	OrderDate = DateTime.Now,
});

ctx.Add(newCustomer); //Aqui se esta haciendo una orden, para saber si todo esta bien y agregar el objeto
ctx.SaveChanges(); //Aqui hacemos que se suba a la base de datos
```
**UPDATE**
Para editar un objeto, usamos la misma funcion anteriormente descrita (**FirstOrDefault**)
```c#
var customer = context.Customers.FirstOrDefault(c=> c.CustomerId=="ELON");
if(customer!= null){
	customer.CompanyName= "Elon Musk Editado"; //Cambiamos el campo que deseamos
	context.SaveChanges(); // Guardamos los campos editados en la BD
}
```
**DELETE**
Para eliminar un objeto, debemos buscar el obejto a eliminar
```c#
var customer = context.Customers.FirstOrDefault(c=> c.CustomerId=="ELON");
context.Remove(customer); // Pasamos el objeto a ser removido de la BD

var ordersToDelete= context.Orders.Where(r=> r.CustomerId == "ELON"); // Para remover varios, primero debemos seleccionar todos los objetos
context.RemoveRange(ordersToDelete); //Se usa la funcion de RemoveRange porque se supone que son varios objetos lo que estamos pasando
context.SaveChanges(); //Para que se guarde en la BD y se ejecute correctamente los cambios hechos ahi.
```
## SQL PURO
Si deseamos pasar codigo SQL puro, debemos usar la funcion: **FromSqlRaw**

```c#
var sqlRaw = ctx.Customers.FromSqlRaw("SELECT * FROM Customers");
```
Se recomienda usar cuando sea una consulta muy compleja


