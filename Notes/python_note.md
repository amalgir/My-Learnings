# Python


## Contents

1) [Introduction](#id-1)

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