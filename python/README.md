# Guia de estilos en Python

PEP8 (Propuesta de Mejora de Python) Es una guia de estilos que fue adoptada por la comunidad, alli se presenta una forma en la que se puede trabajar en python, un estandar que no entra a ser obligatorio pero si altamente recomendable

## Aplicar estilos

Hay una serie de librerias que nos permiten organizar el codigo de forma automatica:

- autopep8
- black

Tambien existen librerias como pylint que sin realizar el formateo del codigo, reviza el codigo en busca de problemas que se deban mejorar y nos muestra la lista de cosas que debemos mejorar.

Pylint no solo reviza que se debe mejorar de acuerdo al PEP8 si no que nos ayuda a encontrar codigo duplicado

## Esilos

### Identacion

```python
""" YES """
def say_hello():
    print("Hello!!")

""" NO """
def say_hello():
print("Hello!!")

def say_hello():
        print("Hello!!")
```

Identacion a 4 espacios y nunca mezclar espacios y tabulador
En Python 2 se podian mezclar ambas formas de identar, en Python 3 ya no es posible

### Tamaño de linea

```python
foo = funcion_que_crea_bar(variable_1, variable2, variable_3, variable_4="", variable_5="")

income = (gross_wages + taxable_interest + (dividends - qualified_dividends) - ira_deduction)
```

The Python standard library is conservative and requires limiting lines to 79 characters (and docstrings/comments to 72).

No es recomendable

```python
foo = funcion_que_crea_bar(variable_1, variable2
                variable_3)

def long_function_name(
    var_one, var_two, var_three,
    var_four):
    print(var_one)

income = (gross_wages +
          taxable_interest +
          (dividends - qualified_dividends) -
          ira_deduction)

if gross_wages >= 0 and taxable_interest >= 0 and dividends >= 0 and qualified_dividends and ira_deduction >= 0:
    print('Ok')
```

```python
foo = funcion_que_crea_bar(
    variable_1, variable2, variable_3, variable_4="", variable_5=""
)

def long_function_name(
        var_one, var_two, var_three,
        var_four):
    print(var_one)

income = (gross_wages
          + taxable_interest
          + (dividends - qualified_dividends)
          - ira_deduction)

if (
    gross_wages >= 0
    and taxable_interest >= 0
    and dividends >= 0
    and qualified_dividends
    and ira_deduction >= 0
):
    print("Ok")
```

### Lineas en blanco

Para separar clases y funciones separar con 2 lineas en blanco, para los metodos de las clases solo una, ademas separar lineas que realizen tareas diferentes dentro de una funcion.

```python
def function():
    name = "Foo"
    say_hello_to(name)

    close()
```

### Imports

No deben haber imports de diferentes modulos en una sola linea.

```python
""" Yes """
import os
import sys
from subprocess import Popen, PIPE

""" NO """
import os, sys
```

Ademas de esto, los imports deben estar agrupados en el siguiente orden:

- Standar Library
- 3rd Party Libraries
- Local Libraries

Cada grupo separado del otro por una linea en blanco.

### Espacios en blanco en expresiones

Se deben evitar espacios extra

No recomendable

- Entre parentesis
- Sin espacio al declarar la variable
- Espacios antes de la coma

```python
payload={ 'key1' : 'value1' , 'key2' : 'value2' }
r = requests.get( "http://httpbin.org/get" , params = payload )

i=i+1
submitted +=1
x = x*2 - 1
hypot2 = x*x + y*y
c = (a+b) * (a-b)

var_1           = 1
var_2           = 2
var_3           = 3
var_3           = 3
var_4           = 4
variable_num_5  = 5
```

- Despues de las comas o puntos si es recomendable
- Use spaces around arithmetic operators

```python
payload = {'key1': 'value1', 'key2': 'value2'}
r = requests.get("http://httpbin.org/get", params=payload)

i = i + 1
submitted += 1
x = x * 2 - 1
hypot2 = x * x + y * y
c = (a + b) * (a - b)

var_1 = 1
var_2 = 2
var_3 = 3
var_3 = 3
var_4 = 4
variable_num_5 = 5
```

Don't use spaces around the = sign when used to indicate a keyword argument, or when used to indicate a default value for an unannotated function parameter.

Yes:

```python
def complex(real, imag=0.0):
    return magic(r=real, i=imag)
```

No:

```python
def complex(real, imag = 0.0):
    return magic(r = real, i = imag)
```

### Naming Conventions

#### Modules

Modules should have short, all-lowercase names.

#### Class Names

Class names should normally use the CapWords convention.

#### Function and Variable Names

Function names should be lowercase, with words separated by underscores as necessary to improve readability.

Variable names follow the same convention as function names.

#### Function and Method Arguments

Always use self for the first argument to instance methods.
Always use cls for the first argument to class methods.

#### Constants

Constants are usually defined on a module level and written in all capital letters with underscores separating words. Examples include MAX_OVERFLOW and TOTAL.

### Recomendations

Object type comparisons should always use isinstance() instead of comparing types directly.

Yes:

```python
if isinstance(obj, int):
```

No:

```python
if type(obj) is type(1):
```

==========

For sequences, (strings, lists, tuples), use the fact that empty sequences are false.

Yes:

```python
if not seq:
if seq:
```

No:

```python
if len(seq) > 0:
if len(seq) == 0:
if not len(seq):
```

[Function Annotations] <https://www.python.org/dev/peps/pep-0008/#function-annotations>
