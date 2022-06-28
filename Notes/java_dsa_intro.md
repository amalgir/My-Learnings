# Java DSA

These are notes made for revision, after watching the Java DSA playlist of Kunal Kushwaha on youtube.

***


## Main Topics

1) [Introduction](java_dsa_intro.md)


***

## Contents

1) [Basics](#id1)
2) [Flow Chart & PseudoCodes](#id2)
3) [Java Architecture](#id3)
4) [Java Programming Basics](#id4)
5) [Conditionals & Loops in Java](#id5)


***

<div id="id1"></div>

### 1) Basics

#### Types of languages

* Procedural --> steps & procedures to complete task (Python, Java, cpp)
* Functional --> using functions.( First class functions--> `a=10 b=a` doing this with function instead of variables) (Python, not java)
* Object Oriented--> code+data=object  (python, java)

***

#### Static vs Dynamic Languages

| Static                         | Dynamic                    |
|--------------------------------|----------------------------|
| type checking at compile time  | type checking at run time  |
| Error at compile time          | Error might be at run time |
| Declare data type while coding | No need                    |
| More control                   | saves time                 |

***

#### Memory management example

`a = 10`

reference variable `a` is stored in **stack** memory and object `10` is stored in **heap** memory and `a` points to object `10`

Multiple reference variable can point to same object. And one variable changing original object changes for all ref variables (pass by value, pass by reference concept)

```java
public class Example{

    public static void main(String[] args) {
        int array_1[] = {1,2,3};
        int array_2[] = array_1;

        // Changing array 2
        array_2[0] = 99;
        // Array 1 also changes
        System.out.println(Arrays.toString(array_1));
    }
}
```

When java does garbage collection automatically, it removes all those objects with no reference variables pointing to it

***
***

<div id="id2"></div>

### 2) Flow Chart & PseudoCodes

#### Flowchart
* start/stop --> oval
* input/output --> parallelogram  (enter two numbers)
* processing --> rectangle (add to numbers)
* condition --> diamond symbol (if salary greater than 10k )

**Salary Problem Flowchart**

![Salary Problem FlowChart](/Images/JavaDSA/salary_flowchart.jpg)

**Prime Number Problem Flowchart**

![Prime Number Problem Flowchart](/Images/JavaDSA/prime_flowchart.jpg)

***

#### PseudoCodes

**Prime Number Problem Pseudocode**

![Prime Number Problem pseudocode](/Images/JavaDSA/prime_pseudocode.jpg)

**Optimized Prime Number Problem pseudocode**

![Optimized Prime Number Problem pseudocode](/Images/JavaDSA/optimizes_prime_pseudocode.jpg)

***
***

<div id="id3"></div>

### 3)  Java Architecture

![Architecture 1](/Images/JavaDSA/java_architecture_1.jpg)

#### Platform independent 
![Architecture 2](/Images/JavaDSA/java_architecture_2.jpg)

![Architecture 3](/Images/JavaDSA/java_architecture_3.jpg)

![Architecture 4](/Images/JavaDSA/java_architecture_4.jpg)

![Architecture 5](/Images/JavaDSA/java_architecture_5.jpg)

![Architecture 6](/Images/JavaDSA/java_architecture_6.jpg)

![Architecture 7](/Images/JavaDSA/java_architecture_7.png)


***
***

<div id="id4"></div>

### 4) Java Programming Basics

* Every file with .java extension is a class and that class name is the file name
* Class name starts with capital
* `javac FileName.java` --> compiles and creates `FileName.class` file. `java FileName` runs it
* main function is the entry point of a java code. no main function means code wont run
    ```java
    public class Example{
        public static void main(String[] args) {
            System.out.println("Hello");
        }
    }
  ```

* we use `static` for main function, because static function dont need its class' object to call it. If there is no static, then an object for `Example` class needs to be created first to call the function
* For ex, if Human is a class, then world population is `static` as it is same for all human objects

* To create class file in a particular place
`javac -d . Example.java` --> creates at same directory,
`javac -d .. Example.java` --> creates at one directory back of current one

* If javac or java command not found, set it in environment variables by add it to path

#### String[] args
```java
public class OtherRandom{
  public static void main(String[] args) {
    //If 'javac  OtherRandom.java'  and  'java OtherRandom "Hi" 100' in command line
    System.out.println(args[0]); // Hi
    System.out.println(args[1]); // 100
    // If no arguments given --> Index out of bounds error
  }
}
```

***

#### Scanner class for input

```java
// System.in --> gets from keyboard
Scanner scanner = new Scanner(System.in);
System.out.println(scanner.next());      
//INPUT: This is a sentence    OUTPUT: This
```

`scanner.nextLine()`  --> gets full line
`scanner.nextInt()`  --> gets next integer. Error for other types

***

#### Primitive data types

Data types that cannot be broken down again to simpler
`String` is not a primitive data type as it can be broken down again

```java
int integer = 45;
long large_integer = 1548952236654555544L;  // 8 bytes

float floating_no = 45.564f;
double large_floating_no = 755445454.254555464;

char character = 'a';
boolean bool_value = true;
```

***

#### Some Tips

```java
int amount = 45_00_000;  // 45 Lakhs
System.out.println(amount); // 4500000
```

`System.out.print("Hi")` --> no new line at its end

***

#### Type Conversion

**Automatic Type Conversion**
* types should be compatible like int and float. Cant convert between string and float
* `float num = scanner.nextInt()` --> whatever type on left should be greater than on right (float > int). vice versa gives error

**Type Casting**
```java
int num = (int)56.8756f;
System.out.println(num);  // 56
```

**Automatic Type Promotion in expression**

```java
int num = 258;
byte byte_num = (byte)num;  // byte maximum capacity is 256. So it gives 258 % 256 = 2 
System.out.println(byte_num); // 2
```

```java
byte a = 100;
byte b = 50;
System.out.println(a*b); //5000 --> here a and b are converted to int for evaluation automatically

byte c = a*b; // Gives ERROR --> a*b is automatically done as int by java.
```

* java follows unicode principles. So All languages like Hindi can be printed
```java
int num = 'A';
System.out.println(num); //65 --> ASCII value of 'A'
```

* All byte,short, char values --> promoted to int
* if any operand is long/double --> whole operation is promoted to long/double
* `int * float--> float`  `float * byte --> float` `int / char --> int` `double * short --> double` `float + int - double ---> double`

***
***

<div id="id5"></div>

### 5) Conditionals & Loops in Java