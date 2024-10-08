```java
import java.util.Arrays;

public static void simpleExample() {
    List<Integer> ints = Arrays.asList(1, 2, 3);
    int s = 0;
    for (int n : ints) {s += n;}
    assert s == 6;
}
```
* An interface or class may be declared to take one or more type
  parameters, which are written in angle brackets and should be 
  supplied when you declare a variable belonging to the interface or
  class or when you create a new instance of a class.
  For example, look at this example:

```java
import java.util.ArrayList;
import java.util.List;

public static void example() {
    List<String> words = new ArrayList<String>();
    words.add("Hello ");
    words.add("world!");
    String s = words.get(0)+words.get(1);
    assert s.equals("Hello world!");
}
```
* In the Collections Framework, class ArrayList<E> implements interface
  List<E>. 
* The bytecode compiled from a source code that uses generics and
 one that doesn't will be identical.
  We say that generics are implemented by erasure because the
  types List<Integer>, List<String> are all represented at run-time
  by the same type, List.
* Generics implicitly perform the same cast that is explicitly performed
  without generics.
### Boxing and unboxing
* Recall that every type in Java is either a reference type or 
  primitive type.
  A reference type is any class, interface, or array type.
  All reference types are subtypes of class Object, and any 
  variable of reference type may be set to the value null.
* Conversion of a primitive type to the corresponding reference type 
  is called boxing, and conversion of the reference type to the 
  corresponding primitive type is called unboxing.
* Java with generics automatically inserts boxing and unboxing coercions where appropriate. If an expression e of type int appears where a value of type Integer is expected,
  boxing converts it to new Integer(e) (however, it may cache frequently occurring values). If an expression e of type Integer appears where a value of type int is expected,
  unboxing converts it to the expression e.intValue().
* The call Integer.valueOf(1) is similar in effect to the expression new Integer(1), but
  may cache some values for improved performance.
* Generic type parameters must always be bound to reference types,
  not primitive types.
### Foreach

```java
import java.util.Arrays;
import java.util.List;

public static void example() {
    List<Integer> ints = Arrays.asList(1, 2, 3);
    int s = 0;
    for (int n : ints) {s += n;}
}
```

```java
import java.util.Iterator;

public static void oldVersionOfLoop() {
    for (Iterator<Integer> it = ints.iterator(); it.hasNext();) {
        int n = it.next();
        s += n;
    }
}
```
* The code above introduces the variable it of type Iterator<Integer>
  to iterate over the list ints of type List<Integer>.
* The foreach loop can be applied to any object that implements the
  interface Iterable<E>.
### Generic methods and varargs

```java
import java.util.ArrayList;

public static <T> List<T> toList(T[] arr) {
    List<T> list = new ArrayList<T>();
    for(T elt : arr) list.add(elt);
    return list;
}
```
* The static method toList accepts an array of type T[] and returns a list of type
List<T>, and does so for any type T. Writing indicates this <T> at the beginning
of the method signature, which declares T as a new type variable. A method which
declares a type variable in this way is called a generic method. The scope of the type
variable T is local to the method itself; it may appear in the method signature and the
method body, but not outside the method.