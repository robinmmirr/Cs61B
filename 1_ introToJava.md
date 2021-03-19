
# Intro to java
## Essentials: 
### Our first java code: 
```java
// class declaration, which is declared using the key words "public class" 
public class HelloWorld { 
    // the code that is run is inside of a method called "main", which is declared as such:
    public static void main(String[] args) { 
        // with the {} we have the code inside of a java method
        // all statements must end with semi-colons
        System.out.println("Hello world!");
    }
}
```

### Running a Java Program
the most common way to execute a java program is to run it through a sequence of two programs:
1. A Java Compiler called javac
2. A Java interpreter called java

When running the above java code, in the terminal we would type in:
($ represents our terminal's command propmt)

```
$ javac HelloWorld.java
$ java HelloWorld
Hello World!
```
When compiling, we included **.java** but we do not include **.class** when interpreting.

``` java
public class HelloNumbers {
    public static void main(String[] args) {
        // variable x must be declared before it is used, and it must be given a type
        int x = 0;
        // the loop should be contained in {}
        while (x < 10) {
            // print does not include a new line, println does
            System.out.print(x + " ");
            x = x + 1;
        }
    }
}
```

Output:

```
$ javac HelloNumbers.java
$ java HelloNumbers
$ 0 1 2 3 4 5 6 7 8 9 
```

### Static Typing

All variables and expressions have a so-called **Static Type**. 

Java variables can contain values of that type and only that type, the type of variable never change.

Java compiler performs a static type check:

``` java
public class HelloNumbers {
    public static void main(String[] args) {
        // overhere, we declared x is an int
        int x = 0;
        while (x < 10) {
            System.out.print(x + " ");
            x = x + 1;
        }

        // we assigned a string to x in the end, so there will be an error 
        x = "horse";
    }
}
```

Output:
```
$ javac HelloNumbers.java 
HelloNumbers.java:9: error: incompatible types: String cannot be converted to int
        x = "horse";
                ^
1 error
```
The compiler rejects this program out of hand before it runs.
- The compiler ensures that all types are compatible, making it easier for the programmer to debug 
- Every variable, parameter, and function has a declared type, making it easier for a programmer to understand and reason about code

### Defining Functions in Java
In Java, everything is a part of a class, functions should belong to some class as well-- in Java, it is commonly called "methods".

``` java
public class LargerDemo {
    // when we declared our method, we use the keyword "public static", which is similar to python's "def"
    // it give out the return type, int
    public static int larger(int x, int y) {
        if (x > y) {
            return x;
        }
        return y;
    }

    public static void main(String[] args) {
        System.out.println(larger(8, 10));
    }
}
```
## Defining and Using Classes
### Static vs. Non-Static Methods
All code in Java must be part of a class, most code is written inside of methods:
``` java
public class Dog {
    public static void makeNoise() {
        System.out.println("Bark!");
    }
}
```
We cannot run above code:

```
$ java Dog
Error: Main method not found in class Dog, please define the main method as:
       public static void main(String[] args)
```

To actually run the class, we cannot only have def-- we have to have a main method so that function can run.

We can have a seprate DogLauncher class:

``` java
public class DogLauncher {
    public static void main(String[] args) {
        Dog.makeNoise();
    }
}
```
Output:
```
$ java DogLauncher
Bark!
```

A class that use another class is a client of that class. DogLauncher is a client of Dog.
We can add the main method to Dog, or use DogLauncher to call the method. 

### Instance Variables and Object Instantiation

We are instantiating a class-- instances can hold data.

Within the Dog class, we created an instance and make the behavior of Dog based on specific instance:

``` java
public class Dog {
   
    public int weightInPounds;
    // Dog class has its own variables, also known as instance variables or non-static variables.
    // Declared inside the class
    // this method does not have the "statis" keyword-- we call such mthod instance methods or non-static methods
    public void makeNoise() {
        if (weightInPounds < 10) {
            System.out.println("yipyipyip!");
        } else if (weightInPounds < 30) {
            System.out.println("bark. bark.");
        } else {
            System.out.println("woof!");
        }
    }    
}
```
To use this method:

``` java
public class DogLauncher {
    public static void main(String[] args) {
        Dog d;
        // to call the makeNoise method, we want to first instantiate a Dog using the 'new' keyword.
        d = new Dog();
        // we make a specific dog bark by entering the weight
        d.weightInPounds = 20;
        // we called d.makeNoise instead of Dog.makeNoise()
        d.makeNoise();
    }
}
```
### Constructors in Java 

We usually construct objects in OOP using a constructor:

```java
public class DogLauncher {
    public static void main(String[] args) {
        // the instantiation is parameterized, we put 20 inside of new Dog
        Dog d = new Dog(20);
        d.makeNoise();
    }
}
```

To enable the parameterize function, for the Dog class:

``` java

public class Dog {
    public int weightInPounds;
    
    // we added a constructor to our Dog class:
    // similar to python's __init__ method
    public Dog(int w) {
        weightInPounds = w;
    }

    public void makeNoise() {
        if (weightInPounds < 10) {
            System.out.println("yipyipyip!");
        } else if (weightInPounds < 30) {
            System.out.println("bark. bark.");
        } else {
            System.out.println("woof!");
        }    
    }
}
```
### Array Instantiation, Arrays of Objects
We can also instantiate Array in java using the **new** keywoard:

```java
public class ArrayDemo {
    public static void main(String[] args) {
        /* Create an array of five integers. */
        int[] someArray = new int[5];
        someArray[0] = 3;
        someArray[1] = 4;
    }
}
```

In the client we can:

``` java
public class DogArrayDemo {
    public static void main(String[] args) {
        /* Create an array of two dogs. */
        // we just instantiated objects here
        Dog[] dogs = new Dog[2];
        dogs[0] = new Dog(8);
        dogs[1] = new Dog(20);

        /* Yipping will result, since dogs[0] has weight 8. */
        dogs[0].makeNoise();
    }
}
```
### Class Methods vs. Instance Methods

Two type of methods in Java
- Class methods: static methods
    - actions that are taken by the class itself
    - for example, math class has sqrt method, it is static so we call it like this:
    ```
    x = Math.sqrt(100);
    ```
- Instance methods: non-static methods
    - actions that can be taken only by a specific instance of a class
    - it sqrt is an instance method, we need to use this:
    ```
    Math m = new Math();
    x = m.sqrt(100);
    ```

Sometimes we can have a class with both instance and static methods:

``` java 
public static Dog maxDog(Dog d1, Dog d2) {
    if (d1.weightInPounds > d2.weightInPounds) {
        return d1;
    }
    return d2;
}
```

We can invoke the method by: 

``` java 
Dog d = new Dog(15);
Dog d2 = new Dog(100);
Dog.maxDog(d, d2);
``` 

We can also implement the maxDog as a non-static method:

``` java
// no keyword "static" anymore
public Dog maxDog(Dog d2) {
    if (this.weightInPounds > d2.weightInPounds) {
        // we used "this" to refer to teh current object
        return this;
    }
    return d2;
}
```

We can invoke the method by:
``` java
Dog d = new Dog(15);
Dog d2 = new Dog(100);
d.maxDog(d2);
```

### Static Variables
Static var can be useful:

``` java
public class Dog {
    public int weightInPounds;
    // recoding the scientific name for Dogs:
    public static String binomen = "Canis familiaris";
    ...
}
```
Static var should be accessed using teh name of the calss rather than a specific instance
- Dog.binomen, not d.binomen

### public static void main(String[] args)
- public: SO far, all of our methods start with this keyword
- static: it is a static method, not associated with any instance
- void: it has not return type
- main: this is the name of the method
- String[] args: This is a parameter that is passed to the main method 


### Command Line Arguments
Main is called by the java interpreter itself rather than another java class:
``` java 
public class ArgsDemo {
    public static void main(String[] args) {
        System.out.println(args[0]);
    }
}
```
This program prints out the 0th command libe argument:

``` 
$ java ArgsDemo these are command line arguments
these
```
args in here should be an array of Strings, where the entries are {"these", "are", "command", "line", "arguments"}.