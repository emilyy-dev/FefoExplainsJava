# Fefo Explains Java
## Part Two
**Once again, I encourage you to ask questions, because I know this isn't perfect, I know this is boring and I know this isn't as engaging as one might expect first, but the cool stuff comes last. I reckon that after this 2nd part, we'll have the very basics covered, maybe explain a couple things more after, and we can start working on actual abilities.**

In this part we'll be using Bukkit's `Location` class as an example, how is it that, even though there is one single `Location` class, each block and each entity has its own location, with its own set of grouped variables (`x`, `y`, `z`, `yaw` and `pitch` (although `yaw` and `pitch` are for entities, since it's for indicating at which direction they're looking at, horizontally and vertically, blocks don't do that lmao)). And besides that: how can one, as an "outsider" of that class, modify those variables? What if I want to change the player's location?

Remember how last time I said that "a `class` *is a model, a template* of somewhere where I can keep a set of variables and methods grouped together"? Emphasis on "a `class` *is a model, a template*"; think of it this way: an `int` or a `double` is a template for storing a number (integral and decimal numbers, respectively), but the `int` and `double` themselves don't store it, it *tells the variable how* to store the number; well, same thing with `class`es, I can make variables following the class's model (called objects), each entity or each block has its own `Location` object, `Location` tells the object how to store the grouped data based on that `Location` model, and just how variables are independent of each other, each `Location` object also is.

So in my `MyClass` class, I can do something like this (and this is also how you call the methods that a class holds):
```java
public class MyClass {
  // I declare a Location object, that will indicate... well... a location.
  // It's the object itself what's going to hold the actual data (x, y, z, yaw and pitch)
  // and the methods (getX, getY, getZ...)
  private Location someLocation;
  // Note that there is no =, means that this is an uninitialised variable/object,
  // it has no initial value. We'll see later how to "make it work".

  // Remember that the x variable inside the Location class is a double,
  // so we'll return a double.
  public double getLocationX() {
    // This is how you call a method,
    // you call it "through" the object with a period.
    return someLocation.getX();
    // So if another place has a MyClass object,
    // it'll be able to call objectName.getLocationX() to get that piece of data.
  }
}
```
So, several things here:
* First, we can make variables (called objects) "out of classes", out of those models.
> What's the difference between an object and a variable? An object is a "variable of a class", and a variable is one of the "primitive types" (`int`, `long`, `float`, `double`, etc.).
* Second, that's how the methods are called: `ourVariable.theMethod()`, note that we put the parentheses too, remember: methods have parentheses, variables don't. When a method is called, it'll execute the instructions and statements inside of it, from top to bottom, it can't jump to the next statement without first finishing the one above it.
> Note: that's also how any `public` member (variable, object or method) is accessed, through the object with a period between our object's name and the thing we're trying to access. If it's a method, it'll call the method (and we use the parentheses for calling methods too).
* And third: we can declare variable/objects without an initial value, leaving them uninitialised, for us to give it a value afterwards. If we don't give it a value, errors will eventually pop up if we try work with it.

"But wouldn't it always return 0.0 since that's what `Location` says `x` is equal to? And I can't even change that value.".. chill, okay? Now, if `x` was `public` instead of being `private`, at any point we could do somehting like `someLocation.x = 35.4;` (no parentheses since it's not a method we can call, instead we assign a new value to it) and boom, done, new value, but, since it's `private`, we can't do that because `private` doesn't let us access that variable, only `Location` can. What do instead? Let me bring back the `Location` class again:
```java
public class Location {
  private double x = 0.0;
  private double y = 0.0;
  private double z = 0.0;
  private float yaw = 0.0f;   // Don't forget the f at the end of a "float type number".
  private float pitch = 0.0f;

  // The "usual" get methods.
  public double getX() {
    return x;
  }
  public double getY() {
    return y;
  }
  public double getZ() {
    return z;
  }
  public float getYaw() {
    return yaw;
  }
  public float getPitch() {
    return pitch;
  }

  // And just like we have get methods, we'll have set methods.
  public void setX(double newX) {
    x = newX;
  }
  public void setY(double newY) {
    y = newY;
  }
  public void setZ(double newZ) {
    z = newZ;
  }
  public void setYaw(float newYaw) {
    yaw = newYaw;
  }
  public void setPitch(float newPitch) {
    pitch = newPitch;
  }
}
```
Again, couple new things:
1. `void` is a special type, well, not-type, it's precisely the *abcense* of a type, when a method return type is `void`, it means it will not return anything, there is no return value; thus, that method will **only** execute some instructions, generally to update some internal values, and give nothing in return. In the case of these set methods, it updates the values of the variables of the location, and none of them give anything back.
> Note on `void`: since it indicates the absence of a type, you can't declare a `void` variable, it can't hold any value.
2. Oh look, now the parentheses have new things inside of it, looks almost like a new variable, but no value assigned to it. That is the method's parameter, it can have several parameters (separated by commas, we'll see later). The parameters are variables that are only visible to that method. And just like a normal variable: it has a type and a name. The value is provided by the caller.

So, how do we call these "parametrised" (yes, with an 's') methods? Ez: `variableName.methodName(value OR variable of the same type)`, say for example I want to set the `y` value of a location to be, idk, 45.81, then we'd call `someLocation.setY(45.81)` (and not `45.81f` because it's not a float, it's a double), and that will execute the instructions within the method (`y = newY;` in this case) with `newY` being 45.81, and so the new value of `y` inside `someLocation` will be 45.81.

Neato, now we can change a player's position, since there is a `Player` class, it has a `teleport(Location location)` method, we can use a `Location` variable to teleport a player to any location we want, we just need to `setX`, `Y` and `Z` with the appropriate coordinates; we can even use the `yaw` and `pitch` to make them look at a specific direction.
___
### Constructors:
There is one special kind of method, and it's called a constructor; a class constructor is used to (you guessed it) construct a class, what the hell does that even mean? Remember when I said:
> Note that there is no =, means that this is an uninitialised variable, it has no initial value. We'll see later how to "make it work".

A constructor is what lets us initialise an object. Just like any other method, it can have parameters; just like any other method, it can be `public` or `private`; and just like any other method, it will have a name, and a block, containing a set of instructions. Then if it's "just like any other method", why is it a *special* kind of method? For two main reasons:
1. The constructor's name *must* match that of the class.
2. You don't give it a return type.

Let's have a look, shall we? We'll stick with the `Location` class from now on:
```java
public class Location {
  // Notice how I'm leaving these variables uninitialised.
  private double x;
  private double y;
  private double z;
  private float yaw;
  private float pitch;

  // Oh look, no return type. Also, several parameters, separated by commas.
  // It's going to be the constructor what gives the private variables an initial value, those of the parameters.
  public Location(double newX, double newY, double newZ, float newYaw, float newPitch) {
    // Also, several instructions now, this is where the semicolon shines.
    // The semicolon indicates the end of an instruction/statement
    // and the start of a new one (the one below it).
    x = newX;
    y = newY;
    z = newZ;
    yaw = newYaw;
    pitch = newPitch;
  }

  public double getX() {
    return x;
  }
  public double getY() {
    return y;
  }
  public double getZ() {
    return z;
  }
  public float getYaw() {
    return yaw;
  }
  public float getPitch() {
    return pitch;
  }

  public void setX(double newX) {
    x = newX;
  }
  public void setY(double newY) {
    y = newY;
  }
  public void setZ(double newZ) {
    z = newZ;
  }
  public void setYaw(float newYaw) {
    yaw = newYaw;
  }
  public void setPitch(float newPitch) {
    pitch = newPitch;
  }
}
```
Let's go over what I just said:
1. The constructor's name *must* match that of the class (which it does).
2. You don't give it a return type.

First point is easy to follow. The second one, how does that work? This is something I like to dislike, but meh, it is how it is: the constructor has an "implicit return type", and that is the class itself; instead of returning `int` or `double`, it will return itself, in this case, it will return a `Location`, and not only that, it will return a `Location` *object*, with the variables initialised to the ones I put in the constructor parameters.

Back to the drawing board, and back to `MyClass`:
```java
public class MyClass {
  private Location someLocation;

  // We can now give MyClass a constructor too, can't we?
  public MyClass() {
    // This is how you initialise an object:
    // varname = new className(parameters, if any, separated by commas);
    someLocation = new Location(70.0, 64.0, -120.0, 0.0f, 0.0f);;
    // Now someLocation will be a valid object, with x, y, z, yaw and pitch having the values I just passed through the constructor.
  }

  public void multiplyLocationBy(double factor) {
    // This down here is a local variable, only visible to the method, just like parameters,
    // difference being, the caller can't give it a value.
    // Notice how the type of the variable matches the return type of the method we're calling.
    double x = someLocation.getX();
    // We grab the current value of x, and set its new value to be the one we just grabbed times the factor passed as parameter.
    someLocation.setX(x * factor);
    
    // Rinse and repeat:
    double y = someLocation.getY();
    someLocation.setY(y * factor);
    
    double z = someLocation.getZ();
    someLocation.setZ(z * factor);
  }
}
```
Now `MyClass` has a constructor, whenever someone wants to create a `MyClass` object, it will call its constructor, that will initialise `someLocation` to be a valid `Location` object, and its private variables will have the values we pass to it as parameters.
___
#### General Review:
* A variable whose type is a class is called an *object* (`int`, `long`, `double`, etc. are NOT classes, but there are classes for those too, cuz Java..), and a variable whose type is a primitive type is called a variable.
* We make an object's method execute its instructions by "calling" it as follows: `myObject.theMethod();`.
* We can give a method certain values for it to work with, those values are the parameters. It is the method that asks for those values, and not us who forcefully give them to it.
* The instructions/statements a method holds are executed from top to bottom. You define the end of a statement with a semicolon `;`, and when that instruction finishes executing, the one below it will start.
* The type that represents a "no-type" is `void`, it is used by methods that have nothing to return back.
* We can give a variable/object an initial value (by putting `= blah blah` when we declare it) or we can leave it uninitialised and give it a value later. **If we never do, that object/variable will never be valid. If we try to use it before giving it a value, errors will be thrown.**
* Methods can have its own local variables/objects, only visible by the method, as if it were `private` to it, but that variable only exists when the method is called, and does not persist through the runtime of the program, unlike the ones inside a `class`.
___
Okay I'm done for today. Now, all this is just textbook theory; as I said at the very beginning, I reckon that after this 2nd part, we'll have the very basics covered, and we can move onto practice, explaining the development environment (AFAIK you two downloaded IntelliJ IDEA (ehem, like one should to program in Java, ehem)), how it's laid out, how to use it, set it up, and all those things one doesn't really take into account, until you hit that "oh shit, how do I do this" wall.

Also, in the 1st part I said that Java is a very robust and conscise language, and while yes, we'll be ignoring the stuff we don't really need, we'll also be learning and using some (if not a lot) of the things it provides on-the-fly. I believe that a third and final part will be enough to cover everything we need to know to create abilities, so I'm looking forward to that, and after that, the fun will begin: code, mess up, and trial and error. What's great about it is that, since Minecraft is a game (a very popular one, apparently, that's what I was told), we can directly see, experience and feel the results almost immediately, so we get that instant feedback, which is always nice.

