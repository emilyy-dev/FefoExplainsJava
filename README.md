# Fefo Explains Java
## oh no · -·
What an absolute nightmare of a language to make programs... but Bukkit doesn't give us any other options, huh.
**I'll let you know from the very beginning that I *encourage* you to ask me (or look for online resources) if you think you don't understand something, even if it's the very slightest, meaningless thing, as I'll try to cover what we'll be using and what's necessary.**

You won't be able to create abilities without at least understanding how a Java program is laid out.
While yes, Java does offer a robust and concise programming model for one to work with, we'll be ignoring all of that because it's none of our business.
So I'll do what every other book/website does and I'll first show a small example and explain each of its components (I mean, if they keey doing that, means it must work, right?):

```java
public class MyClass {
  private int myVeryFancyNumber = 123;

  // This down here is a normal method the class contains.
  public int getFancyNumber() {
    return myVeryFancyNumber;
  }
}
```
First and foremost, the very most important thing about all this are comments, what comes after `//`, the program won't read those, since it isn't code, it's for us humans to read; for this explanation I'll probably be writing more comments in the examples themselves rather than citing things afterwards, since it's way more comfortable and I can makem well, comments directly where I want to point something out.
As said before, comments don't provide any additional functionality whatsoever, but it's also importrant for us to tell ourselves what the hell is it we're doing.

Second most important thing to know is to see how the "structure" of the code is laid out, when declaring something, it'll say something like `public/private`, followed by ""what is it this is representing"" (more on this now), followed by the name of whatever I'm declaring.

Now onto the real deal, we'll start with what the hell is a `class` and why is it the very first line of my program: a `class` *is a model, a template* of somewhere where I can keep a set of data (called variables) and functionality (called methods) grouped together. What do I mean by data? Practically anything you can think of, I mean, at the end of the day, it's just a set of numbers. So classes are models that let us hold data (variables) grouped together, and functionality (methods) that will interact with those variables in some way or another. For now, let's say that's all a class can store: variables and methods.
We'll see how one can use that model later.

One thing to note is that each pair of corresponding curly brackets `{}` (or "braces") denotes a block, marking beginning and end of a class or method.
Let me bring that example down here again, as I can't see it on my screen anymore :c
```java
public class MyClass { // That is where MyClass begins.

  // This is a variable, who would have thought!
  private int myVeryFancyNumber = 123;

  // This down here is a normal method the class contains.
  public int getFancyNumber() { // This is where the method begins.
    return myVeryFancyNumber;
  } // This is where the method ends.
	
} // That is where MyClass ends.
```
So, in this case, I'm declaring a class called `MyClass` because I lack creativity and originality. You might have already noticed that I declared `MyClass` to be `public`, what the hell does that mean?? Means that any method from any other place in a program can make use of this class. Anything declared as `public` is accessible from everywhere, and if it's declared as `private` means only the class itself can access it;
like `myVeryFancyNumber`, `MyClass` holds one single variable, called `myVeryFancyNumber`, which.. well.. will store a number.. how impressive. Variables is what actually stores the data we want to store.
A variable can be a whole number, a true/false value, a single character, a string (sequence of characters, normal people call them "words" or "phrases", weirdos..), decimal numbers: anything you can think of, a variable can store. You just need to tell it what *kind* of data it'll store, there are several types:
* `int` and `long` are for storing whole numbers, 0, 1, 2, 42, 69, 626, 62419684, -1, -2, -9641526, -48614596. Why are there two types for whole numbers? Well, you can't store an arbitrarily large number, each one of those types, while both storing whole numbers, `long` lets you store *way* larger numbers. There are other integer types, but we can safely ignore them (for now).
* `float` and `double` are for storing decimal numbers, 0.1, 0.2, 0.0001, 984.15648, -4.2000001, 0.0, -90.0. Why are there two of them then? `double` is more precise than `float`. But unlike the integers, we'll be using both of them.
* `boolean` is for storing a true/false (yes/no) state. That's it, that's all there is to it. It'll be used widely, since, for the abilities, we'll want the player to meet certain conditions evaluated to true/false values, and based on that, do or not do a certain task; like, for example, if it's true that the player is on an ability's cooldown, we won't let them use it, but if they're not on cooldown, we'll let them use it; or another example, we'll stop a player from using the ability if some time has passed (has this amount of time passed? yes/no).
* `String`, basically text, any text. Note that this one starts with a capital S, unlike the rest of the types.

Variables *must* have a value assigned to them for you to use it, you do that by saying it's equal to whatever value you want to assign to it, in this case
```java
private int myVeryFancyNumber = 123;
```
We're saying that `myVeryFancyNumber` will store the number 123, and that's the value it'll have assigned to it.

So `MyClass` is a `class` that holds an `int` variable named `myVeryFancyNumber`, and while `MyClass` is accessible everywhere within the program, `myVeryFancyVariable` can only be seen by `MyClass` and no one else.

LET ME BRING MY EXAMPLE DOWN HERE ONCE AGAIN:
```java
public class MyClass {
  private int myVeryFancyNumber = 123;

  // Normal method.
  public int getFancyNumber() {
    return myVeryFancyNumber;
  }

}
```
### FUCKING FINALLY: METHODS:
After this, we'll see an actual *real world example* of a class and why this programming model is so popular.
Again, like the other two: `public/private` followed by what that will represent, followed by the name.
Unlike variables, methods don't store data, methods store instructions (which will, in most cases, interact with the variables), methods are called to execute those instructions, and the methods can or cannot return a value back, give something in return to the caller.

Just like variables, you tell it it's going to be either for `public` or `private` access; just like variables, you tell it what type it represents (in the case of methods, what is it it's going to return back); and just like variables, you give it a name.
The differences here being:
* First, the round brackets `()` ("parenthesis", nobody calls them that..), we'll ignore them *for now*, but they are important.
* Second, it doesn't make sense to "assign" a value to a set of instructions, therefore: the braces, the method is defining a block with braces, and it's inside that block where the instructions are stored. 
***VERY IMPORTANT BEGINNER MISTAKE:*** *every instruction a method executes, **must** end with a semicolon `;`. Why? Cuz.. Java..* See how the `return` statement, at the end of the line it has a semicolon appended to it. That indicates the end of the instruction.

In this example, `getFancyNumber()` is a method that can be called anywhere within the program, it returns an `int` value, and this method has one single instruction: `return myVeryFancyVariable;` **(note the semicolon)**, and so it returns the value of `myVeryFancyNumber` (that is 123), so if an outsider calls `getFancyNumber()`, it'll get 123 back from it.

Let's go back up, review all I just wrote and look at this real world example:
**Classes:** lets you "draw" a model for a group of variables and methods.
**Variables:** lets you store data.
**Methods:** lets you.. do.. stuff? This is where the magic happens, like, modify those variables, call other methods, evaluate conditions/expressions.
___
### A real world example, yes, it wasn't a hoax:
```java
// This is Bukkit's Location class (part of it), used to define the location of almost everything:
// Entities, blocks, events, particles, sounds...
public class Location {
  private double x = 0.0;
  private double y = 0.0;     // Note the semicolons.
  private double z = 0.0;     // Yes, they are necessary in variable declarations too.
  private float yaw = 0.0f;   // float numbers are defined with an 'f' at the end of it.
  private float pitch = 0.0f;

  // Gets the x-coordinate of the location.
  public double getX() {
    return x; // Semicolons
  }
  // Gets the y-coordinate of the location.
  public double getY() {
    return x; // everywhere
  }
  // Gets the z-coordinate of the location.
  public double getZ() {
    return x; // lmao.
  }
}
```
Now, all fancy dandy, but, how do I modify the variables if you only provide "getters" for them? Wouldn't them always be 0? How can an entity change its position if it can't be modified? And how would each entity and each block have its own location if there is only one `Location` class? And all that.. I'll answer tomorrow, I'm tired now to write more ;-;
___
### Again, I highly *encourage* you to make questions about anything, and I'll try my best to answer them, and if I can't, provide online resources, there are tons of them everywhere, but it's not easy to find the adequate ones.

