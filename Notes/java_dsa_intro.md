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

![Salary Problem FlowChart](/Images/JavaDSA/salary_flowchart.jpg)

![Prime Number Problem Flowchart](/Images/JavaDSA/prime_flowchart.jpg)

***

#### PseudoCodes

![Prime Number Problem pseudocode](/Images/JavaDSA/prime_pseudocode.jpg)

![Optimized Prime Number Problem pseudocode](/Images/JavaDSA/optimizes_prime_pseudocode.jpg)

***
***

#### 3)  Java Architecture


