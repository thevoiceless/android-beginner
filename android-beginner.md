Java
=====
While it would be nice to be able to write Android apps without knowing how to code, the simple truth is that it's just not possible. You really do need to have at least a basic idea of how code works. But don't worry! I'll be giving a very basic overview of Java before diving into the Android stuff (it wouldn't make sense any other way). Things may not make sense at first since I'll be giving a very very fast overview of a very very big language, but stick with it and you'll see more examples when we get to the Android code.

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
    /* 
     * You can also put text between /* and */ like this if you want to span multiple lines or only part of a line
     */
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

Get in the habit of ending lines with semicolons; the only time you don't need them is in comments or if a line ends with `{` and usually `}` (there are times when you need a semicolon after `}`).

#### Variables
  
    private int wheels = 4;
    private String color;

These two lines define two variables that are contained within our `car` class. Variables are like boxes that let you store values. Every variable that you define must have a type, otherwise Java will not know what value you can store in it. In this case, `wheels` is an integer (`int`) equal to 4. `color` is a String, which means that it can store text values (a "string" of characters). However, note that you don't have to assign a value at the same time you declare the variable. The `color` String doesn't get assigned until later on in the constructor.

Variable names must start with either a letter, a dollar sign ($), or an underscore (_). The latter two are extremely uncommon; you'll pretty much always start them with letters. Names are case-sensitive, too. "FOO" and "foo" are treated separately. After the first letter you can use any combination of letters, digits, dollar signs, or underscores (again, you'll rarely see those last two).

An important note: `int` is lowercase while `String` is capitalized. Why is that? It's because `int` is one of the eight [primitive types](https://docs.oracle.com/javase/tutorial/java/nutsandbolts/datatypes.html) in Java. These are the only variable types that are not instances of a class; they do not contain any special behavior and are defined only by the value they hold. An `int` just stores an integer value, that's it. A `boolean` can only have two possible values: true and false.

A [String](https://developer.android.com/reference/java/lang/String.html), on the other hand, *is* an object and can do much more than simply store text values. If you click on that link and scroll down to the "Public methods" table, you'll see a bunch of different things that the String class can do. I'll explain what methods are later, but for now the important thing to note is that capitalized types indicate classes whereas lowercase types are always primitive.

#### Constructors

    public Car(String c) {
        color = c;
    }

Every class must have a constructor, which is what you use to create ("construct") a new instance of the class (again, ignore the `public` for now).

    Car myCar = new Car("red");

If you executed that line of code from somewhere in your application, it would create a variable named `myCar` that would contain a new instance of the `Car` class. Notice that the String "red" was passed to the constructor (between the parenthesis); You can require that certain values be provided when creating a new object, and in this case we require a String value. If you tried to write

    Car myCar = new Car();

you would get an error because there is only one constructor for the `Car` class and it requires a String. You would also get an error if you tried to write

    Car myCar = new Car(4);

because the constructor specifically says that you must pass a String (but 4 is an integer). Inside of that constructor we have the line

    color = c;

where `c` refers to the String value that was passed in, and then that value is assigned to our `color` variable. You can think of the parameters as placeholders; When you write `new Car("red")`, the `c` parameter from the constructor will contain "red". Every `Car` will have its own `color` variable, and its value will be equal to whatever you pass in when you created it.

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

Methods are defined by their name and the parameters they require (the things in the parenthesis). The `setColor` method requires a String (just like the constructor) whereas teh `getColor` method requires no parameters. There are two important things to note about the parameter passed to `setColor`:
1. While the parameter is named `c`, it is NOT the same `c` that is used in the constructor. Parameter names are unique to each method and only "exist" between the curly braces. You'll get an error if you try to use `c` outside of the braces because it hasn't been declared anywhere else.
2. Parameter names follow the same rules as variable names. It's also recommended that you use different names for method parameters and variables. For example, you *can* change `String c` to `String color` in `setColor`, but then how do you know which `color` you'd be referring to inside of the curly braces? `color = c;` would become `color = color;` which doesn't really makes sense. If you wanted to do things that way, you would have to say `this.color = color`; the `this` keyword says "use the `color` variable for this class, not that other one". 

In our `Car` class, we define a method named `setColor` that requires a String parameter (just like the constructor did). When the method is executed, it will set the `color` variable equal to the given String. For example, after we've created our car with an initial color of "red", we might want to change its color later. However, if we created a new `Car` object as assigned it to `myCar` (instead of using `setColor`):

    Car myCar = new Car("red");
    myCar = new Car("blue");  // Assigning a new value to myCar

we would lose everything that was stored in the `myCar` variable because it would be overwritten by the new car! Instead, the `setColor` method lets us change the value of `color` without overwriting the entire variable. To call a method, type the name of the variable that contains the object followed by a period and then the name of the method:

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

In the real world, your code will have classes that could have tons of different variables. However, not all of those may matter outside of the class itself. For example, if this was our Car class:

    public class Car {
        public int wheels = 4;
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

Notice that the `wheels` variable is now marked as public instead of private. This means that any code can access that variable on any Car object:

    Car myCar = new Car("red");
    // Note that you access public variables the same way as methods
    myCar.wheels = 100;

After executing that code, `myCar`'s `wheels` variable would be 100 instead of 4. If you wrote all of your other code under the assumption that Car objects would always have 4 wheels, you've now got a problem. So how do you fix this? Like in the original Car class example, you can make the variable private. If you do that, accessing the `wheels` variable is no longer possible...unless you add a method to the Car class:

    public int getNumberOfWheels() {
        return wheels;
    }

Now you can call `myCar.getNumberOfWheels()` to retrieve the number of wheels, but you have no way to change the value. Of course if you declared the `getNumberOfWheels()` method as `private`, there would be no way to get or set the value outside of the class. `public` and `private` allow you to control how other code can access your code.

In addition to `public` and `private`, there's one other access modifier you should know about: `protected`. And that leads us to...

#### Inheritance

What if someone else had written the Car class and it's exactly what you need except for one little detail? For example, what if you want to make a Truck class that's exactly like the Car class except that it has 18 wheels? Or even if you wanted to write a bunch of different classes for all of the different kinds of vehicles? There's a good chance those classes would have a lot of code in common. Inheritance can be a lifesaver in situations like these.

Inheritance is a concept in object-oriented programming that lets you write code that says "x is a y". For example: "A car is a vehicle", "A motorcycle is a vehicle", "A truck is a vehicle". All of these things have characterisitics common to all vehicles. They also have things that make them unique. So how would you represent something like this? You could have a base Vehicle class:

    public class Vehicle {
        protected int wheels;
        private String color;

        public Vehicle(String c) {
            color = c;
        }

        public void setColor(String c) {
            color = c;
        }

        public String getColor() {
            return color;
        }
    }

    public class Car extends Vehicle {
        public Car(String c) {
            super(c);
            wheels = 4;
        }
    }

Notice the `extends Vehicle` and that `wheels` is marked as `protected`. The `extends` keyword is how you denote the "is a" relationship; a Car is a Vehicle. Now when you create a Car

    Car myCar = new Car("red");

the constructor first calls `super` which means "invoke the constructor for my parent class", which in this case is Vehicle. This is requires so that the parent class can do any set-up that it needs to do (in this example, it sets the `color` variable). After that finishes, the constructor in the Car class sets `wheels = 4`.

The Car class knows about the `wheels` variable because it's defined in the parent class as `protected`. `protected` means "private except to subclasses". Because Car is a sublcass of (extends) Vehicle, it has access to all public and protected members. It does *not* have access to any private members! That means that the Car class cannot access the `color` String directly, it *must* use `getColor` and `setColor`.

An important limitation of inheritance in Java is that you can only extend from a single class. That is, you can NOT write

    public class YourClass extends SomeClass, SomeOtherClass {
        ...
    }

There are languages that support multiple inheritance, but Java does not.

Now stop a think for a second...this means that you could easily say

    Vehicle myVehicle = new Vehicle("red");

and you'd get a Vehicle object back. But what use is a Vehicle object if you don't know what "kind" of Vehicle it is? What if you only want to be able to create Cars, Motorcycles, Trucks, etc? How do you prevent people from using a generic class that's only meant for sharing common behavior? The answer is to declare the class as `abstract`, which I'll discuss next.

#### Other Keywords

The `abstract` keyword basically means "I exist, but someone else provides the actual implementation". By marking the Vehicle class as abstract, you're saying no one is allowed to directly create a new instance of it, only its sublcasses. For example:

    Vehicle myVehicle = new Vehicle("red");

would not be allowed (you'd get an error when you try to compile the code). However, 

    Car myCar = new Car("red");

is allowed because the Car class is not marked as `abstract`.

If a class is marked as `abstract` you can also mark methods within that class as `abstract`. For example, what if you wanted every Vehicle subclass to have a specific noise when you honk the horn? You could do that following (some of the previous code is removed for simplicity):

    public abstract class Vehicle {
        private String color;

        public Vehicle(String c) {
            color = c;
        }

        public abstract String honk();
    }

`honk` is declares as abstract and has no implementation (no curly braces with code between them). Now you *must* implement that method in any subclasses:

    public class Car extends Vehicle {
        public Car(String c) {
            super(c);
        }

        @Override
        public String honk() {
            return "Beep!";
        }
    }

    public class Truck extends Vehicle {
        public Truck(String c) {
            super(c);
        }

        @Override
        public String honk() {
            return "HOOOOONK!";
        }
    }

Car and Truck both extend Vehicle and therefore must implement the `honk` method. While it's not required, when you are implementing something from a parent class you usually mark it with the text `@Override`. That way it's obvious what exactly you're doing (obvious to other people that may read your code, and obvious to any programs that may help you write it correctly). You can override anything from a parent class (except the constructor) as long as it is not marked `private` or `final` (which I'll talk about next). Even if the constructor is marked `public` you can't override it, it's just a special case. And yes, that does mean you can mark a contructor as `private` although it's not common except in a specific scenario that I'll talk about later. 

So what does `final` mean? It actually means different things depending on where in the code you use it.

- A `final` class cannot be extended. If you declared `Vehicle` as `final` then you wouldn't be able to make the Car class or anything else. This also means that you can't have a class that is both `abstract` and `final`. You probably won't see `final` classes very often.
- A `final` method cannot be overridden in a child class. The method could be `public`, `private`, or `protected`; it doesn't matter as long as it's `final`. This is useful if you don't want child classes to be able to change a specific behavior.
- A `final` member variable can only be assigned once. If we marked the `wheels` variable as `final` then we would only be able to assign its value once. As a rule, the value would have to be assigned either when the variable is declared or in the constructor. This is useful if you know that a certain variable should only ever have its value written once. You'll get an error if you try to change it after that.

        public class Car {
            public final int wheels = 4;

            public Car() {
                // Alternatively, you could assign the value here
            }
        }

- A `final` parameter passed to a method cannot be reassigned:

        public void someMethod(final String s) {
            // The following line will cause an error
            s = "some other string";
        }

`static` is another keyword that you'll probably run into. Like `final`, its meaning depends on where it is used:
- A class can only be `static` if it is defined within another class (yes, you can define classes inside of classes). If that is the case, the inner class can be instantiated without a reference to the outer class. This is kind of a weird concept, so don't worry if it doesn't make sense yet:

        public class OuterClass {
            public OuterClass() { }

            public static class InnerClass {
                public InnerClass() { }
            }
        }

        // If InnerClass was not static, we would have to do this:
        OuterClass outer = new OuterClass();
        InnerClass inner = outer.new InnerClass();
        // If InnerClass is static, we can do this instead:
        InnerClass inner = new OuterClass.InnerClass();

- Similarly, a `static` method can be called without needing an instance of the class. This is useful if you have a bunch of "utility" methods that you want to use in a lot of different places. For example, Android has a TextUtils class with a lot of static methods for String objects. Compare these two:

        // Using static methods
        boolean isEmpty = TextUtils.isEmpty("");
        // After running that code, isEmpty would contain the value 'true'

        // Compare that to what we'd have to do if not using static methods:
        TextUtils tu = new TextUtils();
        boolean isEmpty = tu.isEmpty("")
        // The result would be the same, except that we needlessly created an instance of the TextUtils class

- If a class has a `static` member variable, then there is only *one* instance of the variables across *all* instances of the class. If it's modified in one place, *all* instances of the class will see the change:

        public class Example {
            private static int myNumber = 0;

            public Example() { }

            public void incrementNumber() {
                myNumber = myNumber + 1;
            }

            public int getNumber() {
                return myNumber;
            }
        }

        // Create two instances of the Example class
        Example ex1 = new Example();
        Example ex2 = new Example();
        // Both of those variables reference the same myNumber variable
        ex1.incrementNumber();
        // Now getNumber will return the SAME value for both of them!
        ex1.getNumber()     // Returns 1
        ex2.getNumber()     // Also returns 1
        ex2.incrementNumber()
        ex1.getNumber()     // Returns 2
        ex2.getNumber()     // Returns 2

Be *very* careful about how you use static member variables, they can cause a lot of weird issues. One of the common ways to use them is to ensure that only one instance of a class ever exists. This is called the [Singleton pattern](https://en.wikipedia.org/wiki/Singleton_pattern). This is the special case I mentioned before where you may want the constructor to be private. If someone wants to create an instance of your class, they can't simply call `new YourClass()`; instead, you provide a `getInstance` method that will create a static instance of the class if it doesn't exist and then return it. Next time `getInstance` is called, it will return that *same* instance of your class rather than creating a new one:

    public class Singleton {
        // 'null' means 'nothing', the variable has no value
        private static Singleton myInstance = null;

        private Singleton() { }
     
        public static Singleton getInstance() {
            if (myInstance == null) {
                myInstance = new Singleton();
            }
     
            return myInstance;
        }
    }

#### Interfaces

We've seen that classes can have variables and methods that work together to define certain behavior. Inheritance lets you extract out common behavior across classes and put it in a base class, and access modifiers let you control what can be changed. However, you may run insto situations where you don't know what *class* you need, but you do know what *behavior* you need. That is, you'll find yourself thinking "hmm it would be really nice if I could guarantee that an object has these 3 methods no matter what". That's where interfaces come in. An interface is simply a list of methods that must be implemented; they act as a sort of contract.

For example: pretend you're writing some method that takes a single parameter, and lets say that you will always need to be able to call 3 methods on that parameter: `foo`, `bar`, and `baz`.

    public void doSomething(______ param) {
        param.foo();
        param.bar();
        param.baz();
    }

How can you guarantee that those methods will always be available? If you know you'll only ever be passing one type of object to the method, that's no problem:

    public void doSomething(SomeClass param) { ... }

Then you just have to go into your `SomeClass` code and implement those 3 methods. All done...right? Well, what if you find yourself wanting to pass two different types of objects? You could create a new class that implements those 3 methods and then have your two existing classes extend them. Okay, that works. But what if you want to be able to pass a bunch of different types of objects to `doSomething`? Rather than defining a bunch of classes or multiple versions of `doSomething` that each take a different type of parameter, you could define an interface:

    public interface DoesSomething {
        void foo();
        int bar(int someInt);
        String baz();
    }

That's all there is to an interface; a list of methods without implementations. The methods are always considered `public` and `abstract` so you can omit those. However, you can declare the entire interface as `public`, `private`, or `protected`. They affect the interface the same way they affect everything else; if you declare and interface within a class as `private`, only that class will know that it exists. You'll almost always want them to be `public`.

Then you can guarantee that those methods will always be available by specifying that the given parameter must be an instance of that interface:

   public void doSomething(DoesSomething param) {
        param.foo();
        param.bar();
        param.baz();
    }

Now, `doSomething` doesn't care what class you give it as long as it implements the methods defined by the `DoesSomething` interface. If you want to pass an instance of `YourClass` to the `doSomething` method, you have to explicitly declare that `YourClass` adheres to the contract:

    public class YourClass implements DoesSomething {
        // The existing code in your class stays the same
        ...

        // But now you must also implement the methods in the interface
        @Override
        public void foo() { ... }

        @Override
        public int bar(int someInt) { ... }

        @Override
        public String baz() { ... }
    }

Another nice thing about interfaces is that classes can implement as many as necessary. Eariler I mentioned that Java does not support multiple inheritance; luckily you can almost always accomplish what you need by implementing interfaces instead.

    public class YourClass implements SomeInterface, SomeOtherInterface {
        ...
    }

If a parent class implements an interface, then the child classes will as well. Abstract classes can implement interfaces or they can mark the methods as `abstract` to force their child classes to implement them.

    public abstract class SomeClass implements SomeInterface {
        ...

        @Override
        public abstract void someInterfaceMethod();
    }

#### Null

I mentioned that Java is object-oriented and that everything is an object except the eight primitive types. When you create a primitive, they get initialized with a default value. For example, `int` defaults to zero and `boolean` defaults to `false`. But what about objects?

    Car myCar;

What value does `myCar` have after that line is executed? Because `myCar` is an object (an instance of the `Car` class), it will default to a special value called `null` if you don't assign it anything. `null` is not an object, it's not a type, it's not anything. `null` is nothing. It's Java's way of saying "nothing here, I'm empty". This is important because it means you cannot call methods on `null`. The `Car` class may have a `getColor` method, but your code will crash if you do

    Car myCar;
    myCar.getColor();

The problem is that although `myCar` has been declared, it has not been initialized with a value. It contains nothing; it is `null`. And while sometimes it would be nice if nothing happened when you called a method on `null`, that's not the way Java works. Instead, you must always check for `null` if it's possible that the variable may not have a value. You saw this in the singleton example above; it's simply a matter of checking `if (someVariable == null)`.

#### Control structures

Java code is executed line-by-line. Since you may need to change which lines are executed, there are many different control structures that let you skip or repeat parts of your code depending on certain conditions.

The simplest is the `if` statement:

    if (/* Some condition here */) {
        // Code to execute if the condition is true
    } else if (/* Some other condition */) {
        // Code to execute if some other condition is true
    } else {
        // Code to execute in all other cases
    }

At minimum, an `if` statement is made up of the keywork `if` followed by a condition in parenthesis. The condition can be any code that returns a boolean (`true` or `false`) value. For example:

    if (someVariable == 4) { ... }
    if (someFunctionThatReturnsBoolean()) { ... }
    if (someVariable != someOtherVariable) { ... }
    if (someFunctionThatReturnsBoolean() && someVariable == 4) { ... }
    if (someBooleanVariable) { ... }

There are multiple different comparison operators you can use:
- Equal: `==`
- Not equal: `!=`
- Less than, greater than: `<` and `>`
- Less than or equal, greater than or equal: `<=` and `>=`
- And: `&&`
- Or: `||`

Also notice that you can use a variable if that variable contains a boolean value. You can combine these operators in any way that you want; things surrounded by parenthesis will be grouped together and evaluated first.

    if (someVariable == 4 || (someOtherVariable / 2 == 0 && someOtherVariable > 100)) { ... }

You can also negate an entire group  with `!`:

    if (someVariable == 4 || !(someOtherVariable / 2 == 0 && someOtherVariable > 100)) { ... }

**Important note**: When comparing objects, use the `equals` method:

   if (someStringVariable.equals("foo")) { ... }
   if (myCar.equals(someOtherCar)) { ... }

You can write any code that you want inside of the curly braces after the `if`. However, keep in mind that any new variables you declare inside the curly braces will not exist outside of them:

    if (/* Condition */) {
        // Create the variable inside the curly braces
        int foo = 6;
    }
    // This will cause an error; the variable does not exist anymore
    foo = 5;

This is what you would need to do instead:

    int foo;
    if (/* Condition */) {
        foo = 6;
    }
    foo = 5;

However, `foo` would always end up with a value of 5. Why? Because even if the condition evaluated to `true` and the `if` statement set `foo` equal to 6, the line after the `if` statement *always* gets executed! If you wanted `foo` to have a value of *either* 5 or 6 you would add an `else` statement:

    int foo;
    if (/* Some condition */) {
        foo = 6;
    } else {
        foo = 5;
    }

As shown above, you can also check multiple conditions using `else if`. Order does matter: `if` always comes first (you can't use `else if` or `else` otherwise), then `else if`, then `else`.

The next control structure is the `while` loop. It's called a "loop" because the code inside of it will repeat as long as the condition is true:

    while (/* Condition */) {
        // Code to execute as long as the condition is true
    }

If the condition evaluates to true, each line inside the loop will be executed until it reaches the closing curly brace. At that point the condition will be checked again; if it evaluates to true, the loop runs again. If not, execution continues with whatever comes after the `while` loop.

There is also the `for` loop which can be used in two ways:
1. Iterate a certain number of times as long as a condition is true
2. Iterate over each item in a collection

For example:

    for (int i = 0; i < 5; i++) {
        ...
    }

That loop will execute 5 times. The variable `i` will start at 0, the loop will check the condition `i < 5` which will evaluate to `true`, the code inside the loop will execute, and then `i++` increments the value of `i` by 1. At that point the loop begins again by checking if `i < 5`. This will repeat for 0, 1, 2, 3, and 4. Once `i` is incremented to 5 the condition `i < 5` will no longer be true, so the code inside the loop will not execute.

Another example:

    for (Integer i : someCollectionOfIntegers) {
        ...
    }

This will iterate over each `Integer` value in the collection `someCollectionOfIntegers` and store the value in `i`, which you can then use in code inside the `for` loop. You might be wondering two things:
1. Why are we using `Integer` instead of `int`?
2. What is a collection?

Answering #2 will also anser #1.

#### Collections

    // TODO: Left off here for now

switch (verify info)
do while (brush up)

collections (segue from for loop)

<br/>
<br/>
<br/>


Need to find places for these
-----

object types for primitives (Integer, etc)

If you always know what values you will be comparing against, you can use a `switch` statement:

    switch (someVariable) {
        case 1:
            // What to do if someVariable == 4
            break;
        case 5:
            // What to do if someVariable == 5
            break;
        default:
            // What to do in all other cases
    }

It's important to notice that the values used as `case`s are all known. You cannot do something like this:

    switch (someVariable) {
        case someOtherVariable:
        ...
    }

    switch (someVariable) {
        case someFunction():
        ...
    }

The problem is that the value of `someOtherVariable` and 