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

