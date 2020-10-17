# Maps and routing

Maps and routes are used in flutter to go to different screens ..... navigating to other screens.

Maps in Dart can be used like....

```dart
void main()
{
  Map route= { 'name' : 'Vikas', 'age': '29'};
  print(route['name']);
}
//Output
Vikas
```

### 

### Main.dart

```dart
import 'package:flutter/material.dart';
import 'package:world_time_app/pages/home.dart';
import 'package:world_time_app/pages/loading.dart';
import 'package:world_time_app/pages/choose_location.dart';

void main() {
  runApp(MaterialApp(
    debugShowCheckedModeBanner: false,
    initialRoute: '/home',			//this is so that 1st page is home page
    routes: {							//Route property of material app
      '/': (context) => Loading(),	//This is the first screen at the start of the app but is 											//overriden by the intialRoute property
      '/home': (context) => Home(),		
      '/location': (context) => Location(),
    },
  ));
}
```

**context** is used so that the widget knows where it's at in widget tree.

### Home.dart

```dart
import 'package:flutter/material.dart';

class Home extends StatefulWidget {
  @override
  _HomeState createState() => _HomeState();
}

class _HomeState extends State<Home> {
  @override
  Widget build(BuildContext context) {
    return Scaffold(
      body: SafeArea(			//Just keep things inside the visible screen
          child: Column(
        children: [
          FlatButton.icon(
              onPressed: () {
                Navigator.pushNamed(context,	//This Navigator.pushNamed pushes the location page
                    '/location'); //Pushes the location screen over the home page
              },
              icon: Icon(Icons.add_location),
              label: Text('Edit Location'))
        ],
      )),
    );
  }
}
```



### going to choose location page from home page

### choose_location.dart

```dart
import 'package:flutter/material.dart';

class Location extends StatefulWidget {
  @override
  _LocationState createState() => _LocationState();
}

class _LocationState extends State<Location> {
  @override
  Widget build(BuildContext context) {
    return Scaffold(
      appBar: AppBar(
        //The appbar will automatically create an icon to go back to the home screen
        backgroundColor: Colors.teal,
        title: Text('Choose Location'),
        centerTitle: true,
      ),
      body: FlatButton.icon(
          onPressed: () {
            Navigator.pushNamed(context, '/');	//Pushed the loading screen over the choose
          },								//location screen
          icon: Icon(Icons.launch_rounded),
          label: Text('Loading')),
    );
  }
}
```

