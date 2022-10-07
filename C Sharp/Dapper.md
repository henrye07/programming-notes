Es un micro ORM que permite realizar y gestionar API's
# Install
Para instalar se puede realizar a traves del gestor de paquetes de Nuget Package Manager.

```
Dapper
System.Data.SqlClient
```

# GET STARTED
De igual manera que Entity Framework, es necesario crear los modelos que se va a crear o como esta elaborada la DB:

Como buena practica es conveniente crear diferentes carpetas como Models, Controllers, Data, Rules.

	- Models -> Se crean los modelos, es decir, la tabla con sus respectivos campos
	- Controllers -> Se crean las rutas y lo que devuelve cada endpoint
	- Rules -> Se creara las acciones/funciones correspondientes a cada Modelo
	- Data -> Aqui se define lo que realizara cada funcion, desde la coneccion hasta lo que retorna.

```c#
//Models
namespace ApiDapper.Models
{
    public class Products
    {
      public int ProductID {get; set;}
      public string ProductName {get; set;}
      public int SupplierID {get; set;}
      public int CategoryID {get; set;}
      public string QuantityPerUnit {get; set;}
      public decimal UnitPrice {get; set;}
      public int UnitsInStock {get; set;}
      public int UnitsOnOrder {get; set;}
      public int ReorderLevel {get; set;}
      public bool Discontinued {get; set;}
    }
}
```

```c#
//Data
using ApiDapper.Models;
using Dapper;
//using Microsoft.Data.SqlClient; //Problemas de autenticacion
using System.Data.SqlClient;

namespace ApiDapper.Data
{
    public class NorthwindData
    {
        public List<Products> GetAllProducts()
        {
            using (var conn = new SqlConnection("Server=localhost\\SQLEXPRESS;Database=Northwind;Trusted_Connection=True; Integrated Security=true;"))
            {
                conn.Open();
                var query = "SELECT * FROM Products";
                var listProduct = conn.Query<Products>(query).ToList();
                //conn.Close(); Si uso using no necesito usar esta funcion
                return listProduct;
            }
        }

        public Products GetProductById(int id)
        {
            using (var conn = new SqlConnection("Server=localhost\\SQLEXPRESS;Database=Northwind;Trusted_Connection=True; Integrated Security=true;"))
            {
                conn.Open();
                var query = "SELECT * FROM Products WHERE ProductId = @NuestroId";
                //var product = conn.Query<Products>(query).FirstOrDefault();
                var product = conn.QueryFirstOrDefault<Products>(query, new { NuestroId = id });
                return product;
            }
        }
    }
}
```

```c#
//Rules
using ApiDapper.Data;
using ApiDapper.Models;

namespace ApiDapper.Rule
{
    public class ProductRule
    {
        public List<Products> GetAllProducts()
        {
            var data = new NorthwindData();
            return data.GetAllProducts();
        }

        public Products GetProductById(int id)
        {
            var data = new NorthwindData();
            return data.GetProductById(id);
        }

        public Products GetProductById(Products p)
        {
            var data = new NorthwindData();
            return data.GetProductById(p);
        }
    }
}
```

```c#
//Controllers
using ApiDapper.Models;
using ApiDapper.Rule;
using Microsoft.AspNetCore.Http;
using Microsoft.AspNetCore.Mvc;

namespace ApiDapper.Controllers
{
    [Route("api/[controller]")]
    [ApiController]
    public class TestController : ControllerBase
    {
        [HttpGet("/api/products")]
        public List<Products> GetAllProducts()
        {
            var rule = new ProductRule();
            return rule.GetAllProducts();
        }

        [HttpGet("/api/products/{id}")]
        public Products GetProductById(int id)
        {
            var rule = new ProductRule();
            return rule.GetProductById(id);
        }
    }
}
```

La implementacion de Dapper se da simplemente en la carpeta de ***'Data'***, ya que, es ahí donde se genera la conexion a la BD y request respectivas.

```c#
conn.Query<Products>(query).ToList(); // Sirve para una query sin parametros
conn.Query<Products>(query, new {nuevoNombre=table.columnName,...}).ToList(); // Sirve para una query con parametros, como primer parametro recibe la query y como 2do recibe los parametros
conn.Query<Products>(query, param).ToList();
```

Existe una propiedad muy comun de Dapper que es el ***Execute*** que permite realizar querys de tipos Delete o donde se vean afectadas las filas. Ya que este metodo retorna un **int** de las filas afectadas.

```c#
 var queryDetail = "DELETE FROM [Order Details] WHERE OrderID = @orderId";
var cant = conn.Execute(queryDetail, new { orderId },tran);
```
Este tipo de codigos es preferible utilizar a traves de un Try-Catch para manejar los errores. Ademas, cuando se esta haciendo este tipo de funciones se puede decir que estamos realizando transacciones, por tanto, un codigo con buenas practicas del ejemplo anterior seria:

```c#
public int DeleteOrderById(int orderId)
        {
            using var conn = new SqlConnection(_urlconn);
            conn.Open();
            var tran = conn.BeginTransaction();
            try
            {
                var queryDetail = "DELETE FROM [Order Details] WHERE OrderID = @orderId";
                var cant = conn.Execute(queryDetail, new { orderId },tran);
                
                var queryOrder = "DELETE FROM Orders WHERE OrderID = @orderId";
                cant += conn.Execute(queryOrder, new { orderId },tran);
                
                tran.Commit();
                return cant;
            }
            catch (Exception)
            {
                tran.Rollback();
                throw;
            }
            finally
            {
                conn.Close();
            }
            
        }
```