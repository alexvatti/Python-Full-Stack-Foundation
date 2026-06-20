# Python Full Stack Foundation

# Week-03 – Day-12

# Functions in Python – Parameters, Arguments & Return Values

---

# Learning Objectives

By the end of this session, learners will be able to:

- Understand what a function is
- Define and call functions
- Pass data to functions using parameters
- Understand parameters and arguments
- Use positional arguments
- Use keyword arguments
- Use default arguments
- Use variable-length arguments (`*args`)
- Use keyword variable-length arguments (`**kwargs`)
- Return values from functions
- Return multiple values
- Understand local and global variables
- Write reusable functions
- Solve interview-based function programs

---

# Recap

Previously we learned:

- if, if-else, if-elif
- for Loop
- while Loop
- break
- continue
- pass

Today we will learn one of the most important topics in Python:

```
Functions
```

---

# 1. What is a Function?

## Definition

A **function** is a reusable block of code that performs a specific task.

Instead of writing the same code multiple times, we write it once inside a function and call it whenever required.

---

## Why Functions?

Without Function

```python
print("Welcome")
print("Welcome")
print("Welcome")
```

With Function

```python
def welcome():
    print("Welcome")

welcome()
welcome()
welcome()
```

Output

```
Welcome
Welcome
Welcome
```

---

## Advantages of Functions

- Code Reusability
- Reduces Duplicate Code
- Easy to Debug
- Easy to Maintain
- Improves Readability
- Modular Programming

---

# 2. Function Syntax

```python
def function_name(parameters):
    statements
    return value
```

---

## Example

```python
def greet():
    print("Hello Python")

greet()
```

Output

```
Hello Python
```

---

# 3. Function Definition vs Function Call

## Function Definition

```python
def greet():
    print("Hello")
```

Only creates the function.

---

## Function Call

```python
greet()
```

Executes the function.

---

# 4. Function with No Parameters

```python
def display():
    print("Python Full Stack")

display()
```

Output

```
Python Full Stack
```

---

# 5. Function with Parameters

Parameters receive values.

```python
def greet(name):
    print("Hello", name)

greet("Alex")
```

Output

```
Hello Alex
```

---

## Multiple Parameters

```python
def add(a, b):
    print(a + b)

add(10, 20)
```

Output

```
30
```

---

# 6. Parameters vs Arguments

| Parameter | Argument |
|-----------|----------|
| Variable in function definition | Actual value passed during function call |
| Receives data | Sends data |

Example

```python
def greet(name):      # name → Parameter
    print(name)

greet("Alex")         # Alex → Argument
```

---

# 7. Types of Arguments

Python supports four major argument types.

- Positional Arguments
- Keyword Arguments
- Default Arguments
- Variable-Length Arguments

---

# 8. Positional Arguments

Arguments are assigned according to position.

```python
def student(name, age):
    print(name)
    print(age)

student("Alex", 25)
```

Output

```
Alex
25
```

---

## Wrong Order

```python
student(25, "Alex")
```

Output

```
25
Alex
```

Position matters.

---

# 9. Keyword Arguments

Arguments are passed using parameter names.

```python
def student(name, age):
    print(name)
    print(age)

student(age=25, name="Alex")
```

Output

```
Alex
25
```

Order does not matter.

---

# 10. Positional + Keyword Arguments

```python
def employee(name, salary):
    print(name)
    print(salary)

employee("Alex", salary=50000)
```

Valid.

---

# 11. Default Arguments

Default values are used when an argument is not supplied.

```python
def greet(name="Guest"):
    print("Hello", name)

greet()

greet("Alex")
```

Output

```
Hello Guest
Hello Alex
```

---

## Multiple Default Arguments

```python
def employee(name, city="Hyderabad"):
    print(name)
    print(city)

employee("Alex")
employee("John", "Bangalore")
```

Output

```
Alex
Hyderabad

John
Bangalore
```

---

# 12. Variable-Length Arguments (*args)

Used when the number of arguments is unknown.

```python
def total(*numbers):
    print(numbers)

total(10,20)
total(10,20,30,40)
```

Output

```
(10, 20)
(10, 20, 30, 40)
```

---

## Example

```python
def total(*numbers):

    print(sum(numbers))

total(10,20)

total(10,20,30)

total(10,20,30,40)
```

Output

```
30
60
100
```

---

# 13. Keyword Variable-Length Arguments (**kwargs)

Used to accept multiple keyword arguments.

```python
def student(**details):

    print(details)

student(name="Alex", age=25, city="Hyderabad")
```

Output

```
{'name':'Alex','age':25,'city':'Hyderabad'}
```

---

## Example

```python
def employee(**data):

    for key, value in data.items():
        print(key, ":", value)

employee(name="Alex",
         age=25,
         salary=60000)
```

Output

```
name : Alex
age : 25
salary : 60000
```

---

# 14. Return Statement

A function can return a value back to the caller.

```python
def add(a, b):

    return a + b

result = add(10,20)

print(result)
```

Output

```
30
```

---

# 15. print() vs return

| print() | return |
|----------|---------|
| Displays output | Sends value back |
| Cannot reuse result | Can reuse result |
| Ends on screen | Can be stored in variable |

Example

```python
def square(n):
    return n*n

result = square(5)

print(result)
```

Output

```
25
```

---

# 16. Returning Multiple Values

Python returns multiple values as a tuple.

```python
def calculate(a, b):

    return a+b, a-b

x, y = calculate(20,10)

print(x)

print(y)
```

Output

```
30
10
```

---

# 17. Local Variables

Created inside a function.

```python
def demo():

    x = 100

    print(x)

demo()
```

Output

```
100
```

Outside the function,

```python
print(x)
```

Produces

```
NameError
```

---

# 18. Global Variables

Declared outside the function.

```python
company = "ABC"

def display():

    print(company)

display()
```

Output

```
ABC
```

---

# 19. Using global Keyword

```python
count = 0

def increment():

    global count

    count += 1

increment()

print(count)
```

Output

```
1
```

---

# 20. Real-World Examples

## GST Calculator

```python
def calculate_gst(price, gst=18):

    return price + price*gst/100

print(calculate_gst(1000))
```

---

## Salary Calculator

```python
def salary(basic, hra, da):

    return basic+hra+da

print(salary(30000,5000,2000))
```

---

## Area of Rectangle

```python
def area(length, width):

    return length*width

print(area(10,5))
```

---

# 21. Interview Practice Programs

1. Add Two Numbers
2. Find Maximum of Two Numbers
3. Find Minimum of Three Numbers
4. Check Even or Odd
5. Find Factorial (Using Loop)
6. Find Largest in List
7. Sum of List Elements
8. Reverse a String
9. Count Vowels
10. Calculator Using Functions
11. Find Square and Cube
12. Student Grade Calculator
13. GST Calculator
14. Area Calculator
15. Swap Two Numbers

---

# 22. Common Mistakes

- Forgetting parentheses while calling a function
- Forgetting the `return` statement
- Passing fewer arguments
- Passing extra arguments
- Wrong order in positional arguments
- Mixing positional arguments after keyword arguments

---

# 23. Quick Summary

| Topic | Description |
|--------|-------------|
| Function | Reusable block of code |
| Parameter | Variable in function definition |
| Argument | Value passed to function |
| Positional | Order matters |
| Keyword | Name matters |
| Default | Uses default value |
| *args | Variable positional arguments |
| **kwargs | Variable keyword arguments |
| return | Sends value back |
| Local Variable | Exists inside function |
| Global Variable | Exists outside function |

---

# 24. Homework

1. Write a function to add two numbers.
2. Write a function to calculate the square of a number.
3. Write a function to find the largest of three numbers.
4. Write a function using default arguments.
5. Write a function using keyword arguments.
6. Write a function using `*args`.
7. Write a function using `**kwargs`.
8. Write a function to return two values.
9. Write a GST Calculator.
10. Build a simple Calculator using functions.

---

# Next Session Preview

## Week-03 – Day-13

- Modules
- Import Statement
- Creating User-Defined Modules
- Python Standard Library
- `math` Module
- `random` Module
- `datetime` Module
- `os` Module
