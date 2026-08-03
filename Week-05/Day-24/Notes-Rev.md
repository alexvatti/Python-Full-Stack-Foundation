
# Operator Overloading in Python

# What is Operator Overloading?

**Operator Overloading** allows us to define how operators (`+`, `-`, `*`, `==`, `<`, `>`, etc.) behave when used with **objects** of a class.

Instead of writing methods like:

```python
student1.add_marks(student2)
```

We can simply write:

```python
student1 + student2
```

Python internally converts operators into **special methods (Magic/Dunder Methods)**.

For example:

| Operator | Magic Method |
|----------|--------------|
| + | `__add__()` |
| - | `__sub__()` |
| * | `__mul__()` |
| / | `__truediv__()` |
| == | `__eq__()` |
| != | `__ne__()` |
| < | `__lt__()` |
| <= | `__le__()` |
| > | `__gt__()` |
| >= | `__ge__()` |

---

# Why Operator Overloading?

Without Operator Overloading:

```python
total = student1.add_marks(student2)
```

With Operator Overloading:

```python
total = student1 + student2
```

The code becomes

- More readable
- More natural
- Easier to maintain
- Similar to built-in Python objects

---

# Real-Life Example

Imagine two students.

Student 1

- Name : Alex
- Marks : 420

Student 2

- Name : Bob
- Marks : 450

Suppose we want

- Add their marks
- Compare whose marks are greater
- Check if both have equal marks

Python cannot understand

```python
student1 + student2
```

unless we tell Python **what '+' means for Student objects.**

---

# Example 1 : Without Operator Overloading

```python
class Student:

    def __init__(self, name, marks):
        self.name = name
        self.marks = marks

    def add_marks(self, other):
        return self.marks + other.marks


s1 = Student("Alex", 420)
s2 = Student("Bob", 450)

print(s1.add_marks(s2))
```

### Output

```
870
```

Works fine, but the syntax is not very Pythonic.

---

# Example 2 : Using Operator Overloading (__add__)

```python
class Student:

    def __init__(self, name, marks):
        self.name = name
        self.marks = marks

    def __add__(self, other):
        return self.marks + other.marks


s1 = Student("Alex", 420)
s2 = Student("Bob", 450)

print(s1 + s2)
```

### Output

```
870
```

---

## What happens internally?

When Python sees

```python
s1 + s2
```

it automatically calls

```python
s1.__add__(s2)
```

Internally,

```python
print(s1 + s2)
```

becomes

```python
print(s1.__add__(s2))
```

---

# Example 3 : Compare Two Students (__gt__)

Suppose we want to know which student scored more marks.

```python
class Student:

    def __init__(self, name, marks):
        self.name = name
        self.marks = marks

    def __gt__(self, other):
        return self.marks > other.marks


s1 = Student("Alex", 420)
s2 = Student("Bob", 450)

print(s1 > s2)
```

### Output

```
False
```

Since

```
420 > 450
```

is False.

---

Another example

```python
s1 = Student("Alex", 500)
s2 = Student("Bob", 450)

print(s1 > s2)
```

Output

```
True
```

---

# Example 4 : Compare Equality (__eq__)

```python
class Student:

    def __init__(self, name, marks):
        self.name = name
        self.marks = marks

    def __eq__(self, other):
        return self.marks == other.marks


s1 = Student("Alex", 450)
s2 = Student("Bob", 450)

print(s1 == s2)
```

### Output

```
True
```

Because both students have the same marks.

---

# Example 5 : Complete Example

```python
class Student:

    def __init__(self, name, marks):
        self.name = name
        self.marks = marks

    # +
    def __add__(self, other):
        return self.marks + other.marks

    # >
    def __gt__(self, other):
        return self.marks > other.marks

    # ==
    def __eq__(self, other):
        return self.marks == other.marks


s1 = Student("Alex", 420)
s2 = Student("Bob", 450)

print("Total Marks :", s1 + s2)

print("Alex > Bob :", s1 > s2)

print("Equal Marks :", s1 == s2)
```

### Output

```
Total Marks : 870
Alex > Bob : False
Equal Marks : False
```

---

# Another Valid Example : Bank Account

Operator overloading can also represent business logic.

```python
class BankAccount:

    def __init__(self, owner, balance):
        self.owner = owner
        self.balance = balance

    def __add__(self, other):
        return self.balance + other.balance


a1 = BankAccount("Alex", 50000)
a2 = BankAccount("Bob", 35000)

print(a1 + a2)
```

Output

```
85000
```

---

# Another Valid Example : Shopping Cart

```python
class Cart:

    def __init__(self, items):
        self.items = items

    def __add__(self, other):
        return self.items + other.items


cart1 = Cart(4)
cart2 = Cart(6)

print(cart1 + cart2)
```

Output

```
10
```

---

# Flow of Operator Overloading

```
Objects Created
       │
       ▼
s1 + s2
       │
       ▼
Python checks
Does class define __add__() ?
       │
       ├── Yes
       │      │
       │      ▼
       │ Calls
       │ s1.__add__(s2)
       │
       ▼
Returns Result
```

---

# Common Operator Overloading Methods

| Operator | Magic Method | Example |
|-----------|--------------|---------|
| + | `__add__()` | `obj1 + obj2` |
| - | `__sub__()` | `obj1 - obj2` |
| * | `__mul__()` | `obj1 * obj2` |
| / | `__truediv__()` | `obj1 / obj2` |
| // | `__floordiv__()` | `obj1 // obj2` |
| % | `__mod__()` | `obj1 % obj2` |
| ** | `__pow__()` | `obj1 ** obj2` |
| == | `__eq__()` | `obj1 == obj2` |
| != | `__ne__()` | `obj1 != obj2` |
| > | `__gt__()` | `obj1 > obj2` |
| < | `__lt__()` | `obj1 < obj2` |
| >= | `__ge__()` | `obj1 >= obj2` |
| <= | `__le__()` | `obj1 <= obj2` |

---

# Advantages of Operator Overloading

✅ Makes objects behave like built-in data types.

✅ Improves code readability.

✅ Produces cleaner and more intuitive syntax.

✅ Enables natural mathematical and comparison operations.

✅ Widely used in libraries like NumPy, Pandas, and TensorFlow.

---

# Key Points to Remember

- Operator Overloading is achieved using **Magic (Dunder) Methods**.
- Python automatically calls the corresponding magic method when an operator is used.
- It works only if the class defines the required special method.
- It makes custom objects behave like integers, strings, or lists.
- Always implement operator overloading only when the operation has a meaningful interpretation for your objects.

---

# Summary

```
Operator
     │
     ▼
Python converts it into
Magic Method
     │
     ▼
Your Class executes
     │
     ▼
Returns the Result

Example

s1 + s2
   │
   ▼
s1.__add__(s2)

s1 > s2
   │
   ▼
s1.__gt__(s2)

s1 == s2
   │
   ▼
s1.__eq__(s2)
```

**Operator Overloading** allows custom Python objects to behave like built-in types by defining special methods such as `__add__()`, `__gt__()`, and `__eq__()`, making code more expressive, readable, and object-oriented.
````
