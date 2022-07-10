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