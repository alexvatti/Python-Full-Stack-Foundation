# SQL FULL JOIN

## 1. What is SQL FULL JOIN?

The SQL `FULL JOIN` returns **all rows from both tables**.

It includes:

* Matching rows from both tables.
* Rows from the left table that have **no match** in the right table.
* Rows from the right table that have **no match** in the left table.

When there is no matching row:

* Columns from the left table contain `NULL` when the right-side row has no match.
* Columns from the right table contain `NULL` when the left-side row has no match.

---

# 2. FULL JOIN Meaning

```sql
FULL JOIN
```

and

```sql
FULL OUTER JOIN
```

mean exactly the same thing.

The `OUTER` keyword is optional.

Therefore:

```sql
FULL JOIN
```

is equivalent to:

```sql
FULL OUTER JOIN
```

---

# 3. Simple Understanding

Suppose we have two tables:

### Customers

| CustomerID | CustomerName        |
| ---------: | ------------------- |
|          1 | Alfreds Futterkiste |
|          2 | Ana Trujillo        |
|          3 | Antonio Moreno      |

### Orders

| OrderID | CustomerID |
| ------: | ---------: |
|   10308 |          2 |
|   10309 |         37 |
|   10310 |         77 |

The relationship is:

```text
Customers.CustomerID
        =
Orders.CustomerID
```

Now look at the data.

Customer `2` exists in both tables.

Therefore:

```text
Customer 2 → Order 10308
```

Customer `1` exists in `Customers`, but there is no order for customer `1`.

Therefore:

```text
Customer 1 → NULL
```

Customer `3` exists in `Customers`, but there is no order for customer `3`.

Therefore:

```text
Customer 3 → NULL
```

Orders `10309` and `10310` have CustomerIDs `37` and `77`.

Those customers do not exist in the selected `Customers` data.

Therefore:

```text
NULL → Order 10309
NULL → Order 10310
```

This is exactly what `FULL JOIN` is designed to show.

---

# 4. FULL JOIN Syntax

```sql
SELECT column_name(s)
FROM table1
FULL JOIN table2
ON table1.column_name = table2.column_name
WHERE condition;
```

The `WHERE` clause is optional.

A basic FULL JOIN is:

```sql
SELECT *
FROM table1
FULL JOIN table2
ON table1.id = table2.id;
```

---

# 5. FULL OUTER JOIN Syntax

The longer form is:

```sql
SELECT column_name(s)
FROM table1
FULL OUTER JOIN table2
ON table1.column_name = table2.column_name;
```

`FULL JOIN` and `FULL OUTER JOIN` are equivalent.

```sql
FULL JOIN
```

is simply the shorter version.

---

# 6. FULL JOIN Example

Consider these two tables.

## Customers Table

| CustomerID | CustomerName        | Country |
| ---------: | ------------------- | ------- |
|          1 | Alfreds Futterkiste | Germany |
|          2 | Ana Trujillo        | Mexico  |
|          3 | Antonio Moreno      | Mexico  |

## Orders Table

| OrderID | CustomerID | EmployeeID | OrderDate  | ShipperID |
| ------: | ---------: | ---------: | ---------- | --------: |
|   10308 |          2 |          7 | 1996-09-18 |         3 |
|   10309 |         37 |          3 | 1996-09-19 |         1 |
|   10310 |         77 |          8 | 1996-09-20 |         2 |

Now execute:

```sql
SELECT
    Customers.CustomerName,
    Orders.OrderID
FROM Customers
FULL JOIN Orders
ON Customers.CustomerID = Orders.CustomerID;
```

---

# 7. FULL JOIN Result

The result may look like:

| CustomerName        | OrderID |
| ------------------- | ------: |
| NULL                |   10309 |
| NULL                |   10310 |
| Alfreds Futterkiste |    NULL |
| Ana Trujillo        |   10308 |
| Antonio Moreno      |    NULL |

Let's understand every row.

---

## Row 1

```text
NULL | 10309
```

Order `10309` belongs to CustomerID `37`.

But CustomerID `37` does not exist in the Customers table.

Therefore:

```text
CustomerName = NULL
OrderID      = 10309
```

---

## Row 2

```text
NULL | 10310
```

Order `10310` belongs to CustomerID `77`.

CustomerID `77` does not exist in the Customers table.

Therefore:

```text
CustomerName = NULL
OrderID      = 10310
```

---

## Row 3

```text
Alfreds Futterkiste | NULL
```

CustomerID `1` exists in Customers.

But CustomerID `1` has no matching order.

Therefore:

```text
CustomerName = Alfreds Futterkiste
OrderID      = NULL
```

---

## Row 4

```text
Ana Trujillo | 10308
```

CustomerID `2` exists in both tables.

Therefore there is a match:

```text
CustomerID 2
      ↓
Order 10308
```

---

## Row 5

```text
Antonio Moreno | NULL
```

CustomerID `3` exists in Customers.

But there is no matching order.

Therefore:

```text
CustomerName = Antonio Moreno
OrderID      = NULL
```

---

# 8. FULL JOIN Visual Explanation

Think of the two tables as two sets.

```text
        CUSTOMERS                ORDERS

       ┌───────────┐            ┌───────────┐
       │    1      │            │    2      │
       │    2      │◄──────────►│   37      │
       │    3      │            │   77      │
       └───────────┘            └───────────┘
```

The common value is:

```text
2
```

FULL JOIN keeps:

```text
Customers only
        +
Matching rows
        +
Orders only
```

Therefore:

```text
        FULL JOIN
           ↓
 ┌───────────────────────┐
 │ Customers only        │
 │ Matching rows         │
 │ Orders only           │
 └───────────────────────┘
```

---

# 9. FULL JOIN = LEFT + RIGHT + MATCH

A useful way to remember FULL JOIN is:

```text
FULL JOIN
    =
LEFT JOIN
+
RIGHT JOIN
```

Conceptually, it returns:

```text
LEFT TABLE ONLY
       +
MATCHING ROWS
       +
RIGHT TABLE ONLY
```

Therefore:

```text
FULL JOIN
```

does not discard unmatched rows from either side.

---

# 10. Comparison of JOIN Types

| JOIN       | Matching Rows | Left Unmatched | Right Unmatched |
| ---------- | ------------- | -------------- | --------------- |
| INNER JOIN | Yes           | No             | No              |
| LEFT JOIN  | Yes           | Yes            | No              |
| RIGHT JOIN | Yes           | No             | Yes             |
| FULL JOIN  | Yes           | Yes            | Yes             |

This table is extremely important.

---

# 11. INNER JOIN vs FULL JOIN

### INNER JOIN

```sql
SELECT *
FROM Customers
INNER JOIN Orders
ON Customers.CustomerID = Orders.CustomerID;
```

Returns only customers who have matching orders.

```text
Customers        Orders

1                -
2  ────────────  2
3                -

Result:
2
```

---

### FULL JOIN

```sql
SELECT *
FROM Customers
FULL JOIN Orders
ON Customers.CustomerID = Orders.CustomerID;
```

Returns everything:

```text
Customers        Orders

1                -
2  ────────────  2
3                -
-                37
-                77
```

So:

```text
INNER JOIN → only matches

FULL JOIN → matches + unmatched from both sides
```

---

# 12. LEFT JOIN vs FULL JOIN

### LEFT JOIN

```sql
SELECT *
FROM Customers
LEFT JOIN Orders
ON Customers.CustomerID = Orders.CustomerID;
```

Keeps:

```text
ALL Customers
+
Matching Orders
```

It does not include orders that have no matching customer.

---

### FULL JOIN

```sql
SELECT *
FROM Customers
FULL JOIN Orders
ON Customers.CustomerID = Orders.CustomerID;
```

Keeps:

```text
ALL Customers
+
ALL Orders
```

Therefore:

```text
LEFT JOIN
→ protects the LEFT table

FULL JOIN
→ protects BOTH tables
```

---

# 13. RIGHT JOIN vs FULL JOIN

### RIGHT JOIN

```sql
SELECT *
FROM Customers
RIGHT JOIN Orders
ON Customers.CustomerID = Orders.CustomerID;
```

Keeps:

```text
ALL Orders
+
Matching Customers
```

---

### FULL JOIN

```sql
SELECT *
FROM Customers
FULL JOIN Orders
ON Customers.CustomerID = Orders.CustomerID;
```

Keeps:

```text
ALL Customers
+
ALL Orders
```

---

# 14. FULL JOIN with SELECT Columns

You do not have to select every column.

For example:

```sql
SELECT
    Customers.CustomerName,
    Orders.OrderID
FROM Customers
FULL JOIN Orders
ON Customers.CustomerID = Orders.CustomerID;
```

You can also select additional columns:

```sql
SELECT
    Customers.CustomerID,
    Customers.CustomerName,
    Customers.Country,
    Orders.OrderID,
    Orders.OrderDate
FROM Customers
FULL JOIN Orders
ON Customers.CustomerID = Orders.CustomerID;
```

---

# 15. FULL JOIN with WHERE

You can use a `WHERE` condition.

Example:

```sql
SELECT
    Customers.CustomerName,
    Orders.OrderID
FROM Customers
FULL JOIN Orders
ON Customers.CustomerID = Orders.CustomerID
WHERE Customers.Country = 'Mexico';
```

However, be careful with `WHERE` conditions.

A `WHERE` condition can remove rows containing `NULL`.

For example:

```sql
WHERE Customers.Country = 'Mexico'
```

will remove rows where:

```text
Customers.Country = NULL
```

Therefore, although FULL JOIN initially preserves unmatched rows, a `WHERE` condition can filter some of them out.

---

# 16. Finding Unmatched Customers

FULL JOIN can be useful for identifying customers who do not have orders.

Example:

```sql
SELECT
    Customers.CustomerID,
    Customers.CustomerName
FROM Customers
FULL JOIN Orders
ON Customers.CustomerID = Orders.CustomerID
WHERE Orders.CustomerID IS NULL;
```

This identifies customers with no matching order.

Conceptually:

```text
Customer exists
+
Order does not exist
```

---

# 17. Finding Unmatched Orders

Similarly, you can find orders that do not have a matching customer.

```sql
SELECT
    Orders.OrderID,
    Orders.CustomerID
FROM Customers
FULL JOIN Orders
ON Customers.CustomerID = Orders.CustomerID
WHERE Customers.CustomerID IS NULL;
```

This identifies orders whose CustomerID has no matching customer.

Conceptually:

```text
Order exists
+
Customer does not exist
```

---

# 18. Finding All Unmatched Records

You can find unmatched records from either table:

```sql
SELECT
    Customers.CustomerID,
    Customers.CustomerName,
    Orders.OrderID,
    Orders.CustomerID
FROM Customers
FULL JOIN Orders
ON Customers.CustomerID = Orders.CustomerID
WHERE Customers.CustomerID IS NULL
   OR Orders.CustomerID IS NULL;
```

This gives:

```text
Customer only
      OR
Order only
```

It excludes the matching rows.

---

# 19. FULL JOIN and NULL

`NULL` is an important part of FULL JOIN.

Suppose:

```text
Customers
CustomerID = 1
```

but there is no corresponding order.

The FULL JOIN result might contain:

```text
CustomerID = 1
CustomerName = Alfreds Futterkiste
OrderID = NULL
```

The `NULL` means:

> There is no matching value from the other table.

Similarly, if an order exists without a matching customer:

```text
CustomerName = NULL
OrderID = 10309
```

The `NULL` means:

> There is no matching customer record.

---

# 20. FULL JOIN with Three Tables

FULL JOIN can also be combined with additional tables.

Example:

```sql
SELECT
    Customers.CustomerName,
    Orders.OrderID,
    Shippers.ShipperName
FROM Customers
FULL JOIN Orders
ON Customers.CustomerID = Orders.CustomerID
LEFT JOIN Shippers
ON Orders.ShipperID = Shippers.ShipperID;
```

Multiple joins should be used carefully because the result can become complex.

---

# 21. FULL JOIN with Aliases

Aliases can make the query easier to read.

```sql
SELECT
    C.CustomerName,
    O.OrderID
FROM Customers AS C
FULL JOIN Orders AS O
ON C.CustomerID = O.CustomerID;
```

Here:

```text
C → Customers
O → Orders
```

Therefore:

```sql
C.CustomerName
```

means:

```sql
Customers.CustomerName
```

and:

```sql
O.OrderID
```

means:

```sql
Orders.OrderID
```

---

# 22. FULL JOIN Using Table Aliases

A more complete example:

```sql
SELECT
    C.CustomerID,
    C.CustomerName,
    O.OrderID,
    O.OrderDate
FROM Customers AS C
FULL JOIN Orders AS O
ON C.CustomerID = O.CustomerID;
```

This is usually easier to maintain than repeatedly writing full table names.

---

# 23. FULL JOIN with Multiple Conditions

A FULL JOIN can use more than one condition.

Example:

```sql
SELECT *
FROM TableA AS A
FULL JOIN TableB AS B
ON A.ID = B.ID
AND A.Country = B.Country;
```

Both conditions must be satisfied for the rows to match.

---

# 24. FULL JOIN Does Not Mean "All Columns"

This is an important point.

`FULL JOIN` does **not** mean:

```text
select every column
```

It means:

```text
keep all matching and unmatched rows from both tables
```

You still decide which columns to display using `SELECT`.

For example:

```sql
SELECT
    C.CustomerName,
    O.OrderID
FROM Customers C
FULL JOIN Orders O
ON C.CustomerID = O.CustomerID;
```

Only these two columns are displayed.

---

# 25. FULL JOIN Does Not Automatically Remove Duplicates

Suppose multiple orders belong to the same customer.

Customers:

| CustomerID | CustomerName |
| ---------: | ------------ |
|          2 | Ana Trujillo |

Orders:

| OrderID | CustomerID |
| ------: | ---------: |
|   10308 |          2 |
|   10311 |          2 |
|   10315 |          2 |

A FULL JOIN produces:

| CustomerName | OrderID |
| ------------ | ------: |
| Ana Trujillo |   10308 |
| Ana Trujillo |   10311 |
| Ana Trujillo |   10315 |

This is not a duplicate caused by FULL JOIN.

There are genuinely three matching orders.

---

# 26. FULL JOIN and One-to-Many Relationships

This is common in real databases.

For example:

```text
One Customer
      ↓
Many Orders
```

Customer:

```text
CustomerID = 2
```

Orders:

```text
10308
10311
10315
```

FULL JOIN returns:

```text
Customer 2 → Order 10308
Customer 2 → Order 10311
Customer 2 → Order 10315
```

The customer information appears on multiple result rows because there are multiple matching orders.

---

# 27. FULL JOIN Example with Simple Tables

Consider:

### Employees

| EmployeeID | EmployeeName |
| ---------: | ------------ |
|          1 | John         |
|          2 | David        |
|          3 | Sarah        |

### Salaries

| EmployeeID | Salary |
| ---------: | -----: |
|          2 |  50000 |
|          3 |  60000 |
|          4 |  70000 |

Query:

```sql
SELECT
    E.EmployeeID,
    E.EmployeeName,
    S.Salary
FROM Employees AS E
FULL JOIN Salaries AS S
ON E.EmployeeID = S.EmployeeID;
```

Result:

| EmployeeID | EmployeeName | Salary |
| ---------: | ------------ | -----: |
|          1 | John         |   NULL |
|          2 | David        |  50000 |
|          3 | Sarah        |  60000 |
|       NULL | NULL         |  70000 |

The result tells us:

```text
Employee 1
→ exists in Employees
→ no salary record

Employee 2
→ exists in both

Employee 3
→ exists in both

Employee 4
→ salary exists
→ employee record does not exist
```

This is a practical use of FULL JOIN for finding data inconsistencies.

---

# 28. FULL JOIN for Data Validation

FULL JOIN is especially useful when comparing two datasets.

For example:

```text
System A
     +
System B
```

Suppose both systems should contain the same customer records.

You can use:

```sql
SELECT
    A.CustomerID,
    A.CustomerName,
    B.CustomerID,
    B.CustomerName
FROM SystemA AS A
FULL JOIN SystemB AS B
ON A.CustomerID = B.CustomerID;
```

This allows you to identify:

```text
Records existing only in System A
Records existing only in System B
Records existing in both systems
```

Therefore FULL JOIN is useful for:

* Data migration validation
* Data synchronization
* Reconciliation
* Data-quality checking
* Comparing two datasets
* Finding missing records

---

# 29. FULL JOIN Result Concept

The easiest mental model is:

```text
                FULL JOIN

        ┌───────────────────────┐
        │                       │
        │   LEFT TABLE          │
        │                       │
        │      ┌─────────┐      │
        │      │ MATCH   │      │
        │      └─────────┘      │
        │                       │
        │             RIGHT     │
        │             TABLE     │
        │                       │
        └───────────────────────┘
```

More simply:

```text
LEFT ONLY
   +
MATCHING
   +
RIGHT ONLY
```

---

# 30. FULL JOIN vs INNER JOIN

```text
INNER JOIN

LEFT TABLE        RIGHT TABLE
     │                │
     │    MATCH       │
     └───────┬────────┘
             │
          RESULT
```

Only the intersection is returned.

FULL JOIN:

```text
FULL JOIN

LEFT ONLY
    +
MATCHING
    +
RIGHT ONLY
```

So:

```text
INNER JOIN → intersection

FULL JOIN → complete combined set
```

---

# 31. FULL JOIN vs LEFT JOIN vs RIGHT JOIN

## INNER JOIN

```sql
FROM A
INNER JOIN B
ON A.id = B.id;
```

Result:

```text
A ∩ B
```

Only matching rows.

---

## LEFT JOIN

```sql
FROM A
LEFT JOIN B
ON A.id = B.id;
```

Result:

```text
ALL A
+
matching B
```

---

## RIGHT JOIN

```sql
FROM A
RIGHT JOIN B
ON A.id = B.id;
```

Result:

```text
matching A
+
ALL B
```

---

## FULL JOIN

```sql
FROM A
FULL JOIN B
ON A.id = B.id;
```

Result:

```text
ALL A
+
ALL B
```

---

# 32. Important SQL Server Note

`FULL JOIN` is supported by SQL Server.

For example:

```sql
SELECT *
FROM Customers
FULL JOIN Orders
ON Customers.CustomerID = Orders.CustomerID;
```

You can also write:

```sql
SELECT *
FROM Customers
FULL OUTER JOIN Orders
ON Customers.CustomerID = Orders.CustomerID;
```

Both are valid.

---

# 33. Important MySQL Note

MySQL does **not** have a native `FULL JOIN` / `FULL OUTER JOIN` syntax.

Therefore this will not work directly in MySQL:

```sql
SELECT *
FROM Customers
FULL JOIN Orders
ON Customers.CustomerID = Orders.CustomerID;
```

A common workaround is to combine:

```text
LEFT JOIN
+
RIGHT JOIN
```

using `UNION`.

Example:

```sql
SELECT
    C.CustomerID,
    C.CustomerName,
    O.OrderID
FROM Customers AS C
LEFT JOIN Orders AS O
ON C.CustomerID = O.CustomerID

UNION

SELECT
    C.CustomerID,
    C.CustomerName,
    O.OrderID
FROM Customers AS C
RIGHT JOIN Orders AS O
ON C.CustomerID = O.CustomerID;
```

This conceptually produces a FULL JOIN result.

---

# 34. FULL JOIN in PostgreSQL

PostgreSQL supports FULL JOIN directly.

```sql
SELECT
    C.CustomerName,
    O.OrderID
FROM Customers AS C
FULL JOIN Orders AS O
ON C.CustomerID = O.CustomerID;
```

---

# 35. FULL JOIN in SQL Server

SQL Server supports FULL JOIN directly.

```sql
SELECT
    C.CustomerName,
    O.OrderID
FROM Customers AS C
FULL JOIN Orders AS O
ON C.CustomerID = O.CustomerID;
```

---

# 36. FULL JOIN in Oracle

Oracle supports ANSI SQL FULL OUTER JOIN syntax.

```sql
SELECT
    C.CustomerName,
    O.OrderID
FROM Customers C
FULL OUTER JOIN Orders O
ON C.CustomerID = O.CustomerID;
```

---

# 37. Performance Consideration

A FULL JOIN can potentially return a **very large result set**.

This is because it keeps:

```text
Matching rows
+
Unmatched rows from table 1
+
Unmatched rows from table 2
```

If both tables contain many records, the result can become large.

Therefore, use FULL JOIN carefully on large datasets.

---

# 38. Use Appropriate Indexes

For large tables, the columns used in the JOIN condition should generally be indexed appropriately.

Example:

```sql
ON Customers.CustomerID = Orders.CustomerID
```

The database can benefit from appropriate indexes on:

```text
Customers.CustomerID
Orders.CustomerID
```

The exact indexing strategy depends on:

* Database system
* Table size
* Query frequency
* Data distribution
* Existing indexes
* Execution plan

---

# 39. FULL JOIN with ORDER BY

You can sort the result.

```sql
SELECT
    C.CustomerID,
    C.CustomerName,
    O.OrderID
FROM Customers AS C
FULL JOIN Orders AS O
ON C.CustomerID = O.CustomerID
ORDER BY C.CustomerID;
```

Because unmatched rows can contain `NULL`, the position of `NULL` values depends on the database system and ordering rules.

---

# 40. FULL JOIN with DISTINCT

If you specifically need distinct result rows, you can use:

```sql
SELECT DISTINCT
    C.CustomerName,
    O.OrderID
FROM Customers AS C
FULL JOIN Orders AS O
ON C.CustomerID = O.CustomerID;
```

Remember:

```text
FULL JOIN does not automatically mean DISTINCT.
```

`DISTINCT` is a separate operation.

---

# 41. FULL JOIN with Aggregation

FULL JOIN can also be combined with aggregate functions.

For example:

```sql
SELECT
    C.CustomerName,
    COUNT(O.OrderID) AS OrderCount
FROM Customers AS C
FULL JOIN Orders AS O
ON C.CustomerID = O.CustomerID
GROUP BY C.CustomerName;
```

However, when using aggregation with unmatched rows, pay close attention to how `NULL` values are handled.

---

# 42. Common Mistake

A common mistake is thinking:

```text
FULL JOIN = INNER JOIN
```

This is incorrect.

### INNER JOIN

```text
Only matching rows
```

### FULL JOIN

```text
Matching rows
+
Left-only rows
+
Right-only rows
```

---

# 43. Another Common Mistake

Some beginners think:

```sql
FULL JOIN
```

means:

```text
All columns from both tables
```

This is also incorrect.

The word `FULL` refers to the **rows**, not the number of columns.

You control the columns using:

```sql
SELECT
```

---

# 44. Another Common Mistake with WHERE

Consider:

```sql
SELECT *
FROM Customers C
FULL JOIN Orders O
ON C.CustomerID = O.CustomerID
WHERE O.OrderID > 10000;
```

Rows where:

```text
O.OrderID = NULL
```

will not satisfy:

```sql
O.OrderID > 10000
```

Therefore some unmatched customer rows will disappear.

Always consider whether your `WHERE` condition unintentionally removes the unmatched rows that FULL JOIN was supposed to preserve.

---

# 45. FULL JOIN Summary Example

Tables:

```text
A
1
2
3

B
2
3
4
```

FULL JOIN on the ID:

```text
A.id = B.id
```

Result conceptually:

| A.id | B.id | Status |
| ---: | ---: | ------ |
|    1 | NULL | A only |
|    2 |    2 | Match  |
|    3 |    3 | Match  |
| NULL |    4 | B only |

Therefore:

```text
1 → LEFT ONLY
2 → MATCH
3 → MATCH
4 → RIGHT ONLY
```

---

# 46. Easy Memory Trick

Remember the four major JOINs like this:

```text
INNER JOIN
→ ONLY MATCH

LEFT JOIN
→ ALL LEFT

RIGHT JOIN
→ ALL RIGHT

FULL JOIN
→ ALL BOTH
```

Or:

```text
INNER → Match only
LEFT  → Left + Match
RIGHT → Right + Match
FULL  → Left + Match + Right
```

---

# 47. FULL JOIN Syntax — Quick Reference

### Basic

```sql
SELECT *
FROM table1
FULL JOIN table2
ON table1.id = table2.id;
```

### FULL OUTER JOIN

```sql
SELECT *
FROM table1
FULL OUTER JOIN table2
ON table1.id = table2.id;
```

### With aliases

```sql
SELECT
    A.name,
    B.value
FROM table1 AS A
FULL JOIN table2 AS B
ON A.id = B.id;
```

### With WHERE

```sql
SELECT *
FROM table1 AS A
FULL JOIN table2 AS B
ON A.id = B.id
WHERE condition;
```

### With ORDER BY

```sql
SELECT *
FROM table1 AS A
FULL JOIN table2 AS B
ON A.id = B.id
ORDER BY A.id;
```

---

# 48. Complete Example

## Customers

```text
CustomerID | CustomerName
-----------+----------------------
1          | Alfreds Futterkiste
2          | Ana Trujillo
3          | Antonio Moreno
```

## Orders

```text
OrderID | CustomerID
--------+-----------
10308   | 2
10309   | 37
10310   | 77
```

## Query

```sql
SELECT
    C.CustomerID,
    C.CustomerName,
    O.OrderID,
    O.CustomerID AS OrderCustomerID
FROM Customers AS C
FULL JOIN Orders AS O
ON C.CustomerID = O.CustomerID;
```

## Conceptual Result

```text
CustomerID | CustomerName           | OrderID | OrderCustomerID
-----------+------------------------+---------+----------------
NULL       | NULL                   | 10309   | 37
NULL       | NULL                   | 10310   | 77
1          | Alfreds Futterkiste    | NULL    | NULL
2          | Ana Trujillo           | 10308   | 2
3          | Antonio Moreno         | NULL    | NULL
```

The result contains:

```text
Customer 1 → No order
Customer 2 → Order 10308
Customer 3 → No order
Order 10309 → No matching customer
Order 10310 → No matching customer
```

---

# 49. Real-World Use Cases

FULL JOIN is particularly useful when you need to compare or reconcile two datasets.

### 1. Data Migration

Compare old database and new database:

```text
Old Database
     FULL JOIN
New Database
```

Find:

```text
Missing records
New records
Matching records
```

---

### 2. Data Reconciliation

Compare:

```text
Bank records
     FULL JOIN
Accounting records
```

Identify records that exist on only one side.

---

### 3. Data Synchronization

Compare:

```text
Application A
     FULL JOIN
Application B
```

Identify records that are missing or inconsistent.

---

### 4. Data Quality

Compare:

```text
Employee Master
     FULL JOIN
Payroll
```

Find employees without payroll records and payroll records without corresponding employees.

---

# 50. Key Points to Remember

1. `FULL JOIN` returns **all rows from both tables**.

2. Matching rows are combined.

3. Unmatched rows from the left table are retained.

4. Unmatched rows from the right table are retained.

5. `NULL` appears for missing values from the opposite table.

6. `FULL JOIN` and `FULL OUTER JOIN` are equivalent.

7. `OUTER` is optional.

8. `FULL JOIN` is different from `INNER JOIN`.

9. `INNER JOIN` returns only matching rows.

10. `LEFT JOIN` keeps all rows from the left table.

11. `RIGHT JOIN` keeps all rows from the right table.

12. `FULL JOIN` keeps rows from **both** tables.

13. FULL JOIN is useful for finding unmatched records.

14. FULL JOIN is useful for data reconciliation and comparison.

15. A `WHERE` clause can remove rows containing `NULL`.

16. FULL JOIN can produce a large result set.

17. Appropriate indexes can help JOIN performance.

18. SQL Server and PostgreSQL support FULL JOIN directly.

19. MySQL does not provide native FULL JOIN syntax and commonly requires a `LEFT JOIN` + `RIGHT JOIN` + `UNION` workaround.

---

# 51. One-Line Definition

> **FULL JOIN returns all matching rows plus all unmatched rows from both the left and right tables.**

```text
FULL JOIN
    =
LEFT ONLY
+
MATCHING
+
RIGHT ONLY
```

---

# 52. Final JOIN Cheat Sheet

| JOIN              | What it returns                     |
| ----------------- | ----------------------------------- |
| `INNER JOIN`      | Matching rows only                  |
| `LEFT JOIN`       | All left rows + matching right rows |
| `RIGHT JOIN`      | All right rows + matching left rows |
| `FULL JOIN`       | All rows from both tables           |
| `FULL OUTER JOIN` | Same as FULL JOIN                   |

### Remember:

```text
INNER → MATCH ONLY

LEFT  → ALL LEFT

RIGHT → ALL RIGHT

FULL  → ALL BOTH
```

And the most important FULL JOIN idea:

```text
        FULL JOIN
            ↓
     ┌──────────────┐
     │ LEFT ONLY    │
     │ MATCHING     │
     │ RIGHT ONLY   │
     └──────────────┘
```

**FULL JOIN = everything from both sides.**
