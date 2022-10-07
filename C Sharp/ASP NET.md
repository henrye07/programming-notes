En Visual Studio 2022 tenemos diferentes templates que nos permiten crear aplicaciones base con algunos documentos o archivos por defecto. De entre las cuales podemos destacar unas carpetas:

	-WWWROOT ->Es donde se encuentran todos los archivos estaticos y dinamicos de la app
	-Properties -> Es donde se encuentra la configuracion del servidor
	-Appsettings.json -> Es el archivo que permite configurar los permisos y otras configuraciones de nuestra app
	-Pages -> Se van a encontrar las paginas que se mostraran en el app, las cuales tienen extencion .cshtml para permitir incluir codigo c#

# MVC
Si se utiliza el modelo MVC (Model-View-Controller), tiene la misma sintaxis, pero se dividiran en diferentes carpetas para tener otra manera de organizar los datos.

	-Model -> Tendra todos los modelos que se implementaran en la aplicacion
	-Controller -> Contendra las acciones para ejecutar y visualizar una VIEW. Es donde pasan los datos para ser mostrados en la View.
	-View -> Es donde se encuentran las vistas o paginas, es decir, los archivos cshtml

[Detalles de las carpetas y funciones de MVC](https://learn.microsoft.com/es-es/aspnet/core/mvc/overview?view=aspnetcore-6.0)

```c#
//Controller/HomeController.cs
public class HomeController : Controller
{
	public IActionResult Index() //El nombre de el archivo en la carpeta View es el nombre de la funcion para crear la funcion en el archivo de Controller, esta es la manera para visualizar una pagina
        {
            return View();//Dentro de la funcion View, es donde se debe pasar parametros si esta requiere o tiene funciones especiales una vez se pasa una variable, ejemplo en Error
        }
        public IActionResult Error()
        {
            return View(new ErrorViewModel { RequestId = Activity.Current?.Id ?? HttpContext.TraceIdentifier }); // Aqui se esta usando la clase creada en Models y la View de Error a visualizar
        }
}
```
```c#
//Models/Error.cs
namespace WebApplication1.Models
{
    public class ErrorViewModel
    {
        public string? RequestId { get; set; }

        public bool ShowRequestId => !string.IsNullOrEmpty(RequestId);
    }
}
```
```c# 
//View/Error.cshtml
@model ErrorViewModel
@{
    ViewData["Title"] = "Error";
}

<h1 class="text-danger">Error.</h1>
<h2 class="text-danger">An error occurred while processing your request.</h2>

@if (Model.ShowRequestId)
{
    <p>
        <strong>Request ID:</strong> <code>@Model.RequestId</code>
    </p>
}

<h3>Development Mode</h3>
<p>
    Swapping to <strong>Development</strong> environment will display more detailed information about the error that occurred.
</p>
<p>
    <strong>The Development environment shouldn't be enabled for deployed applications.</strong>
    It can result in displaying sensitive information from exceptions to end users.
    For local debugging, enable the <strong>Development</strong> environment by setting the <strong>ASPNETCORE_ENVIRONMENT</strong> environment variable to <strong>Development</strong>
    and restarting the app.
</p>

```

# CSHTML
Para poder ejecutar codigo c# en los archivos **.cshtml** debemos hacer a traves del **@**:
```cshtml || c#
@{
	ViewData["Title"]= "Cabecera Pagina";
}
```

El archivo **_ViewStart.cshtml_** contiene el layout que se mostrara en todas las paginas.
```cshtml || c#
@{
	Layout = "_Layout";
}
```
El archivo **_ViewImports.cshtml_** contiene los paquetes que pueden ser implementados dentro de las View o paginas



