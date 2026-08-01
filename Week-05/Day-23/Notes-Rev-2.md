# Types of Inheritance in Python

Inheritance allows one class to acquire the properties and methods of another class.

## Types of Inheritance

1. Single Inheritance
2. Multiple Inheritance
3. Multilevel Inheritance
4. Hierarchical Inheritance
5. Hybrid Inheritance

---

# 1. Single Inheritance

## What?

A child class inherits from **one parent class**.

### Diagram

```text
Animal
   │
   ▼
 Dog
```

### Example

```python
class Animal:
    def eat(self):
        print("Animal is eating")


class Dog(Animal):
    def bark(self):
        print("Dog is barking")


dog = Dog()

dog.eat()
dog.bark()
```

### Output

```text
Animal is eating
Dog is barking
```

---

# 2. Multiple Inheritance

## What?

A child class inherits from **more than one parent class**.

### Diagram

```text
 Father      Mother
     \        /
      \      /
       \    /
        Child
```

### Example

```python
class Father:
    def skills(self):
        print("Father: Driving")


class Mother:
    def cooking(self):
        print("Mother: Cooking")


class Child(Father, Mother):
    def hobby(self):
        print("Child: Playing Cricket")


child = Child()

child.skills()
child.cooking()
child.hobby()
```

### Output

```text
Father: Driving
Mother: Cooking
Child: Playing Cricket
```

---

# 3. Multilevel Inheritance

## What?

A class inherits from a class that already inherits from another class.

### Diagram

```text
Grandparent
      │
      ▼
   Parent
      │
      ▼
    Child
```

### Example

```python
class Grandparent:
    def grandparent_method(self):
        print("Grandparent Method")


class Parent(Grandparent):
    def parent_method(self):
        print("Parent Method")


class Child(Parent):
    def child_method(self):
        print("Child Method")


child = Child()

child.grandparent_method()
child.parent_method()
child.child_method()
```

### Output

```text
Grandparent Method
Parent Method
Child Method
```

---

# 4. Hierarchical Inheritance

## What?

Multiple child classes inherit from the **same parent class**.

### Diagram

```text
        Animal
        /    \
       /      \
     Dog      Cat
```

### Example

```python
class Animal:
    def eat(self):
        print("Animal is eating")


class Dog(Animal):
    def bark(self):
        print("Dog is barking")


class Cat(Animal):
    def meow(self):
        print("Cat is meowing")


dog = Dog()
cat = Cat()

dog.eat()
dog.bark()

cat.eat()
cat.meow()
```

### Output

```text
Animal is eating
Dog is barking
Animal is eating
Cat is meowing
```

---

# 5. Hybrid Inheritance

## What?

Hybrid inheritance is a combination of **two or more inheritance types**.

### Diagram

```text
        A
       / \
      B   C
       \ /
        D
```

### Example

```python
class A:
    def method_a(self):
        print("Class A")


class B(A):
    def method_b(self):
        print("Class B")


class C(A):
    def method_c(self):
        print("Class C")


class D(B, C):
    def method_d(self):
        print("Class D")


obj = D()

obj.method_a()
obj.method_b()
obj.method_c()
obj.method_d()
```

### Output

```text
Class A
Class B
Class C
Class D
```

---

# Summary Table

| Inheritance Type | Description | Example |
|------------------|-------------|---------|
| Single | One child inherits from one parent | `Animal → Dog` |
| Multiple | One child inherits from multiple parents | `Father + Mother → Child` |
| Multilevel | Child inherits from parent, which inherits from grandparent | `A → B → C` |
| Hierarchical | Multiple children inherit from one parent | `Animal → Dog, Cat` |
| Hybrid | Combination of multiple inheritance types | `A → B, C → D` |

---

# Easy Memory Trick

| Type | Remember As |
|------|-------------|
| Single | One Parent → One Child |
| Multiple | Many Parents → One Child |
| Multilevel | Grandparent → Parent → Child |
| Hierarchical | One Parent → Many Children |
| Hybrid | Mix of Different Inheritance Types |
