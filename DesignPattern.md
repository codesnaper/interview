# Design Pattern
## What Are Advantages of Design Patterns?

-   A design patterns are  **well-proved solution**  for solving the specific problem.
-   The benefit of design patterns lies in reusability and extensibility of the already developed applications.
-   Design patterns use  _object-oriented concepts_  like decomposition, inheritance and polymorphism.
-   They provide the solutions that help to define the system architecture.
## What Are Disadvantages of Design Patterns?

-   Design Patterns do not lead to direct code reuse.
-   Design Patterns are deceptively simple.
-   Teams may suffer from patterns overload.
-   Integrating design patterns into a software development process is a human-intensive activity.
## When to use Singleton?

Use the Singleton when

-   There must be only one instance of class
- Class have some state and method which are only read only
- Class have some state and some method and the state is not read only but also it is sharable state.

## Difference between Singleton v/s static class
- A Singleton can implement interfaces, inherit from other classes and allow inheritance. While a static class cannot inherit their instance members. So Singleton is more flexible than static classes and can maintain state.
- A Singleton can be initialized lazily but static will load at time.While a static class is generally initialized when it is first loaded
- Singleton class follow the Object Oriented Principles, so that singletons can be handled polymorphically.
-  Singleton Objects stored on heap while static class stored in stack.
-  Singleton Objects can have constructor while Static Class cannot.

## Disadvantages of singleton

-   Violates Single Responsibility Principle (SRP) by controlling their own creation and lifecycle.
-   Encourages using a global shared instance which prevents an object and resources used by this object from being deallocated.
-   Creates tightly coupled code that is difficult to test.  Makes it almost impossible to subclass a Singleton.

### In how many ways can you create singleton pattern in Java?
Singleton objects can be created in two ways.
-   Lazy loading
	- example:
		```
		public static LazyInitialized getInstance(){
        if(instance == null){
            instance = new LazyInitialized();
        }
        return instance;
    }
    ```
-   Eager loading
	- Example: `private static final EagerInitialized instance = new EagerInitialized();`

### Question:  Can you write thread-safe Singleton in Java?
There are multiple ways to write thread-safe singleton in Java

-   By writing singleton using double checked locking.
-   By using static Singleton instance initialized during class loading.
-   By the way using Java enum to create thread-safe singleton this is most simple way.

### What is Enum Singleton in Java?

To overcome this situation with Reflection, Joshua Bloch suggests the use of Enum to implement Singleton design pattern as Java ensures that any enum value is instantiated only once in a Java program.

Since Java Enum values are globally accessible, so is the singleton. The drawback is that the enum type is somewhat inflexible; for example, it does not allow lazy initialization.
```
public enum EnumSingleton {

    INSTANCE;
    
    public static void doSomething(){
        //do something
    }
}
```

### How to implement singleton class with Serialization in Java?
By overriding readResolve methof
```
protected Object readResolve() {
    return getInstance();
}
```

## Factory Method v/s Abstract Factory 
### **Factory Method**: 
Define an interface for creating an object, but let subclasses decide which class to instantiate. Factory Method lets a class defer instantiation to subclasses.
**Exmple**  :To  Create  a maruti car we will create a factory and it will give different maruti cars.

- Create a interface or abstartc class for creating the object:
 ```
public abstarct Workshop{
	public void assembleCar(Car c){
		sout("Assemble Car");
   }
	public abstract Car createCar(String type);
}
```

- Create a subclass which will have the implementation of factory method
```
//SUVCar and sedanCar and Car is implement from Car interface
public Class Zone1Workshop extends Workshop{
	@Override
	public Car createCar(String type){
		if(type == "sedan"){
			return new SedanCar();
		}
		else if (type == "SUV")
		{
			return new SUVCar();
		}
		return new Car();
	}

	public void produceCar(Car c){
		super.assembleCar(c);
	}
}
```
**Main.class**
```
	Car c = new Zone1Workshop().createCar("sedan");
	new Zone1Workshop().produceCar(c);
```

### Abstract Factory
It can be treated as super factory or factories of factory. There is only one class who is responsible for creation of  object of another class
Example :  we have DBDao Facotry and XMLDao facotry which save the employee or company data to database.
So we will create one more factory class DAO Maker which will be super factory and will use composition as DaoFactory to hold DBDaoFactory or EmpDaoFactory.

### **Difference**:
1. Factory Method depends on _inheritance_ to decide which product to be created. in Abstract Factory, there’s a _separate class dedicated to create_ a family of object and it depends on composition
2. Factory Method is _just a method_ while Abstract Factory is an _object_. The _purpose_ of a Class having factory method is _not just create_ objects, it does other work also, _only a method is responsible_ for _creating_ object. In Abstract Factory, the _whole purpose_ of the class is to _create family of objects_.
3. Abstract Factory is one level _higher in abstraction_ than Factory Method. Factory Method _abstracts the way objects are created_, while Abstract Factory also _abstracts the way factories are created_ which in turn abstracts the way objects are created.

## Strategy Pattern:
We define multiple algorithms and let client application pass the algorithm to be used as a parameter.

One of the best example of strategy pattern is  `Collections.sort()`  method that takes Comparator parameter. Based on the different implementations of Comparator interfaces, the Objects are getting sorted in different ways.

### What does builder pattern do?

Builder pattern separates the construction of a complex object from its representation so that the same construction process can create different representations.
## When to use Builder pattern?

Use the Builder pattern when

-   the algorithm for creating a complex object should be independent of the parts that make up the object and how they're assembled
-   the construction process must allow different representations for the object that's constructed
#### Typical use cases

-   java.lang.StringBuilder
-  java.nio.ByteBuffer
-   java.lang.StringBuffer

#### Rules of thumb

-   Builder focuses on constructing a complex object step by step. Abstract Factory emphasizes a family of product objects (either simple or complex). Builder returns the product as a final step, but as far as the Abstract Factory is concerned, the product gets returned immediately.
-   Builder often builds a Composite.
-   Often, designs start out using Factory Method (less complicated, more customizable, subclasses proliferate) and evolve toward Abstract Factory, Prototype, or Builder (more flexible, more complex) as the designer discovers where more flexibility is needed.

### What are advantage of Builder Design Pattern?


The main advantages of Builder Pattern are as follows:

-   It provides clear separation between the construction and representation of an object.
-   It provides better control over construction process.
-   It supports to change the internal representation of objects.

### What specific problems builder pattern solves?

This pattern was introduced to solve some of the problems with Factory and Abstract Factory design patterns.

When the Object contains a lot of attributes. Builder pattern solves the issue with large number of optional parameters and inconsistent state by providing a way to build the object step-by-step and provide a method that will actually return the final Object.

## Adapter:
Adapter pattern works as a bridge between two incompatible interfaces.This pattern involves a single class which is responsible to join functionalities of independent or incompatible interfaces.
<br>
There are two approaches – class adapter and object adapter – however both these approaches produce same result.

1.  **Class Adapter**  – This form uses  **java inheritance**]and extends the source interface, in our case Socket class.
2.  **Object Adapter**  – This form uses  **Java Composition** and adapter contains the source object.

Example:
Volt.class
```
public class Volt {

	private int volts;
	
	public Volt(int v){
		this.volts=v;
	}

	public int getVolts() {
		return volts;
	}

	public void setVolts(int volts) {
		this.volts = volts;
	}
	
}
```
**Socket .class** :  It can create only one volt. 
```
public class Socket {

	public Volt getVolt(){
		return new Volt(120);
	}
}

```

Now i want socket to have volt like 140, 150
**SocketAdapter.class**
```

public interface SocketAdapter {

	public Volt get120Volt();
		
	public Volt get12Volt();
	
	public Volt get3Volt();
}

```

**USING CLASS ADAPTER**
```
//Using inheritance for adapter pattern
public class SocketClassAdapterImpl extends Socket implements SocketAdapter{

	@Override
	public Volt get120Volt() {
		return getVolt();
	}

	@Override
	public Volt get12Volt() {
		Volt v= getVolt();
		return convertVolt(v,10);
	}

	@Override
	public Volt get3Volt() {
		Volt v= getVolt();
		return convertVolt(v,40);
	}
	
	private Volt convertVolt(Volt v, int i) {
		return new Volt(v.getVolts()/i);
	}

}

```
**USING OBJECT ADAPTER**
```

public class SocketObjectAdapterImpl implements SocketAdapter{

	//Using Composition for adapter pattern
	private Socket sock = new Socket();
	
	@Override
	public Volt get120Volt() {
		return sock.getVolt();
	}

	@Override
	public Volt get12Volt() {
		Volt v= sock.getVolt();
		return convertVolt(v,10);
	}

	@Override
	public Volt get3Volt() {
		Volt v= sock.getVolt();
		return convertVolt(v,40);
	}
	
	private Volt convertVolt(Volt v, int i) {
		return new Volt(v.getVolts()/i);
	}
}

```
## What does proxy pattern do?

Proxy pattern provides a substitute or placeholder for another object to control access to it.

## When to use proxy pattern?

Proxy pattern is applicable whenever there is a need for a more versatile or sophisticated reference to an object than a simple pointer. Here are several common situations in which the Proxy pattern is applicable

-   Remote proxy provides a local representative for an object in a different address space.
-   Virtual proxy creates expensive objects on demand.
-   Protection proxy controls access to the original object. Protection proxies are useful when objects should have different access rights.

#### Typical Use Case

-   Control access to another object
-   Lazy initialization
-   Implement logging
-   Facilitate network connection
-   Count references to an object

##### Rules of thumb

-   Adapter provides a different interface to its subject. Proxy provides the same interface. Decorator provides an enhanced interface.
-   Decorator and Proxy have different purposes but similar structures. Both describe how to provide a level of indirection to another object, and the implementations keep a reference to the object to which they forward requests.

### What are different proxies?

There are multiple use cases where the proxy pattern is useful.

**Protection proxy:**  limits access to the real subject. Based on some condition the proxy filters the calls and only some of them are let through to the real subject.

**Virtual proxies:**  are used when an object is expensive to instantiate. In the implementation the proxy manages the lifetime of the real subject.

It decides when the instance creation is needed and when it can be reused. Virtual proxies are used to optimize performance.

**Caching proxies:**  are used to cache expensive calls to the real subject. There are multiple caching strategies that the proxy can use.

Some examples are read-through, write-through, cache-aside and time-based. The caching proxies are used for enhancing performance.

**Remote proxies:**  are used in distributed object communication. Invoking a local object method on the remote proxy causes execution on the remote object.

**Smart proxies:**  are used to implement reference counting and log calls to the object.

### Difference between Proxy and Adapter?


Adapter object has a different input than the real subject whereas Proxy object has the same input as the real subject.

Proxy object is such that it should be placed as it is in place of the real subject.


# solid:
- **Single Responsibility Principle:** This principle states that “_a class should have only one reason to change_”
- **Open/Closed Principle:** This principle states that “_software entities (classes, modules, functions, etc.) should be open for extension, but closed for modification_”
- **Liskov’s Substitution Principle:**: according to this principle “_Derived or child classes must be substitutable for their base or parent classes_“
- **Interface Segregation Principle:**:it states that “_do not force any client to implement an interface which is irrelevant to them_“
- **Dependency Inversion Principle:**: Now two key points are here to keep in mind about this principle

	-   High-level modules/classes should not depend on low-level modules/classes. Both should depend upon abstractions.
	-   Abstractions should not depend upon details. Details should depend upon abstractions.
