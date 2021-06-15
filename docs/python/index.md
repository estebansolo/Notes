# Style guide in Python

PEP (Python Enhancement Proposals) are different proposals designed to improve the python code. PEP8 is a style guide that was adopted by the community where standards for the code are defined. It is not mandatory but highly recommended.

## Usage

There are different libraries that allow us to format the code automatically:

- autopep8
- black
- yapf

There are also libraries such as pylint that without formatting the code, reviews the code and generates a report with the problems found.

Pylint not only checks that must be improved according to the PEP8 but also helps us find duplicate code.

## Guide

### Indentation

  - Indentation to 4 spaces
  - Never mix spaces and tabulator

In Python 2 it was possible to mix both forms, in Python 3 it is no longer possible.

No:

```python
def say_hello():
print("Hello!!")

def say_hello():
        print("Hello!!")
```

Yes:

```python
def say_hello():
    print("Hello!!")
```

### Line Size

The Python standard library is conservative and requires limiting lines to 79 characters (and docstrings/comments to 72).

```python
foo = long_function_name(variable_1, variable2, variable_3, variable_4="", variable_5="")

income = (gross_wages + taxable_interest + (dividends - qualified_dividends) - ira_deduction)
```

No:

```python
foo = long_function_name(variable_1, variable2
                variable_3)
```

Yes:

```python
foo = long_function_name(
    variable_1, variable2, variable_3, variable_4="", variable_5=""
)
```

No:

```python
def long_function_name(
    var_one, var_two, var_three,
    var_four):
    print(var_one)
```

Yes:

```python
def long_function_name(
        var_one, var_two, var_three,
        var_four):
    print(var_one)
```

No:

```python
income = (gross_wages +
          taxable_interest +
          (dividends - qualified_dividends) -
          ira_deduction)
```

Yes:

```python
income = (gross_wages
          + taxable_interest
          + (dividends - qualified_dividends)
          - ira_deduction)
```

No:


```python
if gross_wages >= 0 and taxable_interest >= 0 and dividends >= 0 and qualified_dividends and ira_deduction >= 0:
    print('Ok')
```

Yes:

```python
if (
    gross_wages >= 0
    and taxable_interest >= 0
    and dividends >= 0
    and qualified_dividends
    and ira_deduction >= 0
):
    print("Ok")
```

### Blank Lines

To separate classes and functions must be done with 2 blank lines, for the methods of classes only one, also separate lines that perform different tasks within a function.

No:

```python
def function_one():
    name = "Foo"
    say_hello_to(name)
def function_two():
    name = "Foo"
    say_hello_to(name)
```

Yes:

```python
def function_one():
    name = "Foo"
    say_hello_to(name)
    
    
def function_two():
    name = "Foo"
    say_hello_to(name)
```

### Imports

There should be no imports of different modules in a single line. In addition to this, imports should be grouped in the following order:

- Standar Library
- 3rd Party Libraries
- Local Libraries

Each group separated from the other by a blank line.

No:

```python
from my_module import area # Local
import os, sys # Standar
import pymongo # 3rd
from subprocess import Popen, PIPE # Standar
```

Yes:

```python
import os
import sys
from subprocess import Popen, PIPE

import pymongo

from my_module import area
```

### Blank spaces in expressions

Extra spaces should be avoided

No:

```python
var_1           = 1
var_2           = 2
var_3           = 3
var_3           = 3
var_4           = 4
variable_num_5  = 5
```

Yes:

```python
var_1 = 1
var_2 = 2
var_3 = 3
var_3 = 3
var_4 = 4
variable_num_5 = 5
```

- Spaces between parentesis
- Spaces before commas

No:

```python
payload={ 'key1' : 'value1' , 'key2' : 'value2' }
r = requests.get( "http://httpbin.org/get" , params = payload )
```

Yes:

```python
payload = {'key1': 'value1', 'key2': 'value2'}
r = requests.get("http://httpbin.org/get", params=payload)
```

 - No spaces when declaring the variable
 - Do not use spaces around arithmetic operators


No:

```python
i=i+1
submitted +=1
x = x*2 - 1
hypot2 = x*x + y*y
c = (a+b) * (a-b)
```

Yes:

```python
i = i + 1
submitted += 1
x = x * 2 - 1
hypot2 = x * x + y * y
c = (a + b) * (a - b)
```

  - Do not use spaces around the = sign when indicating a keyword argument, or when used to indicate a default value for an unannotated function parameter.

No:

```python
def complex(real, imag = 0.0):
    return magic(r = real, i = imag)
```

Yes:

```python
def complex(real, imag=0.0):
    return magic(r=real, i=imag)
```

### Naming Conventions

#### Modules

Modules should have short, all-lowercase names.

```python
my_module
```

#### Class Names

Class names should normally use the ***CapWords*** convention.

```python
class MyClass:
```

#### Function and Variable Names

Function names should be lowercase, with words separated by underscores as necessary to improve readability.

Variable names follow the same convention as function names.

```python
def my_function():
```

#### Function and Method Arguments

Always use self for the first argument to instance methods.
Always use cls for the first argument to class methods.

```python
def my_function(self, first_var, second_var):
```

#### Constants

Constants are usually defined on a module level and written in all capital letters with underscores separating words. Examples include MAX_OVERFLOW and TOTAL.

```python
DB_HOST = ""
DB_PORT = ""
```

### Recomendations

1. Object type comparisons should always use `isinstance()` instead of comparing types directly.

No:

```python
if type(obj) is int:
```

Yes:

```python
if isinstance(obj, int):
```

2. For sequences, (strings, lists, tuples), use the fact that empty sequences are false.

No:

```python
if len(seq) > 0:
if len(seq) == 0:
if not len(seq):
if string != "":
```

Yes:

```python
if seq:
if not seq:
if string:
```


<hr />
  
  - PEP 3101 -- Advanced String Formatting
  - PEP 498 -- Literal String Interpolation
  - [Pyformat]

In Python source code, an f-string is a literal string, prefixed with 'f', which contains expressions inside braces. The expressions are replaced with their values.

```python
name = 'Fred'
age = 50
print(f'My name is {name}, my age next year is {age+1}.')

'My name is Fred, my age next year is 51.'
```

```python
"The story of {0}, {1}, and {c}".format(a, b, c=d)

f"The story of {a}, {b}, and {d}"
```  

```python
"{:.0f}".format(3.99) # 4

"{:.2f}".format(3.1416) # 3.14

"{:03d}".format(1) # 001

"{:03d}".format(41) # 041

"{:b}".format(145) # 10010001

"*{0:40}*".format("Hello World")
# *Hello World                             *

"*{0:>40}*".format("Hello World")
# *                             Hello World*

"{:*^20s}".format("Hello World")
# ****Hello World*****
```

[Function Annotations]: <https://www.python.org/dev/peps/pep-0008/#function-annotations>
[Pyformat]: <https://pyformat.info/>
[Type Methods in Python]: <https://blog.nearsoftjobs.com/tipos-de-m%C3%A9todos-en-python-cls-vs-self-d6da1e08efa8>