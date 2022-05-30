# Python


## Contents

1) [Introduction](#id-1)
2) [Flow Control](#id-2)
3) [Functions](#id-3)
4) [Datatypes](#id-4)

***

<div id="id-1"></div>

## 1) Introduction

### Multi line statement

* Line continuation character (\)
```python
result = 11 + 55 + \
         44 + 8
```

* line continuation is implied inside parentheses ( ), brackets [ ], and braces { }
```python
result = (11 + 55 +
          44 + 8)
```

* semicolon
```python
a = 1; b = 2; c = 3
```

***

### Comments

* triple quotes ``` or """ for multiline comment, # for single line

```python
"""These
are
comments"""

#These
#are
#comments
```

***

### Docstrings

Used below definition of a function, class or a module

```python
def get_square(number):
    """Function to square a value"""
    return number*number

if __name__ == "__main__":
    print(get_square(6))
    print(get_square.__doc__)
```

```text
36
Function to square a value
```

***

### Literals
values of variables or constants

* #### Numerical Literal
```python
binary_literal = 0b1111
# OUTPUT 15 (print() converts binary to decimal and prints)

decimal_literal = 100
# OUTPUT 100

octal_literal = 0o11
# OUTPUT 9  (print() converts octal to decimal and prints)

hex_literal = 0xf
# OUTPUT 15 (print() converts hex to decimal and prints)

float_literal_1 = 100.5
# OUTPUT 100.5

float_literal_2 = 1.52e3
# OUTPUT 1520.0

complex_literal = 5 + 2.55j
print(complex_literal, complex_literal.real, complex_literal.imag)

# OUTPUT  (5+2.55j) 5.0 2.55
```

* #### String Literal

```python
# Special string literals

unicode_string = u"\u00dc \u00f6"
raw_string = r"RAW \n\n\n String"
```

* #### Boolean Literals

True value is 1, False value is 0

```python
a = True + 5  # value of 'a' is 6
a = False + 5 # value of 'a' is 5

a = (1==True) # value of 'a' is True
a = (1==False) # value of 'a' is False

a = (0==False) # value of 'a' is True
a = (0==True) # value of 'a' is False
```

***
***

### Data Types

- variables are instance or objects of classes ie data types

- Python numbers classes - `int`, `float`, `complex`

```python
a = 12 + 4j
print(type(a))
# Output: <class 'complex'>
print(isinstance(a, complex))
# Output: True
```

***

* #### List
Ordered, mutable

```python 
a = [1, True, "Good", 4 ,5, 6, 7]
```

```text
Indexing

a[0] returns index 0 element
a[0:2] returns index 0, 1 elements (total 2)
a[1:4] returns index 1,2,3
a[3:] returns index 3 to last

Changing a value in list
a[1] = False
```

***

* #### Tuples

```python 
a = (1, True, "Good", 4 ,5, 6, 7)
```

same indexing as list, but immutable. Ordered

***

* #### String

```python 
a = "This is a String"
```

same indexing as list, but immutable. Ordered

***

* #### Set

Has unique values. Not ordered, so indexing don't work


```python
a = {1,2,3,4,5}
```

*** 

* #### Dictionary

Key value pairs

```python
a = {
    "job": "software engineer",
    "experience": 3
}

print(a["experience"])  # prints 3
```

***

#### Conversion of datatypes

```text
float(10)
int(11.5)
str(5)
set([1,2,3])    # returns {1,2,3}
tuple({1,2,3})  # returns (1,2,3)
list("hi")      # returns ['h', 'i']

dict([["key1", "value1"], ["key2", "value2"]])
    OR
dict([("key1", "value1"), ("key2", "value2")])
```

***
***

### Type Conversion

* #### Implicit Type Conversion
    Python automatically converts one datatype to another
    
    `float + int ---> float`

***

* #### Explicit Type Conversion / Type Casting
    User converts one datatype to required one
    `<required_datatype>(expression)`

  ```python
  int("4568") # returns int 4568
  ```

***
***

### Print, Input, Import

* #### Print


`print(*objects, sep=' ', end='\n', file=sys.stdout, flush=False)`


Examples:
```python
print("Value of the variable is", 5)
# Here space is default after 'is'

print(1, 2, 3, 4, 5, 6)
# 1 2 3 4 5 6

print(1, 2, 3, 4, 5, 6, sep='--', end="&&&&")
# 1--2--3--4--5--6&&&&
```

***

* #### Output Formatting

```python
print("LANGUAGE:{}  EXPERIENCE:{}".format("Python", 3))
# LANGUAGE:Python  EXPERIENCE:3

print("No:{1} LANGUAGE:{0}  EXPERIENCE:{1}".format("Python", 3))
# No:3 LANGUAGE:Python  EXPERIENCE:3

print("LANGUAGE:{lang}  EXPERIENCE:{exp}".format(lang="Python", exp=3))
# LANGUAGE:Python  EXPERIENCE:3

x = 987.123456789
print("Value is %3.4f" % x)
# Value is 987.1235
```

***

* #### Input
```python
name = input('Enter name: ') # returns string
```

Note: `x = eval("55 + 2")` where x is int 57

***

* #### Import

```python
import math
print(math.pi)
# 3.141592653589793

from math import sqrt
print(sqrt(25))
# 5.0

import sys
print(sys.path) # list of locations where python looks for model to be imported
```

***
***

### Operators

* #### Arithmetic Operators
  `+` `-` `*` `/` 
  
  `%` modulus 

  `**` exponent  `x**y means x to the power y`

  `//` Floor division  - returns whole number adjusted to left in mumber line

***

* #### Comparison Operator

  `>` `<` `==` `!=` `>=` `<=`    returns True or False

***

* #### Logical Operators

`and` `or` `not`

***

* #### Bitwise Operator

  - `&` Bitwise AND   
  - `|` Bitwise OR
  - `~` Bitwise NOT
  - `^` Bitwise XOR
  - `|` Bitwise OR
  - `>>` Bitwise right shift
  - `<<` Bitwise left shift

```python
x = 10  # 0000 1010
y = 16  # 0001 0000

print(x & y)  # 0000 0000   decimal: 0
print(x | y)  # 0001 1010   decimal: 26
print(~y)     # 1110 1111   2's complement: 0001 0001   decimal: -17
print(x >> 2) # 0000 0010  decimal: 2
# Shifting adds 0 for new ones and deletes digit when gone
```

***

* #### Assignment Operator
 `=` `+=` `*=` `&=` `<<=`

`x<<=5`  means `x = x << 5`

***

#### Special Operators

* #### Identity Operator  `is`  `is not`

  Checks if two values are on same location
  **Special case** - list

```python
x = [1, 2]
y = [1, 2]
print(x is y)
# False

x = (1, 2)
y = (1, 2)
print(x is y)
# True

x = "Python"
y = "Python"
print(x is y)
# True
```

***

* #### Membership Operator  `in`  `not in`

  Checks if a value is in a sequence

  Sequence means a list/tuple/set/string/dictionary(for only keys)

***
***

### Namespace and Scope

* **Name (Identifier)** - a name given to object.  
`'a' is the name in a=2`
  Function is also an object. So function name is the name


* **Namespace** - collection of names. 
inside function has local namespace, so is for modules.


* **id()** - to get RAM address of an object
`id(a)` and `id(2)` are same for `a=2` expression

  ```python
  a=2
  print(id(a))
  print(id(2))
  
  # 3076934467856
  # 3076934467856
   ```


* **global** - To access global variable
  ```python
  def outer_function():
      # variable `a` in scope of function outer_function
      a = 100
  
      def inner_function():
          global a
          # changes value of  `a` outside outer_function.
          a = 200
  ```

***
***
***
***

<div id="id-2"></div>

## 2) Flow Control

###  Loops

* #### if else
`None` `0` --> False

`non-zero number` --> True

```text
if test expression:
    Body of if
elif test expression:
    Body of elif1
elif test expression:
    Body of elif2
else: 
    Body of else
```

***

* #### for Loop

```python
x = [2, 4, 6, 8, 10]
# to print all values in x

for i in range(len(x)):
    print(x[i])
else:
    print("All items printed")

# OR

for j in x:
    print(j)
else:
    print("All items printed")
```
**Note:** a for loop's else part runs if no break occurs

**Note:** range(start, stop, step_size)  default stepsize is 1

**Note:** range does not generate all at once, for that use `list(range(10))`

***

* #### while loop

```text
while test_expression:
    Body of while
```

```python
x = 10
while x > 5:
    print(x)
    x -= 1

'''OUTPUT
10
9
8
7
6'''

```

**Note:** Loop stops when test_expression becomes False

**Note:** similar to for loop, while also has optional `else`, which runs if no break occurs

***

* #### Break, Continue

`break` stops loop. If it is in inner loop it exits inner loop only.
`continue` stops current iteration of loop only. Loop continues with next iteration

***
***

### pass

`pass`  Nothing happens when its executed. no operation (NOP)

```python
# can be used with function, class or anywhere
def some_function():
    pass
```

***
***
***
***

<div id="id-3"></div>

## 3) Functions

### Basics

```python
def function_name(parameters):
	"""docstring"""
	statement(s)
```

```python
def get_cube(number):
    """
    This function returns the
    cube of the number passed
    in as a parameter
    """
    return number * number * number


print(get_cube(5))
# Output 125
```

**Note**  `return` default is None.

***
***

### Arguments

* #### Default Arguments
  `def show_details(state, language="English"):`

***

* #### Keyword Argument
  Argument position we can change using keyword argument in function call

  `show_details(language="Hindi", state="UP")`   

***

* #### Arbitrary Argument
Used when number of parameters are unknown, becomes tuple of arguments

```python
def show_details(*states):
    print(states)

show_details("Kerala", "Tamil Nadu", "UP")
# Output: ('Kerala', 'Tamil Nadu', 'UP')

show_details("California")
# Output: ('California',)
```

***
***

### Recursion / Recursive function

Process of defining something in terms of itself

```python
def factorial(number):
    if number == 1:
        return 1
    else:
        return number*factorial(number-1)

print(factorial(5))  # 5*4*3*2*1 = 120
```

**Note**: Recursive function must have a **Base Condition**. Here Base Condition is to stop the function when it reaches 1

***
***

### Anonymous Function / Lambda Function

```
lambda arguments: expression
```

* #### Lambda function
  Function with no name. Multiple arguments possible. Only one expression
  ```python
  cube = lambda x: x*x*x
  print(cube(5))  # 125
  ```
  
***

* #### filter and map builtin functions

`filter` and `map` has two arguments - a function and a sequence/iterable

filter takes each value from sequence and put it in function and checks if function returns True. If True, then that value is returned

map is similar to filter, except it returns the item returned by the function. not the input value itself from sequence

```python
number_list = [1, 2, 3, 4, 5, 6, 7]
even_numbers = list(filter(lambda x: (x % 2 == 0), number_list))
print(even_numbers)  # [2, 4, 6]

cube_numbers = list(map(lambda x: x*x*x, number_list))
print(cube_numbers)  # [1, 8, 27, 64, 125, 216, 343]
```

***
***

### Global, Local and Nonlocal Variables

We can access global variable inside local scope ie inside a function
But we cannot change it. For that specify it as `global`

`nonlocal` is used in nested functions to tell a variable is not local to that function

```python
def outer():
    x = "outer variable"

    def inner():
        nonlocal x
        x = "inner variable"
        print("Inner: {}".format(x))  # Inner: inner variable

    inner()
    print("Outer: {}".format(x))  # Outer: inner variable

outer()
```

Global can be used to make global variables without declaring one outside, though not recommended practice

```python
def outer():
    x = "edit 1"

    def inner():
        global x
        x = "edit 2"

    inner()
    print("x in outer() after calling inner(): {}".format(x))
    # prints 'edit 1' as this x is not global one but one in local scope of outer


outer()
print("x in global scope: {}".format(x))
# prints 'edit 2' 
```

***
***

### Modules

Module ---> a python file

* Importing a builtin module with different user defined name
```python
import pandas as pd  
df = pd.DataFrame()
```

* Importing all names from a module
```python
from math import *
```

* Interpreter imports only once for multiple imports. To reload already imported module,

```python
import imp

import user_made_module
imp.reload(user_made_module) # imports it again
```

* Use `dir()` to get all names in a module 
```python
dir(user_made_module)
```

using just `dir()` only gives names of current namespace as a list

***
***

### Packages

Package --> directory with a `__init__.py` file (Group of modules/python files)

```python
# If 'Animal' is a package, 'Mammal' is a sub package and 'characteristics' is a module
from Animal.Mammal import characteristics
characteristics.get_sound("Elephant")
```

***
***
***
***

<div id="id-4"></div>

## 4) Datatypes

### Some important modules for numbers

* #### Decimal

used for more precision

```python
from decimal import Decimal

print(2.1 * 3.25)  # 6.825
print(Decimal(2.1) * Decimal(3.25))  # 6.825000000000000288657986403
print(Decimal('2.1') * Decimal('3.25'))  # 6.825  Preferred way
```

***

* #### Fraction

```python
from fractions import Fraction

print(Fraction(1.3))     # 5854679515581645/4503599627370496
print(Fraction('1.3'))   # 13/10  Preferred
print(Fraction(11, 10))  # 11/10
print(Fraction(-3, 10))  # -3/10
```

***

* #### Math

```python
import math


print(math.sin(math.pi))  # 1.2246467991473532e-16
print(math.exp(10))       # 22026.465794806718
print(math.factorial(5))  # 120
print(math.sinh(1))       # 1.1752011936438014
print(math.log10(10000))  # 4.0
```

***

* #### random

```python
import random

print(random.random())           # 0.884265406004155  
print(random.randrange(10, 18))  # 17 (random b/w 10 & 18)

x = ["a", "b", "c", "d", "e", "f", "g", "h"]
print(random.choice(x))  # e

random.shuffle(x)
print(x)  # ['d', 'e', 'h', 'g', 'b', 'f', 'c', 'a']
```

***
***

### List

* #### Empty list `x = []`
* #### Mixed datatype `x = [10, "Hi", True]`
* #### Nested List  `x = ["hi", [10, 20, 30], ["How", "are", "you"]]`
* #### List index  `x[0] --> first item` `x[-1] --> last item` `x[-2] --> second last item`
* #### List slicing 
  ```python
  x = [0, 1, 2, 3, 4, 5, 6]
  
  print(x[2:4])   # [2, 3]  start index is inclusive, end index is exclusive
  print(x[2:])    # [2, 3, 4, 5, 6]
  print(x[:4])    # [0, 1, 2, 3]
  print(x[:])     # [0, 1, 2, 3, 4, 5, 6]
  ```
