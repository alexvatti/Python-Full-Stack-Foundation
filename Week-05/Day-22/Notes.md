# Python Full Stack Foundation

# Week-05 – Day-22

# Object-Oriented Programming (OOP)

## Methods, self, Constructors and Instance Variables

---

# Learning Objectives

By the end of this session, you will be able to:

- Understand Methods
- Understand why methods are required
- Explain the self keyword
- Create Constructors using __init__()
- Initialize Objects
- Understand Instance Variables
- Differentiate Local and Instance Variables
- Create Object Methods
- Pass Arguments to Methods
- Build simple real-world classes using constructors

---

# Recap

Yesterday we learned

- Object-Oriented Programming
- Classes
- Objects
- Attributes
- Creating Multiple Objects

Example

```python
class Student:
    pass

s1 = Student()

s1.name = "Alex"
s1.age = 22
```

Although this works, it has one major problem.

Every time we create an object, we have to manually assign attributes.

```python
s1.name = "Alex"
s1.age = 22

s2.name = "John"
s2.age = 21

s3.name = "David"
s3.age = 20
```

Imagine creating 10,000 students.

This is repetitive and error-prone.

---

# Why Do We Need Methods?

Objects are not just data.

They also perform actions.

Example

A Car

Data

- Brand
- Colour
- Speed

Behaviour

- Start()
- Stop()
- Accelerate()

A Student

Data

- Name
- Marks

Behaviour

- Study()
- WriteExam()
- DisplayDetails()

Without methods, an object only stores information.

Methods give objects behaviour.

---

# What is a Method?

## Definition

A Method is a function defined inside a class.

Methods describe what an object can do.

General Syntax

```python
class ClassName:

    def method_name(self):
        pass
```

---

# Example

```python
class Student:

    def study(self):
        print("Student is studying")
```

Creating an object

```python
s = Student()

s.study()
```

Output

```
Student is studying
```

---

# Methods vs Functions

Function

```python
def greet():
    print("Hello")
```

Calling

```python
greet()
```

Method

```python
class Student:

    def greet(self):
        print("Hello")
```

Calling

```python
s = Student()

s.greet()
```

Difference

Functions belong to a module.

Methods belong to an object.

---

# Understanding self

One of the most important concepts in Python OOP.

Every instance method has

```python
self
```

Example

```python
class Student:

    def display(self):
        print("Hello")
```

Notice

```python
self
```

Why?

Because Python needs to know **which object is calling the method**.

---

# Real Example

Imagine three students.

```
Student

↓

Alex

↓

John

↓

David
```

Each student has different information.

When Alex calls

```
display()
```

Python automatically sends

```
Alex
```

as self.

When John calls

```
display()
```

Python sends

```
John
```

as self.

---

# Behind the Scenes

You write

```python
s.display()
```

Python internally does

```python
Student.display(s)
```

The object becomes the first argument.

That argument is named

```
self
```

---

# Example

```python
class Student:

    def show(self):
        print(self)
```

```python
s = Student()

s.show()
```

Output

```
<__main__.Student object at ...>
```

self refers to the current object.

---

# Example

```python
class Student:

    def display(self):
        print("Current Object :", self)

s1 = Student()
s2 = Student()

s1.display()
s2.display()
```

Notice

Different objects produce different memory addresses.

---

# Why self is Needed

Without self

```python
class Student:

    def display():
        print("Hello")
```

Calling

```python
s = Student()

s.display()
```

Produces

```
TypeError
```

Python automatically passes the object.

Therefore every instance method needs self.

---

# Accessing Attributes using self

Example

```python
class Student:

    def display(self):

        print(self.name)
```

Creating object

```python
s = Student()

s.name = "Alex"

s.display()
```

Output

```
Alex
```

---

# Example

```python
class Employee:

    def display(self):

        print(self.name)
        print(self.salary)

e = Employee()

e.name = "Ravi"
e.salary = 55000

e.display()
```

Output

```
Ravi

55000
```

---

# The Problem

Suppose we forget to assign

```python
name
```

```python
s = Student()

s.display()
```

Python raises

```
AttributeError
```

Solution

Use Constructors.

---

# Constructors

## Definition

A Constructor is a special method that automatically executes whenever an object is created.

Python constructor

```python
__init__()
```

---

# Why Constructors?

Without constructor

```python
s = Student()

s.name = "Alex"

s.age = 22
```

With constructor

```python
s = Student("Alex",22)
```

Much cleaner.

---

# Constructor Syntax

```python
class Student:

    def __init__(self):

        print("Constructor Executed")
```

Object Creation

```python
s = Student()
```

Output

```
Constructor Executed
```

Notice

No method call is required.

The constructor executes automatically.

---

# Constructor with Parameters

```python
class Student:

    def __init__(self,name):

        self.name = name
```

Creating object

```python
s = Student("Alex")

print(s.name)
```

Output

```
Alex
```

---

# Multiple Parameters

```python
class Student:

    def __init__(self,roll,name,marks):

        self.roll = roll
        self.name = name
        self.marks = marks
```

Creating object

```python
s = Student(101,"Alex",95)

print(s.roll)
print(s.name)
print(s.marks)
```

---

# Understanding self.name = name

This line confuses many beginners.

Example

```python
self.name = name
```

Left Side

```
self.name
```

Attribute inside the object.

Right Side

```
name
```

Parameter received from the constructor.

Memory

```
Parameter

↓

name

↓

"Alex"

↓

self.name

↓

Stored inside object
```

---

# Instance Variables

Definition

Variables that belong to an object are called Instance Variables.

Example

```python
class Student:

    def __init__(self,name):

        self.name = name
```

```
self.name
```

is an Instance Variable.

Every object has its own copy.

---

# Example

```python
class Student:

    def __init__(self,name):

        self.name = name

s1 = Student("Alex")
s2 = Student("John")

print(s1.name)
print(s2.name)
```

Output

```
Alex

John
```

Each object stores different values.

---

# Local Variable vs Instance Variable

```python
class Student:

    def display(self):

        marks = 90

        self.name = "Alex"
```

Local Variable

```
marks
```

Exists only during method execution.

Instance Variable

```
self.name
```

Exists as long as the object exists.

---

# Object Methods

Example

```python
class Student:

    def __init__(self,name,marks):

        self.name = name
        self.marks = marks

    def display(self):

        print(self.name)
        print(self.marks)
```

Creating object

```python
s = Student("Alex",95)

s.display()
```

---

# Passing Arguments to Methods

```python
class Calculator:

    def add(self,a,b):

        print(a+b)

c = Calculator()

c.add(10,20)
```

Output

```
30
```

---

# Example

Bank Account

```python
class BankAccount:

    def __init__(self,name,balance):

        self.name = name
        self.balance = balance

    def deposit(self,amount):

        self.balance += amount

    def withdraw(self,amount):

        self.balance -= amount

    def display(self):

        print("Name :", self.name)
        print("Balance :", self.balance)

account = BankAccount("Alex",1000)

account.deposit(500)

account.withdraw(300)

account.display()
```

Output

```
Name : Alex

Balance : 1200
```

---

# Example

Rectangle

```python
class Rectangle:

    def __init__(self,length,width):

        self.length = length
        self.width = width

    def area(self):

        return self.length * self.width

r = Rectangle(10,5)

print(r.area())
```

Output

```
50
```

---

# Best Practices

✔ Always initialize important attributes inside `__init__()`.

✔ Use meaningful method names.

✔ Keep methods focused on one task.

✔ Access object data using `self`.

✔ Prefer constructors over assigning attributes manually.

---

# Common Mistakes

❌ Forgetting `self`

```python
def display():
```

Should be

```python
def display(self):
```

---

❌ Forgetting to initialize attributes

```python
print(self.name)
```

before assigning `self.name`.

---

❌ Calling constructor manually

Incorrect

```python
s.__init__()
```

Normally, constructors are invoked automatically when an object is created.

---

# Summary

Today we learned

- Methods
- Instance Methods
- self Keyword
- Constructors
- __init__()
- Instance Variables
- Local Variables
- Object Initialization
- Passing Arguments to Methods
- Building Real-World Classes

---

# Coming Next (Day-23)

Inheritance

- Parent Class
- Child Class
- Code Reuse
- super()
- Constructor Chaining
- Types of Inheritance
- Method Overriding Introduction
