# Java DSA

These are notes made for revision, after watching the Java DSA playlist of Kunal Kushwaha on youtube.

***


## Main Topics

1) [Introduction](java_dsa_intro.md)


***

## Contents

1) Basics
2) FlowChart


***

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

