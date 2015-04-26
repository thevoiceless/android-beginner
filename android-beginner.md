Java
=====
While it would be nice to be able to write Android apps without knowing how to code, the simple truth is that it's just not possible. You really do need to have at least a basic idea of how code works. But don't worry! I'll be giving a very basic overview of Java before diving into the Android stuff (it wouldn't make sense any other way).

Background
-----
Java is the official programming language used for writing Android apps. There are ways to use other languages, but they aren't as common and you won't find as many helpful resources if you go that route. Keep reading if you want to know why Java is used, otherwise you can skip to the next section.

Programming languages let you write things in human-readable form that get translated ("compiled") into a form that computers can understand. Not all computers are the same, though. For example, while 32-bit and 64-bit processors both do the same thing (execute code), the instructions for a 32-bit processor can be different from a 64-bit one. This means that the code you write would have to be translated into different instructions for the different processors, meaning more work is involved if you want your code to run on lots of different hardware.  

One way to get around this is to use something called a "virtual machine" (or VM for short) and have code talk to the VM instead of the real processor. When using a VM, code gets compiled into instructions that the VM understands and then the VM takes care of telling the processor what to do. This allows you to compile code only once and it will run anywhere that the VM is installed.  

This is the approach that Java uses. The Java Virtual Machine (JVM) defines a specific set of instructions that it understands, regardless of what kind of hardware it's running on. This means you can write Java code that will run on a 32-bit Windows computer as well as a 64-bit Mac without needing to change anything. It's also what allows Android to run on so many different kinds of hardware.  

Because the VM specifies the instructions that it understands, you can use any language that gets translated into those instructions. So even though Java is the official language used for making Android apps, it is technically possible to use [other languages](https://en.wikipedia.org/wiki/List_of_JVM_languages).

Writing Code
-----
Java is an "object oriented" programming language. This means that everything is done using the concept of "objects". So what are objects? An object is an instance of a class. But what's a class? A class is a self-contained collection of code. That probably doesn't make much sense, so here's an example:

Let's say you wanted to write code to represent a car. A `Car` class could contain all of the stuff that you think defines a car (this is just a simple example, a real car obviously has more details):

    // Any text (like this) that follows the characters '//' is called a comment
    // Comments do not count as code; the computer completely ignores them
    public class Car {
        private int wheels = 4;
        private String color;

        public Car(String c) {
            color = c;
        }

        public void setColor(String c) {
            color = c;
        }

        public String getColor() {
            return color;
        }
    }

The code to create a new `Car` would be:

    Car myCar = new Car("red");

We'll go through this line-by-line.

#### Classes

    public class Car {

Ignore the `public` for now, I'll come back to that. Otherwise, it's a pretty simple line of code. `class Car` indicates that you're declaring a class named `Car` and the opening curly brace is where the code for the class begins. Also note that class names must begin with an uppercase letter. Inside the class, we first declare some variables, then we declare a constructor, and then we declare a couple methods.

#### Variables
  
    private int wheels = 4;
    private String color;

These two lines define two variables that are contained within our `car` class. Variables are like boxes that let you store values. Every variable that you define must have a type, otherwise Java will not know what value you can store in it. In this case, `wheels` is an integer (`int`) equal to 4. `color` is a String, which means that it can store text values (a "string" of characters). However, note that you don't have to assign a value at the same time you declare the variable. The `color` String doesn't get assigned until later on in the constructor.

#### Constructors

    public Car(String c) {
        color = c;
    }

Every class must have a constructor, which is what you use to create ("construct") a new instance of the class (again, ignore the `public` for now).

    Car myCar = new Car("red");

If you executed that line of code from somewhere in your application, it would create a variable named `myCar` that would contain a new instance of the `Car` class. Notice that the String "red" was passed to the constructor; You can require that certain values be provided when creating a new object, and in this case we require a String value. If you tried to write

    Car myCar = new Car();

you would get an error because there is only one constructor for the `Car` class and it requires a String. Inside of that constructor we have the line

    color = c;

where `c` refers to the String value that was passed in, and then that value is assigned to our `color` variable. You can think of the parameters (written between the parenthesis) as placeholders; When you write `new Car("red")`, the `c` parameter from the constructor will contain "red". Every `Car` will have its own `color` variable, and its value will be equal to whatever you pass in when you created it.

    Car greenCar = new Car("green");
    Car blueCar = new Car("blue");

Those two lines would create two new variables, `greenCar` and `blueCar`, each containing a new `Car` object.

#### Methods

    public void setColor(String c) {
        color = c;
    }

    public String getColor() {
        return color;
    }

Methods allow you to give names to multiple lines of code. Then whenever you want to run those lines, you can simply reference the method name. So if you were writing code and found yourself copy/pasting the same few lines over and over, you could instead put them in a method and call that method instead. Then you only have to type one line, but it's equivalent to executing as many lines as you want!

In our `Car` class, we define a method named `setColor` that requires a String parameter (just like the constructor did). When the method is executed, it will set the `color` variable equal to the given String. For example, after we've created our car with an initial color of "red", we might want to change its color later. However, if we created a new `Car` object as assigned it to `myCar` (instead of using `setColor`):

    Car myCar = new Car("red");
    myCar = new Car("blue");  // Assigning a new value to myCar

we would lose everything that was stored in the `myCar` variable because it would be overwritten by the new car! Instead, the `setColor` method lets us change the value of `color` without overwriting the entire variable:

    myCar.setColor("blue");

From that point on, `myCar` would contain the same object as before, but its `color` would be "blue" instead of "red".

We also define a method named `getColor` that is a bit different from `setColor`. See the word `void` when we declared the `setColor` method? Every method in Java must specify a return type. If all your method does is execute some code (it doesn't return a value after you execute it), then you use `void`. However, our `getColor` method returns the `color` variable, so the return type is `String`. You would use it as such:

    Car myCar = new Car("red");
    String carColor = myCar.getColor();

After executing those two lines, `myCar` would contain an instance of the `Car` class and `carColor` would contain the result of calling `myCar.getColor()`, which would be the String "red" because that's what we provided when we created the car.

You may be wondering why `setColor` and `getColor` are even needed, rather than just writing

    color = "some color name here";

Well, that's where the `public` and `private` words come in.

#### Access Modifiers

    // TODO: Left off here for now


<br/>
<br/>
<br/>


Need to find places for these
-----

variable scope; the `c` parameter in the constructor is not the same `c` in `setColor`  

An important note: `int` is lowercase while `String` is capitalized. Why is that? It's because `int` is one of the eight [primitive types](https://docs.oracle.com/javase/tutorial/java/nutsandbolts/datatypes.html) in Java. These are the only variable types that are not instances of a class; they do not contain any special behavior and are defined only by the value they hold. An `int` just stores an integer value, that's it.  

A [String](https://developer.android.com/reference/java/lang/String.html), on the other hand, is an object and can do much more than simply store text values. If you click on that link and scroll down to the "Public methods" table, you'll see a bunch of different things that the String class can do. I'll explain what methods are later, but for now the important thing to note is that 