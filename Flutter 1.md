# Flutter

## Container widget

```dart
import 'package:flutter/material.dart';

void main() {
  runApp(MyApp());
}
//can create a statelesswidget by simply writing stlss
class MyApp extends StatelessWidget {     //using stateless widgets for hot reloading
  @override
  Widget build(BuildContext context) {
    return MaterialApp(
      home: Scaffold(
        backgroundColor: Colors.black12,
        body: SafeArea(             //used for keeping the widgets from being cut by the bezels
          child: Container(
            color: Colors.teal,
            child: Text('hello'),
            height: 100.0,
            width: 100.0,
            margin: EdgeInsets.all(23),   //used for margins from the scaffold
            padding: EdgeInsets.all(34),  // used for margins inside the container(or any widget) 
          ),
        ),
      ),
    );
  }
}
```

- We can use Row or column for putting in multiple containers inside it.

  ```dart
  body: SafeArea(
  	child: Row(		//Or column
              verticalDirection: VerticalDirection.down, //can use .down
              mainAxisSize: MainAxisSize.max, //can use .max to maximize the space taken up by column on screen
             	mainAxisAlignment: MainAxisAlignmen.spaceAround, //used to move & space between the different 															//widgets in the column
              crossAxisAlignment: CrossAxisAlignment.end,
  		children: <Widget>[					//square brackets because it's a list of widgets
              								//We use children inside row or column	
  			Container(
                  color: Colors.red,
                  child: Text('Container 1'),
                  height: double.infinity,
                  width: 70.0,
                ),
              SizedBox(		//space between containers	
                  width: 120, 	//we are inside row so we use width, if Column then use height
                ),
              Container(
                  color: Colors.white,
                  child: Text('Container 2'),
                  height: double.infinity,
                  width: 70.0,
                ),
  		]						
  	)
  )
  ```

- More Widgets (changing the font, font size, color of text..etc.)

  ```dart
  CircleAvatar(			//Generally used for profile picture image
                radius: 50,										//also don't forget to update pubspec.yaml
                backgroundImage: AssetImage('images/hand.jpg'),		//So the image fits in a circular manner
              ),
              Text(
                'Vikas Pradhan',
                style: TextStyle(
                  fontSize: 23,
                  fontWeight: FontWeight.bold,
                  color: Colors.white,
                ),
              )
  ```

- Icon Widget....Different type of icons preloaded with flutter

  ```dart
  Container(			//Inside a container 
      child: Row(			//make a row
          children: <Widget>[		//a children a list of widgets
                    Icon(			//icon widget
                      Icons.phone,		//phone call icon
                      size: 25,
                      color: Colors.teal[500],
                    ),
     )
  )
  ```

  
  
- Can resize App icon by going to android/app/main/src/res  then right click- new - image assets ...change the size of the app icon.

- To make just a simple horizontal line between texts or Containers we can use **Divider** in **SizedBox**.

  ```dart
  Sized (
                  height: 20,
                  width: 150,
                  child: Divider(
                    color: Colors.teal.shade100,
                  ),
                ),
  //OUTPUT it'll just make a simple horizontal line in between wherever you put it.
  //____________
  ```

- To make our Containers Look better...like curvy edges and have a bit of shadow underneath it....we can use **Card** instead of Container.

  ```dart
  Card(							//Used instead of Container.
                  elevation: 20,
                  shadowColor: Colors.teal[900],
                  color: Colors.white,
                  margin: EdgeInsets.symmetric(vertical: 10, horizontal: 30),
                  child: Padding(			//Padding is used as a parent since ListTitle can't have Padding
                      padding: EdgeInsets.all(0),
                      child: ListTile(	//If you use ListTitle you can easily manage icon and texts  
                        leading: Icon(		//leading widget
                          Icons.phone,
                          size: 25,
                          color: Colors.red[500],
                        ),
                        title: Text(
                          '+123 543 5468',
                          style: TextStyle(
                            fontSize: 20,
                            fontFamily: 'SourceSansPro',
                          ),
                        ),
                      ),
                  ),
                ),
  ```

- We can use **Image widget** in other ways as like this

  ```dart
  child: Image.asset('images/dice1.png'),
  //Instead of 
  child: Image(
      image: ImageAssest('images/dice1.png'),
  )
  ```

- **Expanded widget** so it fits every screen size automatically

  ```dart
  Expanded(
              child: Padding(
                padding: const EdgeInsets.all(16.0),
                child: Image.asset('images/dice1.png'),
              ),
            ),
  ```

- Can use **flex** **property** inside of Expanded widget so...to define the ratios of widgets inside it...like an Image widget.

  ```dart
  Expanded(
              flex: 2,   //It's decides how much part of the screen should be given according to ratio.
              child: Padding(
                padding: const EdgeInsets.all(16.0),
                child: Image.asset('images/dice2.png'),
              ),
            ),
  ```

- **FlatButton** , it is one of many buttons.

  ```dart
  Expanded(
  	child: FlatButton(				//The button is on the image
  		onPressed:(){
  			print('hello');
  		},
          child: Image.assest('images/dice.png'),
  	),
  ),			
  ```


## Stateful widgets

We use Stateful widgets when there is supposed to a change on screen when the user presses something.

Stateless widgets are used for something that isn't gonna change ...like the AppBar.

```dart
//stful and enter will create everything for you
//like this
class dice extends StatefulWidget {		//you can change the name of class from dice to anything
  @override
  _diceState createState() => _diceState();
}

class _diceState extends State<dice> {
  @override
  Widget build(BuildContext context) {
    return Container();			//we delete the Container() and do everything here.
  }
}

```

Example of widgets inside Stateless widget

```dart
class _DicePageState extends State<DicePage> {
  int leftImg = 1; //int variable
  @override
  Widget build(BuildContext context) {
    return Center(
      child: Row(
        children: <Widget>[
          Expanded(
            child: FlatButton(
              onPressed: () {	//what the app should do upon being pressed the button
                setState(() {
                  //Calls the build function and updates it for user.
                  leftImg += 1;
                });
              },
              child: Image.asset('images/dice$leftImg.png'),	// $ sign is used to access the value of variable 
            ),
          ),
          Expanded(
            //flex: 2,
            //It's decides how much part of the screen should be given according to ratio.
            child: FlatButton(
              onPressed: () {},
              child: Image.asset('images/dice2.png'),
            ),
          ),
        ],
      ),
    );
  }
}

```

## Creating a Method(Function) in Dart

```dart
void randInt() {
    //Creating a method in dart
    setState(() {
      //Calls the build function and updates it for user.
      img = Random().nextInt(5) + 1;
      img2 = Random().nextInt(5) + 1;
    });
  }
```

### Calling the Method(Function) in Dart

```dart
child: FlatButton(
              onPressed: () {
                randInt();
                //Calling the created randInt() method
              },
              child: Image.asset('images/dice$img.png'),
            ),
```

Using it in Flutter dart code.

```dart
class DicePage extends StatefulWidget {
  //stateful widgets which allows you to change the state of app when something is pressed
  @override
  _DicePageState createState() => _DicePageState();
}

class _DicePageState extends State<DicePage> {
  int img = 1, img2 = 1;

  void randInt() {
    //Creating a method in dart
    setState(() {
      //Calls the build function and updates it for user.
      img = Random().nextInt(5) + 1;
      img2 = Random().nextInt(5) + 1;
    });
  }

  //int variable
  @override
  Widget build(BuildContext context) {
    return Center(
      child: Row(
        children: <Widget>[
          Expanded(
            child: FlatButton(
              onPressed: () {
                randInt();
                //Calling the created randInt() method
              },
              child: Image.asset('images/dice$img.png'),	//$ sign is used in dart for String Interpolation
            ),
          ),
          Expanded(
            //flex: 2,
            //It's decides how much part of the screen should be given according to ratio.
            child: FlatButton(
              onPressed: () {
                randInt(); //Calling the created randInt() method for 2nd time
              },
              child: Image.asset('images/dice$img2.png'),
            ),
          ),
        ],
      ),
    );
  }
}
```



## Magic Ball 8 Code

```dart
import 'package:flutter/material.dart';
import 'dart:math';

void main() => runApp(
      MaterialApp(
        home: BallPage(),
      ),
    );

class BallPage extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    return Scaffold(
      backgroundColor: Colors.deepPurple,
      appBar: AppBar(
        backgroundColor: Colors.purpleAccent[200],
        title: Text('Ask Me Anything'),
      ),
      body: Ball(),
    );
  }
}

class Ball extends StatefulWidget {
  @override
  _BallState createState() => _BallState();
}

int x = 3;
void randInt() {
  x = Random().nextInt(5) + 1;
}

class _BallState extends State<Ball> {
  @override
  Widget build(BuildContext context) {
    return FlatButton(
      onPressed: () {
        setState(() {
          randInt();
        });
      },
      child: Center(
        child: Image.asset('images/ball$x.png'),
      ),
    );
  }
}
```

## Packages in flutter

- Get the packages from here - https://pub.dev/flutter/packages?q=

- For Installing the pacakge we should take a look at the installation page in the website for the package.

- Then update the pubspec.yaml file and add dependencies like this...

```yaml
dependencies:
  flutter:
    sdk: flutter
  english_words: ^3.1.5		#English words package was taken from that website(It had higher rating than others) 
  cupertino_icons: ^0.1.2	#Icons package is developed by flutter team and is preloaded with flutter projects
```

- After that run pub get (if not using Android studio then type pub get in terminal)

- After that import your package

```dart
import 'package:english_words/english_words.dart';
```

- Now if you check in External Libraries=>Dart Packages you should see this =>english_words - 3.1.5 package added.

- Note that the version of the package doesn't matter that much after 3.  | You could have also written 3.0.7 and it would still run the same. But If you don't add any number just (english_words: ) it would still run but it would get any version and may be unstable.

- The above goes for any package on that website.

- For using the package in code ...

  ```dart
  import 'package:flutter/material.dart';
  import 'package:english_words/english_words.dart';
  
  void main() => runApp(XylophoneApp());
  
  class XylophoneApp extends StatelessWidget {
    @override
    Widget build(BuildContext context) {
      return MaterialApp(
        home: Scaffold(
          backgroundColor: Colors.red,
          body: SafeArea(
            child: Center(
              child: Text(
                adjectives[123],	//Here we use the 123rd word from adjectives list...there are nouns also
              ),
            ),
          ),
        ),
      );
    }
  }
  ```

- To see what is inside the package we got go to External Libraries=>Dart Packages=>english_words - 3.1.5=>src=>words.

### The Xylophone App

- We have to download a package from https://pub.dev/packages?q=

- Downloaded the  audioplayers Package....Installed and imported it and all.

- Then in the Package web page we read the ReadMe docs and searched for what we want 

- In this case we see the Play Audio part...There are three ways to play an audio 

  - from the Internet
  - Local file on the user's device
  - Local asset from your Flutter project

- Then After reading a bit more we find "For Local Assets, you have to use the `AudioCache` class (see below)."

- So we scroll down below and we find the AudioCache.

- There we the whole docs for it.

- There we see in detail about how to play an audio...import then update pubspec.yaml file then create an object for AudioCache then play it using the play method in AudioCache.

  ```dart
  //Method 1 for the Xylophone app
  
  import 'package:flutter/material.dart';
  import 'package:audioplayers/audio_cache.dart';
  
  void main() => runApp(XylophoneApp());
  
  class XylophoneApp extends StatelessWidget {
    @override
    Widget build(BuildContext context) {
      return MaterialApp(
        home: Scaffold(
          backgroundColor: Colors.white,
          body: SafeArea(
              child: Column(
            crossAxisAlignment: CrossAxisAlignment.stretch,
            children: <Widget>[
              Container(
                height: 92.57142857142857,
                color: Colors.red,
                child: FlatButton(
                  onPressed: () {
                    AudioCache player = new AudioCache();//here we create the player object to access the methods 													//from AudioCache class
                    player.play('note1.wav');	//Here we use the play method to play a sound on press.
                  },
                  child: Text('note1'),
                ),
              ),
              Container(
                height: 92.57142857142857,
                color: Colors.orange,
                child: FlatButton(
                  onPressed: () {
                    AudioCache player = new AudioCache();
                    player.play('note2.wav');
                  },
                  child: Text('note2'),
                ),
              ),
              Container(
                height: 92.57142857142857,
                color: Colors.white,
                child: FlatButton(
                  onPressed: () {
                    AudioCache player = new AudioCache();
                    player.play('note3.wav');
                  },
                  child: Text('note3'),
                ),
              ),
              Container(
                height: 92.57142857142857,
                color: Colors.yellowAccent,
                child: FlatButton(
                  onPressed: () {
                    AudioCache player = new AudioCache();
                    player.play('note4.wav');
                  },
                  child: Text('note4'),
                ),
              ),
              Container(
                height: 92.57142857142857,
                color: Colors.teal,
                child: FlatButton(
                  onPressed: () {
                    AudioCache player = new AudioCache();
                    player.play('note5.wav');
                  },
                  child: Text('note5'),
                ),
              ),
              Container(
                height: 92.57142857142857,
                color: Colors.greenAccent,
                child: FlatButton(
                  onPressed: () {
                    AudioCache player = new AudioCache();
                    player.play('note6.wav');
                  },
                  child: Text('note6'),
                ),
              ),
              Container(
                height: 92.57142857142857,
                color: Colors.green,
                child: FlatButton(
                  onPressed: () {
                    AudioCache player = new AudioCache();
                    player.play('note7.wav');
                  },
                  child: Text('note7'),
                ),
              )
            ],
          )),
        ),
      );
    }
  }
  ```

  ## Function in Dart (Important)
  
  **Important for any OOP language**
  
  ```dart
  void main() {
    
   int step1Result = add(n1: 5, n2: 9);		//Calls the add function...By specifying the name of the parameters
      									//we can give the pass arguments with no sequence according to 											//formal parameter
    
   int step2Result = multiply(step1Result, 5);
    
   double finalResult = step2Result / 3;
    
   print(finalResult);			
    
  }
  
  int add({n1, n2}){		//Those curly paranthesis is only for dart languange so they specify the name while 						//passing the arguments
    return n1+n2;			//Adds the parameters and returns it. 
  }
  
  int multiply(a,b){
    return a*b;
  }
  ```
  
  **In Java language**
  
  ```java
  //Same above program in JAVA
  public class HelloWorld{
  
       public static void main(String []args){
      
    
   int step1Result = add( 5, 9);
    
   int step2Result = multiply(step1Result, 5);
    
   double finalResult = step2Result / 3;
    
   System.out.print(finalResult);
    }
       
       public static int add(int n1, int n2){	//we have to specify the data type we are returning in this case 											//it's int data type we are returning
           return n1+n2;
       }
       public static int multiply( int a,int  b){
           return a*b;
       }
  }
  ```
  
  The Best Version of Xylophone App
  
  ```dart
  import 'package:flutter/material.dart';
  import 'package:audioplayers/audio_cache.dart';
  
  void main() => runApp(XylophoneApp());	//The Arrow Syntax in Dart
  
  class XylophoneApp extends StatelessWidget {
    void playSound(int num) {
      AudioCache player = new AudioCache();
      player.play('note$num.wav');
    }
  
    Expanded buildKey({color, int soundNumber, int noteNum}) {	//Type of fuction is Expanded because it's 																//returning Expanded data type
      return Expanded(
        child: FlatButton(
          color: color,
          onPressed: () {
            playSound(soundNumber);
          },
          child: Text('note$noteNum'),
        ),
      );
    }
  
    @override
    Widget build(BuildContext context) {
      return MaterialApp(
        home: Scaffold(
          backgroundColor: Colors.black,
          body: SafeArea(
            child: Column(
              crossAxisAlignment: CrossAxisAlignment.stretch,
              children: <Widget>[
                buildKey(color: Colors.red, soundNumber: 1, noteNum: 1),
                buildKey(color: Colors.orange, soundNumber: 2, noteNum: 2),
                buildKey(color: Colors.yellow, soundNumber: 3, noteNum: 3),
                buildKey(color: Colors.green, soundNumber: 4, noteNum: 4),
                buildKey(color: Colors.teal, soundNumber: 5, noteNum: 5),
                buildKey(color: Colors.blue, soundNumber: 6, noteNum: 6),
                buildKey(color: Colors.purple, soundNumber: 7, noteNum: 7),
              ],
            ),
          ),
        ),
      );
    }
  }
  ```
  
  ### Dart Arrow Function
  
  ***This only works for Methods which have Single Line of Code inside them.***
  
  ```dart
  void main() => runApp(XylophoneApp());	//The Arrow Syntax in Dart
  
  //This is Same as 
  
  void main(){
   runApp(XylophoneApp());
  }
  ```
  
  For Eg.
  
  ```dart
  Void main(){
  int result = add(3,6);
  print(result);
  }
  
  int add(n1,n2){
  return n1+n2;
  }
  //The above add function will work same as the below add function
  
  int add(n1,n2) => n1+n2;	//Here we don't have to use the return keyword
  
  //OutPut
  9
  ```
  
  ## Lists in Dart
  
  ```dart
  List <int> nums = [1,2,3,4,5,6]; 	//If you don't specify the data type of list it'll be dynamic by default
  ```
  
  - In a dynamic list you can add any type data you want but it can get messy...so it's better to add the data type.
  
  - In Flutter Only Row and Column can have multiple widgets in a children list.
  
    For eg..
  
    ```dart
    List<Icon> icons = [
        Icon(
          Icons.check,
          color: Colors.green,
        ),
        Icon(
          Icons.close,
          color: Colors.red,
        )
      ];
    ....
    {
        Row(children: icons)
    }
    ```
  
  ## Classes and Objects in dart
  
  - When we say a **property** of a class it simply means a variable inside a class.
  
  - A function inside a class is called a method.
  
  ```dart
  void main() {
    
    Human james = new Human(20);    //Creating a object james
    
    print(james.height);      //Tapping into the Human class property
    
    Human vikas = new Human(25);    //Creating a object vikas
    
    print(vikas.height);      //Tapping into the Human class property
    
  }
  
  class Human{
    double height;    //variable are properties
    int age = 0;
    
    Human(double startingHeight){   //Constructor
      height = startingHeight;
    }
  }
  //Output
  20
  25
  ```
  
  Passing the Arguments in style
  
  ```dart
  //Passing the Arguments in Style Just Like the methods one
  void main() {
    
    Human james = new Human(startingHeight: 20);    //So you don't have to remeber                                    										//in what order you pass the arguments
    
    print(james.height);      //Tapping into the Human class property
    
    Human vikas = new Human(startingHeight: 25);    //Creating a object vikas
    
    print(vikas.height);      //Tapping into the Human class property
    
  }
  
  class Human{
    double height;    //variable are properties
    int age = 0;
    
    Human({double startingHeight}){   //But in the Constructor Curly brackets
      height = startingHeight;
    }
  }
  ```
  
  Accessing the Methods of Classes
  
  ```dart
  void main() {
    
    Human james = new Human(startingHeight: 20);    //So you don't have to remeber                                    in what order you pass the arguments
    
    print(james.height);      //Tapping into the Human class property
    
    Human vikas = new Human(startingHeight: 25);    //Creating a object vikas
    
    print(vikas.height);      //Tapping into the Human class property
    
    vikas.talk('What\'s up bro?');    //Using the talk method of Human Class.
  }
  
  class Human{
    double height;    //variable are properties
    int age = 0;
    
    Human({double startingHeight}){   //But in the Constructor Curly brackets
      height = startingHeight;
    }
    
    void talk (String whatToSay){   //Creating a method talk with a formal parameter
      print(whatToSay);
    }
  }
  ```
  
  

## Abstraction 

- Abstraction is just making our code a bit simpler.

- We can create different classes and add various properties ...then access those properties by creating a object for that class

- We should create the new class in a different file.

- For. eg. we put our lists of Questions in a different file called quiz_brain, and in it we created a class(QuizBrain) in which it had a list of all the questions and answers.

- Then we imported the quiz_brain.dart file to our main.dart file, there we created a new object(quizBrain) for the QuizBrain class.

- Then we referenced the QuizBrain list questionBank by...

  ```dart
  quizBrain.questionBank[n];
  ```


## Encapsulation

- Encapsulation is just dividing the work between sperate classes(files) and access it only by using a method or a constructor.

- We can also make our variables or methods private by adding a underscore in front of them so that they are not accessible by other classes except in the class which it is created. 

- Encapsulation is just making our code a bit cleaner and organized.

- **Basically we have to make our properties private and then make getter and setter to methods to interact with other classes.** 

  ```dart
  void main() {
   Student s = new Student();
    s.setAge(23);
    int resultAge = s.getAge();
    print('you are = $resultAge');
  }
  
  class Student{
    int _age;   //The class property which is private
    void setAge(int _age){    //The setter method
      if(_age>20){
        print("You're too Old");
      }
      else{
        this._age = _age;
      }
    }
    int getAge(){   //The getter method
      return _age;
    }
    
  }
  ```

  

## Inheritance

- In inheritance we inherit some properties and methods made available to a class from another class.
- The Class from which the properties will be inherited is called the Parent/Super class....And the class which will be inheriting is a child/sub class.

```dart
void main() {
  Chef vikas = new Chef();
  SouChef vivaan = new SouChef();
  vikas.bakingTech();   
  vivaan.bakingTech();    //SouChef has inherited all methods of the parent Chef                              //class
  vivaan.cuttingTech();
  }

class Chef{
  int cake = 10;
  void bakingTech(){
    print(' the secret Chef baking technique');
  }
}

class SouChef extends Chef{   //The SouChef is the child of Chef class
  int cutOnions = 20;
  void cuttingTech(){
    print('Master in cutting onions');
  }
}
```



## Polymorphism

Polymorphism is actually to do apply everything else in the OOP like inheritance, abstraction and encapsulation at one time.

```dart
void main() {
 SelfDriveCar myBMW = new SelfDriveCar('The Hacker Lane');
  myBMW.drive();
}
class Car{    //Parent class
  int seats = 5;
  void drive(){
    print('turning wheels');
  }
}
class SelfDriveCar extends Car{   //SelfDriveCar is child class of Parent Car class
    String destination;
  SelfDriveCar(String destination){   //Creating a custom constructor
    this.destination = destination;		//this keyword does the same job in dart as in java.
  }
  @override     //This annotation will be used everytime we do method overriding
  void drive(){   
    super.drive();    //This is calling the subclass drive method
    print('self drive to $destination');
  }
}
```



## Dart Constructors

```dart
class SuperUser extends User{
  
  int id;
  int height;
  SuperUser({int id, int height}){		//SuperUser Constructor
    this.id = id;
    this.height = height;
  }
  
  //The Above Constructor does the same job as this constructor
  
  SuperUser({this.id, this.height});		//SuperUser Constructor
}
```



### Container  Background image

```dart
body: Container(
        decoration: BoxDecoration(
          image: DecorationImage(
            image: AssetImage('images/background.png'),
            fit: BoxFit.cover,
          ),
        ),
```



### Visibility  widget

```dart
child: Visibility(		//Visibity widget
                  visible: storyBrain.buttonShouldBeVisible(),	//A bool value
    )
```





## Stateful Widget

To make a stateful widget, we need two classes — one for the widget itself, and a second which creates the state. This setup allows the state to be easily saved, and enables the use of features such as hot reloading.

- **Why does a stateful widget need two classes?**
  *Imagine that we have a todo list widget which contains five todo items. When we add another one to the list, Flutter updates the screen differently to how you might imagine. You may expect that it simply adds this item to the existing widget. **In fact, it creates a whole new widget, and compares it to the old one to determine which changes to make on screen.*** 
- ***Since we create a new widget with every change, we cannot store any state in the widget itself, as it will be lost with the next change. This is why we need a separate State class.***

For Eg.

```dart
//Two classes for stateful widget
class ToDoList extends StatefulWidget {
  @override
  _ToDoListState createState() => _ToDoListState();
}

class _ToDoListState extends State<ToDoList> {
  @override
  Widget build(BuildContext context) {
    return Container();
  }
}
```



# A New Start



### RaisedButton Widget

Generated a rectangular widget with a bit of shadow behind it, so as to make it look like as it's raised.

```dart
Center(
          child: RaisedButton(			
            highlightElevation: 100.0,		//The Height of the button when it's pressed 
            elevation: 30.0,			//The height of the button from the screen
            color: Colors.orange,
            onPressed: () {
              print('clicked');
            },
```



### FlatButton Widget

Generates just a normal Button without a shadow or anything

```dart
Center(
          child: FlatButton(
            focusColor: Colors.red,
            splashColor: Colors.green,
            color: Colors.orange,
            onPressed: () {
              print('clicked');
            },
            child: Icon(
              Icons.ac_unit,
              size: 55,
              color: Colors.white,
            ),
          ),
        )
```



## Icon and Text Inside a button

### Using the RaisedButton.icon or FlatButton.icon  widget	

```dart
Center(
          child: RaisedButton.icon(
            onPressed: () {},
            icon: Icon(		//The Icon
              Icons.mail,
              color: Colors.white,
            ),
            label: Text(	//The Text
              'Mail me',
              style: TextStyle(color: Colors.white, fontSize: 20.0),
            ),
            color: Colors.orange,
          ),
        ),
```



### Using a Icon as a Button

```dart
Center(
            child: IconButton(
          onPressed: () {
            print('Hello');
          },
          icon: Icon(Icons.access_time),	
          color: Colors.orange,
        )),
```



### Container and Padding and Margin

- Padding is for spacing inside of the widget.

- While, Margin is for spacing outside of the widget.

- Container is used for containing various other widgets like text...etc.

  ```dart
  body: Container(
            margin: EdgeInsets.all(20.0),
            padding: EdgeInsets.symmetric(horizontal: 20, vertical: 10),
            child: Text('HEllO'),
            color: Colors.amber,
          ),
  ```

  

### To Iterate through a List using map() function.

For eg. the list is....

```dart
List<String> quotes = [
    'Be yourself; everyone else is already taken',
    'I have nothing to declare except my genius',
    'The truth is rarely pure and never simple'
  ];
```

And to iterate through every in the list we use the map() function.....It kind of works like for each loop

```dart
body: Column(
          children: quotes.map((quote) {
            return Text(quote);
          }).toList(),
        ));
```

 Now we a need a author after the quote then we create a class called Quote

```dart
class Quote {
  String text;
  String author;

  Quote({this.text, this.author});		//This is Equivalent to Quote({String text, String author})										  //{this.text=text;
                					    //this.author=author}
}
```

Then we replace the List quotes with....

```dart
List<Quote> quotes = [		//Note here we changed the type from String to Quote
    Quote(
        author: 'Oscar Wilde',
        text: 'Be yourself; everyone else is already taken'),
    Quote(
        author: 'Oscar Wilde',
        text: 'I have nothing to declare except my genius'),
    Quote(
        author: 'Oscar Wilde',
        text: 'The truth is rarely pure and never simple')
  ];
```

And then print the text on the screen by using....

```dart
Column(
          children: quotes.map((quote) {
            return Text('${quote.text} - ${quote.author}');
          }).toList(),
        )
```

