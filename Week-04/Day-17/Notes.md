# Python Full Stack Foundation

# Week-04 – Day-17

# `random` Module & `datetime` Module

## Learning Objectives

By the end of this session, learners will be able to:

* Understand Python's `random` module
* Generate random numbers
* Select random elements
* Shuffle data
* Understand the `datetime` module
* Get the current date and time
* Format dates and times
* Perform date arithmetic
* Build real-world date and time applications

---

# 1. What is a Module?

A **module** is a Python file containing reusable functions, classes, and variables.

Examples:

* `math`
* `os`
* `random`
* `datetime`

---

# 2. random Module

## What is the `random` Module?

The `random` module is used to generate random numbers and make random selections.

```python
import random
```

---

## random()

Returns a random floating-point number between **0.0** and **1.0**.

```python
import random

print(random.random())
```

Example Output

```
0.673214
```

---

## randint()

Returns a random integer within the given range.

```python
import random

print(random.randint(1,10))
```

Example Output

```
7
```

---

## randrange()

Returns a random number from a range.

```python
import random

print(random.randrange(1,20,2))
```

Example Output

```
15
```

---

## uniform()

Returns a random floating-point number.

```python
import random

print(random.uniform(1,10))
```

Example Output

```
5.73
```

---

## choice()

Returns one random element from a sequence.

```python
import random

subjects = ["Python","SQL","HTML","CSS"]

print(random.choice(subjects))
```

Example Output

```
SQL
```

---

## choices()

Returns multiple random elements (duplicates possible).

```python
import random

colors = ["Red","Blue","Green"]

print(random.choices(colors,k=5))
```

Example Output

```
['Blue', 'Red', 'Blue', 'Green', 'Blue']
```

---

## sample()

Returns unique random elements.

```python
import random

numbers = [10,20,30,40,50]

print(random.sample(numbers,3))
```

Example Output

```
[20, 50, 10]
```

---

## shuffle()

Randomly rearranges a list.

```python
import random

numbers = [1,2,3,4,5]

random.shuffle(numbers)

print(numbers)
```

Example Output

```
[4, 1, 5, 3, 2]
```

---

# Common `random` Functions

| Function      | Purpose                  |
| ------------- | ------------------------ |
| `random()`    | Random float             |
| `randint()`   | Random integer           |
| `randrange()` | Random number from range |
| `uniform()`   | Random decimal number    |
| `choice()`    | One random item          |
| `choices()`   | Multiple random items    |
| `sample()`    | Unique random items      |
| `shuffle()`   | Shuffle list             |

---

# Real-World Examples

## Roll a Dice

```python
import random

print(random.randint(1,6))
```

---

## Toss a Coin

```python
import random

print(random.choice(["Head","Tail"]))
```

---

## Random OTP

```python
import random

otp = random.randint(1000,9999)

print(otp)
```

---

## Random Password Character

```python
import random

chars = "ABCDEFGHIJKLMNOPQRSTUVWXYZ0123456789"

print(random.choice(chars))
```

---

# 3. datetime Module

## What is the `datetime` Module?

The `datetime` module is used to work with dates and times.

```python
import datetime
```

---

## Current Date and Time

```python
import datetime

now = datetime.datetime.now()

print(now)
```

Example Output

```
2026-07-10 19:45:20.345678
```

---

## Current Date

```python
import datetime

print(datetime.date.today())
```

Example Output

```
2026-07-10
```

---

## Current Time

```python
import datetime

print(datetime.datetime.now().time())
```

Example Output

```
19:45:20.345678
```

---

## Create a Date

```python
import datetime

d = datetime.date(2026,7,10)

print(d)
```

Output

```
2026-07-10
```

---

## Create Date and Time

```python
import datetime

dt = datetime.datetime(2026,7,10,19,30,0)

print(dt)
```

Output

```
2026-07-10 19:30:00
```

---

## Access Date Components

```python
import datetime

today = datetime.datetime.now()

print(today.year)
print(today.month)
print(today.day)
```

Output

```
2026
7
10
```

---

## Access Time Components

```python
import datetime

now = datetime.datetime.now()

print(now.hour)
print(now.minute)
print(now.second)
```

---

## Format Date

### `strftime()`

```python
import datetime

today = datetime.datetime.now()

print(today.strftime("%d-%m-%Y"))
```

Output

```
10-07-2026
```

---

## Common Format Codes

| Code | Meaning         | Example |
| ---- | --------------- | ------- |
| `%d` | Day             | 10      |
| `%m` | Month           | 07      |
| `%Y` | Year            | 2026    |
| `%y` | Year (2 digits) | 26      |
| `%H` | Hour (24-hour)  | 19      |
| `%I` | Hour (12-hour)  | 07      |
| `%M` | Minute          | 45      |
| `%S` | Second          | 20      |
| `%A` | Weekday         | Friday  |
| `%B` | Month Name      | July    |

---

## Parse String to Date

### `strptime()`

```python
from datetime import datetime

date = datetime.strptime("15-08-2026","%d-%m-%Y")

print(date)
```

Output

```
2026-08-15 00:00:00
```

---

## Date Arithmetic

### `timedelta`

```python
from datetime import datetime, timedelta

today = datetime.now()

future = today + timedelta(days=10)

print(future)
```

---

## Yesterday

```python
from datetime import datetime, timedelta

print(datetime.now() - timedelta(days=1))
```

---

## Tomorrow

```python
from datetime import datetime, timedelta

print(datetime.now() + timedelta(days=1))
```

---

## Difference Between Two Dates

```python
from datetime import date

d1 = date(2026,1,1)

d2 = date(2026,1,20)

print(d2 - d1)
```

Output

```
19 days, 0:00:00
```

---

# Real-World Programs

## Calculate Age (Approximate)

```python
from datetime import date

birth = date(2000,5,15)

today = date.today()

print(today.year - birth.year)
```

---

## Print Current Date and Time

```python
from datetime import datetime

print(datetime.now())
```

---

## Display Date in DD/MM/YYYY Format

```python
from datetime import datetime

print(datetime.now().strftime("%d/%m/%Y"))
```

---

# Quick Summary

| Module     | Common Functions                                                                         |
| ---------- | ---------------------------------------------------------------------------------------- |
| `random`   | `random()`, `randint()`, `randrange()`, `choice()`, `choices()`, `sample()`, `shuffle()` |
| `datetime` | `now()`, `today()`, `date()`, `datetime()`, `strftime()`, `strptime()`, `timedelta()`    |

---

# Homework

1. Generate a random number between 1 and 100.
2. Simulate rolling a dice.
3. Simulate tossing a coin.
4. Generate a 6-digit OTP.
5. Print today's date.
6. Print the current time.
7. Display the current date in `DD-MM-YYYY` format.
8. Find tomorrow's date.
9. Find yesterday's date.
10. Calculate the number of days between two dates.

---

# Session Summary

Today we learned:

✔ `random` Module

✔ `random()`

✔ `randint()`

✔ `choice()`

✔ `sample()`

✔ `shuffle()`

✔ `datetime` Module

✔ Current Date & Time

✔ Date Formatting

✔ Date Arithmetic

✔ Real-World Examples

---

# Next Session Preview

