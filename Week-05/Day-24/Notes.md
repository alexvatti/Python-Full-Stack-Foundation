# Python Full Stack Foundation

# Week-05 – Day-24

# Object-Oriented Programming (OOP)

# Polymorphism in Python

**Level:** Beginner → Intermediate

---

# Learning Objectives

By the end of this session, you will be able to:

- Understand Polymorphism
- Explain why Polymorphism is useful
- Differentiate Method Overloading and Method Overriding
- Implement Method Overriding
- Understand Runtime Polymorphism
- Learn Duck Typing
- Understand Operator Overloading
- Use Magic (Dunder) Methods
- Override __str__()
- Override __repr__()
- Override __len__()
- Override __add__()
- Build reusable object-oriented programs

---

# Recap

Previous Topics

✓ Classes

✓ Objects

✓ Constructors

✓ Methods

✓ Inheritance

Today we learn

# Polymorphism

One of the four major pillars of Object-Oriented Programming.

---

# Four Pillars of OOP

```
Object-Oriented Programming

│

├── Encapsulation

├── Inheritance

├── Polymorphism

└── Abstraction
```

Today we focus on

Polymorphism

---

# What is Polymorphism?

## Definition

Polymorphism means

> One Interface, Many Forms.

The same method or operation behaves differently depending on the object that uses it.

---

# Simple Definition

The same action

Different behaviour.

---

# Real World Example

Person

↓

Speak()

English Teacher

↓

Speaks English

Hindi Teacher

↓

Speaks Hindi

French Teacher

↓

Speaks French

Same action

Different behaviour.

---

# Another Example

Animal

↓

sound()

Dog

↓

Bark

Cat

↓

Meow

Cow

↓

Moo

The method name is the same.

Behaviour changes.

---

# Why Do We Need Polymorphism?

Suppose we have

Dog

Cat

Cow

Without polymorphism

```python
dog.bark()

cat.meow()

cow.moo()
```

Different methods.

Not reusable.

---

Using polymorphism

```python
animal.sound()
```

Every object responds differently.

Cleaner code.

---

# Advantages of Polymorphism

✓ Flexible code

✓ Reusable code

✓ Easy maintenance

✓ Better scalability

✓ Less conditional statements

---

# Types of Polymorphism

```
Polymorphism

│

├── Compile-Time

└── Runtime
```

Python mainly supports

Runtime Polymorphism.

---

# Compile-Time Polymorphism

Languages like

- Java
- C++
- C#

support Method Overloading.

Python does not support true method overloading.

Instead,

Python uses

- Default Arguments
- *args
- **kwargs

---

# Runtime Polymorphism

Runtime Polymorphism is achieved through

Method Overriding.

---

# Method Overriding

## Definition

When a child class defines a method having the same name as the parent class,

the child method replaces the parent's implementation.

---

# Example

```python
class Animal:

    def sound(self):

        print("Animal Sound")


class Dog(Animal):

    def sound(self):

        print("Bark")


dog = Dog()

dog.sound()
```

Output

```
Bark
```

---

# Another Example

```python
class Animal:

    def sound(self):

        print("Unknown Sound")


class Cat(Animal):

    def sound(self):

        print("Meow")


class Cow(Animal):

    def sound(self):

        print("Moo")


Cat().sound()

Cow().sound()
```

Output

```
Meow

Moo
```

---

# Runtime Polymorphism

```python
class Animal:

    def sound(self):

        print("Animal")


class Dog(Animal):

    def sound(self):

        print("Bark")


class Cat(Animal):

    def sound(self):

        print("Meow")


animals = [Dog(), Cat()]

for animal in animals:

    animal.sound()
```

Output

```
Bark

Meow
```

Notice

The same method call

```
sound()
```

produces different outputs.

---

# How Python Decides

When

```python
dog.sound()
```

is executed,

Python searches

```
Dog

↓

Animal

↓

object
```

The first matching method is executed.

---

# Calling Parent Method

Sometimes we want to use

both

Parent

+

Child implementation.

---

Example

```python
class Animal:

    def sound(self):

        print("Animal Sound")


class Dog(Animal):

    def sound(self):

        super().sound()

        print("Bark")
```

Output

```
Animal Sound

Bark
```

---

# Example

Vehicle

```python
class Vehicle:

    def start(self):

        print("Vehicle Starting")


class Car(Vehicle):

    def start(self):

        super().start()

        print("Car Started")


c = Car()

c.start()
```

Output

```
Vehicle Starting

Car Started
```

---

# Method Overloading

Python does not support true method overloading.

Incorrect

```python
class Test:

    def add(self,a,b):

        return a+b

    def add(self,a,b,c):

        return a+b+c
```

Only the second method exists.

---

# Correct Alternative

Using Default Arguments

```python
class Test:

    def add(self,a,b,c=0):

        return a+b+c
```

Output

```python
t=Test()

print(t.add(10,20))

print(t.add(10,20,30))
```

Output

```
30

60
```

---

# Another Alternative

Using *args

```python
class Calculator:

    def add(self,*numbers):

        print(sum(numbers))
```

```python
c=Calculator()

c.add(10,20)

c.add(10,20,30)

c.add(10,20,30,40)
```

Output

```
30

60

100
```

---

# Duck Typing

## Definition

"If it walks like a duck and quacks like a duck,

it is treated as a duck."

Python cares about behaviour,

not object type.

---

# Example

```python
class Duck:

    def walk(self):

        print("Duck Walking")


class Human:

    def walk(self):

        print("Human Walking")


def walking(obj):

    obj.walk()


walking(Duck())

walking(Human())
```

Output

```
Duck Walking

Human Walking
```

Notice

Both objects work.

Python never checks their class.

---

# Another Example

```python
class PDF:

    def open(self):

        print("Opening PDF")


class Image:

    def open(self):

        print("Opening Image")


def display(file):

    file.open()


display(PDF())

display(Image())
```

---

# Operator Overloading

Operators already support different behaviours.

Example

```python
print(5+4)
```

Output

```
9
```

---

Strings

```python
print("Hello"+" Python")
```

Output

```
Hello Python
```

---

Lists

```python
print([1,2]+[3,4])
```

Output

```
[1,2,3,4]
```

Same operator

Different behaviour.

This is Operator Overloading.

---

# Magic Methods

Magic Methods are also called

Dunder Methods

(Double Underscore Methods)

Examples

```
__init__

__str__

__repr__

__len__

__add__

__eq__
```

---

# __str__()

Controls

```
print(object)
```

---

Example

```python
class Student:

    def __init__(self,name):

        self.name=name

    def __str__(self):

        return self.name


s=Student("Alex")

print(s)
```

Output

```
Alex
```

Without __str__()

Output would be

```
<__main__.Student object at ...>
```

---

# __repr__()

Definition

Returns an official string representation.

Usually used for debugging.

Example

```python
class Student:

    def __repr__(self):

        return "Student Object"
```

---

# __len__()

Example

```python
class Team:

    def __init__(self,members):

        self.members=members

    def __len__(self):

        return len(self.members)


t=Team(["A","B","C"])

print(len(t))
```

Output

```
3
```

---

# __add__()

Example

```python
class Money:

    def __init__(self,amount):

        self.amount=amount

    def __add__(self,other):

        return self.amount+other.amount


m1=Money(100)

m2=Money(250)

print(m1+m2)
```

Output

```
350
```

---

# __eq__()

Checks object equality.

```python
class Student:

    def __init__(self,id):

        self.id=id

    def __eq__(self,other):

        return self.id==other.id


s1=Student(1)

s2=Student(1)

print(s1==s2)
```

Output

```
True
```

---

# Practical Example

Payment System

```python
class Payment:

    def pay(self):

        print("Processing Payment")


class UPI(Payment):

    def pay(self):

        print("Paid using UPI")


class Card(Payment):

    def pay(self):

        print("Paid using Card")


class Cash(Payment):

    def pay(self):

        print("Paid using Cash")


payments=[UPI(),Card(),Cash()]

for payment in payments:

    payment.pay()
```

Output

```
Paid using UPI

Paid using Card

Paid using Cash
```

---

# Another Example

Shapes

```python
class Shape:

    def area(self):

        pass


class Rectangle(Shape):

    def __init__(self,l,w):

        self.l=l

        self.w=w

    def area(self):

        return self.l*self.w


class Square(Shape):

    def __init__(self,s):

        self.s=s

    def area(self):

        return self.s*self.s


shapes=[Rectangle(10,5),Square(4)]

for shape in shapes:

    print(shape.area())
```

Output

```
50

16
```

---

# Best Practices

✓ Override methods only when behaviour changes.

✓ Use super() when parent behaviour is also needed.

✓ Use __str__() for user-friendly output.

✓ Use operator overloading only when it improves readability.

✓ Prefer Duck Typing over unnecessary type checking.

---

# Common Mistakes

❌ Forgetting to override the method.

❌ Using different method names in child classes.

❌ Misusing operator overloading.

❌ Returning non-string values from __str__().

Incorrect

```python
def __str__(self):

    return 100
```

Correct

```python
def __str__(self):

    return "Student"
```

---

# Summary

Today we learned

✓ Polymorphism

✓ Runtime Polymorphism

✓ Method Overriding

✓ Parent Method Calling

✓ Method Overloading Alternatives

✓ Default Arguments

✓ *args

✓ Duck Typing

✓ Operator Overloading

✓ Magic Methods

✓ __str__()

✓ __repr__()

✓ __len__()

✓ __add__()

✓ __eq__()

---

# Coming Next (Day-25)

Advanced OOP

- Encapsulation
- Name Mangling
- Properties (@property)
- Class Variables
- Static Methods
- Class Methods
- Composition
- Aggregation
- Association
- Abstraction
- Abstract Base Classes (ABC)
- Complete College Management System
