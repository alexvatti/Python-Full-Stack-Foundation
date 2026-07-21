# Python `math` Module – Real-World Examples

The Python **`math`** module provides mathematical functions and constants that are commonly used in engineering, finance, science, gaming, and day-to-day programming.

```python
import math
```

---

# 1. Area of a Circle

### Problem
Find the area of a circular garden with a radius of **7 meters**.

### Formula

\[
Area = \pi r^2
\]

```python
import math

radius = 7

area = math.pi * radius ** 2

print("Area =", area)
```

**Output**

```
Area = 153.93804002589985
```

---

# 2. Circumference of a Circle

### Problem
Find the circumference of a circular playground having a radius of **10 meters**.

### Formula

\[
Circumference = 2\pi r
\]

```python
import math

radius = 10

circumference = 2 * math.pi * radius

print(circumference)
```

---

# 3. Distance Between Two Points

### Problem
Find the straight-line distance between two GPS locations.

### Formula

\[
Distance=\sqrt{(x_2-x_1)^2+(y_2-y_1)^2}
\]

```python
import math

x1, y1 = 2, 3
x2, y2 = 8, 10

distance = math.sqrt((x2 - x1) ** 2 + (y2 - y1) ** 2)

print(distance)
```

---

# 4. Building Height Using Trigonometry

### Problem
A ladder **15 meters** long leans against a wall making an angle of **60°**.

Find the height reached.

### Formula

\[
Height = Ladder \times \sin(\theta)
\]

```python
import math

ladder = 15
angle = 60

height = ladder * math.sin(math.radians(angle))

print(round(height, 2))
```

**Output**

```
12.99
```

---

# 5. Ramp Length Calculation

### Problem

A building entrance is **1.2 meters** above ground.

Ramp angle = **20°**

Find the ramp length.

```python
import math

height = 1.2

length = height / math.sin(math.radians(20))

print(round(length, 2))
```

---

# 6. Compound Interest

### Problem

Calculate the final amount after **3 years**.

- Principal = ₹100000
- Rate = 8%

### Formula

\[
A=P(1+\frac{R}{100})^T
\]

```python
import math

P = 100000
R = 8
T = 3

amount = P * math.pow((1 + R / 100), T)

print(round(amount, 2))
```

---

# 7. Round Marks Up

### Problem

Round a student's marks upward.

```python
import math

marks = 67.2

print(math.ceil(marks))
```

**Output**

```
68
```

---

# 8. Round Salary Down

### Problem

Round a salary down to the nearest integer.

```python
import math

salary = 25489.99

print(math.floor(salary))
```

**Output**

```
25489
```

---

# 9. Square Root

### Problem

Find the side of a square whose area is **196 sq.units**.

```python
import math

area = 196

side = math.sqrt(area)

print(side)
```

---

# 10. Cube Root

### Problem

Find the cube root of **125**.

```python
number = 125

cube_root = number ** (1 / 3)

print(cube_root)
```

---

# 11. Maximum Height of a Projectile

### Formula

\[
H=\frac{u^2\sin^2\theta}{2g}
\]

```python
import math

u = 40
theta = 45
g = 9.8

height = (u ** 2 * math.sin(math.radians(theta)) ** 2) / (2 * g)

print(round(height, 2))
```

---

# 12. Temperature Conversion

### Problem

Convert **36.5°C** into Fahrenheit.

```python
celsius = 36.5

fahrenheit = (celsius * 9 / 5) + 32

print(fahrenheit)
```

---

# 13. Hypotenuse of a Triangle

### Problem

Find the hypotenuse when

- Base = 6
- Height = 8

```python
import math

base = 6
height = 8

hypotenuse = math.hypot(base, height)

print(hypotenuse)
```

**Output**

```
10.0
```

---

# 14. Find Angle Using atan()

### Problem

Calculate the angle of elevation.

```python
import math

opposite = 10
adjacent = 5

angle = math.degrees(math.atan(opposite / adjacent))

print(round(angle, 2))
```

---

# 15. Student Arrangement

### Problem

Find the number of ways to arrange **6 students**.

```python
import math

students = 6

print(math.factorial(students))
```

**Output**

```
720
```

---

# 16. Greatest Common Divisor (GCD)

### Problem

Two gears have **48** and **60** teeth.

```python
import math

print(math.gcd(48, 60))
```

**Output**

```
12
```

---

# 17. Least Common Multiple (LCM)

```python
import math

print(math.lcm(48, 60))
```

**Output**

```
240
```

---

# 18. Logarithm

### Problem

Find the base-10 logarithm of **1000**.

```python
import math

number = 1000

print(math.log10(number))
```

**Output**

```
3.0
```

---

# 19. Exponential Growth

### Problem

Calculate the value of \(e^2\).

```python
import math

growth = math.exp(2)

print(growth)
```

---

# 20. Robot Navigation

### Problem

Find the distance between a robot and its target.

```python
import math

robot_x = 5
robot_y = 8

target_x = 20
target_y = 15

distance = math.dist([robot_x, robot_y], [target_x, target_y])

print(distance)
```

---

# 21. Wind Direction Using atan2()

### Problem

Determine the direction angle from x and y coordinates.

```python
import math

x = 4
y = 7

angle = math.degrees(math.atan2(y, x))

print(round(angle, 2))
```

---

# 22. Packaging Problem

### Problem

Pack **53** items into boxes that hold **8** items each.

```python
import math

items = 53
capacity = 8

boxes = math.ceil(items / capacity)

print(boxes)
```

**Output**

```
7
```

---

# 23. Banking Interest

### Problem

Find the future value of ₹50,000 invested for **5 years** at **7.5%** interest.

```python
import math

principal = 50000
rate = 7.5
years = 5

future = principal * math.pow((1 + rate / 100), years)

print(round(future, 2))
```

---

# 24. Bicycle Wheel Rotation

### Problem

A bicycle wheel has a radius of **0.35 meters**.

How many rotations are required to travel **1000 meters**?

```python
import math

radius = 0.35
distance = 1000

circumference = 2 * math.pi * radius

rotations = distance / circumference

print(round(rotations))
```

---

# 25. GPS Distance

### Problem

Find the straight-line distance between home and office.

```python
import math

home = (2, 4)
office = (15, 18)

print(math.dist(home, office))
```

---

# Common `math` Module Functions

| Function | Description | Example |
|----------|-------------|---------|
| `math.sqrt()` | Square root | `math.sqrt(25)` |
| `math.pow()` | Raises a number to a power | `math.pow(2,5)` |
| `math.pi` | Value of π | `math.pi` |
| `math.sin()` | Sine | `math.sin(math.radians(30))` |
| `math.cos()` | Cosine | `math.cos(math.radians(60))` |
| `math.tan()` | Tangent | `math.tan(math.radians(45))` |
| `math.ceil()` | Round upward | `math.ceil(4.2)` |
| `math.floor()` | Round downward | `math.floor(4.9)` |
| `math.factorial()` | Factorial | `math.factorial(5)` |
| `math.gcd()` | Greatest Common Divisor | `math.gcd(24,36)` |
| `math.lcm()` | Least Common Multiple | `math.lcm(24,36)` |
| `math.log()` | Natural logarithm | `math.log(10)` |
| `math.log10()` | Base-10 logarithm | `math.log10(100)` |
| `math.exp()` | Exponential function \(e^x\) | `math.exp(2)` |
| `math.hypot()` | Hypotenuse | `math.hypot(3,4)` |
| `math.dist()` | Euclidean distance | `math.dist([1,2],[4,6])` |
| `math.atan2()` | Angle from coordinates | `math.atan2(y,x)` |
| `math.radians()` | Degrees → Radians | `math.radians(90)` |
| `math.degrees()` | Radians → Degrees | `math.degrees(math.pi/2)` |

---

# Summary

The **`math`** module is widely used in:

- Engineering calculations
- Financial applications
- Scientific computing
- Computer graphics
- Robotics
- Navigation systems
- Data analysis
- Game development
- Machine learning
- Geometry and trigonometry problems

Learning these functions will help you solve real-world mathematical problems efficiently in Python.
