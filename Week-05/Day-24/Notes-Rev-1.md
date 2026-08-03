
# Operator Overloading Example using Point Objects

## Problem Statement

We have two points:

- Point 1 → `(x1, y1)`
- Point 2 → `(x2, y2)`

Find the **distance between the two points** in two different ways:

1. Using a normal class method
2. Using Operator Overloading (`-` operator)

---

# Distance Formula

The Euclidean distance between two points is

\[
Distance=\sqrt{(x_2-x_1)^2+(y_2-y_1)^2}
\]

---

# Method 1 : Using a Normal Method

```python
from math import sqrt

class Point:

    def __init__(self, x, y):
        self.x = x
        self.y = y

    def distance(self, other):
        return sqrt((self.x - other.x) ** 2 +
                    (self.y - other.y) ** 2)


# Creating Objects
p1 = Point(2, 3)
p2 = Point(5, 7)

# Calling Normal Method
d = p1.distance(p2)

print("Distance =", d)
```

### Output

```
Distance = 5.0
```

---

## How it Works

```
p1.distance(p2)

        │
        ▼

distance()

        │
        ▼

Calculates

√((x2-x1)² + (y2-y1)²)

        │
        ▼

Returns Distance
```

---

# Method 2 : Using Operator Overloading

Instead of writing

```python
p1.distance(p2)
```

we would like to write

```python
p1 - p2
```

To achieve this, overload the `-` operator using `__sub__()`.

```python
from math import sqrt

class Point:

    def __init__(self, x, y):
        self.x = x
        self.y = y

    # Operator Overloading
    def __sub__(self, other):
        return sqrt((self.x - other.x) ** 2 +
                    (self.y - other.y) ** 2)


# Creating Objects
p1 = Point(2, 3)
p2 = Point(5, 7)

# Using - Operator
d = p1 - p2

print("Distance =", d)
```

### Output

```
Distance = 5.0
```

---

# What Happens Internally?

When Python sees

```python
p1 - p2
```

it automatically converts it into

```python
p1.__sub__(p2)
```

So,

```
p1 - p2
      │
      ▼

Python calls

p1.__sub__(p2)

      │
      ▼

Calculates Distance

      │
      ▼

Returns Result
```

---

# Complete Example

```python
from math import sqrt

class Point:

    def __init__(self, x, y):
        self.x = x
        self.y = y

    # Normal Method
    def distance(self, other):
        return sqrt((self.x - other.x) ** 2 +
                    (self.y - other.y) ** 2)

    # Operator Overloading
    def __sub__(self, other):
        return sqrt((self.x - other.x) ** 2 +
                    (self.y - other.y) ** 2)


# Creating Point Objects
p1 = Point(2, 3)
p2 = Point(5, 7)

# Method 1
print("Using Normal Method")
print(p1.distance(p2))

# Method 2
print("\nUsing Operator Overloading")
print(p1 - p2)
```

### Output

```
Using Normal Method
5.0

Using Operator Overloading
5.0
```

---

# Comparison

| Normal Method | Operator Overloading |
|---------------|----------------------|
| `p1.distance(p2)` | `p1 - p2` |
| Explicit method call | Natural operator syntax |
| More typing | Cleaner and easier to read |
| Good for beginners | More Pythonic and object-oriented |

---

# Key Points

- `distance()` is a normal instance method.
- `__sub__()` overloads the **`-`** operator.
- `p1 - p2` internally calls `p1.__sub__(p2)`.
- Both approaches produce the same result.
- Operator overloading makes custom objects behave like built-in Python data types.

---

# Summary

```
Normal Method

p1.distance(p2)
        │
        ▼
Calculates Distance
        │
        ▼
Returns Result


Operator Overloading

p1 - p2
    │
    ▼
p1.__sub__(p2)
    │
    ▼
Calculates Distance
    │
    ▼
Returns Result
```
````
