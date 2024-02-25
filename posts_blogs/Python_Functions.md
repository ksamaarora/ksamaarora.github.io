---
layout: default
title: Python Functions
---
> ## Functions

```bash
def func_1():
    print("hello function!")
    return "heyy"

func_1()  # If only this, the return value is not returned
print(func_1().upper())  # Prints "hello function!" twice and capitalized "heyy"

```

- Function with Parameters and Default Values

```bash
def func_2(greeting, name):
    return greeting + ' Heyoo! ' + name

print(func_2('Hi', 'Sam')) # Output: Hi Heyoo! Sam
```

> ## LEGB rule: Local, Enclosing, Global, Built-in

- Global & Local variable

```bash 
x = 'global x'
def test():
    x = 'local x'
    print(x)  
test()
print(x)
```

- Built-in functions

```bash
import builtins
print(dir(builtins)) # prints list of builtins
```

- Enclosing variable

```bash
def outer():
    x = 'outer x'

    def inner():
        x = 'inner x'
        print(x)  # prints inner x

    inner()
    print(x)  # prints outer x 

outer()
```

- Nonlocal variable

```bash
def outer():
    x = 'outer x'

    def inner():
        nonlocal x  # Declares 'x' as a nonlocal variable, referring to the outer 'x'
        x = 'inner x'
        print(x)  # Prints inner x

    inner()
    print(x)  # prints inner x

outer()

```