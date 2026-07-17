# Python Exception Handling - Complete Beginner to Intermediate Guide

## Contents
1. What is an Exception?
2. Why Exception Handling?
3. Program Flow
4. try / except / else / finally
5. raise
6. assert
7. Custom Exceptions
8. Common Built-in Exceptions
9. What Happens if an Exception is NOT Caught?
10. Best Practices
11. 10 Practice Examples

---

## What is an Exception?

An exception is an error that occurs while a program is executing.

```python
print(10/0)
```

Output:

```
ZeroDivisionError: division by zero
```

---

## Why Exception Handling?

- Prevents program crashes
- Shows meaningful error messages
- Allows graceful recovery
- Cleans up resources

---

## Program Flow

```
Program Starts
      │
      ▼
try block
      │
      ├── No Exception ─────────► else ► finally ► Continue
      │
      └── Exception Raised
               │
      Matching except?
          │         │
         Yes       No
          │         │
      except     Program Stops
          │         │
      finally   Traceback Printed
```

---

## Basic try-except

```python
try:
    x=10/0
except ZeroDivisionError:
    print("Cannot divide by zero")
```

## try-except-else

```python
try:
    x=10/2
except ZeroDivisionError:
    print("Error")
else:
    print(x)
```

## finally

```python
try:
    f=open("demo.txt")
except FileNotFoundError:
    print("Missing")
finally:
    print("Cleanup")
```

## raise

```python
age=-5
if age<0:
    raise ValueError("Age cannot be negative")
```

## assert

```python
assert 5>0
```

## Custom Exception

```python
class AgeError(Exception):
    pass

raise AgeError("Invalid Age")
```

## What happens if Exception is NOT caught?

- Current statement stops immediately.
- Remaining statements are skipped.
- Python searches for another handler.
- If none exists, traceback is printed.
- Program terminates.

```python
print("Start")
print(10/0)
print("End")
```

Only **Start** prints.

## Common Exceptions

| Exception | Cause |
|---|---|
| ZeroDivisionError | Divide by zero |
| ValueError | Invalid value |
| TypeError | Wrong type |
| NameError | Variable missing |
| IndexError | Bad index |
| KeyError | Missing key |
| AttributeError | Missing attribute |
| FileNotFoundError | File absent |
| PermissionError | Permission denied |
| ModuleNotFoundError | Module missing |
| ImportError | Import failed |
| AssertionError | assert failed |
| MemoryError | Out of memory |
| OverflowError | Numeric overflow |
| RecursionError | Too much recursion |
| RuntimeError | Runtime problem |
| EOFError | End of input |
| KeyboardInterrupt | Ctrl+C |
| StopIteration | Iterator finished |
| UnicodeEncodeError | Encoding |
| UnicodeDecodeError | Decoding |
| TimeoutError | Timed out |
| ConnectionError | Network |
| ConnectionRefusedError | Refused |
| ConnectionResetError | Reset |
| BrokenPipeError | Pipe closed |
| OSError | OS error |

## Best Practices

- Catch specific exceptions.
- Avoid bare except.
- Use finally for cleanup.
- Log errors.
- Raise meaningful exceptions.

# 10 Practice Examples

## 1. Division
```python
try:
    print(100/0)
except ZeroDivisionError:
    print("Cannot divide by zero")
```

## 2. Integer Conversion
```python
try:
    x=int("abc")
except ValueError:
    print("Invalid integer")
```

## 3. List Index
```python
try:
    a=[1,2]
    print(a[5])
except IndexError:
    print("Index out of range")
```

## 4. Dictionary
```python
try:
    d={}
    print(d["name"])
except KeyError:
    print("Key missing")
```

## 5. File
```python
try:
    open("abc.txt")
except FileNotFoundError:
    print("File not found")
```

## 6. Multiple Exceptions
```python
try:
    x=int(input())
    print(10/x)
except (ValueError,ZeroDivisionError):
    print("Input error")
```

## 7. Generic Exception
```python
try:
    print(name)
except Exception as e:
    print(type(e).__name__,e)
```

## 8. finally
```python
try:
    print("Work")
finally:
    print("Always executes")
```

## 9. raise
```python
def withdraw(balance,amount):
    if amount>balance:
        raise ValueError("Insufficient balance")
```

## 10. Custom Exception
```python
class LoginError(Exception):
    pass

raise LoginError("Invalid credentials")
```


---

# Advanced Exception Handling

## Exception Hierarchy (Simplified)

```text
BaseException
├── SystemExit
├── KeyboardInterrupt
├── GeneratorExit
└── Exception
    ├── ArithmeticError
    │   ├── ZeroDivisionError
    │   ├── OverflowError
    │   └── FloatingPointError
    ├── LookupError
    │   ├── IndexError
    │   └── KeyError
    ├── OSError
    │   ├── FileNotFoundError
    │   ├── PermissionError
    │   └── TimeoutError
    ├── ImportError
    │   └── ModuleNotFoundError
    ├── RuntimeError
    │   ├── NotImplementedError
    │   └── RecursionError
    ├── ValueError
    ├── TypeError
    ├── NameError
    └── AttributeError
```

## Exception Chaining

```python
try:
    int("abc")
except ValueError as e:
    raise RuntimeError("Conversion failed") from e
```

## Re-raising Exceptions

```python
try:
    risky()
except Exception:
    print("Logging...")
    raise
```

## Catching Multiple Exceptions

```python
except (ValueError, TypeError) as e:
    print(e)
```

## Creating Rich Custom Exceptions

```python
class ValidationError(Exception):
    def __init__(self, field, message):
        self.field = field
        super().__init__(message)

raise ValidationError("email", "Invalid email")
```

## Logging Exceptions

```python
import logging

try:
    10/0
except Exception:
    logging.exception("Unexpected error")
```

## File Handling

```python
with open("data.txt") as f:
    print(f.read())
```

`with` automatically closes the file even when an exception occurs.

## API Example

```python
try:
    response = requests.get(url, timeout=5)
    response.raise_for_status()
except requests.Timeout:
    print("Request timed out")
except requests.RequestException as e:
    print(e)
```

## JSON Example

```python
import json

try:
    obj=json.loads(data)
except json.JSONDecodeError:
    print("Invalid JSON")
```

## Good Practices

- Catch the most specific exception first.
- Never silently ignore errors (`except: pass`) unless intentional.
- Use `finally` for cleanup.
- Use logging in production.
- Create custom exceptions for business rules.
- Re-raise exceptions after logging when appropriate.
- Keep `try` blocks small.
- Do not use exceptions for normal program flow.

## Common Interview Questions

1. Difference between syntax errors and exceptions?
2. Difference between `BaseException` and `Exception`?
3. When are `else` and `finally` executed?
4. Difference between `raise` and `assert`?
5. Why avoid `except:`?
6. What is exception chaining?
7. Why use custom exceptions?
8. Can `finally` execute after `return`? (Yes.)
9. What happens if `finally` raises another exception?
10. What is the benefit of `with`?

