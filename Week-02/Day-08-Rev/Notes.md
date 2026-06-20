# Week-02 Day-08 — Python Tuples
### Complete Theory, Syntax, Code Examples & Interview Programs

---

## Table of Contents

1. [Theory & Introduction](#1-theory--introduction)
2. [Syntax & Creation](#2-syntax--creation)
3. [Indexing](#3-indexing)
4. [Slicing](#4-slicing)
5. [Mathematical Operators](#5-mathematical-operators)
6. [Membership Operators](#6-membership-operators)
7. [Comparison Operators](#7-comparison-operators)
8. [Built-in Functions](#8-built-in-functions)
9. [Iteration](#9-iteration)
10. [count() and index()](#10-count-and-index)
11. [Packing & Unpacking](#11-packing--unpacking)
12. [Tuple vs List](#12-tuple-vs-list)
13. [15 Interview Programs](#13-15-interview-programs)
14. [Summary](#14-summary)
15. [Self-Study Exercises](#15-self-study-exercises)

---

## 1. Theory & Introduction

### What is a Tuple?

A **tuple** is an **ordered, immutable** collection of elements in Python. Once created, the elements of a tuple **cannot be changed, added, or removed**. Tuples are one of Python's four built-in sequence data types (list, tuple, range, str).

### Key Characteristics

| Property | Description |
|----------|-------------|
| **Ordered** | Elements maintain their insertion order |
| **Immutable** | Cannot modify, add, or delete elements after creation |
| **Allows Duplicates** | Same value can appear multiple times |
| **Heterogeneous** | Can store mixed data types (int, str, float, etc.) |
| **Indexed** | Elements accessible via zero-based index |
| **Hashable** | Tuples of hashable elements can be used as dict keys |

### Why Use Tuples?

- **Data integrity** — Protect data that should not change (e.g., coordinates, RGB values, database records)
- **Performance** — Faster than lists for read-only operations
- **Dictionary keys** — Lists cannot be dict keys; tuples can
- **Return multiple values** — Functions commonly return tuples
- **Named constants** — Store fixed configuration values

### Memory Layout

```
t = (10, 20, 30, 40, 50)

Index:  [0]  [1]  [2]  [3]  [4]
Value:   10   20   30   40   50

Negative:[-5] [-4] [-3] [-2] [-1]
```

---

## 2. Syntax & Creation

### Basic Syntax

```python
# Empty tuple
t1 = ()
t2 = tuple()

# Single-element tuple — MUST have trailing comma
t3 = (42,)          # ✅ This is a tuple
t4 = (42)           # ❌ This is just an integer — common mistake!

print(type(t3))     # <class 'tuple'>
print(type(t4))     # <class 'int'>

# Multi-element tuple
t5 = (1, 2, 3)
t6 = (1, 2, 3,)     # Trailing comma is allowed

# Without parentheses (tuple packing)
t7 = 10, 20, 30
print(type(t7))     # <class 'tuple'>

# Heterogeneous tuple
t8 = (1, "hello", 3.14, True, None)

# Nested tuple
t9 = (1, (2, 3), (4, (5, 6)))

# From iterable using tuple()
t10 = tuple([1, 2, 3])      # From list
t11 = tuple("Python")       # From string → ('P','y','t','h','o','n')
t12 = tuple(range(1, 6))    # From range → (1, 2, 3, 4, 5)
```

### Output

```
<class 'tuple'>
<class 'int'>
<class 'tuple'>
```

---

## 3. Indexing

Tuples use **zero-based indexing**. Negative indexing counts from the end.

```python
fruits = ("apple", "banana", "cherry", "date", "elderberry")

# Positive indexing
print(fruits[0])    # apple
print(fruits[1])    # banana
print(fruits[4])    # elderberry

# Negative indexing
print(fruits[-1])   # elderberry  (last element)
print(fruits[-2])   # date
print(fruits[-5])   # apple  (first element)

# Nested tuple indexing
matrix = ((1, 2, 3), (4, 5, 6), (7, 8, 9))
print(matrix[0])        # (1, 2, 3)
print(matrix[1][2])     # 6   → row index 1, column index 2
print(matrix[-1][-1])   # 9   → last row, last column

# IndexError example
try:
    print(fruits[10])
except IndexError as e:
    print(f"Error: {e}")  # Error: tuple index out of range
```

### Output

```
apple
banana
elderberry
elderberry
date
apple
(1, 2, 3)
6
9
Error: tuple index out of range
```

---

## 4. Slicing

Slicing extracts a sub-tuple without modifying the original.

**Syntax:** `tuple[start : stop : step]`

| Parameter | Default | Description |
|-----------|---------|-------------|
| `start` | 0 | Start index (inclusive) |
| `stop` | len(t) | Stop index (exclusive) |
| `step` | 1 | Step size (can be negative) |

```python
t = (0, 1, 2, 3, 4, 5, 6, 7, 8, 9)

# Basic slicing
print(t[2:6])       # (2, 3, 4, 5)      — index 2 to 5
print(t[:4])        # (0, 1, 2, 3)      — from start to index 3
print(t[6:])        # (6, 7, 8, 9)      — from index 6 to end
print(t[:])         # (0, 1, 2, 3, 4, 5, 6, 7, 8, 9)  — full copy

# Step slicing
print(t[::2])       # (0, 2, 4, 6, 8)  — every 2nd element
print(t[1::2])      # (1, 3, 5, 7, 9)  — odd-indexed elements
print(t[::3])       # (0, 3, 6, 9)     — every 3rd element

# Reverse
print(t[::-1])      # (9, 8, 7, 6, 5, 4, 3, 2, 1, 0)
print(t[7:2:-1])    # (7, 6, 5, 4, 3)  — from 7 down to 3

# Negative index slicing
print(t[-4:])       # (6, 7, 8, 9)
print(t[-6:-2])     # (4, 5, 6, 7)
```

### Output

```
(2, 3, 4, 5)
(0, 1, 2, 3)
(6, 7, 8, 9)
(0, 1, 2, 3, 4, 5, 6, 7, 8, 9)
(0, 2, 4, 6, 8)
(1, 3, 5, 7, 9)
(0, 3, 6, 9)
(9, 8, 7, 6, 5, 4, 3, 2, 1, 0)
(7, 6, 5, 4, 3)
(6, 7, 8, 9)
(4, 5, 6, 7)
```

---

## 5. Mathematical Operators

Tuples support `+` (concatenation) and `*` (repetition). They do NOT support `-` or `/`.

```python
t1 = (1, 2, 3)
t2 = (4, 5, 6)

# Concatenation with +
t3 = t1 + t2
print(t3)           # (1, 2, 3, 4, 5, 6)

# Repetition with *
t4 = t1 * 3
print(t4)           # (1, 2, 3, 1, 2, 3, 1, 2, 3)

t5 = 2 * ("ha",)
print(t5)           # ('ha', 'ha')

# Combining + and *
t6 = (0,) + t1 * 2 + t2
print(t6)           # (0, 1, 2, 3, 1, 2, 3, 4, 5, 6)

# += and *= (create new tuple — tuples are immutable)
t7 = (10, 20)
t7 += (30, 40)       # Creates a NEW tuple, rebinds t7
print(t7)           # (10, 20, 30, 40)

t8 = (1, 2)
t8 *= 3
print(t8)           # (1, 2, 1, 2, 1, 2)

# What does NOT work
try:
    t1[0] = 99      # Tuples are immutable!
except TypeError as e:
    print(f"Error: {e}")
```

### Output

```
(1, 2, 3, 4, 5, 6)
(1, 2, 3, 1, 2, 3, 1, 2, 3)
('ha', 'ha')
(0, 1, 2, 3, 1, 2, 3, 4, 5, 6)
(10, 20, 30, 40)
(1, 2, 1, 2, 1, 2)
Error: 'tuple' object does not support item assignment
```

---

## 6. Membership Operators

`in` and `not in` check whether a value exists in a tuple.

```python
colors = ("red", "green", "blue", "yellow")

# in operator
print("red" in colors)         # True
print("purple" in colors)      # False

# not in operator
print("purple" not in colors)  # True
print("green" not in colors)   # False

# Use in conditional
if "blue" in colors:
    print("Blue is available!")

# Membership in nested tuples (only checks top-level)
nested = ((1, 2), (3, 4), (5, 6))
print((1, 2) in nested)        # True  — checks top-level elements
print(1 in nested)             # False — 1 is not a top-level element

# Practical: validate user input
valid_grades = ("A", "B", "C", "D", "F")
grade = "B"
if grade in valid_grades:
    print(f"Valid grade: {grade}")
else:
    print("Invalid grade!")
```

### Output

```
True
False
True
False
Blue is available!
True
False
Valid grade: B
```

---

## 7. Comparison Operators

Tuples compare **element by element from left to right**. All six comparison operators are supported.

```python
t1 = (1, 2, 3)
t2 = (1, 2, 3)
t3 = (1, 2, 4)
t4 = (1, 2)
t5 = (2, 0, 0)

# Equality
print(t1 == t2)     # True  — same elements
print(t1 == t3)     # False — differ at index 2

# Inequality
print(t1 != t3)     # True

# Less than / Greater than
print(t1 < t3)      # True  — 3 < 4 at index 2
print(t1 > t4)      # True  — t1 is longer after equal prefix
print(t5 > t1)      # True  — 2 > 1 at index 0 (stops immediately)

# Comparing different lengths
print((1,) < (1, 2))    # True  — shorter tuple is "less"
print((1, 2) < (1, 2))  # False — equal, not less

# Sorting tuples using comparison
students = [("Alice", 85), ("Bob", 92), ("Charlie", 78)]
students.sort()             # Sorts by first element (name)
print(students)

students.sort(key=lambda x: x[1], reverse=True)  # Sort by score descending
print(students)
```

### Output

```
True
False
True
True
True
True
True
False
[('Alice', 85), ('Bob', 92), ('Charlie', 78)]
[('Bob', 92), ('Alice', 85), ('Charlie', 78)]
```

---

## 8. Built-in Functions

```python
t = (3, 1, 4, 1, 5, 9, 2, 6, 5, 3, 5)

# len() — number of elements
print(len(t))           # 11

# max() and min()
print(max(t))           # 9
print(min(t))           # 1

# sum()
print(sum(t))           # 44

# sorted() — returns a NEW list (not a tuple)
print(sorted(t))                    # [1, 1, 2, 3, 3, 4, 5, 5, 5, 6, 9]
print(sorted(t, reverse=True))      # [9, 6, 5, 5, 5, 4, 3, 3, 2, 1, 1]

# Convert sorted result back to tuple
print(tuple(sorted(t)))             # (1, 1, 2, 3, 3, 4, 5, 5, 5, 6, 9)

# enumerate() — index + value pairs
for i, v in enumerate(("a", "b", "c")):
    print(i, v)

# zip() — combine multiple tuples
names = ("Alice", "Bob", "Charlie")
scores = (85, 92, 78)
zipped = tuple(zip(names, scores))
print(zipped)       # (('Alice', 85), ('Bob', 92), ('Charlie', 78))

# any() and all()
t2 = (0, 1, 2, 3)
print(any(t2))      # True  — at least one truthy element
print(all(t2))      # False — 0 is falsy

# reversed()
print(tuple(reversed(t)))   # (5, 3, 5, 6, 2, 9, 5, 1, 4, 1, 3)

# type(), id()
print(type(t))      # <class 'tuple'>
print(id(t))        # Memory address (varies)
```

### Output

```
11
9
1
44
[1, 1, 2, 3, 3, 4, 5, 5, 5, 6, 9]
[9, 6, 5, 5, 5, 4, 3, 3, 2, 1, 1]
(1, 1, 2, 3, 3, 4, 5, 5, 5, 6, 9)
0 a
1 b
2 c
(('Alice', 85), ('Bob', 92), ('Charlie', 78))
True
False
(5, 3, 5, 6, 2, 9, 5, 1, 4, 1, 3)
<class 'tuple'>
```

---

## 9. Iteration

```python
# Basic for loop
colors = ("red", "green", "blue")
for color in colors:
    print(color)

# With index using enumerate()
for index, color in enumerate(colors):
    print(f"Index {index}: {color}")

# With enumerate() — custom start index
for index, color in enumerate(colors, start=1):
    print(f"{index}. {color}")

# While loop with indexing
i = 0
while i < len(colors):
    print(colors[i])
    i += 1

# Iterate nested tuple
matrix = ((1, 2), (3, 4), (5, 6))
for row in matrix:
    for val in row:
        print(val, end=" ")
    print()

# List comprehension from tuple
t = (1, 2, 3, 4, 5)
squares = [x**2 for x in t]
print(squares)          # [1, 4, 9, 16, 25]

evens = [x for x in t if x % 2 == 0]
print(evens)            # [2, 4]

# Tuple comprehension — use tuple() with generator
sq_tuple = tuple(x**2 for x in t)
print(sq_tuple)         # (1, 4, 9, 16, 25)
```

### Output

```
red
green
blue
Index 0: red
Index 1: green
Index 2: blue
1. red
2. green
3. blue
red
green
blue
1 2
3 4
5 6
[1, 4, 9, 16, 25]
[2, 4]
(1, 4, 9, 16, 25)
```

---

## 10. `count()` and `index()`

These are the **only two methods** available on tuples.

### `count(value)` — Count Occurrences

```python
t = (1, 2, 3, 2, 4, 2, 5, 1)

print(t.count(2))       # 3  — 2 appears 3 times
print(t.count(1))       # 2  — 1 appears 2 times
print(t.count(9))       # 0  — 9 does not appear

# Count in string tuple
words = ("hi", "hello", "hi", "hey", "hi")
print(words.count("hi"))    # 3
```

### `index(value, start, stop)` — Find Position

```python
t = (10, 20, 30, 20, 40, 20)

# Basic index
print(t.index(20))          # 1  — first occurrence at index 1
print(t.index(40))          # 4

# With start position — search from index 2 onward
print(t.index(20, 2))       # 3  — second occurrence

# With start and stop
print(t.index(20, 2, 5))    # 3  — searches only in t[2:5]

# ValueError if not found
try:
    print(t.index(99))
except ValueError as e:
    print(f"Error: {e}")    # Error: tuple.index(x): x not in tuple

# Practical: find all indices of a value
t2 = (5, 3, 5, 8, 5, 1)
indices = [i for i, v in enumerate(t2) if v == 5]
print(indices)              # [0, 2, 4]
```

### Output

```
3
2
0
3
1
4
3
3
Error: tuple.index(x): x not in tuple
[0, 2, 4]
```

---

## 11. Packing & Unpacking

### Tuple Packing

When multiple values are assigned to a single variable without parentheses, Python automatically **packs** them into a tuple.

```python
# Packing
coordinates = 10, 20, 30      # Packed automatically
print(coordinates)            # (10, 20, 30)
print(type(coordinates))      # <class 'tuple'>

point = "Hyderabad", 17.38, 78.47
print(point)                  # ('Hyderabad', 17.38, 78.47)
```

### Tuple Unpacking

Tuple unpacking assigns each element of a tuple to individual variables.

```python
# Basic unpacking — number of variables must match
t = (1, 2, 3)
a, b, c = t
print(a, b, c)          # 1 2 3

# Swapping variables (classic Python idiom)
x, y = 10, 20
x, y = y, x             # Under the hood: packs then unpacks
print(x, y)             # 20 10

# Unpacking with * (extended unpacking)
first, *rest = (1, 2, 3, 4, 5)
print(first)            # 1
print(rest)             # [2, 3, 4, 5]  — rest becomes a list

*start, last = (1, 2, 3, 4, 5)
print(start)            # [1, 2, 3, 4]
print(last)             # 5

first, *middle, last = (1, 2, 3, 4, 5)
print(first)            # 1
print(middle)           # [2, 3, 4]
print(last)             # 5

# Ignoring values with _ (underscore)
name, _, age = ("Alex", "male", 30)
print(name, age)        # Alex 30

# Nested unpacking
(a, b), c = (1, 2), 3
print(a, b, c)          # 1 2 3

# Function returning multiple values (returns a tuple)
def min_max(nums):
    return min(nums), max(nums)

lo, hi = min_max([4, 7, 1, 9, 3])
print(lo, hi)           # 1 9
```

### Output

```
(10, 20, 30)
<class 'tuple'>
('Hyderabad', 17.38, 78.47)
1 2 3
20 10
1
[2, 3, 4, 5]
[1, 2, 3, 4]
5
1
[2, 3, 4]
5
Alex 30
1 2 3
1 9
```

---

## 12. Tuple vs List

| Feature | Tuple | List |
|---------|-------|------|
| **Syntax** | `(1, 2, 3)` | `[1, 2, 3]` |
| **Mutability** | Immutable ❌ | Mutable ✅ |
| **Performance** | Faster (read) | Slower (read) |
| **Memory** | Less memory | More memory |
| **Methods** | `count()`, `index()` | 11+ methods |
| **Hashable** | Yes (if elements are hashable) | No |
| **Dict Key** | Yes ✅ | No ❌ |
| **Set Element** | Yes ✅ | No ❌ |
| **Use case** | Fixed/constant data | Dynamic/changing data |

```python
import sys
import timeit

# Memory comparison
t = (1, 2, 3, 4, 5)
l = [1, 2, 3, 4, 5]
print(f"Tuple size: {sys.getsizeof(t)} bytes")   # ~80 bytes
print(f"List size:  {sys.getsizeof(l)} bytes")   # ~120 bytes

# Speed comparison
t_time = timeit.timeit("(1, 2, 3, 4, 5)", number=10_000_000)
l_time = timeit.timeit("[1, 2, 3, 4, 5]", number=10_000_000)
print(f"Tuple creation: {t_time:.3f}s")
print(f"List creation:  {l_time:.3f}s")

# Tuple as dict key (list cannot do this)
location_data = {(17.38, 78.47): "Hyderabad", (28.61, 77.20): "Delhi"}
print(location_data[(17.38, 78.47)])        # Hyderabad

# Mutability demonstration
my_list = [1, 2, 3]
my_list[0] = 99
print(my_list)      # [99, 2, 3] — list allows modification

my_tuple = (1, 2, 3)
try:
    my_tuple[0] = 99
except TypeError as e:
    print(f"Tuple error: {e}")

# When to use what:
# Tuple → RGB color, GPS coordinates, DB row, function return, fixed config
# List  → Shopping cart, student scores, dynamic queue/stack
```

### Output

```
Tuple size: 80 bytes
List size:  120 bytes
Tuple creation: 0.051s
List creation:  0.368s
Hyderabad
[99, 2, 3]
Tuple error: 'tuple' object does not support item assignment
```

---

## 13. 15 Interview Programs

---

### Program 1: Reverse a Tuple

```python
def reverse_tuple(t):
    return t[::-1]

t = (1, 2, 3, 4, 5)
print(reverse_tuple(t))         # (5, 4, 3, 2, 1)

# Alternative using reversed()
print(tuple(reversed(t)))       # (5, 4, 3, 2, 1)
```

**Output:**
```
(5, 4, 3, 2, 1)
(5, 4, 3, 2, 1)
```

---

### Program 2: Find Maximum and Minimum Without Built-ins

```python
def find_min_max(t):
    minimum = t[0]
    maximum = t[0]
    for val in t:
        if val < minimum:
            minimum = val
        if val > maximum:
            maximum = val
    return minimum, maximum

t = (3, 7, 1, 9, 4, 6, 2)
lo, hi = find_min_max(t)
print(f"Min: {lo}, Max: {hi}")      # Min: 1, Max: 9
```

**Output:**
```
Min: 1, Max: 9
```

---

### Program 3: Remove Duplicates from Tuple

```python
def remove_duplicates(t):
    seen = set()
    result = []
    for item in t:
        if item not in seen:
            seen.add(item)
            result.append(item)
    return tuple(result)

t = (1, 2, 3, 2, 4, 1, 5, 3)
print(remove_duplicates(t))         # (1, 2, 3, 4, 5)

# One-liner (doesn't preserve order)
print(tuple(set(t)))
```

**Output:**
```
(1, 2, 3, 4, 5)
```

---

### Program 4: Flatten a Nested Tuple

```python
def flatten(t):
    result = []
    for item in t:
        if isinstance(item, tuple):
            result.extend(flatten(item))
        else:
            result.append(item)
    return tuple(result)

nested = (1, (2, 3), (4, (5, 6)), 7)
print(flatten(nested))              # (1, 2, 3, 4, 5, 6, 7)
```

**Output:**
```
(1, 2, 3, 4, 5, 6, 7)
```

---

### Program 5: Check if a Tuple is Palindrome

```python
def is_palindrome(t):
    return t == t[::-1]

t1 = (1, 2, 3, 2, 1)
t2 = (1, 2, 3, 4, 5)
print(is_palindrome(t1))    # True
print(is_palindrome(t2))    # False
```

**Output:**
```
True
False
```

---

### Program 6: Concatenate Two Tuples Without + Operator

```python
def concat_tuples(t1, t2):
    return tuple(list(t1) + list(t2))

t1 = (1, 2, 3)
t2 = (4, 5, 6)
print(concat_tuples(t1, t2))        # (1, 2, 3, 4, 5, 6)
```

**Output:**
```
(1, 2, 3, 4, 5, 6)
```

---

### Program 7: Sort Tuple of Tuples by Second Element

```python
students = (("Alice", 85), ("Bob", 92), ("Charlie", 78), ("David", 92))

# Sort by score descending, then name ascending
sorted_students = tuple(sorted(students, key=lambda x: (-x[1], x[0])))

for name, score in sorted_students:
    print(f"{name}: {score}")
```

**Output:**
```
Bob: 92
David: 92
Alice: 85
Charlie: 78
```

---

### Program 8: Count Frequency of Each Element

```python
def count_frequency(t):
    freq = {}
    for item in t:
        freq[item] = freq.get(item, 0) + 1
    return freq

t = (1, 2, 3, 2, 1, 4, 1, 2, 5)
freq = count_frequency(t)
for k, v in sorted(freq.items()):
    print(f"{k} → {v} times")
```

**Output:**
```
1 → 3 times
2 → 3 times
3 → 1 times
4 → 1 times
5 → 1 times
```

---

### Program 9: Find Common Elements Between Two Tuples

```python
def common_elements(t1, t2):
    return tuple(set(t1) & set(t2))

t1 = (1, 2, 3, 4, 5)
t2 = (3, 4, 5, 6, 7)
print(common_elements(t1, t2))      # (3, 4, 5) — order may vary

# Preserving order of t1
def common_ordered(t1, t2):
    s2 = set(t2)
    return tuple(x for x in t1 if x in s2)

print(common_ordered(t1, t2))       # (3, 4, 5)
```

**Output:**
```
(3, 4, 5)
(3, 4, 5)
```

---

### Program 10: Convert Tuple to Dictionary (Paired Tuples)

```python
keys = ("name", "age", "city")
values = ("Alex", 30, "Hyderabad")

# Method 1: zip
result = dict(zip(keys, values))
print(result)       # {'name': 'Alex', 'age': 30, 'city': 'Hyderabad'}

# Method 2: from tuple of pairs
pairs = (("a", 1), ("b", 2), ("c", 3))
d = dict(pairs)
print(d)            # {'a': 1, 'b': 2, 'c': 3}
```

**Output:**
```
{'name': 'Alex', 'age': 30, 'city': 'Hyderabad'}
{'a': 1, 'b': 2, 'c': 3}
```

---

### Program 11: Sum of All Elements in Nested Tuple

```python
def nested_sum(t):
    total = 0
    for item in t:
        if isinstance(item, tuple):
            total += nested_sum(item)
        else:
            total += item
    return total

t = (1, (2, 3), (4, (5, 6)), 7)
print(nested_sum(t))    # 28   (1+2+3+4+5+6+7)
```

**Output:**
```
28
```

---

### Program 12: Rotate a Tuple by k Positions

```python
def rotate_tuple(t, k):
    n = len(t)
    k = k % n           # Handle k > len(t)
    return t[k:] + t[:k]

t = (1, 2, 3, 4, 5)
print(rotate_tuple(t, 2))      # (3, 4, 5, 1, 2)
print(rotate_tuple(t, -1))     # (5, 1, 2, 3, 4)  — rotate right by 1
```

**Output:**
```
(3, 4, 5, 1, 2)
(5, 1, 2, 3, 4)
```

---

### Program 13: Find Second Largest Element

```python
def second_largest(t):
    unique = tuple(set(t))
    if len(unique) < 2:
        return None
    sorted_t = sorted(unique, reverse=True)
    return sorted_t[1]

t = (3, 1, 4, 1, 5, 9, 2, 6, 5)
print(second_largest(t))        # 6
```

**Output:**
```
6
```

---

### Program 14: Zip Multiple Tuples and Unzip

```python
# Zipping
names  = ("Alice", "Bob", "Charlie")
scores = (85, 92, 78)
grades = ("B", "A", "C")

zipped = tuple(zip(names, scores, grades))
print(zipped)
# (('Alice', 85, 'B'), ('Bob', 92, 'A'), ('Charlie', 78, 'C'))

# Unzipping using * (splat operator)
n, s, g = zip(*zipped)
print(n)    # ('Alice', 'Bob', 'Charlie')
print(s)    # (85, 92, 78)
print(g)    # ('B', 'A', 'C')
```

**Output:**
```
(('Alice', 85, 'B'), ('Bob', 92, 'A'), ('Charlie', 78, 'C'))
('Alice', 'Bob', 'Charlie')
(85, 92, 78)
('B', 'A', 'C')
```

---

### Program 15: Check if One Tuple is a Subset of Another

```python
def is_subset(t1, t2):
    """Check if t1 is a subset of t2 (all elements of t1 exist in t2)"""
    return set(t1).issubset(set(t2))

t1 = (1, 2, 3)
t2 = (1, 2, 3, 4, 5)
t3 = (1, 2, 6)

print(is_subset(t1, t2))    # True  — t1 ⊆ t2
print(is_subset(t3, t2))    # False — 6 not in t2

# With duplicates preserved logic
def is_multiset_subset(t1, t2):
    from collections import Counter
    c1, c2 = Counter(t1), Counter(t2)
    return all(c2[k] >= v for k, v in c1.items())

print(is_multiset_subset((1, 1, 2), (1, 1, 2, 3)))   # True
print(is_multiset_subset((1, 1, 2), (1, 2, 3)))       # False — only one 1 in t2
```

**Output:**
```
True
False
True
False
```

---

## 14. Summary

| Topic | Key Points |
|-------|-----------|
| **Definition** | Ordered, immutable sequence |
| **Creation** | `()`, `tuple()`, packing, `(x,)` for single element |
| **Indexing** | Zero-based; negative indexing from end |
| **Slicing** | `t[start:stop:step]`; returns new tuple |
| **`+` operator** | Concatenation — creates new tuple |
| **`*` operator** | Repetition — creates new tuple |
| **`in` / `not in`** | Membership check — O(n) |
| **Comparisons** | Element-wise left to right |
| **Built-ins** | `len`, `max`, `min`, `sum`, `sorted`, `enumerate`, `zip` |
| **Iteration** | `for`, `while`, `enumerate`, comprehension via `tuple(gen)` |
| **`count()`** | Count occurrences of a value |
| **`index()`** | Find first occurrence index; raises `ValueError` if absent |
| **Packing** | `a, b, c = 1, 2, 3` — auto-tuple |
| **Unpacking** | `x, y, z = t`; extended with `*rest` |
| **vs List** | Tuple: immutable, faster, less memory, hashable |

### Immutability Clarification

```python
# Tuple itself is immutable — but mutable objects inside CAN change
t = ([1, 2], [3, 4])
t[0].append(99)         # This works! The list object is mutable
print(t)                # ([1, 2, 99], [3, 4])
# But t[0] = [5, 6] would fail — you can't rebind the reference
```

---

## 15. Self-Study Exercises

### Level 1 — Basic

1. Create a tuple of 7 days of the week. Print the 1st day and last day using indexing.
2. Create a tuple `(10, 20, 30, 40, 50)`. Slice and print elements from index 1 to 3.
3. Create a single-element tuple containing your name. Verify it is of type `tuple`.
4. Write a program to check if a given number exists in a tuple of 10 numbers.
5. Create two tuples and concatenate them. Then repeat the result 3 times.

### Level 2 — Intermediate

6. Write a function that takes a tuple of numbers and returns a new tuple containing only the even numbers.
7. Given a tuple `(5, 3, 8, 1, 9, 2, 7)`, sort it in descending order without using the built-in `sort()` method on the tuple directly.
8. Write a program to find how many times a given element appears in a tuple — without using `count()`.
9. Unpack a tuple `(city, country, pin) = ("Hyderabad", "India", 500001)` and print each value on a separate line.
10. Write a function that merges two tuples and removes duplicate values, preserving the order of first occurrence.

### Level 3 — Advanced

11. Write a program that takes a tuple of (name, marks) pairs and prints the top 3 students sorted by marks in descending order.
12. Create a tuple of tuples representing a 3×3 matrix. Write code to print it row-by-row and compute the sum of the main diagonal.
13. Write a function `deep_count(t, val)` that counts occurrences of `val` even inside nested tuples.
14. Implement a function that converts a flat tuple into a list of 2-element tuples: `(1, 2, 3, 4)` → `((1, 2), (3, 4))`.
15. Write a program using `zip()` and unpacking that takes two tuples of equal length (keys and values) and creates a dictionary, then prints keys sorted alphabetically.

---

*End of Week-02 Day-08 — Python Tuples*
