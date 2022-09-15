# Tipo de Dato
Entre los tipos de datos mas frecuentes, se encuentran:
```c#
int , string , bool , float , decimal
```
Sin embargo, tambien se puede usar la palabra reservada
```c#
var 
```
La cual le asigna el TD que tiendra esta variable segun el valor/función que se le asigne
```c#
var name= 123; //Será del tipo int 
```
Además, toda variable o linea de codigo debe finalizar con **; (Punto y coma)**
# Variables
```c#
//  Privado, Publico | Tipo de Dato | Nombre de la variable
public int name;
``` 
Cuando una variable es del tipo privado, se recomienda la siguiente sintaxis en el nombre:
```c#
private var _name;
```
# Print/Set Value
La manera de imprimir un valor es la siguiente:
```c#
Console.WriteLine("Mensaje a mostrar");
//Con variable seria:
Console.WriteLine($"Mensaje con la variable {name}");
Console.WriteLine("Mensaje con la variable "+name);
```
Para ingresar/pedir un valor:
```c#
var name = Console.ReadLine();
//Se almace en la variable 'name' el valor ingresado
//Esto regresa un STRING
```
Para convertir un valor se debe usar el tipo de dato al que se desea cambia, junto a la funcion **PARSE**
```c#
var name = int.Parse(Console.ReadLine());
//Regresa un int
```
# Array
Para crear un Array se debe usar la siguiente sintaxis:
```c#
//Tipo de dato+[] | Nombre de la variable += | new Tipo de dato+[cantidad de datos]
int[] name = new int[10];
//Para conocer el tamaño, usamos:
name.Length
```
## Matriz
```c#
//Tipo de dato+[,] | Nombre de la variable += | new Tipo de dato+[filas,columnas]
//La coma representa las dimensiones
int[,] name = new int[10,2];
//Existen funciones para conocer estos valores asignados en las filas y columnas
 name.GetLength(0); //Filas
 name.GetLength(1); //Columnas
```
# Condicionales
```c#
// if-else
if(condicion){
	accion
}else if(condicion 2){
	accion 2
}else{
	accion 3
}
```
## Iteradores
```c#
// definimos el iterador | definimos la condicion para finalizar | definimos el incremento
for(int i=0; i>n;i++){
	accion
}
```
```c#
// definimos la condicion para que termine
while(condicion){
	accion
}
```
# Class
Una clase en C# tiene la sigueinte sintaxis:
```C#
namespace nombrePaquete //Nombre del paquete
{
    internal class Billetera //Nombre de la Clase en UpperCase
    {

        public int BilletesDe10 {get;set;} //Inicializacion de variables

        public decimal Total() { //Funcion, si se define el tipo de dato se debe generar una return al final
			return accion
        }
        public void Total() { //Funcion, cuando tiene 'void' significa que no devuelve nada la funcion, solo ejecuta una accion
			accion
        }
    }
}
```
Para poder usar la clase en otro ventana, se debe en primer lugar llamar al nombre del paquete. Asi:
```C#
using nombrePaquete;

var name = new Billetera();
//Tambien se le puede asignar valores si se desea, dependiendo el tipo de variable que tenga
var name = new Billetera()
{
	BilletesDe10=12,
	...
};
```
Para crear un metodo constructor, este debe tener el mismo nombre que la **class**
```C#
namespace nombrePaquete 
{
    internal class Baraja //Nombre de la Clase en UpperCase
    {
        private int _var1;
        ...
        
		public Baraja() //Constructor es lo que primero se ejecuta despues de inicializar las variables, se le puede asignar variables o parametros de entrada
        {
            accion...
        }

		public Baraja(var const1,var const2,...)
		{
			_var1=const1;
			...;
		}
        
    }
}
```
## Herencia
La herencia se realiza para unir 2 o más clases, sin embargo, esta solo acepta 1 class. Para agregar mas, se debe realizar a traves de interfaces.
### Clase Abstracta
Este tipo de clases simplemente permiten generalizar un metodo y en la clase que se herede se encarga de darle su propia funcionalidad, asi:
```c#
public abstract class Cuadrilatero
    {
        public Cuadrilatero(int cord_x_1, int cord_y_1, int cord_x_2, int cord_y_2, int cord_x_3, int cord_y_3, int cord_x_4, int cord_y_4) { }
           

        public abstract void Area();
      
    }
```

```c#
public class Cuadrado : Cuadrilatero
{
	... //Inicializar variables
	public Cuadrado(int cord_x_1, int cord_y_1, int cord_x_2, int cord_y_2, int cord_x_3, int cord_y_3, int cord_x_4, int cord_y_4) : base(cord_x_1, cord_y_1, cord_x_2, cord_y_2, cord_x_3, cord_y_3, cord_x_4, cord_y_4)
        {
            _cord_x_1 = cord_x_1;
            ...
            //Como hereda de Cuadrilatero, se debe tener las misma cantidad de parametros que la clase Padre
        }
	public override void Area() //Se escribe override para darle la funcionalidad a esa clase del padre
	{
		var bas = _cord_x_4 - _cord_x_1;
		var altura = _cord_y_2 - _cord_y_1;
		var area = altura * bas;
		Console.WriteLine($"El area del cuadrado es: {area}");
	}
}
```
