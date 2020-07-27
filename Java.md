# Core Java
## Object

### int x=10
10 --> Constant | literal
x --> Identifier
int--> data Type

### Primitive Data Type:
Specifies the size and type of variable values, and it has no additional methods. There are 3 primitive data type.
1. Numeric Data Type: int, byte, short, long. This all can represent -ve or +ve number.
2. Char Type
3. Boolean Data Type

### public static void main(String[] args):
Whether the class contain the main method or not is been checked by JVM at runtime. If it dont found any method then it will throw noSuchMethodError. It is the starting point.
public: JVM to give access that it can call the method.
static: Without Object JVM can call by using class refrence.
void: no outut return from JVM.
main: Name which is configured inside JVM.
String[] args: Command Line arguments.

### Why Java is not object oriented programming language?
Pure Object Oriented Language or Complete Object Oriented Language are Fully Object Oriented Language which supports or have features which treats everything inside program as objects. It doesn’t support primitive datatype(like int, char, float, bool, etc.). But in Java it support primitive data Type.
### 1. Abstraction

Abstraction is the concept of hiding the internal details and describing things in simple terms. For example, a method that adds two integers. The internal processing of the method is hidden from the outer world. There are many ways to achieve abstraction in object-oriented programmings, such as encapsulation and inheritance.

### Encapsulation

Encapsulation is the technique used to implement abstraction in object-oriented programming. Encapsulation is used for access restriction to class members and methods.

Access Modifier keyword are used for encapsulation in object oriented programming. For example, encapsulation in java is achieved using  `private`,  `protected`  and  `public`  keywords.
### Polymorphism

Polymorphism is the concept where an object behaves differently in different situations. There are two types of polymorphism – compile time polymorphism and runtime polymorphism.
### Inheritance

Inheritance is the object-oriented programming concept where an object is based on another object. It is a is-a relationship
### 5. Association

Association is the OOPS concept to define the relationship between objects. The association defines the multiplicity between objects. For example Teacher and Student objects. There is a one-to-many relationship between a teacher and students. Similarly, a student can have a one-to-many relationship with teacher objects. However, both student and teacher objects are independent of each other.

### Aggregation

Aggregation is a special type of association. In aggregation, objects have their own life cycle but there is ownership. Whenever we have “HAS-A” relationship between objects and ownership then it’s a case of aggregation.

### 6. Composition

The composition is a special case of aggregation. The composition is a more restrictive form of aggregation. When the contained object in “HAS-A” relationship can’t exist on its own, then it’s a case of composition.

### Why Java is not pure Object Oriented language?

Java is not said to be pure object-oriented because it supports primitive types such as int, byte, short, long, etc. I believe it brings simplicity to the language while writing our code. Java could have wrapper objects for the primitive types but just for the representation, they would not have provided any benefit.

As we know, for all the primitive types we have wrapper classes such as Integer, Long etc that provides some additional methods.

## String
### What is String in Java? String is a data type?

String is a Class in java and defined in java.lang package. It’s not a primitive data type like int and long. String class represents character Strings. String is used in almost all the Java applications and there are some interesting facts we should know about String. String in immutable and final in Java and JVM uses String Pool to store all the String objects.

### What are different ways to create String Object?
String str = "str"
String str = new String("str")
When we create a String using double quotes, JVM looks in the String pool to find if any other String is stored with the same value. If found, it just returns the reference to that String object else it creates a new String object with given value and stores it in the String pool.  <br>
When we use the new operator, JVM creates the String object but don’t store it into the String Pool. We can use `intern()` method to store the String object into String pool or return the reference if there is already a String with equal value present in the pool.

### How to compare two Strings in java program?

Java String implements  `Comparable`  interface and it has two variants of  `compareTo()`  methods.<br>

`compareTo(String anotherString)`  method compares the String object with the String argument passed lexicographically. If String object precedes the argument passed, it returns negative integer and if String object follows the argument String passed, it returns a positive integer. It returns zero when both the String have the same value, in this case  `equals(String str)`  method will also return true.<br>

compareToIgnoreCase(String str): This method is similar to the first one, except that it ignores the case. It uses String CASE_INSENSITIVE_ORDER Comparator for case insensitive comparison. If the value is zero then  `equalsIgnoreCase(String str)`  will also return true.

### Can we use String in switch case?
Java 7 extended the capability of switch case to use Strings also, earlier Java versions don’t support this.

### Difference between String, StringBuffer and StringBuilder?

The **string** is immutable and final in Java, so whenever we do String manipulation, it creates a new String. String manipulations are resource consuming, so java provides two utility classes for String manipulations – **StringBuffer** and **StringBuilder**.  
StringBuffer and StringBuilder are mutable classes. StringBuffer operations are thread-safe and synchronized where StringBuilder operations are not thread-safe. So in a multi-threaded environment, we should use StringBuffer but in the single-threaded environment, we should use StringBuilder.  
StringBuilder performance is fast than StringBuffer because of no overhead of synchronization.

### Why String is immutable or final in Java

There are several benefits of String because it’s immutable and final.

-   String Pool is possible because String is immutable in java.
-   It increases security because any hacker can’t change its value and it’s used for storing sensitive information such as database username, password etc.
-   Since String is immutable, it’s safe to use in multi-threading and we don’t need any synchronization.
-   Strings are used in java classloader and immutability provides security that correct class is getting loaded by Classloader.
### Why Char array is preferred over String for storing password?

String is immutable in Java and stored in String pool. Once it’s created it stays in the pool until unless garbage collected, so even though we are done with password it’s available in memory for longer duration and there is no way to avoid it. It’s a security risk because anyone having access to memory dump can find the password as clear text.  
If we use a char array to store password, we can set it to blank once we are done with it. So we can control for how long it’s available in memory that avoids the security threat with String.

### How do you check if two Strings are equal in Java?
1. == : it will check the value as well as the refrence 
2. equal : it will only check the value
```
String s1 = "abc"; 
String s2 = "abc"; 
String s3= new String("abc"); 
System.out.println("s1 == s2 ? "+(s1==s2)); //true 
System.out.println("s1 == s3 ? "+(s1==s3)); //false 
System.out.println("s1 equals s3 ? "+(s1.equals(s3))); //true
```

## String Coding question
```

public class Test {

	public void foo(Object o) {
		System.out.println("Object");
	}

	public void foo(String s) {
		System.out.println("String");
	}
	public static void main(String[] args) {
		new Test().foo(null);
	}

}
```
**Output**: String
So the method `foo(String s)` was called by the program. The reason behind this is java compiler tries to find out the method with most specific input parameters to invoke a method. We know that Object is the parent class of String, so the choice was easy. Here is the excerpt from Java Language Specification. <br>
If more than one member method is both accessible and applicable to a method invocation … The Java programming language uses the rule that the most specific method is chosen.
<br><br>
```
public class Test {

	public void foo(Object o) {
		System.out.println("Object");
	}

	public void foo(String s) {
		System.out.println("String");
	}
	public void foo(Integer s) {
		System.out.println("Integer");
	}
	public static void main(String[] args) {
		new Test().foo(null);
	}

}
```
**Output**: Ambiguity Error**
As for both Integer and String  the parent class is Object so it will confuse.
<br><br>

```

public class Test {

	public void foo(Object o) {
		System.out.println("Object");
	}

	public void foo(Exception e) {
		System.out.println("Exception");
	}

	public void foo(NullPointerException ne) {
		System.out.println("NullPointerException");
	}

	public static void main(String[] args) {
		new Test().foo(null);
	}

}

```
**Output** : NullPointerException
*As NullPointerException is child class of Exception and Exception is child class of Object so it will go to NullPointerException* 
<br><br>
```

String s1 = new String("abc");
String s2 = new String("abc");
System.out.println(s1 == s2); //false

```
<br><br>
```

String s1 = "abc";
StringBuffer s2 = new StringBuffer(s1);
System.out.println(s1.equals(s2));

```
**Output**: False;
*equals method implementation in the String class, you will find a check using **instanceof** operator to check if the type of passed object is String*
<br><br>
```

String s1 = "abc";
String s2 = new String("abc");
s2.intern();
System.out.println(s1 ==s2);

```
**Output**: False
*We know that intern() method will return the String object reference from the string pool, but since we didn’t assigned it back to s2, there is no change in s2 and hence both s1 and s2 are having different reference.*
<br><Br>
```

String s1 = new String("Hello");  
String s2 = new String("Hello");

```
**Total no of object** : 3
First – line 1, “Hello” object in the string pool as it is in double quote and the refrence will be assign to new operator then it will create the object into the heap memory. So that will be the second object create
Third – line 2, new String with value “Hello” in the heap memory. Here “Hello” string from string pool is reused.

## Stream API
### Collections and Java Stream
A collection is an in-memory data structure to hold values<br>
Java Stream doesn’t store data, it operates on the object stored in collection or array and produce pipelined data that we can use and perform specific operations.
In Stream operation processing on object is done in two manner:
1. **Intermediate Operation** :Java Stream API operations that returns a new Stream are called intermediate operations. Most of the times, these operations are lazy in nature, so they start producing new stream elements and send it to the next operation. Intermediate operations are never the final result producing operations. Commonly used intermediate operations are `filter` and `map`
2. **Terminal Operations:**: Java 8  Stream API operations that returns a result or produce a side effect. Once the terminal method is called on a stream, it consumes the stream and after that we can’t use stream. Terminal operations are eager in nature i.e they process all the elements in the stream before returning the result. Commonly used terminal methods are `forEach`, `toArray`, `min`, `max`, `findFirst`, `anyMatch`, `allMatch`
Java Stream operations use functional interfaces in method argument so we can use lamda expression.
Java Streams are consumable, so there is no way to create a reference to stream for future usage. Since the data is on-demand, it’s not possible to reuse the same stream multiple times.

### Java Stream Short Circuiting Operations

An intermediate operation is called short circuiting, if it may produce finite stream for an infinite stream. For example  `limit()`  and  `skip()`  are two short circuiting intermediate operations.

A terminal operation is called short circuiting, if it may terminate in finite time for infinite stream. For example  `anyMatch`,  `allMatch`,  `noneMatch`,  `findFirst`  and  `findAny`  are short circuiting terminal operations.

### Functional Interfaces in Java 8 Stream
1. **Function and BiFunction**: Function represents a function that takes one type of argument and returns another type of argument. `Function<T, R>` is the generic form where T is the type of the input to the function and R is the type of the result of the function.
2. **Predicate and BiPredicate**: It represents a predicate against which elements of the stream are tested. This is used to filter elements from the java stream.
3. **Consumer and BiConsumer**: It represents an operation that accepts a single input argument and returns no result
4. **Supplier**: Supplier represent an operation through which we can generate new values in the stream.


## Collections:
java release contained few classes for collections: **Vector**, **Stack**, **Hashtable**, **Array**. 
Although Map interface and its implementations are part of the Collections Framework, Map is not collections and collections are not Map.
### What do you understand by iterator fail-fast property?

Iterator fail-fast property checks for any modification in the structure of the underlying collection everytime we try to get the next element. If there are any modifications found, it throws  `ConcurrentModificationException`. All the implementations of Iterator in Collection classes are fail-fast by design except the concurrent collection classes like ConcurrentHashMap and CopyOnWriteArrayList.
### What is difference between fail-fast and fail-safe?

Iterator fail-safe property work with the clone of underlying collection, hence it’s not affected by any modification in the collection. By design, all the collection classes in  `java.util`  package are fail-fast whereas collection classes in  `java.util.concurrent`  are fail-safe.  
Fail-fast iterators throw ConcurrentModificationException whereas fail-safe iterator never throws ConcurrentModificationException.
### How to avoid ConcurrentModificationException while iterating a collection?

We can use concurrent collection classes to avoid  `ConcurrentModificationException`  while iterating over a collection, for example CopyOnWriteArrayList instead of ArrayList.
### How HashMap works in Java?

HashMap stores key-value pair in  `Map.Entry`  static nested class implementation. HashMap works on hashing algorithm and uses hashCode() and equals() method in  `put`  and  `get`  methods.

When we call  `put`  method by passing key-value pair, HashMap uses Key hashCode() with hashing to find out the index to store the key-value pair. The Entry is stored in the LinkedList, so if there is an already existing entry, it uses equals() method to check if the passed key already exists, if yes it overwrites the value else it creates a new entry and stores this key-value Entry else on the same key it will add new entry to the linkedlist and in java 8 it will be in binary tree.

When we call  `get`  method by passing Key, again it uses the hashCode() to find the index in the array and then use equals() method to find the correct Entry and return its value.
### What is the importance of hashCode() and equals() methods?

HashMap uses the Key object hashCode() and equals() method to determine the index to put the key-value pair. These methods are also used when we try to get value from HashMap. If these methods are not implemented correctly, two different Key’s might produce the same hashCode() and equals() output and in that case, rather than storing it at a different location, HashMap will consider the same and overwrite them.

Similarly all the collection classes that doesn’t store duplicate data use hashCode() and equals() to find duplicates, so it’s very important to implement them correctly. The implementation of equals() and hashCode() should follow these rules.

-   If  `o1.equals(o2)`, then  `o1.hashCode() == o2.hashCode()`should always be  `true`.
-   If  `o1.hashCode() == o2.hashCode`  is true, it doesn’t mean that  `o1.equals(o2)`  will be  `true`.

### What are different Collection views provided by Map interface?

Map interface provides three collection views:

1.  **Set<K> keySet()**: Returns a Set view of the keys contained in this map. The set is backed by the map, so changes to the map are reflected in the set, and vice-versa. If the map is modified while an iteration over the set is in progress (except through the iterator’s remove operation), the results of the iteration are undefined. The set supports element removal, which removes the corresponding mapping from the map, via the Iterator remove, Set.remove, removeAll, retainAll, and clear operations. It does not support the add or addAll operations.
2.  **Collection<V> values()**: Returns a Collection view of the values contained in this map. The collection is backed by the map, so changes to the map are reflected in the collection, and vice-versa. If the map is modified while an iteration over the collection is in progress (except through the iterator’s remove operation), the results of the iteration are undefined. The collection supports element removal, which removes the corresponding mapping from the map, via the Iterator remove, Collection.remove, removeAll, retainAll, and clear operations. It does not support the add or addAll operations.
3.  **Set<Map.Entry<K, V>> entrySet()**: Returns a Set view of the mappings contained in this map. The set is backed by the map, so changes to the map are reflected in the set, and vice-versa. If the map is modified while an iteration over the set is in progress (except through the iterator’s remove operation, or the setValue operation on a map entry returned by the iterator) the results of the iteration are undefined. The set supports element removal, which removes the corresponding mapping from the map, via the Iterator remove, Set.remove, removeAll, retainAll, and clear operations. It does not support the add or addAll operations.
### What is difference between HashMap and Hashtable?

HashMap and Hashtable both implements Map interface and looks similar, however, there is the following difference between HashMap and Hashtable.

1.  HashMap allows null key and values whereas Hashtable doesn’t allow null key and values.
2.  Hashtable is synchronized but HashMap is not synchronized. So HashMap is better for single threaded environment, Hashtable is suitable for multi-threaded environment.
3.  `LinkedHashMap`  was introduced in Java 1.4 as a subclass of HashMap, so incase you want iteration order, you can easily switch from HashMap to LinkedHashMap but that is not the case with Hashtable whose iteration order is unpredictable.
4.  HashMap provides Set of keys to iterate and hence it’s fail-fast but Hashtable provides Enumeration of keys that doesn’t support this feature.
5.  Hashtable is considered to be legacy class and if you are looking for modifications of Map while iterating, you should use ConcurrentHashMap.
### How to decide between HashMap and TreeMap?

For inserting, deleting, and locating elements in a Map, the HashMap offers the best alternative. If, however, you need to traverse the keys in a sorted order, then TreeMap is your better alternative. Depending upon the size of your collection, it may be faster to add elements to a HashMap, then convert the map to a TreeMap for sorted key traversal.
### What are similarities and difference between ArrayList and Vector?

ArrayList and Vector are similar classes in many ways.

1.  Both are index based and backed up by an array internally.
2.  Both maintains the order of insertion and we can get the elements in the order of insertion.
3.  The iterator implementations of ArrayList and Vector both are fail-fast by design.
4.  ArrayList and Vector both allows null values and random access to element using index number.

These are the differences between ArrayList and Vector.

1.  Vector is synchronized whereas ArrayList is not synchronized. However if you are looking for modification of list while iterating, you should use CopyOnWriteArrayList.
2.  ArrayList is faster than Vector because it doesn’t have any overhead because of synchronization.
3.  ArrayList is more versatile because we can get synchronized list or read-only list from it easily using Collections utility class.
4. 1.  ### What is difference between Array and ArrayList? When will you use Array over ArrayList?
    
    Arrays can contain primitive or Objects whereas ArrayList can contain only Objects.  
    Arrays are fixed-size whereas ArrayList size is dynamic.  
    Arrays don’t provide a lot of features like ArrayList, such as addAll, removeAll, iterator, etc.
    
    Although ArrayList is the obvious choice when we work on the list, there are a few times when an array is good to use.
    
    -   If the size of list is fixed and mostly used to store and traverse them.
    -   For list of primitive data types, although Collections use autoboxing to reduce the coding effort but still it makes them slow when working on fixed size primitive data types.
    -   If you are working on fixed multi-dimensional situation, using [][] is far more easier than List<List<>>

3.  ### What is difference between ArrayList and LinkedList?
    
    ArrayList and LinkedList both implement List interface but there are some differences between them.
    
    1.  ArrayList is an index based data structure backed by Array, so it provides random access to its elements with performance as O(1) but LinkedList stores data as list of nodes where every node is linked to its previous and next node. So even though there is a method to get the element using index, internally it traverse from start to reach at the index node and then return the element, so performance is O(n) that is slower than ArrayList.
    2.  Insertion, addition or removal of an element is faster in LinkedList compared to ArrayList because there is no concept of resizing array or updating index when element is added in middle.
    3.  LinkedList consumes more memory than ArrayList because every node in LinkedList stores reference of previous and next elements.

### While passing a Collection as argument to a function, how can we make sure the function will not be able to modify it?

We can create a read-only collection using  `Collections.unmodifiableCollection(Collection c)`  method before passing it as argument, this will make sure that any operation to change the collection will throw  `UnsupportedOperationException`.
### What are best practices related to Java Collections Framework?

-   Chosing the right type of collection based on the need, for example if size is fixed, we might want to use Array over ArrayList. If we have to iterate over the Map in order of insertion, we need to use LinkedHashMap. If we don’t want duplicates, we should use Set.
-   Some collection classes allows to specify the initial capacity, so if we have an estimate of number of elements we will store, we can use it to avoid rehashing or resizing.
-   Write program in terms of interfaces not implementations, it allows us to change the implementation easily at later point of time.
-   Always use Generics for type-safety and avoid ClassCastException at runtime.
-   Use immutable classes provided by JDK as key in Map to avoid implementation of hashCode() and equals() for our custom class.
-   Use Collections utility class as much as possible for algorithms or to get read-only, synchronized or empty collections rather than writing own implementation. It will enhance code-reuse with greater stability and low maintainability.
### Enumeration, Iterator, ListIterator
|Property| Enumeration |Iterator| ListIterator
|--|--|--|--|
| Applicable |Legacy class  | Collection object| List Object |
| Movment | Single direction |Single Direction |Bi-direction |
| Get Element |element()  |iterator() |listIterator() |
|  Access Permission| Read |Read/ Remove | Read / Remove/ Replace/ Add|




## Exception
### Explain Java Exception Hierarchy?

Java Exceptions are hierarchical and is used to categorize different types of exceptions.  `Throwable`  is the parent class of Java Exceptions Hierarchy and it has two child objects –  `Error`  and  `Exception`. Exceptions are further divided into checked exceptions and runtime exception.

**Errors**  are exceptional scenarios that are out of scope of application and it’s not possible to anticipate and recover from them, for example hardware failure, JVM crash or out of memory error.

**Checked Exceptions**  are exceptional scenarios that we can anticipate in a program and try to recover from it, for example FileNotFoundException. We should catch this exception and provide useful message to user and log it properly for debugging purpose.  `Exception`  is the parent class of all Checked Exceptions.

**Runtime Exceptions**  are caused by bad programming, for example trying to retrieve an element from the Array. We should check the length of array first before trying to retrieve the element otherwise it might throw  `ArrayIndexOutOfBoundException`  at runtime.  `RuntimeException`  is the parent class of all runtime exceptions.

### Explain Java 7 ARM Feature and multi-catch block
```
catch(IOException | SQLException | Exception ex){
 logger.error(ex); throw  new MyException(ex.getMessage()); 
}

```
### What is difference between final, finally and finalize in Java?
Final: its is a keyword in class varibale so that it cannot be reassigned.
Finally: If we want to execute any logic after try or catch block
Finalize: When garbage collector is destroying the object and before that we want to perform some clean up logic on that object.

### Provide some Java Exception Handling Best Practices?

Some of the best practices related to Java Exception Handling are:

-   Use Specific Exceptions for ease of debugging.
-   Throw Exceptions Early (Fail-Fast) in the program.
-   Catch Exceptions late in the program, let the caller handle the exception.
-   Use Java 7 ARM feature to make sure resources are closed or use finally block to close them properly.
-   Always log exception messages for debugging purposes.
-   Use multi-catch block for cleaner close.
-   Use custom exceptions to throw single type of exception from your application API.
-   Follow naming convention, always end with Exception.
-   Document the Exceptions Thrown by a method using @throws in javadoc.
-   Exceptions are costly, so throw it only when it makes sense. Else you can catch them and provide null or empty response.

### When to use custom Exception:
Any Exception that provide information or functionality that is not part of standard Java exception, then its good to write the custom exception. Ex: TicketNotAvailable, By checking certain creiteria as per business functionality if we run out from seat then I have to throw this exception otherwise it always better to use the Java standard exception.

## Java Question:
### What is the importance of main method in Java?

main() method is the entry point of any standalone java application. The syntax of main method is  `public static void main(String args[])`.

Java’s main method is public and static so that Java runtime can access it without initializing the class. The input parameter is an array of String through which we can pass runtime arguments to the java program.
### What is overloading and overriding in java?

When we have more than one method with the same name in a single class but the arguments are different, then it is called method overloading.

The overriding concept comes in picture with inheritance when we have two methods with the same signature, one in the parent class and another in child class. We can use @Override annotation in the child class overridden method to make sure if the parent class method is changed, so as child class.
### What are different types of classloaders?

There are three types of built-in Class Loaders in Java:

1.  Bootstrap Class Loader – It loads JDK internal classes, typically loads rt.jar and other core classes.
2.  Extensions Class Loader – It loads classes from the JDK extensions directory, usually $JAVA_HOME/lib/ext directory.
3.  System Class Loader – It loads classes from the current classpath that can be set while invoking a program using -cp or -classpath command line options.

## Serialization and Deserialization
Serializable Interface : JVM control the serialization logic we can user readObject(ObectInputStream) and writeObject(ObjectOutputStream)  for custom serialization. The value which we dont want to serialize we can use transient keyword and transient keyword dont work with static or final because in static the variable is not object variable but it is class variable and final directly serialize with value.

Externalization Interface: If you dont want complete object , you only want partial object or you want to control the serialization process instead of JVM to control . Method available readExternal and writeExternal. It is more fast then serialization
