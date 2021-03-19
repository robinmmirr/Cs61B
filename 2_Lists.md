# Lists
## Mystery of the Walrus
Arrays have a fixed size in Java that can never change.

Intro to list type, e.g. in Python:
``` python
L = [1,2,3]
L.append(7)
```
Jave has its own built-in list type, but we will build our own list in this chapter:

Does the change to b affect a?
``` java
Walrus a = new Walrus(1000, 8.3);
Walrus b;
b = a;
b.weight = 5;
System.out.println(a);
System.out.println(b);
```

 Does the change to x affect y?
``` java
int x = 5;
int y;
y = x;
x = 2;
System.out.println("x is: " + x);
System.out.println("y is: " + y);
```
In comupter thing are stored in 1 and 0, e.g. both 72 and H are stored as 01001000-- how does Java interpret 01001000? Through types:
``` Java 
char c = 'H';
int x = c;
System.out.println(c);
System.out.println(x);
// we get: 
// c = H
// x = 72
```
In this case, both x and c var contains the same bits, but Java interpreter treats them differently when printed.

Primitive types in Java:
- byte
- short
- int
- long
- float
- double
- boolean
- char

## Declaring a variable (Simplified)
When you declare a variable of a certain type, Java finds a contiguous block with exactly enough bits to hold a thing of that type.

In addition to setting aside memory, the Java interpreter also creates an entry in an internal table that maps each variable name to the location of the first bit in the box.

When creating a varibale, Java is going to put that variable in a bits box it belongs to.

``` java 
int x;
double y;
```
Java does not write anything to the reserved box when a var is declared, there are no default values.

``` java
x = -1431195969;
y = 567213.112;
```
Once you used the "=" to assign value, java will fill the box with the value in bits.


## The Golden Rule of Equals (GRoE)
When write `y = x` you are telling the Java to copy the bits from x to y:
``` java
int x = 5;
int y;
y = x;
x = 2;
System.out.println("x is: " + x);
System.out.println("y is: " + y);
```

## Reference Types
Everything else besides the primitive types are called a `reference type`.

WHen we instantiate an object using `new`, Java first allocates a box for each instance var of the class, and fills them with a defult value. Then the constructor ususally fills every box with some other value.

For example:

```Java
public static class Walrus {
    public int weight;
    public double tuskSize;

    public Walrus(int w, double ts) {
          weight = w;
          tuskSize = ts;
    }
}
```
We are creating a Walrus using ` new Walrus (1000, 8.3);` Then we end up with a Walrus consisting of two boxes of 32 bits (int) and 64 bits (double).

## Reference Variable Declaration
When we declare a var of any refrence type, Java allocates a box of 64 bits, no matter what the type of object--> the 64 bit box contains the address of the Walrus in memory.

``` Java
Walrus someWalrus; // creates a box of 64 bits
someWalrus = new Walrus(1000, 8.3); // creates a new Walrus, and the address is returned by the "new" operator, and these bits are copied into the someWalrus.
```
## Box and Pointer Notation

- If an address is all zeros, we will represent it with null
- A non-zero address will be represented by an arrow pointing at an object instantiation  

## Resolving the Mystery of the Walrus

``` java
Walrus a = new Walrus(1000, 8.3); // we have a Walrus a with weight 1000 and size 8.3
Walrus b; // we have an empty box for Walrus b
b = a; // this line copies the bits in the a box to the b box, b will copy exactly the arrow in a and now show an arrow pointing at the same object
```

## Parameter Passing

When pass a parameter to function, we are simply copying the bits. The GRoE also applies to parameter passing.

Copying the bits is usually called "pass by value".

For example:
``` java
public static double average(double a, double b) {
    return (a + b) / 2;
}
```
Then we invoke this function:

``` java
public static void main(String[] args) {
    double x = 5.5; // create a box x with value as 5.5 
    double y = 10.5;// create a box y with value as 10.5 
    double avg = average(x, y); // when invoke the function average, the a and b in the average function is copying the x and y here. so a = 5.5 and b = 10.5
}
```

## Instantiation of Arrays

``` java 
int[] x;// create memory box of 64 bits, x can only hold the address of an int array
Planet[] planets; // plants can only hold the address of a plant array
```

Instantiating an  array is similar to instantiating an object. For example, if we create an integer array of size 5 as shown below:

``` java
x = new int[] [1,2,3,4,5]
```
`new` will create 5 boxes of 32 bits each and returns the address of the overall object for assignment to x.

If lose the bits corresponding to the address object can be lost as well. 
If the only copy of the address of a particular Walrus is stored in x, then x = null will cause you to permanently lose this Walrus. 

## The Law of the Broken Futon

Building our own list class:
``` java
public class IntList{
    public int first;
    public IntList rest;

    public IntList(int f, IntList r){
        first = f;
        rest = r;
    }
}
```
If we want to make a list of [5,10,15]

```java
IntList L = new IntList(15,null);
L = new IntList(10, L);
L = new IntList(5,L);
```
## size and iterativeSize
Adding the method `size` to the `IntList` class.

When call `L.size()` , get back the number of items in `L`.

- size: use recursion
    - for recursive code, we will need a base case.
    - here our base case is ` if rest = null return 0 `
``` java
/** Return the size of the list using... recursion! */
public int size() {
    if (rest == null) {
        return 1;
    }
    return 1 + this.rest.size();
}
```
- iterativeSize: not use recursion
    - p is a variable that is holding a pointer.
    - we need that pointer becasue we cannot reassign "this" in Java.
``` java
/** Return the size of the list using no recursion! */
public int iterativeSize() {
    IntList p = this; // we cannot override "this" so we would need to have a pointer
    int totalSize = 0;
    while (p != null) {
        totalSize += 1;
        p = p.rest;
    }
    return totalSize;
}
```


