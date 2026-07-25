# Python Full Stack Foundation

# Week-05 – Day-23

# Object-Oriented Programming (OOP)

# Inheritance in Python

**Level:** Beginner → Intermediate

---

# Learning Objectives

By the end of this session, you will be able to:

- Understand Inheritance
- Explain why Inheritance is needed
- Create Parent and Child classes
- Reuse existing code
- Understand the `super()` function
- Learn Constructor Chaining
- Understand Method Overriding (Introduction)
- Learn Types of Inheritance
- Use `isinstance()` and `issubclass()`
- Understand Method Resolution Order (MRO)

---

# Recap

Previously we learned

- Classes
- Objects
- Methods
- self
- Constructors
- Instance Variables

Today we will learn one of the biggest advantages of OOP:

# Inheritance

---

# What is Inheritance?

## Definition

Inheritance is an OOP feature that allows one class to acquire the properties and methods of another class.

Instead of writing the same code repeatedly, we create a new class from an existing class.

---

# Simple Definition

Inheritance means

> "A child class automatically gets the features of its parent class."

---

# Real World Examples

Human

↓

Employee

↓

Software Engineer

Software Engineer automatically has

- Name
- Age
- Address

and also has

- Programming Language
- Experience

---

Vehicle

↓

Car

Car automatically has

- Engine
- Wheels
- Fuel Tank

Car additionally has

- Music System
- Air Conditioner

---

Animal

↓

Dog

Dog automatically has

- Eat()
- Sleep()

Dog additionally has

- Bark()

---

# Why Do We Need Inheritance?

Suppose we have three classes.

Employee

Teacher

Student

All contain

- Name
- Age
- Phone Number
- Address

Without inheritance

```python
class Student:

    def __init__(self,name,age):
        self.name=name
        self.age=age


class Teacher:

    def __init__(self,name,age):
        self.name=name
        self.age=age


class Employee:

    def __init__(self,name,age):
        self.name=name
        self.age=age
```

Notice

The same code is repeated.

This is called **Code Duplication**.

---

Using inheritance

```text
                Person
              /    |     \
      Student Teacher Employee
```

Now

Person stores

- Name
- Age
- Phone

Every child class automatically inherits them.

---

# Advantages of Inheritance

## Code Reuse

Write once.

Reuse everywhere.

---

## Less Code

No duplication.

---

## Easy Maintenance

Modify parent class once.

All child classes automatically receive updates.

---

## Better Organization

Large applications become easier to understand.

---

## Extensibility

New features can be added without changing existing code.

---

# Parent Class

Definition

The class whose properties are inherited is called the

- Parent Class
- Base Class
- Super Class

All three names mean the same thing.

---

Example

```python
class Person:

    def __init__(self,name):

        self.name=name
```

Person is the Parent Class.

---

# Child Class

Definition

The class that inherits another class is called

- Child Class
- Derived Class
- Sub Class

---

Syntax

```python
class Student(Person):
    pass
```

Student inherits Person.

---

# First Example

```python
class Person:

    def display(self):

        print("I am a Person")


class Student(Person):

    pass


s=Student()

s.display()
```

Output

```
I am a Person
```

Although Student has no methods,

it automatically inherits display().

---

# Another Example

```python
class Animal:

    def eat(self):

        print("Eating")


class Dog(Animal):

    pass


d=Dog()

d.eat()
```

Output

```
Eating
```

Dog inherited eat().

---

# Parent with Constructor

```python
class Person:

    def __init__(self,name):

        self.name=name

    def display(self):

        print(self.name)
```

---

# Child Class

```python
class Student(Person):

    pass
```

Creating Object

```python
s=Student("Alex")

s.display()
```

Output

```
Alex
```

The constructor was inherited.

---

# Adding New Methods

```python
class Person:

    def display(self):

        print("Person")


class Student(Person):

    def study(self):

        print("Studying Python")


s=Student()

s.display()

s.study()
```

Output

```
Person

Studying Python
```

Student has

Inherited Method

+

Own Method

---

# Memory Representation

```
Student Object

--------------------

name

display()

study()

--------------------

↑

Student inherits display()

from Person
```

---

# Using super()

One of the most important concepts.

---

# Definition

super() refers to the Parent Class.

It allows a child class to call

- Parent Constructor
- Parent Methods

---

# Why super()?

Without super()

```python
class Student(Person):

    def __init__(self,name,roll):

        self.name=name

        self.roll=roll
```

Problem

Parent constructor never executes.

---

Correct

```python
class Student(Person):

    def __init__(self,name,roll):

        super().__init__(name)

        self.roll=roll
```

Now

Person constructor

+

Student constructor

both execute.

---

# Example

```python
class Person:

    def __init__(self,name):

        self.name=name


class Student(Person):

    def __init__(self,name,roll):

        super().__init__(name)

        self.roll=roll


s=Student("Alex",101)

print(s.name)

print(s.roll)
```

Output

```
Alex

101
```

---

# Constructor Chaining

Definition

Calling constructors from parent to child is called

Constructor Chaining.

```
Person

↓

Student

↓

GraduateStudent
```

Object Creation

↓

GraduateStudent Constructor

↓

Student Constructor

↓

Person Constructor

---

# Example

```python
class A:

    def __init__(self):

        print("A")


class B(A):

    def __init__(self):

        super().__init__()

        print("B")


class C(B):

    def __init__(self):

        super().__init__()

        print("C")


c=C()
```

Output

```
A

B

C
```

Constructors execute from top to bottom.

---

# Types of Inheritance

Python supports

- Single
- Multilevel
- Multiple
- Hierarchical
- Hybrid

---

# 1 Single Inheritance

```
A

↓

B
```

Example

```python
class Animal:

    def eat(self):

        print("Eating")


class Dog(Animal):

    pass
```

---

# 2 Multilevel Inheritance

```
A

↓

B

↓

C
```

Example

```python
class Animal:

    pass


class Dog(Animal):

    pass


class Puppy(Dog):

    pass
```

Puppy inherits

Dog

and

Animal

---

# 3 Hierarchical Inheritance

```
          Person

       /     |      \

 Student Teacher Employee
```

One parent

Many children.

---

Example

```python
class Person:

    pass


class Student(Person):

    pass


class Teacher(Person):

    pass
```

---

# 4 Multiple Inheritance

```
Teacher

      \

       Student

      /

Sports
```

One child

Multiple parents.

Example

```python
class Father:

    def house(self):

        print("House")


class Mother:

    def jewellery(self):

        print("Jewellery")


class Child(Father,Mother):

    pass


c=Child()

c.house()

c.jewellery()
```

---

# 5 Hybrid Inheritance

Combination of

- Multiple
- Hierarchical
- Multilevel

Python supports Hybrid Inheritance.

---

# Method Overriding (Introduction)

Definition

When a child class defines a method having the same name as the parent class,

the child method replaces the parent method.

---

Example

```python
class Animal:

    def sound(self):

        print("Animal Sound")


class Dog(Animal):

    def sound(self):

        print("Bark")


d=Dog()

d.sound()
```

Output

```
Bark
```

Dog overrides Animal.

We'll study this in detail tomorrow.

---

# isinstance()

Checks whether an object belongs to a class.

Example

```python
class Animal:

    pass


class Dog(Animal):

    pass


d=Dog()

print(isinstance(d,Dog))

print(isinstance(d,Animal))
```

Output

```
True

True
```

Because Dog inherits Animal.

---

# issubclass()

Checks whether one class inherits another.

```python
class Animal:

    pass


class Dog(Animal):

    pass


print(issubclass(Dog,Animal))
```

Output

```
True
```

---

# Method Resolution Order (MRO)

Definition

When Python searches for a method,

it follows a specific order called

Method Resolution Order.

---

Example

```python
class A:

    def show(self):

        print("A")


class B(A):

    pass


b=B()

b.show()
```

Python searches

```
B

↓

A
```

It finds show() in A.

---

# Viewing MRO

```python
class A:

    pass


class B(A):

    pass


print(B.mro())
```

Output

```
[B,A,object]
```

Meaning

Python searches

```
B

↓

A

↓

object
```

---

# Real World Example

```
Person

↓

Employee

↓

Manager
```

Person

- Name
- Age

Employee

- Employee ID
- Salary

Manager

- Department
- Team Size

Manager automatically gets

Everything from Employee

+

Everything from Person.

---

# Best Practices

✔ Create a common Parent Class.

✔ Avoid duplicate code.

✔ Use super() inside constructors.

✔ Child classes should extend functionality, not duplicate it.

✔ Use inheritance only when there is an "IS-A" relationship.

Example

Dog IS-A Animal ✅

Car HAS-A Engine ❌

(HAS-A is Composition, covered on Day-25.)

---

# Common Mistakes

❌ Forgetting super()

```python
class Student(Person):

    def __init__(self,name):

        self.name=name
```

Parent constructor never executes.

---

❌ Copying Parent Code

Do not duplicate code already available in the parent.

---

❌ Wrong Relationship

Student HAS-A Laptop

This is NOT inheritance.

Student IS-A Person

This IS inheritance.

---

# Summary

Today we learned

✓ Inheritance

✓ Parent Class

✓ Child Class

✓ Base Class

✓ Derived Class

✓ Code Reuse

✓ super()

✓ Constructor Chaining

✓ Types of Inheritance

✓ Method Overriding (Introduction)

✓ isinstance()

✓ issubclass()

✓ Method Resolution Order (MRO)

---

# Coming Next (Day-24)

Polymorphism

- Method Overriding (Deep Dive)
- Runtime Polymorphism
- Duck Typing
- Operator Overloading
- Magic (Dunder) Methods
- __str__()
- __repr__()
- __len__()
- __add__()
- Practical Examples
