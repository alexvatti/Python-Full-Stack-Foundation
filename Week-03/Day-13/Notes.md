# Python Full Stack Foundation

# Week-03 – Day-13

# Exception Handling in Python

---

# Learning Objectives

By the end of this session, learners will be able to:

- Understand what exceptions are
- Differentiate between syntax errors and exceptions
- Understand why exception handling is needed
- Use `try`
- Use `except`
- Handle multiple exceptions
- Use `else`
- Use `finally`
- Raise custom exceptions
- Understand common built-in exceptions
- Build robust Python programs

---

# Recap

Previously we learned:

- Functions
- Parameters
- Arguments
- Return Values
- Local and Global Variables

Today we will learn how to handle runtime errors gracefully.

---

# 1. What is an Exception?

## Definition

An **Exception** is an error that occurs while a program is running (runtime).

If not handled, the program terminates immediately.

---

## Example

```python
print(10 / 0)

print("Program Ends")
```

Output

```
ZeroDivisionError
```

The second statement never executes.

---

# Why Exception Handling?

Without Exception Handling

```
Program Starts
      ↓
Error Occurs
      ↓
Program Stops
```

With Exception Handling

```
Program Starts
      ↓
Error Occurs
      ↓
Handle Error
      ↓
Program Continues
```

---

# 2. Types of Errors

Python mainly has two types of errors.

| Error Type | Description |
|------------|-------------|
| Syntax Error | Mistake in Python syntax |
| Exception | Error during execution |

---

## Syntax Error Example

```python
if True
    print("Hello")
```

Output

```
SyntaxError
```

---

## Exception Example

```python
num = 10

print(num / 0)
```

Output

```
ZeroDivisionError
```

---

# 3. Common Built-in Exceptions

| Exception | Cause |
|-----------|-------|
| ZeroDivisionError | Divide by zero |
| NameError | Variable not defined |
| TypeError | Wrong data type |
| ValueError | Invalid value |
| IndexError | Invalid index |
| KeyError | Dictionary key missing |
| AttributeError | Invalid object attribute |
| FileNotFoundError | File does not exist |
| ModuleNotFoundError | Module not installed |
| ImportError | Import failed |
| OverflowError | Number too large |
| MemoryError | Memory exhausted |

---

# 4. try and except

## Syntax

```python
try:
    risky code
except:
    handling code
```

---

## Example

```python
try:
    print(10 / 0)

except:
    print("Cannot divide by zero")

print("Program Continues")
```

Output

```
Cannot divide by zero
Program Continues
```

---

# Flow Diagram

```
try Block
      │
 No Error?
   │       │
 Yes      No
 │         │
Skip     except
 │         │
Continue Program
```

---

# 5. Catching Specific Exceptions

Instead of catching every exception, catch specific ones.

---

## ZeroDivisionError

```python
try:
    print(10 / 0)

except ZeroDivisionError:
    print("Division by zero is not allowed.")
```

---

## ValueError

```python
try:

    age = int(input("Enter Age: "))

except ValueError:

    print("Please enter numbers only.")
```

---

## NameError

```python
try:

    print(total)

except NameError:

    print("Variable is not defined.")
```

---

## IndexError

```python
numbers = [10,20,30]

try:

    print(numbers[5])

except IndexError:

    print("Index is out of range.")
```

---

## KeyError

```python
student = {
    "name":"Alex"
}

try:

    print(student["age"])

except KeyError:

    print("Key not found.")
```

---

## FileNotFoundError

```python
try:

    file = open("sample.txt")

except FileNotFoundError:

    print("File does not exist.")
```

---

# 6. Multiple except Blocks

```python
try:

    number = int(input("Enter Number: "))

    print(100 / number)

except ValueError:

    print("Invalid Number")

except ZeroDivisionError:

    print("Cannot divide by zero")
```

---

# 7. One except for Multiple Exceptions

```python
try:

    number = int(input())

    print(100 / number)

except (ValueError, ZeroDivisionError):

    print("Invalid Input")
```

---

# 8. Generic Exception

```python
try:

    x = 10 / 0

except Exception as e:

    print(e)
```

Output

```
division by zero
```

---

# 9. else Block

Runs only when there is **no exception**.

```python
try:

    number = int(input())

except ValueError:

    print("Invalid")

else:

    print("Valid Number")
```

---

# Flow

```
try
 │
No Error
 │
else
 │
finally
```

---

# 10. finally Block

Always executes.

Used for cleanup activities.

```python
try:

    print(10/2)

except:

    print("Error")

finally:

    print("Program Finished")
```

Output

```
5.0
Program Finished
```

---

# Example with File

```python
try:

    file = open("data.txt")

except FileNotFoundError:

    print("File not found.")

finally:

    print("Closing resources.")
```

---

# 11. Complete Structure

```python
try:

    statements

except ExceptionType:

    statements

else:

    statements

finally:

    statements
```

---

# Execution Order

```
try
 │
 ├── Exception?
 │      │
 │     Yes
 │      │
 │   except
 │
 └── No
        │
      else

finally
```

---

# 12. Raising Exceptions

Python allows us to create exceptions intentionally.

## Syntax

```python
raise ExceptionType("Message")
```

---

## Example

```python
age = -5

if age < 0:

    raise ValueError("Age cannot be negative.")
```

Output

```
ValueError: Age cannot be negative.
```

---

# Example

```python
salary = -1000

if salary < 0:

    raise ValueError("Invalid Salary")
```

---

# 13. Practical Examples

## ATM Withdrawal

```python
balance = 5000

amount = int(input("Enter Amount: "))

try:

    if amount > balance:

        raise ValueError("Insufficient Balance")

    print("Transaction Successful")

except ValueError as e:

    print(e)
```

---

## Student Marks

```python
try:

    marks = int(input("Enter Marks: "))

    if marks < 0 or marks > 100:

        raise ValueError("Marks should be between 0 and 100")

    print("Valid Marks")

except ValueError as e:

    print(e)
```

---

## Login Example

```python
password = input("Enter Password: ")

try:

    if password != "admin123":

        raise ValueError("Invalid Password")

    print("Login Successful")

except ValueError as e:

    print(e)
```

---

# 14. Common Mistakes

❌ Using bare `except` everywhere

❌ Ignoring exception messages

❌ Writing important code inside `except`

❌ Forgetting `finally` for cleanup

❌ Catching `Exception` when a specific exception should be used

---

# 15. Interview Questions

1. What is an exception?
2. Difference between Syntax Error and Exception?
3. Why use exception handling?
4. Difference between `try` and `except`?
5. When does `else` execute?
6. When does `finally` execute?
7. Can multiple `except` blocks be used?
8. What is `Exception as e`?
9. What is `raise`?
10. Difference between `raise` and `except`?

---

# 16. Quick Summary

| Topic | Purpose |
|--------|---------|
| try | Risky code |
| except | Handle exception |
| else | Executes if no exception |
| finally | Always executes |
| raise | Create an exception |
| Exception as e | Capture error message |

---

# 17. Homework

1. Handle division by zero.
2. Handle invalid integer input.
3. Handle list index errors.
4. Handle missing dictionary keys.
5. Handle file not found errors.
6. Create a marks validation program.
7. Create an ATM withdrawal program.
8. Create a login validation program.
9. Raise a custom `ValueError`.
10. Write a program using `try`, `except`, `else`, and `finally`.

---

# Session Summary

Today we learned:

✔ What is an Exception

✔ Syntax Errors vs Runtime Exceptions

✔ Common Built-in Exceptions

✔ try

✔ except

✔ Multiple except Blocks

✔ Generic Exception Handling

✔ else

✔ finally

✔ raise

✔ Practical Exception Handling Programs

✔ Best Practices

---

# Next Session Preview

## Week-03 – Day-14

- Modules
- Import Statement
- Creating User-Defined Modules
- Python Standard Library
- `math` Module
- `random` Module
- `datetime` Module
- `os` Module
