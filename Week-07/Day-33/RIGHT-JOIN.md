# SQL RIGHT JOIN

## 1. What is a RIGHT JOIN?

A `RIGHT JOIN` is used to combine rows from two tables based on a related column.

The most important rule is:

> **RIGHT JOIN returns ALL rows from the RIGHT table and only matching rows from the LEFT table.**

If a row in the right table has **no matching row** in the left table, SQL still returns the right-table row, but the left-table columns contain:

```text
NULL
```

---

# 2. RIGHT JOIN Syntax

```sql
SELECT column_name(s)
FROM table1
RIGHT JOIN table2
ON table1.column_name = table2.column_name;
```

Here:

```text
table1 = LEFT TABLE
table2 = RIGHT TABLE
```

The order matters.

```sql
FROM table1
RIGHT JOIN table2
```

means:

> **Keep every row from `table2`, the RIGHT table.**

---

# 3. RIGHT JOIN and RIGHT OUTER JOIN

These two are exactly the same:

```sql
RIGHT JOIN
```

and:

```sql
RIGHT OUTER JOIN
```

The `OUTER` keyword is optional.

Therefore:

```sql
SELECT *
FROM Orders
RIGHT JOIN Employees
ON Orders.EmployeeID = Employees.EmployeeID;
```

is equivalent to:

```sql
SELECT *
FROM Orders
RIGHT OUTER JOIN Employees
ON Orders.EmployeeID = Employees.EmployeeID;
```

In practice, most SQL developers simply use:

```sql
RIGHT JOIN
```

---

# 4. RIGHT JOIN Mental Model

Think of two tables:

```text
LEFT TABLE                 RIGHT TABLE

   A                           B
+-------+                  +-------+
|       |                  |       |
|   A   |                  |   B   |
|       |                  |       |
+-------+                  +-------+
```

A RIGHT JOIN means:

```text
MATCHING LEFT ROWS
        +
ALL RIGHT ROWS
```

The entire right table is preserved.

---

# 5. RIGHT JOIN vs LEFT JOIN

This is one of the most important concepts.

## LEFT JOIN

```text
ALL LEFT
+
MATCHING RIGHT
```

Example:

```sql
FROM Customers
LEFT JOIN Orders
```

All customers are preserved.

---

## RIGHT JOIN

```text
MATCHING LEFT
+
ALL RIGHT
```

Example:

```sql
FROM Orders
RIGHT JOIN Customers
```

All customers are preserved.

Notice something interesting:

```sql
FROM Customers
LEFT JOIN Orders
```

and:

```sql
FROM Orders
RIGHT JOIN Customers
```

can produce the same logical rows because the preserved table is `Customers`.

---

# 6. Our Database

Our database contains:

| Table          | Records |
| -------------- | ------: |
| `Customers`    |      91 |
| `Categories`   |       8 |
| `Employees`    |      10 |
| `OrderDetails` |     518 |
| `Orders`       |     196 |
| `Products`     |      77 |
| `Shippers`     |       3 |
| `Suppliers`    |      29 |

For understanding `RIGHT JOIN`, we will mainly use:

```text
Orders
Employees
```

---

# 7. Orders Table

Example:

| OrderID | CustomerID | EmployeeID | OrderDate  | ShipperID |
| ------: | ---------: | ---------: | ---------- | --------: |
|   10308 |          2 |          7 | 1996-09-18 |         3 |
|   10309 |         37 |          3 | 1996-09-19 |         1 |
|   10310 |         77 |          8 | 1996-09-20 |         2 |

Important column:

```text
EmployeeID
```

---

# 8. Employees Table

Example:

| EmployeeID | LastName  | FirstName | BirthDate  |
| ---------: | --------- | --------- | ---------- |
|          1 | Davolio   | Nancy     | 1968-12-08 |
|          2 | Fuller    | Andrew    | 1952-02-19 |
|          3 | Leverling | Janet     | 1963-08-30 |

Important column:

```text
EmployeeID
```

The relationship is:

```text
Orders.EmployeeID
        =
Employees.EmployeeID
```

---

# 9. Relationship Diagram

```text
+----------------------+
|        Orders        |
+----------------------+
| PK OrderID           |
| FK CustomerID        |
| FK EmployeeID        |
| OrderDate            |
| FK ShipperID         |
+----------+-----------+
           |
           | EmployeeID
           |
           ↓
+----------------------+
|      Employees       |
+----------------------+
| PK EmployeeID        |
| LastName             |
| FirstName            |
| BirthDate            |
+----------------------+
```

---

# 10. Basic RIGHT JOIN Example

Question:

> Show all employees and any orders associated with them.

SQL:

```sql
SELECT Orders.OrderID,
       Employees.LastName,
       Employees.FirstName
FROM Orders
RIGHT JOIN Employees
ON Orders.EmployeeID = Employees.EmployeeID
ORDER BY Orders.OrderID;
```

Notice:

```text
Orders = LEFT TABLE
Employees = RIGHT TABLE
```

Therefore:

> **Every employee will be included, even if that employee has no matching order.**

---

# 11. How the RIGHT JOIN Works

Suppose we have:

### Orders

| OrderID | EmployeeID |
| ------: | ---------: |
|    1001 |          1 |
|    1002 |          2 |
|    1003 |          2 |

### Employees

| EmployeeID | FirstName |
| ---------: | --------- |
|          1 | Nancy     |
|          2 | Andrew    |
|          3 | Janet     |

Now execute:

```sql
SELECT O.OrderID,
       E.EmployeeID,
       E.FirstName
FROM Orders AS O
RIGHT JOIN Employees AS E
ON O.EmployeeID = E.EmployeeID;
```

SQL checks each employee.

```text
Employee 1 → Order 1001 → MATCH
Employee 2 → Orders 1002, 1003 → MATCH
Employee 3 → No order → NO MATCH
```

Result:

| OrderID | EmployeeID | FirstName |
| ------: | ---------: | --------- |
|    1001 |          1 | Nancy     |
|    1002 |          2 | Andrew    |
|    1003 |          2 | Andrew    |
|    NULL |          3 | Janet     |

Janet remains in the result.

Why?

Because:

```text
Employees = RIGHT TABLE
```

and RIGHT JOIN preserves every employee.

---

# 12. Why Does NULL Appear?

Employee `3` has no matching order.

But RIGHT JOIN must keep employee `3`.

Therefore:

| OrderID | EmployeeID | FirstName |
| ------: | ---------: | --------- |
|    NULL |          3 | Janet     |

The `NULL` belongs to the **left table**:

```text
Orders.OrderID = NULL
```

It means:

> No matching order exists for this employee.

---

# 13. The Most Important RIGHT JOIN Rule

Remember:

> **RIGHT JOIN never removes a row from the RIGHT table merely because there is no match in the LEFT table.**

For example:

```text
Employees = 10 rows
Orders    = 196 rows
```

If we write:

```sql
FROM Orders
RIGHT JOIN Employees
```

all employees are preserved.

---

# 14. One Employee Can Have Many Orders

Suppose:

### Employees

| EmployeeID | FirstName |
| ---------: | --------- |
|          1 | Nancy     |
|          2 | Andrew    |

### Orders

| OrderID | EmployeeID |
| ------: | ---------: |
|    1001 |          1 |
|    1002 |          2 |
|    1003 |          2 |
|    1004 |          2 |

RIGHT JOIN:

```sql
SELECT E.FirstName,
       O.OrderID
FROM Orders AS O
RIGHT JOIN Employees AS E
ON O.EmployeeID = E.EmployeeID;
```

Result:

| FirstName | OrderID |
| --------- | ------: |
| Nancy     |    1001 |
| Andrew    |    1002 |
| Andrew    |    1003 |
| Andrew    |    1004 |

Andrew appears multiple times.

Why?

Because:

```text
1 Employee
     ↓
Many Orders
```

This is a one-to-many relationship.

---

# 15. RIGHT JOIN With an Employee Having No Orders

Suppose:

### Employees

| EmployeeID | FirstName |
| ---------: | --------- |
|          1 | Nancy     |
|          2 | Andrew    |
|          3 | Janet     |

### Orders

| OrderID | EmployeeID |
| ------: | ---------: |
|    1001 |          1 |
|    1002 |          2 |

Janet has no orders.

RIGHT JOIN:

```sql
SELECT E.FirstName,
       O.OrderID
FROM Orders AS O
RIGHT JOIN Employees AS E
ON O.EmployeeID = E.EmployeeID;
```

Result:

| FirstName | OrderID |
| --------- | ------: |
| Nancy     |    1001 |
| Andrew    |    1002 |
| Janet     |    NULL |

Janet is preserved.

---

# 16. RIGHT JOIN vs INNER JOIN

Suppose:

### Employees

| EmployeeID | Name   |
| ---------: | ------ |
|          1 | Nancy  |
|          2 | Andrew |
|          3 | Janet  |

### Orders

| OrderID | EmployeeID |
| ------: | ---------: |
|     101 |          1 |
|     102 |          2 |

## INNER JOIN

```sql
SELECT E.Name,
       O.OrderID
FROM Orders AS O
INNER JOIN Employees AS E
ON O.EmployeeID = E.EmployeeID;
```

Result:

| Name   | OrderID |
| ------ | ------: |
| Nancy  |     101 |
| Andrew |     102 |

Janet disappears.

---

## RIGHT JOIN

```sql
SELECT E.Name,
       O.OrderID
FROM Orders AS O
RIGHT JOIN Employees AS E
ON O.EmployeeID = E.EmployeeID;
```

Result:

| Name   | OrderID |
| ------ | ------: |
| Nancy  |     101 |
| Andrew |     102 |
| Janet  |    NULL |

Janet remains.

---

# 17. RIGHT JOIN vs LEFT JOIN

These are often interchangeable by changing table order.

### LEFT JOIN

```sql
SELECT C.CustomerName,
       O.OrderID
FROM Customers AS C
LEFT JOIN Orders AS O
ON C.CustomerID = O.CustomerID;
```

Means:

```text
ALL Customers
+
Matching Orders
```

Equivalent conceptually:

```sql
SELECT C.CustomerName,
       O.OrderID
FROM Orders AS O
RIGHT JOIN Customers AS C
ON O.CustomerID = C.CustomerID;
```

Means:

```text
Matching Orders
+
ALL Customers
```

Both preserve:

```text
Customers
```

---

# 18. Important Principle

Remember:

```text
LEFT JOIN
→ Preserve the table on the LEFT

RIGHT JOIN
→ Preserve the table on the RIGHT
```

Therefore:

```text
A LEFT JOIN B
```

preserves:

```text
A
```

while:

```text
A RIGHT JOIN B
```

preserves:

```text
B
```

---

# 19. RIGHT JOIN Is Basically a Reversed LEFT JOIN

Consider:

```sql
FROM Orders
RIGHT JOIN Employees
ON Orders.EmployeeID = Employees.EmployeeID;
```

We can rewrite it as:

```sql
FROM Employees
LEFT JOIN Orders
ON Employees.EmployeeID = Orders.EmployeeID;
```

These represent the same matching logic.

Therefore:

> **RIGHT JOIN is essentially LEFT JOIN with the table order reversed.**

Because of this, many SQL developers prefer `LEFT JOIN` in most queries.

---

# 20. Why LEFT JOIN Is More Common

Both are valid:

```sql
FROM Orders
RIGHT JOIN Employees
ON Orders.EmployeeID = Employees.EmployeeID;
```

and:

```sql
FROM Employees
LEFT JOIN Orders
ON Employees.EmployeeID = Orders.EmployeeID;
```

The second is often easier to read:

```text
Employees
   ↓
LEFT JOIN
   ↓
Orders
```

because the primary/preserved table is visibly on the left.

However, `RIGHT JOIN` is still useful to understand because it appears in existing SQL queries and is part of standard SQL.

---

# 21. Using Table Aliases

Instead of:

```sql
SELECT Orders.OrderID,
       Employees.LastName,
       Employees.FirstName
FROM Orders
RIGHT JOIN Employees
ON Orders.EmployeeID = Employees.EmployeeID;
```

we can write:

```sql
SELECT O.OrderID,
       E.LastName,
       E.FirstName
FROM Orders AS O
RIGHT JOIN Employees AS E
ON O.EmployeeID = E.EmployeeID;
```

Here:

```text
O = Orders
E = Employees
```

This is easier to read.

---

# 22. RIGHT JOIN With ORDER BY

Example:

```sql
SELECT O.OrderID,
       E.LastName,
       E.FirstName
FROM Orders AS O
RIGHT JOIN Employees AS E
ON O.EmployeeID = E.EmployeeID
ORDER BY O.OrderID;
```

The result is sorted by:

```text
OrderID
```

---

# 23. RIGHT JOIN With Employee Information

We can select more columns:

```sql
SELECT O.OrderID,
       O.OrderDate,
       E.EmployeeID,
       E.FirstName,
       E.LastName
FROM Orders AS O
RIGHT JOIN Employees AS E
ON O.EmployeeID = E.EmployeeID;
```

This gives:

```text
Order
+
Employee
```

information together.

---

# 24. Finding Employees With No Orders

One of the most useful applications of RIGHT JOIN is finding unmatched records.

Question:

> Which employees have never handled an order?

Query:

```sql
SELECT E.EmployeeID,
       E.FirstName,
       E.LastName
FROM Orders AS O
RIGHT JOIN Employees AS E
ON O.EmployeeID = E.EmployeeID
WHERE O.EmployeeID IS NULL;
```

The logic is:

```text
RIGHT JOIN
     ↓
Keep ALL employees
     ↓
Look for matching orders
     ↓
Order missing?
     ↓
O.EmployeeID IS NULL
     ↓
Employee has no order
```

---

# 25. Why `IS NULL`?

We should not write:

```sql
WHERE O.EmployeeID = NULL;
```

This is incorrect.

Use:

```sql
WHERE O.EmployeeID IS NULL;
```

For NULL checking, SQL uses:

```sql
IS NULL
```

and:

```sql
IS NOT NULL
```

---

# 26. Finding Employees Who Have Orders

We can use:

```sql
SELECT E.EmployeeID,
       E.FirstName,
       E.LastName
FROM Orders AS O
RIGHT JOIN Employees AS E
ON O.EmployeeID = E.EmployeeID
WHERE O.EmployeeID IS NOT NULL;
```

This returns employees for whom a matching order exists.

However, if the goal is simply to return matching records, `INNER JOIN` is generally clearer.

---

# 27. RIGHT JOIN With Three Tables

We can join:

```text
Orders
Employees
Shippers
```

Example:

```sql
SELECT O.OrderID,
       E.FirstName,
       E.LastName,
       S.ShipperName
FROM Orders AS O
RIGHT JOIN Employees AS E
ON O.EmployeeID = E.EmployeeID
LEFT JOIN Shippers AS S
ON O.ShipperID = S.ShipperID;
```

The first JOIN guarantees all employees.

If an employee has an order, order information is available.

If that order has a matching shipper, shipper information is available.

---

# 28. RIGHT JOIN With Customers

We can also use:

```text
Orders
Customers
```

Query:

```sql
SELECT O.OrderID,
       C.CustomerName
FROM Orders AS O
RIGHT JOIN Customers AS C
ON O.CustomerID = C.CustomerID;
```

Because:

```text
Customers = RIGHT TABLE
```

all customers are retained.

Customers without orders will have:

```text
OrderID = NULL
```

---

# 29. RIGHT JOIN With Products and Categories

Suppose we want:

> Show all categories and any products belonging to them.

We can write:

```sql
SELECT P.ProductID,
       P.ProductName,
       C.CategoryID,
       C.CategoryName
FROM Products AS P
RIGHT JOIN Categories AS C
ON P.CategoryID = C.CategoryID;
```

Here:

```text
Products = LEFT
Categories = RIGHT
```

Therefore:

```text
ALL CATEGORIES
+
MATCHING PRODUCTS
```

If a category has no products:

```text
ProductID = NULL
ProductName = NULL
```

but the category remains.

---

# 30. RIGHT JOIN With Products and Suppliers

Question:

> Show every supplier and any products supplied by them.

```sql
SELECT P.ProductID,
       P.ProductName,
       S.SupplierID,
       S.SupplierName
FROM Products AS P
RIGHT JOIN Suppliers AS S
ON P.SupplierID = S.SupplierID;
```

Because:

```text
Suppliers = RIGHT TABLE
```

all suppliers remain.

If a supplier has no matching product:

```text
ProductID = NULL
ProductName = NULL
```

---

# 31. RIGHT JOIN With Shippers

Question:

> Show every shipper and the orders associated with each shipper.

```sql
SELECT O.OrderID,
       O.OrderDate,
       S.ShipperID,
       S.ShipperName
FROM Orders AS O
RIGHT JOIN Shippers AS S
ON O.ShipperID = S.ShipperID;
```

This preserves all three shippers.

If a shipper has no matching order:

```text
OrderID = NULL
```

---

# 32. RIGHT JOIN With Categories

Our database has:

```text
Categories = 8
Products = 77
```

Suppose the requirement is:

> Show all 8 categories, including categories that have no products.

Use:

```sql
SELECT C.CategoryID,
       C.CategoryName,
       P.ProductID,
       P.ProductName
FROM Products AS P
RIGHT JOIN Categories AS C
ON P.CategoryID = C.CategoryID;
```

Because `Categories` is on the right:

```text
ALL CATEGORIES
```

are preserved.

---

# 33. RIGHT JOIN and One-to-Many Relationships

The relationship:

```text
Employees
    1
    |
    +----< Orders
             Many
```

means:

```text
1 Employee
   ↓
Many Orders
```

When we write:

```sql
FROM Orders
RIGHT JOIN Employees
ON Orders.EmployeeID = Employees.EmployeeID;
```

one employee can appear many times.

Example:

```text
Employee Andrew
    |
    +--- Order 1001
    +--- Order 1002
    +--- Order 1003
```

Result:

| Employee | Order |
| -------- | ----: |
| Andrew   |  1001 |
| Andrew   |  1002 |
| Andrew   |  1003 |

This is expected.

---

# 34. RIGHT JOIN Does Not Mean One Row Per Right Table Row

A common beginner misunderstanding is:

> "RIGHT JOIN returns exactly one row for every right-table row."

Not necessarily.

If one right-table row matches multiple left-table rows, it can appear multiple times.

For example:

```text
Employee 1
    ↓
Order 101
Order 102
Order 103
```

The employee appears three times.

The correct rule is:

> **Every right-table row is preserved, but matching relationships can create multiple result rows.**

---

# 35. RIGHT JOIN and NULL

For:

```sql
FROM Orders
RIGHT JOIN Employees
ON Orders.EmployeeID = Employees.EmployeeID;
```

if an employee has no order:

```text
Orders columns = NULL
Employees columns = actual values
```

Example:

| OrderID | EmployeeID | FirstName |
| ------: | ---------: | --------- |
|    NULL |          5 | Steven    |

This means:

```text
Employee 5 exists
BUT
no matching Order exists
```

---

# 36. LEFT JOIN vs RIGHT JOIN — Direct Comparison

| Concept                  | LEFT JOIN                       | RIGHT JOIN                     |
| ------------------------ | ------------------------------- | ------------------------------ |
| Preserves                | Left table                      | Right table                    |
| Matching rows            | Included                        | Included                       |
| Unmatched preserved rows | Included                        | Included                       |
| NULL appears on          | Right side                      | Left side                      |
| Equivalent opposite form | RIGHT JOIN with reversed tables | LEFT JOIN with reversed tables |

---

# 37. Same Result Using LEFT JOIN

RIGHT JOIN:

```sql
SELECT O.OrderID,
       E.FirstName,
       E.LastName
FROM Orders AS O
RIGHT JOIN Employees AS E
ON O.EmployeeID = E.EmployeeID;
```

Equivalent LEFT JOIN:

```sql
SELECT O.OrderID,
       E.FirstName,
       E.LastName
FROM Employees AS E
LEFT JOIN Orders AS O
ON E.EmployeeID = O.EmployeeID;
```

Both mean:

```text
ALL EMPLOYEES
+
MATCHING ORDERS
```

The second form is often easier to understand.

---

# 38. A Very Important Learning Trick

Whenever you see:

```sql
A RIGHT JOIN B
```

mentally rewrite it as:

```sql
B LEFT JOIN A
```

Example:

```sql
Orders RIGHT JOIN Employees
```

Think:

```text
Employees LEFT JOIN Orders
```

Now it becomes easier to remember:

```text
RIGHT JOIN
→ Preserve RIGHT

LEFT JOIN
→ Preserve LEFT
```

---

# 39. RIGHT JOIN Decision Method

When you see a question:

> Show all employees, including employees who have no orders.

Ask:

```text
What must never disappear?
```

Answer:

```text
Employees
```

Therefore, `Employees` must be the preserved table.

You can write:

```sql
FROM Orders
RIGHT JOIN Employees
```

or preferably:

```sql
FROM Employees
LEFT JOIN Orders
```

Both preserve employees.

---

# 40. RIGHT JOIN Example From the Given Data

Given:

### Orders

| OrderID | EmployeeID |
| ------: | ---------: |
|   10308 |          7 |
|   10309 |          3 |
|   10310 |          8 |

### Employees

| EmployeeID | LastName  | FirstName |
| ---------: | --------- | --------- |
|          1 | Davolio   | Nancy     |
|          2 | Fuller    | Andrew    |
|          3 | Leverling | Janet     |

Query:

```sql
SELECT O.OrderID,
       E.LastName,
       E.FirstName
FROM Orders AS O
RIGHT JOIN Employees AS E
ON O.EmployeeID = E.EmployeeID
ORDER BY O.OrderID;
```

The employee rows are preserved even if no order matches.

For employees `1` and `2`, if there are no matching orders in the relevant data:

```text
OrderID = NULL
```

while their employee information remains.

---

# 41. RIGHT JOIN + IS NULL

This pattern is important:

```sql
SELECT E.*
FROM Orders AS O
RIGHT JOIN Employees AS E
ON O.EmployeeID = E.EmployeeID
WHERE O.EmployeeID IS NULL;
```

Read it as:

> **Give me employees that do not have a matching order.**

Conceptually:

```text
ALL Employees
      ↓
Find Orders
      ↓
No Order?
      ↓
IS NULL
      ↓
Return Employee
```

---

# 42. RIGHT JOIN + IS NOT NULL

Opposite:

```sql
SELECT E.*
FROM Orders AS O
RIGHT JOIN Employees AS E
ON O.EmployeeID = E.EmployeeID
WHERE O.EmployeeID IS NOT NULL;
```

Meaning:

> Give me employees that have at least one matching order.

Again, `INNER JOIN` may be more natural if you only want matching records.

---

# 43. RIGHT JOIN With Aggregation

RIGHT JOIN can be useful for reporting.

Question:

> Show every employee and the number of orders handled by each employee.

```sql
SELECT E.EmployeeID,
       E.FirstName,
       E.LastName,
       COUNT(O.OrderID) AS OrderCount
FROM Orders AS O
RIGHT JOIN Employees AS E
ON O.EmployeeID = E.EmployeeID
GROUP BY E.EmployeeID,
         E.FirstName,
         E.LastName;
```

Employees with no orders can appear with:

```text
OrderCount = 0
```

because:

```sql
COUNT(O.OrderID)
```

does not count NULL.

---

# 44. Equivalent LEFT JOIN Aggregation

The same report can be written more naturally as:

```sql
SELECT E.EmployeeID,
       E.FirstName,
       E.LastName,
       COUNT(O.OrderID) AS OrderCount
FROM Employees AS E
LEFT JOIN Orders AS O
ON E.EmployeeID = O.EmployeeID
GROUP BY E.EmployeeID,
         E.FirstName,
         E.LastName;
```

This is why `LEFT JOIN` is often preferred.

The preserved table is visually obvious:

```text
Employees
   ↓
LEFT JOIN
   ↓
Orders
```

---

# 45. RIGHT JOIN and WHERE — Important

Be careful when adding a `WHERE` condition.

For example:

```sql
SELECT O.OrderID,
       E.FirstName
FROM Orders AS O
RIGHT JOIN Employees AS E
ON O.EmployeeID = E.EmployeeID
WHERE O.OrderDate >= '1996-01-01';
```

For employees with no orders:

```text
O.OrderDate = NULL
```

The WHERE condition will not be true.

Therefore those employees may be removed.

The key lesson:

> **A WHERE condition on the non-preserved table can eliminate the NULL rows produced by the outer join.**

---

# 46. ON vs WHERE in RIGHT JOIN

`ON` defines the relationship:

```sql
ON O.EmployeeID = E.EmployeeID
```

Meaning:

> Match orders with employees.

`WHERE` filters the final result:

```sql
WHERE ...
```

Meaning:

> Keep only rows satisfying this condition.

Remember:

```text
ON
→ How should tables match?

WHERE
→ Which result rows should remain?
```

---

# 47. RIGHT JOIN With Multiple Tables

Example:

```sql
SELECT E.EmployeeID,
       E.FirstName,
       O.OrderID,
       C.CustomerName
FROM Orders AS O
RIGHT JOIN Employees AS E
ON O.EmployeeID = E.EmployeeID
LEFT JOIN Customers AS C
ON O.CustomerID = C.CustomerID;
```

The first RIGHT JOIN ensures:

```text
ALL EMPLOYEES
```

are retained.

The later LEFT JOIN attempts to add customer information for any matching orders.

---

# 48. Practical Business Questions Using RIGHT JOIN

RIGHT JOIN can answer questions such as:

```text
Which employees have no orders?

Which categories have no products?

Which suppliers have no products?

Which shippers have no orders?

Which customers have no orders?
```

However, these can usually be written more naturally using `LEFT JOIN`.

For example:

```text
Employees without orders
```

RIGHT JOIN version:

```sql
FROM Orders
RIGHT JOIN Employees
```

LEFT JOIN version:

```sql
FROM Employees
LEFT JOIN Orders
```

Both preserve:

```text
Employees
```

---

# 49. Why Developers Often Prefer LEFT JOIN

Consider:

```sql
FROM Orders
RIGHT JOIN Employees
ON Orders.EmployeeID = Employees.EmployeeID
```

You have to mentally remember:

```text
RIGHT → Employees
```

But:

```sql
FROM Employees
LEFT JOIN Orders
ON Employees.EmployeeID = Orders.EmployeeID
```

reads naturally:

```text
Employees
    ↓
LEFT JOIN
    ↓
Orders
```

The table you want to preserve is directly visible on the left.

Therefore:

> **RIGHT JOIN is valid SQL, but LEFT JOIN is often preferred for readability and consistency.**

---

# 50. RIGHT JOIN — Simple Example

### Table A — Orders

| EmployeeID | OrderID |
| ---------: | ------: |
|          1 |     101 |
|          2 |     102 |

### Table B — Employees

| EmployeeID | Name   |
| ---------: | ------ |
|          1 | Nancy  |
|          2 | Andrew |
|          3 | Janet  |

Query:

```sql
SELECT O.OrderID,
       E.EmployeeID,
       E.Name
FROM Orders AS O
RIGHT JOIN Employees AS E
ON O.EmployeeID = E.EmployeeID;
```

Result:

| OrderID | EmployeeID | Name   |
| ------: | ---------: | ------ |
|     101 |          1 | Nancy  |
|     102 |          2 | Andrew |
|    NULL |          3 | Janet  |

The important observation:

```text
Employee 3
```

has no order, but still appears.

---

# 51. RIGHT JOIN Formula

Remember:

```text
RIGHT JOIN
=
MATCHING LEFT ROWS
+
ALL RIGHT ROWS
+
NULL FOR UNMATCHED LEFT ROWS
```

Or simply:

```text
RIGHT JOIN
=
MATCH LEFT
+
ALL RIGHT
```

---

# 52. LEFT vs RIGHT — Easy Memory Trick

```text
LEFT JOIN
     ↓
KEEP LEFT

RIGHT JOIN
     ↓
KEEP RIGHT
```

Even easier:

```text
LEFT  → Protect LEFT
RIGHT → Protect RIGHT
```

---

# 53. All Three Basic JOINs

## INNER JOIN

```sql
FROM A
INNER JOIN B
ON A.ID = B.ID;
```

Result:

```text
MATCH ONLY
```

---

## LEFT JOIN

```sql
FROM A
LEFT JOIN B
ON A.ID = B.ID;
```

Result:

```text
ALL A
+
MATCHING B
```

---

## RIGHT JOIN

```sql
FROM A
RIGHT JOIN B
ON A.ID = B.ID;
```

Result:

```text
MATCHING A
+
ALL B
```

---

# 54. Visual Comparison

```text
INNER JOIN

A        B
|        |
| MATCH  |
+---+----+
    |
 RESULT
```

```text
LEFT JOIN

A        B
|        |
| MATCH  |
+---+----+
|
| ALL A
|
```

```text
RIGHT JOIN

A        B
|        |
| MATCH  |
+---+----+
         |
         | ALL B
         |
```

---

# 55. RIGHT JOIN — Quick Reference

| Concept                     | RIGHT JOIN                       |
| --------------------------- | -------------------------------- |
| Preserved table             | Right table                      |
| Matching left rows          | Included                         |
| Matching right rows         | Included                         |
| Unmatched right rows        | Included                         |
| Unmatched left-side columns | NULL                             |
| `RIGHT OUTER JOIN`          | Same as `RIGHT JOIN`             |
| `IS NULL`                   | Can find unmatched right records |
| Reverse equivalent          | LEFT JOIN with tables reversed   |

---

# 56. RIGHT JOIN Using Our Database

### All Employees + Orders

```sql
SELECT E.EmployeeID,
       E.FirstName,
       E.LastName,
       O.OrderID,
       O.OrderDate
FROM Orders AS O
RIGHT JOIN Employees AS E
ON O.EmployeeID = E.EmployeeID;
```

### Employees Without Orders

```sql
SELECT E.EmployeeID,
       E.FirstName,
       E.LastName
FROM Orders AS O
RIGHT JOIN Employees AS E
ON O.EmployeeID = E.EmployeeID
WHERE O.EmployeeID IS NULL;
```

### All Categories + Products

```sql
SELECT C.CategoryID,
       C.CategoryName,
       P.ProductID,
       P.ProductName
FROM Products AS P
RIGHT JOIN Categories AS C
ON P.CategoryID = C.CategoryID;
```

### Categories Without Products

```sql
SELECT C.CategoryID,
       C.CategoryName
FROM Products AS P
RIGHT JOIN Categories AS C
ON P.CategoryID = C.CategoryID
WHERE P.CategoryID IS NULL;
```

### All Suppliers + Products

```sql
SELECT S.SupplierID,
       S.SupplierName,
       P.ProductID,
       P.ProductName
FROM Products AS P
RIGHT JOIN Suppliers AS S
ON P.SupplierID = S.SupplierID;
```

### Suppliers Without Products

```sql
SELECT S.SupplierID,
       S.SupplierName
FROM Products AS P
RIGHT JOIN Suppliers AS S
ON P.SupplierID = S.SupplierID
WHERE P.SupplierID IS NULL;
```

### All Shippers + Orders

```sql
SELECT S.ShipperID,
       S.ShipperName,
       O.OrderID,
       O.OrderDate
FROM Orders AS O
RIGHT JOIN Shippers AS S
ON O.ShipperID = S.ShipperID;
```

---

# 57. RIGHT JOIN — Interview Questions

## Q1. What does RIGHT JOIN return?

**Answer:**

All rows from the right table and matching rows from the left table.

---

## Q2. What happens when there is no match?

The right-table row remains, and the left-table columns contain `NULL`.

---

## Q3. Is RIGHT JOIN the same as RIGHT OUTER JOIN?

Yes.

```text
RIGHT JOIN
=
RIGHT OUTER JOIN
```

---

## Q4. Which table is preserved?

The table on the right side of:

```sql
RIGHT JOIN
```

---

## Q5. How do you find employees without orders?

```sql
SELECT E.EmployeeID,
       E.FirstName
FROM Orders AS O
RIGHT JOIN Employees AS E
ON O.EmployeeID = E.EmployeeID
WHERE O.EmployeeID IS NULL;
```

---

## Q6. Can RIGHT JOIN be rewritten using LEFT JOIN?

Yes.

```sql
Orders RIGHT JOIN Employees
```

can be rewritten as:

```sql
Employees LEFT JOIN Orders
```

with the appropriate `ON` condition.

---

# 58. Common RIGHT JOIN Mistakes

## Mistake 1 — Forgetting which table is preserved

For:

```sql
FROM Orders
RIGHT JOIN Employees
```

the preserved table is:

```text
Employees
```

not:

```text
Orders
```

---

## Mistake 2 — Using `= NULL`

Incorrect:

```sql
WHERE O.EmployeeID = NULL;
```

Correct:

```sql
WHERE O.EmployeeID IS NULL;
```

---

## Mistake 3 — Assuming one result row per employee

An employee can have many orders.

Therefore an employee can appear multiple times.

---

## Mistake 4 — Using RIGHT JOIN when LEFT JOIN is clearer

This is not technically wrong:

```sql
FROM Orders
RIGHT JOIN Employees
```

But often this is easier to read:

```sql
FROM Employees
LEFT JOIN Orders
```

---

# 59. RIGHT JOIN Decision Tree

When writing a RIGHT JOIN, ask:

```text
What records must ALWAYS appear?
             |
             ↓
Right table
             |
             ↓
RIGHT JOIN
             |
             ↓
Find related left table
             |
             ↓
Write ON condition
```

Example:

```text
Need all Employees
        ↓
Employees must be RIGHT
        ↓
FROM Orders
RIGHT JOIN Employees
        ↓
ON EmployeeID
```

---

# 60. RIGHT JOIN — Complete Pattern

### All right-side records

```sql
SELECT ...
FROM A
RIGHT JOIN B
ON A.ID = B.ID;
```

Meaning:

```text
ALL B
+
MATCHING A
```

### Find unmatched right-side records

```sql
SELECT B.*
FROM A
RIGHT JOIN B
ON A.ID = B.ID
WHERE A.ID IS NULL;
```

Meaning:

```text
B records
WITHOUT
matching A records
```

---

# 61. The Best Way to Think About RIGHT JOIN

Suppose:

```sql
FROM Orders AS O
RIGHT JOIN Employees AS E
ON O.EmployeeID = E.EmployeeID;
```

Read it in plain English:

> **Take all employees. If an employee has an order, show the order. If the employee has no order, still show the employee and put NULL for the order information.**

That is exactly what RIGHT JOIN does.

---

# 62. Final Summary

The most important concept is:

> **RIGHT JOIN preserves the entire RIGHT table.**

For:

```sql
SELECT O.OrderID,
       E.FirstName,
       E.LastName
FROM Orders AS O
RIGHT JOIN Employees AS E
ON O.EmployeeID = E.EmployeeID;
```

think:

```text
Employees
    ↓
KEEP EVERY EMPLOYEE
    ↓
Look for matching Orders
    ↓
Match found?
    ├── YES → show Order information
    └── NO  → show NULL for Order information
```

The key formula is:

```text
RIGHT JOIN
=
ALL RIGHT ROWS
+
MATCHING LEFT ROWS
+
NULL FOR UNMATCHED LEFT ROWS
```

And the most useful missing-data pattern is:

```sql
RIGHT JOIN
...
WHERE LeftTable.Key IS NULL;
```

which means:

> **Find records in the right table that have no matching record in the left table.**

---

# 63. One-Minute Revision

```text
INNER JOIN
→ Only matching rows

LEFT JOIN
→ All LEFT + matching RIGHT

RIGHT JOIN
→ Matching LEFT + all RIGHT

LEFT OUTER JOIN
→ Same as LEFT JOIN

RIGHT OUTER JOIN
→ Same as RIGHT JOIN

ON
→ Defines the relationship

IS NULL
→ Finds missing/unmatched records

RIGHT JOIN + IS NULL
→ Find right-table records with NO matching left-table record

RIGHT table
→ The table whose rows must be preserved
```

### Remember this example:

```sql
SELECT O.OrderID,
       E.LastName,
       E.FirstName
FROM Orders AS O
RIGHT JOIN Employees AS E
ON O.EmployeeID = E.EmployeeID;
```

Read it as:

> **Give me every employee, and if that employee has an order, show the order. If there is no order, still show the employee and put NULL for the order.**

One final shortcut:

```text
A RIGHT JOIN B
        ↓
B LEFT JOIN A
```

So:

> **RIGHT JOIN is essentially LEFT JOIN with the tables reversed.**
