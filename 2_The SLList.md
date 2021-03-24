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
public class IntNode {
    public int item;
    public IntNode next;

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


