---
layout: default
title: Python Basics
---
> ## Strings

- Print, case, count, find, replace, concatenate, format

```bash
message="Hello World"
print(message[0:5]) # 0 incl and 5 excl
print(message.upper())
print(message.count('llo'))
print(message.find('World'))
print(message.replace('World', 'Universe'))
```

> ## Integers and Floats

- Absolute, round operators

```python
print(abs(3.75))
print(round(3.75)) # returns 4
print(round(3.75, 1))  # 3.8 rounds the first digit after the decimal
```

- Concatenation and Casting

```python
num1 = '100' 
num2 = '200'
print(num1 + num2)  # returns '100200'

# Casting
num1 = int(num1) 
num2 = int(num2)
print(num1 + num2)  # returns 300
```

> ## Conditionals and Booleans 

- If, Else, and Elif Statements, Conditional operators

```bash
language = 'Java'
if language == 'python':
    print('Language is python')
elif language == 'Java':
    print('Language is Java')
else:
    print('No match')

a=[1,2,3]
b=[1,2,3]
print(a == b)
```

- Logical Operators - and, or, not

```bash
user = 'Admin'
logged_in = True

if user == 'Admin' and logged_in:
    print('Admin Page')
else:
    print('Bad Credentials')
# Output: Admin Page

if user == 'Admin' or logged_in:
    print('Admin Page')
else:
    print('Bad Credentials')
# Output: Admin Page

if not logged_in:
    print('Please Log In')
else:
    print('Welcome')
```

> ## Loops and Iterations

- For, While Loops

```bash
nums = [1, 2, 3, 4, 5, 6]

for num in nums:
    if num == 3:
        print("Found!")
        break  # Breaks out of the for loop
    elif num == 2:
        continue  # Skips to the next iteration
    print(num)

# Nested For Loop
for num in nums:
    for letter in 'abc':
        print(num, letter) # Output: 1a 1b 1c 2a 2b 2c 3a ...

# Range Function in For Loop
for i in range(1, 10):
    print(i) # Output: 1 to 9 (10 excluded)

# While Loop
x = 0
while x < 10:
    if x == 5:
        break
    print(x)
    x = x + 1 # Output: 0 to 4
```
