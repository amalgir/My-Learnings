# Java DSA - OOP

These are notes made for revision, after watching the Java DSA playlist of Kunal Kushwaha on youtube.

***


## Main Topics

1) [Introduction](java_dsa_intro.md)
2) [OOP](java_dsa_oop.md)


***

## Contents

1) [OOP - Introduction & Concepts](#id1)
2) [OOP - Packages,Static,Singleton Class,In-built methods](#id2)
3) [OOP - Principles: Inheritance, Polymorphism, Encapsulation, Abstraction](#id3)
4) [OOP - Access Control, In-built Packages, Object Class](#id4)
5) [OOP - Abstract Classes, Interfaces, Annotations](#id5)
6) [Generics, Custom ArrayList, Lambda Expressions, Exception Handling, Object Cloning](#id6)
7) [Collections Framework, Vector Class, Enums in Java](#id7)

***

<div id="id1"></div>

### 1) OOP - Introduction & Concepts

#### Class

Class --> named group of properties and functions (a logical construct)

Object/Instance --> physical reality/ occupies memory space

In Human class, we are all different objects or instance of the class

**new**  --> Dynamically(runtime) allocates memory & returns a reference variable

```java
import java.util.Arrays;

class Student{
    int rno;
    String name;
    float marks;
}

public class Example{
    public static void main(String[] args) {
        Student[] students = new Student[5];
        System.out.println(Arrays.toString(students));  // [null, null, null, null, null]

        Student sam; // Declaration of reference variable in stack memory at compile time  --> no object created
        sam = new Student();  // Dynamic memory allocation in heap memory at runtime
        sam.name = "Sam";  // giving a value to an instance variable
        System.out.println(sam.name);  // Sam
        System.out.println(sam.marks); // 0.0   BY DEFAULT
    }
}
```

* Default value of `sam.rno`-->0, `sam.name`-->null, `sam.marks`-->0.0 ie if nothing is initialized
* In `sam = new Student();`  Student() is the constructor (by default constructor)
***

#### Constructor

* constructor =--> what to do when an object is created
* constructor  is special function, that runs when we create an object & it allocates some variables

* reference variable of the object is accessed using `this`.  Ex: `this.name = "Sam Sam";`

***

#### Constructor Overloading

```java
class Student{
    int rno;
    String name;
    float marks;

    // DEFAULT CONSTRUCTOR
    Student(){
        this.name = "Default User";
    }

    // CONSTRUCTOR
    Student(int rno, String name, float marks ){
        // if we dont put 'this' here, java confuses with both 'rno'- local rno and object rno
        this.rno = rno;
        this.name = name;
        this.marks = marks;
    }

    void displayName(){
        System.out.println("NAME: " + this.name);
    }
}

public class Example{
    public static void main(String[] args) {

        Student student1 = new Student();  // Calls Default Constructor
        Student student2 = new Student(22, "AG", 89.9f );

        student1.displayName(); // NAME: Default User
        student2.displayName(); // NAME: AG

        System.out.println(student1.marks); // 0.0
        System.out.println(student2.marks); // 89.9
        
    }
}
```

Here we can pass even another object as parameter in a constructor

>```java
>// Constructor - Inside class
>Student(Student object){
>this.rno = object.rno;
>this.name = object.name;
>this.marks = object.marks;
>}
>```
>
>```java
>// In main method
>Student ag = new Student(22, "AG", 89.9f );
>Student random = new Student(ag);
>
>System.out.println(random.name);  // AG
>```


***

#### Calling one constructor from another constructor

```java
// DEFAULT CONSTRUCTOR
Student(){
    // internally calls this constructor-->  Student(11, "Default", 25.0f)
    this(11, "Default", 25.0f);
}
```

* Primitive datatypes are not implemented as objects. So they are stored in stack memory (NOT heap)
* Thats why we dont use `new` with primitive (like int, float)

* same object reference variable in stack points to same object in heap
```java
Student one = new Student(12, "SAM", 2.2f);
Student two = one;

one.name = "CHANGED";
System.out.println(one.name); // CHANGED
System.out.println(two.name); // CHANGED
```

***

#### Wrapper class & final

> `int a = 10;`  // not an object
> 
> `Integer a = new Integer(10);`  // Wrapper class creates object
> 
> `Integer a = 10;`  // Wrapper class creates object

* swap does NOT work with primitive data types (like int)
* Usually swap works for objects (like arrays)
* But here Wrapper class objects DO NOT allow swap because it is a `final` class
* `final` object cannot be modified (constant)
* for constants, use capital letters
* final variable must be initialized

```java
final int SLA = 10;
SLA = 25; // ERROR -> Cannot assign a value to final variable 'SLA'
```

* For final objects, the reference name is final. Value of that object can be changed as it is still pointing to the same object

> `final Student one = new Student();`
> 
> Now we can change the value of the object `one` -->  `one.name = "Sam";`
> 
> But we cannot assign another object to this reference object --> `one = another object NOT possible`


When a non primitive is final, we cannot reassign it (but might change its value)

***

#### Garbage collection & finalize

* `finalize` is the method which gets called when an object is destroyed or removed from memory by java automatically. 
* We cannot destroy object manually

```java
class A{

    A(){
        System.out.println("Created object");
    }

    @Override
    protected void finalize() throws Throwable {
        System.out.println("Object is destroyed");
    }
}
```


A trick to check this.. Force java to destroy some objects

```java
A obj;

for (int i=0; i<10000000; i++){
    obj = new A();
}
```

***
***

<div id="id2"></div>

### 2) OOP - Packages,Static,Singleton Class,In-built methods

#### Packages

* packages are folders
* For example: `src` folder --> `com` folder --> `ag` --> `oop` --> `Example.java` file
* Here, `Example.java `file has the statement `package com.ag.oop;`
* Same file names cannot be in one folder, but possible in different folder (like `Example.java` file in `com.ag.intro`)

#### import

Assume folder structure  `com` --> `ag` --> `packages` -->`a` `b`  --> both has one `Sample.java` each

> **b\Sample.java**
>```java
>package com.ag.packages.b;
>
>public class Sample {
>public static void main(String[] args) {
>}
>
>    public static void displayMessage(){
>        System.out.println("This is from class B in package com.ag.packages.b");
>    }
>}
>```
>
> **a\Sample.java** 
> 
>```java
>package com.ag.packages.a;
>
>public class Sample {
>public static void main(String[] args) {
>com.ag.packages.b.Sample.displayMessage();
> // RUNNING THIS -->This is from class B in package com.ag.packages.b
>}
>}
>```
> 
 
NOTE: If displayMessage() is private, then it is NOT accessible in a\Sample.java file

***

#### static

Access static variable using format  -->  `ClassName.staticVariable`

```java
class Human{
    int age;
    String name;
    static long population;

    Human(){
        Human.population += 1;   // No need to use 'this' for static
    }
}

public class Example{
    public static void main(String[] args) {
        // Correct way to call population as static is independent of object
        System.out.println(Human.population);  // 0
        Human person1 = new Human();
        System.out.println(person1.population);  //  ANS:1  --> OR Human.population (Correct way)

        Human person2 = new Human();
        System.out.println(Human.population); // 2

    }
}
```

* `main` is the first thing running in java. If no `main` in class, no run option in intellij
* thats why, `main` is `static`
* We cannot call a non static function inside a static function (say like main) directly.
* To call non static --> create object and then call  `Main obj = new Main();  obj.callNonStaticFunction();`
* To directly call the function without creating object --> make that function also static
* But We can use static function inside a non static function

* Static Function cannot use object or instance variable

```java
class Human{
    int age;
    String name;
    static long population;
    
    // Static function is independent of object. It can be directly called using class without creating object
    // Then how can 'message()' function, which doesnt need an object to call it, get 'age' which is an object/instance variable?
    static void message(){
        System.out.println(this.age);  // ERROR  'Human.this' cannot be referenced from a static context
    }

    Human(){
        Human.population += 1;
    }
}
```

***

#### static block

static block is called only once, when first time a class name is used (for calling a static variable or when creating a object)

```java
public class Example{
    static int a = 5;
    static int b;

    // Will only run once, when the first class name is used
    static {
        System.out.println("In static block");
        b = a * 10;
    }

    public static void main(String[] args) {
        System.out.println("a-->" + Example.a + "  b-->" + Example.b);
        /* 
        In static block
        a-->5  b-->50
         */

        Example obj = new Example();
        System.out.println("a-->" + Example.a + "  b-->" + Example.b);
        // a-->5  b-->50

        Example.b += 3;
        System.out.println("a-->" + Example.a + "  b-->" + Example.b);
        // a-->5  b-->53

        Example obj2 = new Example();
        System.out.println("a-->" + Example.a + "  b-->" + Example.b);
        // a-->5  b-->53
        
    }
}
```

***

#### Inner Class

```java
public class Example{

    // INNER CLASS in 'Example' class --> MUST BE STATIC to use like this, else error
    static class InnerClass{
        String name;

        public InnerClass(String naam){
            this.name = naam;
        }
    }

    // MAIN METHOD IN 'Example' class
    public static void main(String[] args) {
        InnerClass obj1 = new InnerClass("Object 1");
        InnerClass obj2 = new InnerClass("Object 2");

        System.out.println(obj1.name); // Object 1
        System.out.println(obj2.name); // Object 2
    }
    
}
```

* Inner class must be static to use like this
* Inner class is static --> means inner class is independent of outer class (to call inner class, you dont need outer class object)
* This does NOT mean `name` is static. It is not static here. Check the output of above code
* Static stuffs are done during compile time

***

#### Singleton class

Class in which you can create only ONE OBJECT

* For that don't allow people to use its constructor, as calling constructor creates object


```java
class Singleton{
    // private constructor --> so no one can create object from outside this class
    private Singleton(){
        System.out.println("Singleton instance created");
    }

    private static Singleton instance;

    // To get object, use this method only. No way to get another instance/object
    public static Singleton getInstance(){
        if (instance == null){
            instance = new Singleton();  // If instance is null, creates new instance of Singleton class
        }
        return instance;
    }
}


public class Example{
    public static void main(String[] args) {
        /*
        Singleton obj1 = new Singleton();  //ERROR 'Singleton()' has private access in 'Singleton'
         */

        Singleton obj1 = Singleton.getInstance();  // Singleton instance created
        Singleton obj2 = Singleton.getInstance();
        Singleton obj3 = Singleton.getInstance();
        
        // All three reference objects point to the same object/instance created for obj1 
    }
}
```

***
***

<div id="id3"></div>

### 3) Principles - Inheritance, Polymorphism, Encapsulation, Abstraction

#### Inheritance

* Child Class inherits from Base Class
* Child class has its parents properties + its own properties
* `super()` --> calls parent/base class's constructor
* `super(25, 5, 24)` --> calls respective parent constructor
* `extends`  --> to inherit base class like `class BoxWeight extends Box{`
* private variables from Base class are not accessible for child class. Then use methods from Base class or super() to call methods written in Base class
* object of base class cannot access child class variables

```java
class Box{
    int l, w, h;

    // Default Constructor of Base class Box
    Box(){
        this.l = -1;
        this.w = -1;
        this.h = -1;
    }

    Box(int length, int width, int height){
        this.l = length;
        this.w = width;
        this.h = height;
    }
}


class BoxWeight extends Box{
    int weight;

    // Default constructor - to initialize all variables
    BoxWeight(){
        // super calls Parent/Base Class constructor
        // call to super must be the first statement in constructor
        super();  // Since no argument given calls default constructor Box()
        weight = -1;
    }

    BoxWeight(int length, int width, int height, int weight){
        super(length, width, height);
        this.weight = weight;
    }
}


public class Example{
    public static void main(String[] args) {
        BoxWeight box1 = new BoxWeight();
        System.out.println(box1.l + " " + box1.w + " " + box1.h + " " + box1.weight); // -1 -1 -1 -1

        BoxWeight box2 = new BoxWeight(25, 50, 75, 100);
        System.out.println(box2.l + " " + box2.w + " " + box2.h + " " + box2.weight); // 25 50 75 100
    }

}
```

>Box reference variable in stack pointing to BoxWeight object in heap
> cannot access BoxWeight properties
> 
>```java
>Box box3 = new BoxWeight(11, 22, 33, 44);
>// System.out.println(box3.weight);  // ERROR Cannot resolve symbol 'weight'
>```

Above case is done using this code

>One of the constructor in Box
>```java
>Box(Box old){
>    this.l = old.l;
>    this.w = old.w;
>    this.h = old.h;
>}
>```
> 
> One of the constructor in BoxWeight
>```java
>BoxWeight(BoxWeight other){
>   super(other);
>   this.weight = other.weight;
>}
>```
>
>This `super(other);` is same as `Box box3 = new BoxWeight();`

* Vice versa is not possible
* Child reference variable cannot point to parent object
* `BoxWeight box4 = new Box(1,2,3);`  --> not possible as weight is accessible for box4 but not initialized by constructor(Box)


#### super

* super points to direct above (parent) class
* `super in BoxWeight`  --> `Box`
* `super in Box` --> `Object`   Here Object is a class
* All classes we create are child of java's Object class
* so we can use super() in a class we created without parent class
* `this` is used to access object. `super` can be used to access parent class's object
* Example if `Box` too has variable `weight`, How can we distinguish between `weight` in both Box and BoxWeight? 
* `super.weight` is Box's weight.  `this.weight` is BoxWeight's weight (Assuming we are using both in BoxWeight class)
* `BoxWeight box1 = new BoxWeight();`  --> Here Box constructor also gets called first when BoxWeight constructor is called, even if super() is not present in BoxWeight
* That is, child constructor automatically by default calls parents default constructor if we didnt used super() in child constructor


***

#### Types of Inheritance

* **Single Inheritance**

    Base class --> Child class


* **Multilevel inheritance**

    * A class --> B class(child of A, Parent of C) --> C class (child of B)
    * super() in C calls constructor in B & one in B calls constructor in A


* **Multiple Inheritance**  (_NOT PRESENT IN JAVA_)

    * One class extends more than one class
    * class C inherits from both A and B
    * So If A and B has say `n=5` and `n=10`, which n will class C gets?? --> So multiple inheritance not supported in java


* **Hierarchial Inheritance**
    * One class is inherited by many classes
    * `A --> B `  `A --> C`  `A --> D`


* **Hybrid Inheritance** (_NOT PRESENT IN JAVA_)
    * Consists of simple and multiple inheritance --> So NOT IN JAVA

  ![Hybrid Inheritance](/Images/JavaDSA/hybrid_inheritance.jpg)


***

#### Polymorphism

`Poly --> many`    `Morphism --> many ways to represent`

#### Types of polymorphism

1) **Compile time / static polymorphism**

    * Achieved by **method overloading** - same method names, but different arguments, return types..
    * Example - different constructors

***

2) **Runtime / Dynamic Polymorphism**
    * Achieved by **method overriding**
   
```java
class Shapes{
    void area(){
        System.out.println("Shows are of shape");
    }
}

class Circle extends Shapes{
    // @Override Annotation gives error if this method is not present in its super/parent class (Shapes)
    @Override
    void area(){
        System.out.println("Area of circle = pi*r*r");
    }
}

public class Example{
    public static void main(String[] args) {
        Circle circle = new Circle();
        circle.area();  // Area of circle = pi*r*r

        // Works when type is parent and object is child
        // Calls child method, but parent should also have that method and child should override it
        Shapes shapeCircle = new Circle();
        shapeCircle.area();  // Area of circle = pi*r*r
        /*
        Gives error if 'area()' method is absent in Shapes class --> Cannot resolve method 'area' in 'Shapes'
         */

    }
}
```
> **How Overriding works?**
> 
> `Parent obj = new Child();`
> 
> Here which method is called depends on Child().
> 
> This is known as Upcasting
> 
> (Parent) reference type determines what all are accessible , which we already discussed

* Note:  If the method in base class is `final`, then we cannot Override it in the child class (boosts performance a little too)
* In this case, compiler is sure that no one is going to override it, so no need to check this. Hence better performance
* This is called **_Early Binding_**
* If `final` is not there, then compiler decides which method to run (obviously child one if child object used) during compile time
* This is called **_Late Binding_**

***

#### How to prevent a class from inherited to others

* By putting `final` to a class, that class cannot be inherited by others
* `public final class Box{`  --> this prevents `BoxWeight` from extending `Box`

***

**Static method cannot be overriden, But can be inherited**

* Overriding depends on object, But static does not depends on object --> hence static cannot be overriden

***

#### Encapsulation & Abstraction

**Encapsulation** --> Wrapping up the implementation of the data members and methods in a class

**Abstraction**  --> Hiding unnecessary details and showing valuable information

* For ex: we use `ArrayList`. But we dont care how java implements it in ArrayList class. This is **Abstraction**
* Encapsulation is implementation level, Abstraction is design level like what to show and what not needed
* Encapsulation is like containers. Containing things to groups (class). Making data secure
* While data hiding focuses on restricting data use in a program to assure data security, data encapsulation focuses on wrapping (or encapsulating) the complex data to present a simpler view to the user.
* In data hiding, the data has to be defined as private only. In data encapsulation, the data can be public or private.
* Encapsulation is sub process of Data hiding

***
***

<div id="id4"></div>

#### 4) Access Control, In-built Packages, Object Class

#### Access Modifiers

* private --> accessible only in that class
* public  --> accessible everywhere
* default access modifier (no access specified) --> accessible inside package.Cannot access from another package

![Access Modifiers](/Images/JavaDSA/access_modifier.jpg)


**DATA HIDING using private, getters, setters**

* Use private to hide data members
* Use getters and setters methods which are public, to change or access this hidden data member

> class A
> 
>```java
>package com.ag.packages.a;
>
>public class A {
>private int num;
>String name;
>
>    // constructor should be public to access from outside file
>    public A(int num, String name){
>        this.num = num;
>        this.name = name;
>    }
>
>    // getter
>    public int getNum(){
>        return num;
>    }
>
>    //setter
>    public void setNum(int num){
>        this.num = num;
>    }
>
>}
>```
>
>
>class B
> 
>```java
>package com.ag.packages.b;
>
>import com.ag.packages.a.A;
>
>public class B {
>public static void main(String[] args) {
>A objA = new A(100, "AG");
>
>//      System.out.println(objA.num);  ERROR 'num' has private access in 'com.ag.packages.a.A'
>
>        System.out.println(objA.getNum());  // 100
>        objA.setNum(255);
>        System.out.println(objA.getNum());  // 255
>    }
>}
>```

***

#### protected

> class A in package 'a'
> 
>```java
>package com.ag.packages.a;
>
>public class A {
>protected int num;
>String name;
>}
>```
>
> class B in package 'b'
> 
>```java
>package com.ag.packages.b;
>
>import com.ag.packages.a.A;
>
>public class B extends A{
>    B(){
>        System.out.println(this.num);  // B object can access it as it inherit A
>    }
>    public static void main(String[] args) {
>        A obj = new A();  // A object cannot access it here
>        // int n = obj.num;   ERROR--> 'num' has protected access in 'com.ag.packages.a.A'
>
>    }
>}
>```

***

#### Packages

* two types -- user defined & in built

#### In built packages

* **lang** (java language specific ones) --> operators, primitive datatypes 
* **io** (input output) --> file reading, buffer reader
* **util** (utilities)  --> ArrayList, Datastructures stuff, Collections
* **applet**  --> not recommended. try spring instead
* **awt**  --> gui related. not recommended
* **net**  --> network related. not recommended

***

#### Object class - Override

* right click inside class --> select `Generate`
* then select `override methods` --> then select method to override
* Intellij will write the override code for us

* hashcode --> is a random integer value. it takes an object, put some algorithm on it and generate integer

All methods in object class 
```java
public class A {
    @Override
    public int hashCode() {
        return super.hashCode();
    }

    @Override
    public boolean equals(Object obj) {
        return super.equals(obj);
    }

    @Override
    protected Object clone() throws CloneNotSupportedException {
        return super.clone();
    }

    @Override
    public String toString() {
        return super.toString();
    }

    @Override
    protected void finalize() throws Throwable {
        super.finalize();
    }
}
```

***

#### Overriding equals method

equals check if two objects are same

```java
package com.ag.packages.a;

public class A {
    int num;
    float marks;

    A(int num, float marks){
        this.num = num;
        this.marks = marks;
    }

    // equals check if two objects are equal
    // Override this method to check if variable 'num' of two objects are equal
    @Override
    public boolean equals(Object obj) {
        return this.num == ((A)obj).num;  // Cast obj to class A
    }


    public static void main(String[] args) {
        A obj1 = new A(12,125.5f);
        A obj2 = new A(12, 45.8f);
        System.out.println(obj1.equals(obj2));  // true
    }
}

```

***

### instanceof

* `childObject instanceof ChildClass;` --> true
* `childObject instanceof ParentClass;`  --> true
* `childObject instanceof Object;`  --> true   (Object class)

***

### To get data about class of an object

* `obj.getClass()`
* obj.getClass().getName()

```java
System.out.println(obj2.getClass());  // class com.ag.packages.a.A
System.out.println(obj2.getClass().getName());  // com.ag.packages.a.A
```

***
***

<div id="id5"></div>

### 5) Abstract Classes, Interfaces, Annotations

#### Abstract class

* If a class has abstract method, then class must also be abstract 
* For abstract classes, we cannot write object for it simply.. Need to override again
* We can have constructors in abstract class. To use this in child class, use super()
* In abstract class, `abstract constructors are not allowed`
* `static abstract methods are not allowed` (abstract are overriden, static cannot be overriden)
* `static methods are allowed in abstract class`
* `normal methods are also allowed in abstract class`
* `final abstract class is not allowed` --> because final class cannot be inherited
* a class cannot extend 2 classes --> so multiple inheritance not allowed


**_Parent Class_**  (abstract class)

```java
package com.ag.packages.a;

public abstract class Parent {
    int age;

    Parent(int age){
        this.age = age;
    }

    abstract void displayName();
    abstract void displayAge();

    // STATIC METHOD
    static void displayMessage(){
        System.out.println("This is static method in abstract class");
    }

    // NORMAL METHOD
    void displayInfo(){
        System.out.println("This is a regular method from abstract class");
    }
}
```

**_Son.java  (Child of 'Parent class')_**  

```java
package com.ag.packages.a;

public class Son extends Parent{
    Son(int age){
        super(age);
    }

    @Override
    void displayName() {
        System.out.println("Name is Mr. Ram");
    }

    @Override
    void displayAge() {
        System.out.println("Age is " + this.age);
    }
}
```

**_Daughter.java_** (Another child of Parent)

```java
package com.ag.packages.a;

public class Daughter extends Parent{
    Daughter(int age){
        super(age);
    }

    @Override
    void displayName() {
        System.out.println("Name is Mrs Radha");
    }

    @Override
    void displayAge() {
        System.out.println("Age is " + this.age);
    }

    @Override
    void displayInfo() {
        System.out.println("This is a OVERRIDDEN regular method from abstract class");
    }
}
```


**_Main method in some class_**

```java
package com.ag.packages.a;

public class A {
    public static void main(String[] args) {
        // Son Class
        Son son = new Son(12);
        son.displayName(); // Name is Mr. Ram
        son.displayAge();  // Age is 12

        // Daughter Class
        Daughter daughter = new Daughter(23);
        daughter.displayName(); // Name is Mrs Radha
        daughter.displayAge(); // Age is 23

        // Parent Class
        // To create object of Abstract class, Override methods

        Parent parent = new Parent(45) {
            @Override
            void displayName() {
                System.out.println("I am parent");
            }

            @Override
            void displayAge() {
                System.out.println("My age is " + this.age);
            }
        };

        parent.displayName();  // I am parent
        parent.displayAge();  // My age is 45

        // STATIC METHOD
        Parent.displayMessage();  // This is static method in abstract class

        // Regular method from Parent class
        son.displayInfo();  // This is a regular method from abstract class

        // Overridden regular method from 'daughter class'
        daughter.displayInfo();  // This is a OVERRIDDEN regular method from abstract class


    }
}
```

***

#### Interface

* variables in interface are static and final by default
* we cannot create objects for interfaces, so no instance variables
* a class can `implement` more than one interfaces (a class can only extend/inherit one class)
* two unrelated classes can implement same interface.. that makes it different from inheritance
* methods in interface are abstract
* interface methods has some overhead. So avoid it in performance critical situations

***

#### Interface  - Car example

 * **_Engine interface_**

```java
package com.ag.packages.b;

public interface Engine {
    int PRICE = 500000;  // this is public static by default

    void start();
    void stop();
    void accelerate();
}

```

* **_Brake interface_**

```java
package com.ag.packages.b;

public interface Brake {
    void brake();
}
```

* **_Car.java_**

```java
package com.ag.packages.b;

public class Car implements Engine, Brake{
    int a = 25;

    @Override
    public void brake() {
        System.out.println("Brakes Car");
    }

    @Override
    public void start() {
        System.out.println("Starts Car");
    }

    @Override
    public void stop() {
        System.out.println("Stops Car");
    }

    @Override
    public void accelerate() {
        System.out.println("Accelerates Car");
    }
}
```

* **_Main.java_**

```java
package com.ag.packages.b;

public class Main {
    public static void main(String[] args) {
        Car car = new Car();
        car.start();  // Starts Car
        car.stop();  // Stops Car
        car.accelerate();  // Accelerates Car
        car.brake();  // Brakes Car


        Engine car2 = new Car();
        car2.start();
        // System.out.println(car2.a);  // ERROR Cannot resolve symbol 'a'
        // Because Constructor determines which method to choose when overriding
        // and reference type decides what all are accessible
        // As Engine has no variable 'a', car2 cannot access 'a'. Hence ERROR
    }
}

```

***

#### What if two interfaces have same named methods?? - Example

* Same Engine, Brake interface as above


* **_Media interface_**

```java
package com.ag.packages.b;

public interface Media {
    void start();
    void stop();
}
```

* **_CDPlayer class_**

```java
package com.ag.packages.b;

public class CDPlayer implements Media{
    @Override
    public void start() {
        System.out.println("Starts Music");
    }

    @Override
    public void stop() {
        System.out.println("Stops Music");
    }
}
```


* **_PowerEngine class_**

```java
package com.ag.packages.b;

public class PowerEngine implements Engine{
    @Override
    public void start() {
        System.out.println("Starts Power Engine");
    }

    @Override
    public void stop() {
        System.out.println("Stops Power Engine");
    }

    @Override
    public void accelerate() {
        System.out.println("Accelerates Power Engine");
    }
}

```

* **_ElectricEngine class_**

```java
package com.ag.packages.b;

public class ElectricEngine implements Engine{
    @Override
    public void start() {
        System.out.println("Starts Electric Engine");
    }

    @Override
    public void stop() {
        System.out.println("Stops Electric Engine");
    }

    @Override
    public void accelerate() {
        System.out.println("Accelerates Electric Engine");
    }
}

```

* **_NiceCar class_**

```java
package com.ag.packages.b;

public class NiceCar {
    private Engine engine;  // private --> hides data
    private Media player = new CDPlayer();

    public NiceCar(){
        engine = new PowerEngine();
    }

    public NiceCar(Engine engine){
        this.engine = engine;
    }

    public void start(){
        engine.start();
    }

    public void stop(){
        engine.stop();
    }

    public void startMusic(){
        player.start();
    }

    public void stopMusic(){
        player.stop();
    }

    public void upgradeEngine(){
        this.engine = new ElectricEngine();
    }
}

```

* **_Main class_**

```java
package com.ag.packages.b;

public class Main {
    public static void main(String[] args) {
        NiceCar car = new NiceCar();
        car.start();  // Starts Power Engine
        car.startMusic();  // Starts Music

        car.upgradeEngine();
        car.start();  // Starts Electric Engine
        car.startMusic();  // Starts Music

    }
}
```

***

#### interface extends interface

* interface `Two` extends interface `One` works like methods of `One` in `Two`

> One.java
> 
>```java
>package com.ag.packages.c;
>
>public interface One {
>   void greetOne();
>}
>```
> 
> Two.java
> 
>```java
>package com.ag.packages.c;
>
>public interface Two extends One{
>   void greetTwo();
>}
>
>```
> 
> Main.java
> 
>```java
>package com.ag.packages.c;
>
>public class Main implements Two{
>   @Override
>   public void greetOne() {
>       System.out.println("One");
>   }
>
>    @Override
>    public void greetTwo() {
>        System.out.println("Two");
>    }
>}
>
>```
>

***


* Annotations

Annotations are internally @interface

***

#### Default interface

* If there is default interface, we can skip its implementation in class if needed
* Then that default body is used, else it is overriden by implementation in class
* not recommended usually 

```java
public interface One {
    default  void greetOne(){
        System.out.println("Default greet one");
    }
}
```

***

#### static interface

* static interface method should always have a body in interface itself
* Because static method cannot be overriden


> Interface
> 
>```java
>public interface One {
>    default  void greetOne(){
>        System.out.println("Default greet one");
>    }
>
>    static void randomStaticMethod(){
>        System.out.println("Static method in interface");
>    }
>}
>```
> 
> 
>```java
>public static void main(String[] args) {
>     One.randomStaticMethod();  // Static method in interface
>}
>```
>

***

* access modifier of interface method implementation in class should be same or better than that of method's in interface
* it should not go down( if interface method-->protected, Then implementation method should be protected or public, not private)

***

#### Nested Interface

* Top level interface must be public or default one
* But nested interface can have any.. so we are using it

```java
package com.ag.packages.c;

public class C {
    // Nested interface
    public interface NestedInterface{
        boolean isOdd(int num);
    }
}

class B implements C.NestedInterface{

    @Override
    public boolean isOdd(int num) {
        return (num & 1) == 1;
    }
}
```

```java
public static void main(String[] args) {
    B obj = new B();
    System.out.println(obj.isOdd(5));  // true
}
```

***
***

<div id="id6"></div>

### 6) Generics, Custom ArrayList, Lambda Expressions, Exception Handling, Object Cloning

#### Custom ArrayList

```java
package com.ag.packages.c;

import java.util.Arrays;

public class CustomArrayList {
    private int[] data;
    private static int DEFAULT_SIZE = 10;
    private int size = 0;

    // When first called, creates an array of default size
    public CustomArrayList(){
        this.data = new int[DEFAULT_SIZE];
    }

    public void add(int num){
        if(isFull()){
            resize();
        }
        data[size++] = num;  // first put value in index, then increment index
    }


    private boolean isFull() {
        return this.size == this.data.length;
    }


    private void resize() {
        int[] temp = new int[data.length * 2];

        // copy data elements to temp
        for (int i=0; i < data.length; i++){
            temp[i] = data[i];
        }
        data = temp;
    }

    public int remove(){
        int removed = data[--size];
        return removed;
    }

    public int get(int index){
        return data[index];
    }

    public int size(){
        return size;
    }

    public void set(int index, int value){
        data[index] = value;
    }

    @Override
    public String toString() {
        return "CustomArrayList{" +
                "data=" + Arrays.toString(data) +
                ", size=" + size +
                '}';
    }

    public static void main(String[] args) {
        CustomArrayList list = new CustomArrayList();
        for(int i=0; i < 15; i++){
            list.add(i*2);
        }
        System.out.println(list);
        //OUTPUT: CustomArrayList{data=[0, 2, 4, 6, 8, 10, 12, 14, 16, 18, 20, 22, 24, 26, 28, 0, 0, 0, 0, 0], size=15}
        // if to string not overriden we get output as --> com.ag.packages.c.CustomArrayList@4dd8dc3
    }

}

```

* Here it is done only for int
* Real ArrayList can have many datatype
* `ArrayList<Integer> list2 = new ArrayList<>();`  
* Here `<Integer>` is generics

***

#### Genrerics

**Restrictions on Generics**  -> https://docs.oracle.com/javase/tutorial/java/generics/restrictions.html

```java
// CUSTOM GENERIC ARRAYLIST

package com.ag.packages.c;

import java.util.Arrays;

public class CustomGenericArrayList<T> {
    private Object[] data;
    private static int DEFAULT_SIZE = 10;
    private int size = 0;

    // When first called, creates an array of default size
    public CustomGenericArrayList(){
        this.data = new Object[DEFAULT_SIZE];
    }

    public void add(T num){
        if(isFull()){
            resize();
        }
        data[size++] = num;  // first put value in index, then increment index
    }


    private boolean isFull() {
        return this.size == this.data.length;
    }


    private void resize() {
        Object[] temp = new Object[data.length * 2];

        // copy data elements to temp
        for (int i=0; i < data.length; i++){
            temp[i] = data[i];
        }
        data = temp;
    }

    public T remove(){
        T removed = (T)(data[--size]);  // Casting as adding bigger 'Object' to smaller T
        return removed;
    }

    public T get(int index){
        return (T)(data[index]);
    }

    public int size(){
        return size;
    }

    public void set(int index, T value){
        data[index] = value;
    }

    @Override
    public String toString() {
        return "CustomArrayList{" +
                "data=" + Arrays.toString(data) +
                ", size=" + size +
                '}';
    }

    public static void main(String[] args) {
        CustomGenericArrayList<Integer> list = new CustomGenericArrayList<>();
        for(int i=0; i < 15; i++){
            list.add(i*2);
        }
        System.out.println(list);
        // CustomArrayList{data=[0, 2, 4, 6, 8, 10, 12, 14, 16, 18, 20, 22, 24, 26, 28, null, null, null, null, null], size=15}


        CustomGenericArrayList<String> list2 = new CustomGenericArrayList<>();
        for(int i=0; i < 15; i++){
            list2.add("String_" + String.valueOf(i));
        }
        System.out.println(list2);
        // CustomArrayList{data=[String_0, String_1, String_2, String_3, String_4, String_5, String_6, String_7, String_8, String_9, String_10, String_11, String_12, String_13, String_14, null, null, null, null, null], size=15}

    }

}

```

* `T` is used here 
* But object creation time, byte code dont know what `T` is. So we used Object class
* Then type cast it to T 

***

#### Wildcards

* We can restrict the custom array list to have only a particular set of types

```java
// here T should either be Number or its subclasses
// to restrict non numbers like String from used in Custom ArrayList
public class CustomGenericArrayList<T extends Number> {
```

* By doing so, it gives error for this  --> `CustomGenericArrayList<String> list2 = new CustomGenericArrayList<>();`
* But we can use it for Numbers like int, float..



**Here we can only pass Number type**
```java
public void getList(List<Number> list){
    // do something
    // Here you can only pass Number type
}
```


**Here you can only pass Number or its subclasses**


```java
public void getList(List<? extends Number> list){
    // do something
    // Here you can only pass Number or its subclasses
}
```


***


#### Comparison Objects

* Comparable<> is an interface in java
* Interfaces can have generics

```java
package com.ag.packages.c;

public class Student implements Comparable<Student>{
    int rno;
    float marks;

    public Student(int rno, float marks){
        this.rno = rno;
        this.marks = marks;
    }

    @Override
    public int compareTo(Student o) {
        int diff = (int)(this.marks - o.marks);
        return diff;
    }


    // MAIN
    public static void main(String[] args) {
        Student student1 = new Student(12, 25.78f);
        Student student2 = new Student(27, 35.8f);

        if(student1.compareTo(student2) < 0){
            System.out.println("Student2 has more marks");  //Student2 has more marks
        }
    }
}

```


Same code can be modified to sort a list of Student objects

```java
package com.ag.packages.c;

import java.util.Arrays;

public class Student implements Comparable<Student>{
    int rno;
    float marks;

    public Student(int rno, float marks){
        this.rno = rno;
        this.marks = marks;
    }

    @Override
    public int compareTo(Student o) {
        int diff = (int)(this.marks - o.marks);
        return diff;
    }

    @Override
    public String toString() {
        return "Student{" +
                "rno=" + rno +
                ", marks=" + marks +
                '}';
    }

    // MAIN
    public static void main(String[] args) {
        Student student1 = new Student(10, 25.78f);
        Student student2 = new Student(50, 75.8f);
        Student student3 = new Student(40, 89.46f);
        Student student4 = new Student(90, 37.5f);
        Student student5 = new Student(56, 42.8f);

       Student[] list = {student1, student2, student3, student4, student5};
        Arrays.sort(list);
        System.out.println(Arrays.toString(list));
        /*
        [Student{rno=10, marks=25.78}, Student{rno=90, marks=37.5}, Student{rno=56, marks=42.8}, Student{rno=50, marks=75.8}, Student{rno=40, marks=89.46}]

         Sorted in ascending order using marks since we wrote compareto using marks
         */

    }
}

```

We can directly give it inside Arrays.sort() method

```java
public static void main(String[] args) {
    Student student1 = new Student(10, 25.78f);
    Student student2 = new Student(50, 75.8f);
    Student student3 = new Student(40, 89.46f);
    Student student4 = new Student(90, 37.5f);
    Student student5 = new Student(56, 42.8f);

   Student[] list = {student1, student2, student3, student4, student5};
    Arrays.sort(list, new Comparator<Student>() {
        @Override
        public int compare(Student o1, Student o2) {
            return (int)(o1.rno - o2.rno);
        }
    });
    System.out.println(Arrays.toString(list));
    // SORTED USING RNO
    // [Student{rno=10, marks=25.78}, Student{rno=40, marks=89.46}, Student{rno=50, marks=75.8}, Student{rno=56, marks=42.8}, Student{rno=90, marks=37.5}]
    
}
```

* In above code, use `return -(int)(o1.rno - o2.rno);`  for descending order
* Above code can be replaced with lambda function --> `Arrays.sort(list, (o1, o2) -> -(int)(o1.marks - o2.marks));`


***

#### Lambda functions

```java
ArrayList<Integer> arr = new ArrayList<>();
for (int i=0; i<5;i++){
    arr.add(i+1);
}

arr.forEach((item) -> System.out.print(item*2 + " "));  // 2 4 6 8 10 

// OR
        
Consumer<Integer> lambdaFunction =  (item) -> System.out.print(item*2 + " ");  // 2 4 6 8 10
arr.forEach(lambdaFunction);
```

**Lambda functions example with interface**

```java
package com.ag.packages.c;

public class Main{

    public static void main(String[] args) {
        Operation sum = (a,b) -> a+b;
        Operation sub = (a,b) -> a-b;
        Operation prod = (a,b) -> a*b;

        Main myCalculator = new Main();
        System.out.println(myCalculator.operate(5, 4, sum)); // 9

        System.out.println(myCalculator.operate(5, 4, prod)); // 20
        
    }

    private int operate(int a, int b, Operation op){
        return op.operation(a, b);
    }

}

interface Operation{
    int operation(int a, int b);
}

```

***

#### Exception Handling

* checked Exception --> Exception detected by compiler
* unchecked Exception  --> Compiler cannot detect.. (divide by 0)
* `Object` class child is `Throwables`. 
* `Throwables` has two child - `Exceptions` & `Error`
* Exception has 2 type - `Checked` & `Unchecked`
* `finally` is executed always. There can only be ONE finally block

```java
int a = 5;
int b = 0;
try{
    System.out.println(a/b);
}
catch (Exception e){
    System.out.println(e.getMessage());  // / by zero
}
finally {
    // Execute even if there is exception or not
    System.out.println("This will always execute");
}
```

***

**throws**

```java
public class Main{

    public static void main(String[] args) {
        int a = 5;
        int b = 0;
        try{
            divide(a, b);
        }
        catch (ArithmeticException e){
            System.out.println(e.getMessage());  // / by zero
        }
        finally {
            // Execute even if there is exception or not
            System.out.println("This will always execute");
        }
        
        /*
        Please Do not divide by 0
        This will always execute
         */
    }

    static int divide(int a, int b) throws ArithmeticException{
        if(b == 0){
            throw new ArithmeticException("Please Do not divide by 0");
        }
        return a/b;
    }

}
```

* throws  --> declaration saying this method may throw an exception
* throw  --> throw exception
***

* We can use multiple catch
* the order of catch is important as top exception is given priority
* put `Exception` at bottom only, since all other exceptions are sub of it

```java
public static void main(String[] args) {
    try{
        throw new Exception("Dummy Exception to test");
    }
    catch (ArithmeticException e){
        System.out.println(e.getMessage());  // / by zero
    }
    catch (Exception e){
        System.out.println("Regular exception");
    }
    finally {
        // Execute even if there is exception or not
        System.out.println("This will always execute");
    }

    /* OUTPUT
    Regular exception
    This will always execute
     */
    }
```

***

#### Creating Custom Exception

> MyException.java
> 
>```java
>public class MyException extends Exception{
>   public MyException(String message){
>       super(message);
>   }
>}
>```
> 
> Main Method
> 
>```java
>public static void main(String[] args) {
>    try{
>        String name = "AG";
>        if (name.equals("AG")){
>            throw new MyException("Name is AG");
>        }
>    }
>    catch (MyException e){
>        System.out.println("MyException occurred");  // MyException occurred
>        System.out.println(e.getMessage());  // Name is AG
>    }
>    catch (ArithmeticException e){
>        System.out.println(e.getMessage());  // / by zero
>    }
>    catch (Exception e){
>        System.out.println("Regular exception");
>    }
>    finally {
>        // Execute even if there is exception or not
>        System.out.println("This will always execute");
>    }
>
>    /* OUTPUT
>    MyException occurred
>    Name is AG
>    This will always execute
>     */
>}
>```

***

#### Object Cloning

_**Conventional way of creating copies of object**_

> Human.java
> 
>```java
>package com.ag.packages.c;
>
>public class Human {
>    int age;
>    String name;
>
>    public Human(int age, String name){
>        this.age = age;
>        this.name = name;
>    }
>
>    public Human(Human other){
>        this.age = other.age;
>        this.name = other.name;
>    }
>}
>```
>
>Main
> 
>```java
>public class Main{
>    public static void main(String[] args) {
>        // Creating a human and then its copy in conventional way
>        Human me = new Human(22, "AG");
>        Human myTwin = new Human(me);
>
>    }
>}
>```

***

_**Using Cloneable interface**_

>Human.java
> 
>```java
>package com.ag.packages.c;
>
>public class Human implements Cloneable{
>    int age;
>    String name;
>    int[] arr;
>
>    public Human(int age, String name){
>        this.age = age;
>        this.name = name;
>        this.arr = new int[]{ 1, 2, 3, 4, 5};
>    }
>
>    @Override
>    public Object clone() throws CloneNotSupportedException{
>        return super.clone();
>    }
>}
>```
> 
>Main.java
> 
>```java
>package com.ag.packages.c;
>
>public class Main{
>    public static void main(String[] args) throws CloneNotSupportedException {
>        // Creating a human and then its copy in conventional way
>        Human me = new Human(22, "AG");
>        Human myTwin = (Human) me.clone();
>        System.out.println(myTwin.name + " " + myTwin.age);
>
>       // SHALLOW COPY
>        System.out.println(Arrays.toString(me.arr)); // [1, 2, 3, 4, 5]
>        myTwin.arr[0] = 999;
>        System.out.println(Arrays.toString(me.arr)); // [999, 2, 3, 4, 5]
>    }
>}
>```

* `public class Human implements Cloneable` -> This tells the jvm 'Human' class is need to be cloned
* for primitive, the clone is creating new objects. For non primitive say like array & String here, it is pointing to same object
* So this clone is `shallow copy` as we make change in one object, it is reflected in the other one
* In `deep copy`, this wont happen. A new object is created and older object is copied to this new one

#### Making above shallow copy clone to  deep copy

```java
//  MODIFYING ABOVE CLONE METHOD TO MAKE IT DEEP COPY THE ARRAY

@Override
public Object clone() throws CloneNotSupportedException{
    // shallow copy
    Human twin = (Human)super.clone();

    // Deep copy
    twin.arr = new int[twin.arr.length];
    for (int i=0; i < twin.arr.length; i++){
        twin.arr[i] = this.arr[i];
    }
    return twin;
}
```

```java
public static void main(String[] args) throws CloneNotSupportedException {
    // Creating a human and then its copy in conventional way
    Human me = new Human(22, "AG");
    Human myTwin = (Human) me.clone();
    System.out.println(myTwin.name + " " + myTwin.age);

    // DEEP COPY
    System.out.println(Arrays.toString(me.arr));  // [1, 2, 3, 4, 5]
    System.out.println(Arrays.toString(myTwin.arr));  // [1, 2, 3, 4, 5]

    // CHANGING VALUE IN TWIN
    myTwin.arr[0] = 999;

    System.out.println(Arrays.toString(me.arr));  // [1, 2, 3, 4, 5]
    System.out.println(Arrays.toString(myTwin.arr));  // [999, 2, 3, 4, 5]

}
```

***
***

<div id="id7"></div>

### 7) Collections Framework, Vector Class, Enums in Java


