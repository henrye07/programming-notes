# Install
For install Flutter is necessary follow the instructions in the documentation

# First Steps
From the package:

```dart
import 'package:flutter/material.dart'
```

A lot of widgets are in this package of Material Design, that give us SDK Flutter

We can find that in the first app, in ***main.dart***

 The class is known as Widget. It's for that almost all in Flutter is a widget.

# Basic Widgets 
## Text
This is the structure:

```dart
Text( 
	'Hello, $_name! How are you?', //First is the text to show 
	 textAlign: TextAlign.center, //Align of the text
	 overflow: TextOverflow.ellipsis, //Capsule the text or dont show one text front of other
	 style: const TextStyle(fontWeight: FontWeight.bold), //Style of the text
	 )
```

## Row
This widget permit to get multiples widgets within and that show it as differents row
```dart
Row( 
	children: const <Widget>[ 
		Expanded( child: Text('Deliver features faster', textAlign: TextAlign.center), ), 
		Expanded( child: Text('Craft beautiful UIs', textAlign: TextAlign.center), ), 
		Expanded( child: FittedBox( child: FlutterLogo(), ), ), ], 
)
```

## Column
Similar to Row but it's in Column
```dart
Column( 
	children: const <Widget>[ 
		Text('Deliver features faster'), 
		Text('Craft beautiful UIs'), 
		Expanded( child: FittedBox( child: FlutterLogo(), ), ), 
	], 
)
```

## Stack
It's a potential because that allow to give the position like we want in x,y,z
```dart
Stack( 
	children: <Widget>[ 
		Container( width: 100, height: 100, color: Colors.red, ),
		Container( width: 90, height: 90, color: Colors.green, ),
		Container( width: 80, height: 80, color: Colors.blue, ), 
	], 
)
```

## Container
It's similar to **div** in html, that have a great application in every widget
```dart
Center( 
	child: Container( 
	margin: const EdgeInsets.all(10.0), 
	color: Colors.amber[600], 
	width: 48.0, 
	height: 48.0, 
	), 
)
```

# State Widget
the user has a interaction with that widget like checkbox, ratio,Form,...
That widget come from the class ***"StateFulWidget"*** 

# Widget without State
That widget come from the class ***"StateLessWidget"***. This kind of widget is the Icone, Text, Container with color.

# Layout
It's the matter for organizate the position for every widget, or how the widget go to get in the display

# Create a Widget
So how all dependent by the library describe ahead, first is necessary to import the library.

```dart
import 'package:flutter/material.dart';
```
After that we need to know if our widget is a static or no static widget. BEcause for create a new class we need to extend or heredate some father class

```dart
class DescribePerson extends StaticLessWidget {
//Within we need to override the method Build for describe the new Widget
	@override
	Widget build(BuildContext context) {

	final title_class = Column(
	
		children: <Widget>[
			Container(
			margin: EdgeInsets.only(top: 150, left: 15, right: 15),
			child: Text(
				"This, That, These, Those",
				style: TextStyle(fontSize: 20, fontWeight: FontWeight.w600),
				textAlign: TextAlign.right,
			),
			)
		],
	);
	return title_class;
	}
}
```

For use our new widget, we need to import the package. So, if that is in the same folder, we go to do this:

```dart
import 'describe_person.dart';
//if we go to implement direct in the Scaffold Body
class MyApp extends StatelessWidget {

	const MyApp({Key? key}) : super(key: key);

@override
Widget build(BuildContext context) {

return MaterialApp(
	title: 'Flutter Demo',
	theme: ThemeData(
		primarySwatch: Colors.blue,
		),
	home: Scaffold(
		appBar: AppBar(
			title: Text("Hola Mundo"),
			),
			body: new DescribePerson(),
		)
	);
	}
}
```

## Add Typografy
If we want to add a different typografy, fisrt we need to download and after that we go to paste in some folder (Recommend to create a new folder with name **fonts**) the file with extension ttf.

After that, we need to configurate the ***pubspec.yaml*** file, then, below the *flutter* we take down this:

```yaml
...
flutter:
 fonts:
  - family: Lato
	fonts:
		- assest: fonts/Lato-Regular.ttf
```

For to use the new typografy, we go to the widget and within *style*>*TextStyle*. We're going to write fontFamily and the name we give in the file yaml, so:

```dart
style:TextStyle(
	fontFamily: "Lato",
	...
)
```

# Add Images
If we want to add images in the app, we need to do the same as in Typografy. First, we need to edit the file **pubspec.yaml** with this:

```yaml
flutter:
	assests:
		- assets/img/first.jpg
```

That was only for specific file, but we can do it with a directory, like this:
```yaml
flutter:
	assests:
		- assets/img/
```

And for integrate in the project we need to go in the image option and implemment the function ***AssetImage***, like this:
(Always we want to use decoration, we need to apply the valuos for heigth and width)

```dart
heigth: 100,
width: MediaQuery.of(context).size.width,
decoration: BoxDecoration(
	shape: BoxShape.rectangle,
	image: DecorationImage(
		fit: BoxFit.fill, 
		image: AssetImage(pathImage)
	)
),
```

In some times that process can't work but it's necessary refresh or reset the app, that could work.

The other way to integrate some image is with the widget ***Image***, this is the way to implemment that widget:

```dart
Container(
	margin: EdgeInsets.only(
		top: 50,
		right: 15,
		left: 15,
	),
	child: Image(
		fit: BoxFit.cover, 
		image: AssetImage(pathImage)
	),
);
```

They have a great different because the option **decoration** allow to do or add more things, as box shadow, gradient, ...

# Add Gradients
We need to create a Container with the characteristics for boundle our interface. Is similar to a background color in CSS

So, in example that goes to see as this:

```dart
class GradientBack extends StatelessWidget {
	@override
	Widget build(BuildContext context) {
		return Container(
			height: 250,
			decoration: BoxDecoration(
				//This option is the gradient
				gradient: LinearGradient(
					colors: [Color(0xFF4268D3), Color(0xFF584CD1)],
					begin: FractionalOffset(0.2, 0.0), //Oritation for the gradient
					end:
					FractionalOffset(1.0, 0.6), //Darkness color until where that goes
					stops: [0.0, 0.6], //Similar to orientation, up to down or down to up
					tileMode: TileMode.clamp,
				),
			),
		);
}
}
```

# ListView
The **ListView** is a potential tool for do a list vertical or horizontal, and for implemment within our project is just neccesary call that widget, like this:
```dart
Container(
	child: ListView(
		padding:EdgeINsets.all(25),
		scrollDirection:Axis.horizontal, //Direction for scroll
		children: [CourseList()], //This is some way, but we can use this:
		children: <Widget>[
			CardImage("Hola"),
			CardImage("Hola"),
			CardImage("Hola"),
			CardImage("Hola"),
		]
	),
),
```

# Main App with Multiples Widgets (Stack Widget)
For integrate multiples widgets in the main, is the same like in a normal widget. With a option of **Stack**(This Widget allow to put a element front the other) and log in ***children*** 

```dart
body: Stack(
	children: <Widget>[
		ListView(
			children: [			
				CourseList()
			],
		),
		GradientBack()
	],
),
```

# Buttom
