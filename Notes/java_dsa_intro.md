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
6) [Switch & Nested case](#id6)
7) [Functions / Methods ](#id7)
8) [Arrays & ArrayList](#id8)


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

#### if else if

```java
if (num > 5){
    num-=1;
}
else if (num<5){
    num+=1;
}
else{
    num = 0;
}
```

***

#### for loop

```java
for(int num=0; num<10; num++){
    System.out.print(num + " ");  // 0 1 2 3 4 5 6 7 8 9 
}
```

***

#### while loop

```java
int num = 0;  // initialization
while(num<10){  // condition
    System.out.print(num + " ");  // 0 1 2 3 4 5 6 7 8 9 
    num+=1; // update
}
```

use for loop when total iteration count is known ,else use while loop

***

#### do while

```java
do{
    System.out.println("Will run this body ATLEAST once");
}
while (num>3);
```

***

#### Math.max

```java
// To find largest of 3 numbers
int a=10, b=20, c=30;
int max = Math.max(c, (Math.max(a,b)));
```

***

#### To find the case of a character

```java
// To find case of a character
Scanner input = new Scanner(System.in);
char ch = input.next().trim().charAt(0);  // trim() removes all spaces from start and end in the string
if( ch>='A' && ch<='Z'){
    System.out.println("UPPER CASE");
}
else{
    System.out.println("LOWER CASE");
}
```

* `trim` removes trailing spaces
  ```java
  String str = "   Hello Dear          ";
  System.out.println(str.trim());  // "Hello Dear"
  ```
  
* `charAt(index)`  gives character at that index of a string
* `if( ch>='A' && ch<='Z')`  comparison of characters using ASCII

***

#### To count occurrence of a particular digit

```java
int n = 8575787;
int ref_num = 7;
int count = 0;

while (n > 0){
    int rem = n % 10;  // TO GET LAST DIGIT
    if (rem == ref_num) {
        count++;
    }
    n /= 10;  // TO REMOVE LAST DIGIT
}
System.out.println(count);
```

*** 

#### To reverse a integer number
LOGIC: To reverse 745 --> 547
* ans = 5
* ans = 5*10 + 4 = 54
* ans = 54*10 + 7 = 547

```java
int n = 123456789;
int ans =0;

while (n > 0){
    int rem = n % 10;  // TO GET LAST DIGIT
    n /= 10;  // TO REMOVE LAST DIGIT
    ans = ans *10 + rem;  // TO REVERSE THE GIVEN INTEGER
}
System.out.println(ans);  // 987654321
```

***

<div id="id6"></div>

### 6) Switch & Nested case

* for String comparison use equals `animal.equals("tiger")` not `==` as `==` checks if both are same objects only. There is a possibility of having same string value in two different objects

#### switch

```java
String state = "India";

switch(state){
    case "India":
        System.out.println("New Delhi");
        break;
    case "UK":
        System.out.println("London");
        break;
    default:
        System.out.println("Invalid state");
}
```

#### enhanced switch

```java
String state = "India";

switch (state) {
    case "India" -> System.out.println("New Delhi");
    case "UK" -> System.out.println("London");
    default -> System.out.println("Invalid state");
}
```

#### same body for multiple cases

```java
int day = 5;

switch (day) {
    case 1:
    case 2:
    case 3:
    case 4:
    case 5:
        System.out.println("Working Day");
        break;
    case 6:
    case 7:
        System.out.println("Holiday");
        break;
    default:
        System.out.println("Invalid");
}
```

OR

```java
int day = 7;

switch (day) {
    case 1, 2, 3, 4, 5 -> System.out.println("Working Day");
    case 6, 7 -> System.out.println("Holiday");
    default -> System.out.println("Invalid");
}
```

* Try to use enhanced switch always
* we can use a switch inside case of another switch --> Nested switch

***
***

<div id="id7"></div>

### 7) Functions / Methods 

* There is no pass by reference in java. - Only pass by value
* pass by value --> when we pass a variable as argument in method, only a copy of its value is passed to that argument variable. So changing that variable wont change the value of the outside variable

This creates a problem in swap method

**pass by value for primitive data type argument**

```java
public class Example{
    public static void main(String[] args) {
        int a = 10;
        int b = 20;
        swap(a, b);
        System.out.println("Outside swap Method:  a-->" + a + "  b-->" + b);  // 10 , 20  SWAP FAILED
    }

    private static void swap(int a, int b) {  // Only static method can be called inside a static method
        int temp = a;
        a = b;
        b = temp;
        System.out.println("Inside swap Method:  a-->" + a + "  b-->" + b);   // 20, 10  SWAP DONE
    }
}
```

***

**For objects, complex datatypes --> pass by value of that reference variable, so original object changes**

```java
public class Example{
    public static void main(String[] args) {
        int[] array = {0, 1, 2, 3, 4, 5};
        modifyArray(array);  // CHANGES ORIGINAL ARRAY VALUES
        System.out.println(Arrays.toString(array));  // [9999, 1, 2, 3, 4, 5]
    }

    private static void modifyArray(int[] arr) {
        arr[0] = 9999;
        // arr = {1, 2, 3};   ERROR: Array initializer is not allowed here
    }
}
```

* Here object aka array value is modified only, not able to initialize
* Not applicable to string as string is immutable, we cannot modify string

***

* Cannot initialize same variable multiple times in same scope
* Values initialized in block remain in the block

#### BLOCK SCOPE

```java
public static void main(String[] args) {
   int a = 22;
   
   // BLOCK SCOPE
    {
    //  int a =77;  Already initialized outside the block in same method, So cannot initialize again
        a = 77;  // But the original ref variable can be MODIFIED
        int b = 33;  // this variable created here is accessible only inside this block
    }

    System.out.println(a);  // 77
    // System.out.println(b);  // ERROR Cannot resolve symbol 'b'

}
```

* Any variable outside scope (block or loop) but in same method which is already initialized are available inside block, cannot be initialized again
* Any new variable initialized inside these scopes are not available outside the scope


#### Shadowing

Shadowing is the practice of using two variables with same name within scopes that overlaps


```java
public class Example{
    static int a = 77;  // CLASS VARIABLE

    public static void main(String[] args) {
        System.out.println(a);  // 77
        int a;  // CLASS VARIABLE is shadowed by this
        //System.out.println(a);  // ERROR --> Variable 'a' might not have been initialized (scope will begin when value is initialized)
        a = 88;
        System.out.println(a);  // 88
        display();  // 77
    }

    private static void display() {
        System.out.println(a);
    }
}
```

***

#### Variable length arguments (Varargs)

```java
public static void main(String[] args) {
    display(11, "Hi", 4, 5, 6, 7, 8, 9, 0);

}

private static void display(int a, String b, int ...c) {
    System.out.println(a);  // 11
    System.out.println(b); // Hi
    System.out.println(Arrays.toString(c));  // [4, 5, 6, 7, 8, 9, 0]

}
```

* in arguments, varargs should be the last one
* varargs is internally stored as an array
* varargs can contain any number of arguments

**Function overloading** 

* Same name functions with different arguments
* Happens at compile time
* Either number of arguments or type of argument should be different
* ambiguity error occurs when compiler cant decide which method is called. happens when we give no arguments and didnt created a method with empty arguments


`static void display(int a)` `static void display(String a)` `static void display(int a, int b)`

***

#### PRIME Problem Using Method

```java
public class Example{
    
    public static void main(String[] args) {
        int a = 17;
        boolean ans = isPrime(a);
        System.out.println(ans);
    }

    private static boolean isPrime(int num) {
        if (num <=1){
            return false;
        }
        int c = 2;
        while (c * c <= num){
            if (num % c == 0){
                return false;
            }
            c++;
        }
        return c * c > num;
    }
}
```

***

#### ARMSTRONG NUMBER

153 is Armstrong number

`153 = cube(1) + cube(5) + cube(3) = 1 + 125 + 27 = 153`

**Problem to get all 3 digit armstrong numbers**

```java
public class Example{

    public static void main(String[] args) {
        for (int i=100; i<1000; i++){
            if (isArmstrong(i)){
                System.out.print(i + " ");  // 153 370 371 407 
            }
        }

    }

    private static boolean isArmstrong(int num) {
        int original = num;
        int sum = 0;
        while(num>0){
            int rem = num % 10;
            sum += (rem*rem*rem);
            num /= 10;
        }
        return sum == original;
    }
}
```

***
***

<div id="id8"></div>

### 8) Arrays & ArrayList

`int[] arr = new int[5];`  

`int[] arr = {11, 22, 33, 44, 55};`

```java
int[] arr; // Declaration of array --> `arr` is getting defines in the `STACK`
arr = new int[5];  // Initialization --> Object is actually created here in the memory (HEAP)
```

* In cpp,c  array memory allocation is continuous. (memory cells are together)
* In Java, it is not continuous
* In Java, array objects are in heap and heap objects are not continuous
* So in Java, array may not be continuous internally - depends on jvm
* `new` is used to create an object

***

#### null

* null is like a special literal.
* can assign it only to non primitive data type variable  `String str = null;`
* default value for a String array is null, default of int array is 0
* 
```java
String[] str = new String[2];

System.out.println(str[0]); // null
System.out.println(str[1]); // null
System.out.println(str[2]);  // ERROR -> INDEX OUT OF BOND
```

***

#### enhanced for loop

SYNTAX: --> `for (datatype ref_variable: array)`

```java
int[] arr = {1, 2, 3, 4, 5};
System.out.println(arr.length); // 5

for (int i : arr){
    System.out.print(i + " ");  // 1 2 3 4 5
}
```

Converting arrays to string --> `System.out.println(Arrays.toString(arr));`

***

#### 2D Array

row count is must, column count is optional

```java
/*
1 2 3 4 5
1 2
1 2 3
 */

int[][] arr = {
        {1, 2, 3, 4, 5},
        {1, 2},
        {1, 2, 3}
};

System.out.println(Arrays.toString(arr)); // [[I@4dd8dc3, [I@6d03e736, [I@568db2f2]
System.out.println(Arrays.toString(arr[1]));  // [1, 2]
```

```java
int[][] arr = new int[2][];
arr = new int[][]{
        {1, 2},
        {3, 4, 5, 6}
};
```

#### Display 2D Array

```java
static void display2DArray(int[][] arr){
    for(int row=0; row < arr.length; row++){
        for(int col=0; col < arr[row].length; col++){
            System.out.print(arr[row][col] + " ");  // prints all elements in a row
        }
        System.out.println();  // new line after each row
    }
}
```

OR (using enhanced for)

```java
static void display2DArray(int[][] arr){
    for( int[] row: arr){
        for(int col: row){
            System.out.print(col + " ");
        }
        System.out.println();
    }
}
```

***

#### ArrayList

`ArrayList<Integer> list = new ArrayList<Integer>(5);`  initial capacity number here is optional

Wrapper class is used, primitive datatype cannot be used

```java
ArrayList<Integer> list = new ArrayList<Integer>(5);  // We can add more than 5; no problem 
list.add(25);
list.add(45);
System.out.println(list); // [25, 45]
```

`boolean ans = list.contains(25);`

**Update list**

```java
list.set(0, 100);
System.out.println(list); // [100, 45]
```

**Get Item**

if list is int ArrayList --> `int firstElement = list.get(0);`

#### Internal working

* Size is fixed internally
* When array list is filled to some extent, it will create a new arraylist with say double the current size
* Then the old list data is copied to the new list and then old list is deleted

***

#### 2D ArrayList
```java
public class Example{

    public static void main(String[] args) {
        Scanner input = new Scanner(System.in);
        ArrayList<ArrayList<Integer>> list = new ArrayList<>();

        // INITIALIZATION
        for(int i=0;i<3;i++){
            list.add(new ArrayList<>());
        }

        // ADDING ELEMENTS
        for(int i=0; i<3; i++){
            for(int j=0; j<3; j++){
                list.get(i).add(input.nextInt());  // INPUT <-- 1 2 3 4 5 6 7 8 9
            }
        }

        // DISPLAY
        System.out.println(list); // [[1, 2, 3], [4, 5, 6], [7, 8, 9]]

    }
}
```

***

* edge cases - like what if array/input is null or full...like that --> Handle it
* swap method can be easily created using array --> like swapping index 1 and index3
* finding largest number in an array --> assume first one as max, then compare with other elements. If other one is large put it in max
* Reverse array --> if swap method is already written, then use swap to swap start and end elements, then start++, end-- in a while loop with condition start < end

***
***
