# 1 The Basics of Java Programming

Exam objectives:  
- Create classes and records, and define use instance and static fields and methods, constructors, and instance and static initializers.

> ### Note 
>No particular exam objective is covered in this chapter
>
> *Practive makes perfect!*
>  <br> <br>

## 1.1 The Java Ecosystem
There are different Java platforms, each targeting different application domains:
- **Java SE (Standard Edtion)**: designed for developing desktop and server environments
- **Java EE, also known as Jakarta EE (Enterprise Edition)**: designed for developing enterprise applications
- **Java ME (Micro Edition)**: designed for embedded systems, such as mobile devices and set-top boxes
- **Java Card**: designed for tiny memory footprint devices, such as smart cards

Each platform provides a hardware/operating system-specific JVM and an API (application programming interface) to develop applications for that platform. A Java program developed for one Java platform will not necessarily run under the JVM of another platform. The JVM must be compatible with the Java platform that was used to develop the application.  

The API and the tools for developing and running Java applications are bundled together as the JDK.

### Key Features of Java
1. **Multi-paradigm Programming** - java supports object-oriented programming in which the *properties* of an object and its *behaviour* are encapsulated in the object. The properties are represented by **fields** and the behaviour by **methods**. The objects communicate throught method calls in a procedural manner - Java also incorporates the **procedural programming paradigm**. Java has also evolved to support the **functional-style programming paradigm** with the introduction of lambda expressions and their implementation using functional interfaces.

> ## Encapsulation
> Encapsulation ensures that objects are immune to tampering except when manipulated throught their public interface. It exposes only *what* an object does and not *how* it does it, so that its implementation can be changed with minimal impact on its clients.
>  <br> <br>

2. **Bytecode Interpreted by the JVM**  
Java programs are compiled to *bytecode* that is interpreted by the *JVM*.
3. **Architecture-Neutral and Portable Bytecode**  
"write once and run everywhere" is true only if a compatible JVM is available for the hardware and software platform. The specification of the bytecode is architecture neutral, meaning it is independent of any hardware architecture. It is executed by a readily available hardware and operating system-specific JVM. This portability of the Java bytecode thus eases the burden of cross-platform system development.
4. **Simplicity**  
the Java language aimed to simplify the programming process.
5. **Dynamic and Distributed**  
the JVM can dynamically load class libraries from the local file system as well as from machines on the network, when those libraries are needed at runtime.
6. **Robust and Secure**  
it is a strong statically typed language: *the compiler guarantees runtime execution if the code compiles without errors**. Java has a robust security model to ensure the application code executes securely in the JVM.
7. **High Performance and Multithreaded**  
the JIT feature monitors the program at runtime to identify performance-critical bytecode (called hotspots) that can be optimised. Such code is usually translated to machine code to boost performance. Java has always provided high-level support for multithreading, allowing multiple threads of execution to perform different tasks concurrently in an application.

## 1.2 Classes
One of the fundamental ways in which we handle complexity is by using abstractions. An abstraction denotes the essential properties and behaviors of an object that differentiate it from other objects. The essence of OOP is modeling abstractions, using classes and objects. The hardest part of this endeavor is coming up with the right abstractions.  

A **class** denotes a category of objects, and acts as a blueprint for creating objects. A class models an abstraction by defining:
- the properties
- the behaviours

of the objects representing the abstraction. An object exhibits the properties and behaviours defined by its class. 

Properties -> *attributes* -> are defined by **fields**  
A field in a class is a variable that can store a value that represents a particular property of an object.  
The behaviours of of an object of a class are also known as *operations*
Operations -> defined using **methods**

> The fields and methods in a class declaration are collectively called **members**

> ### Contract of a class VS Implementation it provides for its objects
> The contract defines which services are provided  
> The implementation defines how these services are provided by the class  
>
>Clients (i.e., other objects) need only know the contract of an object, and not its implementation, to avail themselves of the object’s services.
> #### Example:
> we will implement a class that models the abstraction of a point as (x, y)-coordinates in a two-dimensional plane. The class Point2D will use two int fields x and y to store the coordinates. Using simplified Unified Modeling Language (UML) notation, the class Point2D is graphically depicted in the table below, which models the abstraction. Both fields, with their type and method names and their return value type, are shown in the table below.

| Class name | Point2D |
|--------|--------|
| Fields | x:int <br> y:int |
| Methods | getX():int <br> getY():int <br> setX():void <br> setY():void <br> toString():String

### Declaring Members: Fields and Methods
The code below displays the basic elements of a Class Declaration:
```java
// File Point2D.java
public class Point2D { // class name
    // Class member declarations

    // Fields:
    private int x;      // The x-coordinate
    private int v;      // The y-coordinate

    // Constructor:
    public Point2D(int xCoord, int yCoord) {
        x = xCoord;
        y = yCoord;
    }

    // Methods:
    public int getX(){ return x; }
    public int getY(){ return y; }
    public void setX(int xCoord) { x = xCoord; }
    public void setY(int xCoord) { y = yCoord; }
    public String toString() { return "(" + x + "," + y + ")"; } // Format: (x,y)
}
```


`//` -> in Java depicts the start of a *single-line comment* - all characters after this sequence and to the end of the line are **ignored by the compiler**.  

Method declarations with the same name as the class are known as *constructors*. A constructor is executed when an object is created from the class.  

## 1.3 Objects
### Class Instantiation, Reference Values, and References
**Instantiation** -> the process of creating objects from a class.  
**Object** -> an instance of a class.  

The object is *constructed* using the class as a blueprint and is a concrete instance of the abstraction that the class represents.  

A *reference value* is returned when an object is created -> this uniquely denotes a particular object.  
A *variable* denotes a location in memory where a value can be stored.  
An *object reference* (or simply a *reference*) is a variable that can store a reference value. -> a reference provides a handle to an object.  

In Java, an object can only be manipulated by a reference that holds its reference value. Direct access to the reference value is not permitted.  

The setup for manipulating objects -> requires that 
- a reference be declared.
- a class be instantiated to create an object
- and the reference value of the object created be stored in the reference

All these steps are accomplished by a *declaration statement*:

```java
Point2D p1 = new Point2D(10, 20); // a point with coordinates (10, 20)
```

- The left hand side of the *assignment operator (=)* declares that `p1` is a reference of class Point2D.
- The reference p1, therefore, can refer to objects of class Point2D.
- The right hand side of the assignment operator creates an object of class Point2D
- This step involves using the `new` operator in conjunction with a call to a constructor of the class

> ### Important Note
> Please understand the difference between *creating a reference of a class* and *creating the actual object (instance) of the class*. <br> <br>


- the `new` operator creates an instance of the Point2D class and returns the reference value of this instance.  

`new` ---> creates an instance of the class  
<--- returns the reference value of this instance  

- The reference `p1` can now be used to to manipulate the object whose reference value it holds.
- Each object that is created has its own copy of the fields declared in the class declaration.  

The fields of an object are also known as **instance variables**.  
-> The values of the instance variables in an object constitute its **state**.

> Two distinct objects can have the same state if their instance variables hold the same value.

Why have the constructor on the RHS of the `new` keyword? -> it is to initialize the fields of the newly created object.

## 1.4 Instance Members
The methods of an object define its behaviour -> such methods are called **instance methods**. There methods pertain to each object of the class.
> In contrast to instance variables, the implementation of the methods is shared by all instances of the class. 

Instance members are different from **static members** (these belong to the class).

### Invoking Methods
A *method call* has this basic form: 
- a reference that refers to the object
- the binary dot (.) operator
- the name of the method to be invoked
- a list of any arguments required by the method.

`reference.methodName(listOfArguments)`


