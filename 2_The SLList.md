# SLLists
IntList not optimal, needs to read and maintain.
- Naked recursive data structure: 
    - In order to use an IntList correctly, the programmer must understand and utilize recursion even for simple list related task.
    - require too many helper methods

## Improvement #1 Rebranding

Our IntList:

``` java
public class IntList {
    public int first;
    public IntList rest;

    public IntList(int f, IntList r) {
        first = f;
        rest = r;
    }
...
```

Our first step:
    - change names
    - through away all helper methods

``` java
// intNode is a class kind of like IntList--> have a first item, the a next item that is also a IntNode-- recursive
public class IntNode {
    public int item;
    public IntNode next;
// when creating a IntNode, give a item i and then a IntNode n
    public IntNode(int i, IntNode n) {
        item = i;
        next = n;
    }
}
```

## Improvement #2: Bureaucracy
We are creating a separate class called SLList:
```java
public class SLList {
    public IntNode first;
// in SLList, when we create a SLList, we do not put null in the method for user, instead we put in inside of the method
    public SLList(int x) {
        first = new IntNode(x, null);
    }
}
```

When creating a SLList:
``` java
IntList L1 = new IntList(5, null);
SLList L2  = new SLList(5);
```
SLList hides the detail of null existing in the list.


## addFirst and getFirst
In IntList, we do ```L = new IntList(5,L)``` to add a new element to the list.

In SLList:

``` java
public class SLList {
    
    public IntNode first;

    public SLList(int x) {
        first = new IntNode(x, null);
    }

    /** Adds an item to the front of the list. */
    // when adding a new element, we alter "first" to a IntNode with x as first item, and first as the next item.
    public void addFirst(int x) {
        first = new IntNode(x, first);
    }
    /* when we do get the first item, we can just call the item from "first" intNode:
    public class IntNode {
    public int item;
    public IntNode next;
    So first.item can call the first item of that intNode
    */
    public int getFirst() {
    return first.item;
}
}
```
