# SQL LEFT JOIN

## 1. What is a LEFT JOIN?

A `LEFT JOIN` is used to combine rows from two tables based on a related column.

The most important rule is:

> **LEFT JOIN returns ALL rows from the LEFT table and only matching rows from the RIGHT table.**

If a row in the left table has **no matching row** in the right table, SQL still returns the left-table row, but the right-table columns contain:

```text
NULL
```

---

# 2. LEFT JOIN Syntax

```sql
SELECT column_name(s)
FROM table1
LEFT JOIN table2
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
LEFT JOIN table2
```

means:

> Keep every row from `table1`.

---

# 3. LEFT JOIN and LEFT OUTER JOIN

These two are exactly the same:

```sql
LEFT JOIN
```

and:

```sql
LEFT OUTER JOIN
```

The `OUTER` keyword is optional.

Therefore:

```sql
SELECT *
FROM Customers
LEFT JOIN Orders
ON Customers.CustomerID = Orders.CustomerID;
```

is equivalent to:

```sql
SELECT *
FROM Customers
LEFT OUTER JOIN Orders
ON Customers.CustomerID = Orders.CustomerID;
```

In practice, most SQL developers simply use:

```sql
LEFT JOIN
```

---

# 4. LEFT JOIN Mental Model

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

A LEFT JOIN means:

```text
KEEP ALL OF A
+
MATCH WHAT IS AVAILABLE FROM B
```

Conceptually:

```text
        LEFT JOIN

+-------------------+
|                   |
|     LEFT TABLE    |
|                   |
|       +-------+   |
|       |MATCHED|   |
|       +-------+   |
|                   |
+-------------------+
```

The entire left table survives.

---

# 5. LEFT JOIN vs INNER JOIN

This is one of the most important differences in SQL.

## INNER JOIN

```text
Only matching rows
```

```text
LEFT TABLE        RIGHT TABLE

   A                 B
   |                 |
   +------ MATCH ----+
          ↓
       RESULT
```

## LEFT JOIN

```text
All left rows
+
Matching right rows
```

```text
LEFT TABLE        RIGHT TABLE

   A                 B
   |                 |
   +------ MATCH ----+
   |
   +------ NO MATCH
```

The unmatched left rows are still included.

For those rows:

```text
Right table columns = NULL
```

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

We will use these tables to understand `LEFT JOIN`.

---

# 7. Customers and Orders

The relationship is:

```text
Customers.CustomerID
        =
Orders.CustomerID
```

The database structure is:

```text
+----------------------+
|      Customers       |
+----------------------+
| PK CustomerID        |
| CustomerName         |
| ContactName          |
| Address              |
| City                 |
| PostalCode           |
| Country              |
+----------+-----------+
           |
           | CustomerID
           |
           ↓
+----------------------+
|        Orders        |
+----------------------+
| PK OrderID           |
| FK CustomerID        |
| FK EmployeeID        |
| OrderDate            |
| FK ShipperID         |
+----------------------+
```

---

# 8. Demo Customers Table

Example rows:

| CustomerID | CustomerName                       | ContactName    | City        | Country |
| ---------: | ---------------------------------- | -------------- | ----------- | ------- |
|          1 | Alfreds Futterkiste                | Maria Anders   | Berlin      | Germany |
|          2 | Ana Trujillo Emparedados y helados | Ana Trujillo   | México D.F. | Mexico  |
|          3 | Antonio Moreno Taquería            | Antonio Moreno | México D.F. | Mexico  |

---

# 9. Demo Orders Table

Example rows:

| OrderID | CustomerID | EmployeeID | OrderDate  | ShipperID |
| ------: | ---------: | ---------: | ---------- | --------: |
|   10308 |          2 |          7 | 1996-09-18 |         3 |
|   10309 |         37 |          3 | 1996-09-19 |         1 |
|   10310 |         77 |          8 | 1996-09-20 |         2 |

The common/related column is:

```text
CustomerID
```

---

# 10. Basic LEFT JOIN Example

Question:

> Show all customers and their orders.

SQL:

```sql
SELECT Customers.CustomerName,
       Orders.OrderID
FROM Customers
LEFT JOIN Orders
ON Customers.CustomerID = Orders.CustomerID;
```

Notice:

```sql
FROM Customers
LEFT JOIN Orders
```

Therefore:

```text
Customers = LEFT TABLE
Orders    = RIGHT TABLE
```

The query says:

> Keep every customer, and show their order when a matching order exists.

---

# 11. What Happens During the JOIN?

Suppose we have:

### Customers

| CustomerID | CustomerName        |
| ---------: | ------------------- |
|          1 | Alfreds Futterkiste |
|          2 | Ana Trujillo        |
|          3 | Antonio Moreno      |
|          4 | Around the Horn     |

### Orders

| OrderID | CustomerID |
| ------: | ---------: |
|   10308 |          2 |
|   10309 |          3 |

Now execute:

```sql
SELECT Customers.CustomerName,
       Orders.OrderID
FROM Customers
LEFT JOIN Orders
ON Customers.CustomerID = Orders.CustomerID;
```

SQL checks each customer.

```text
Customer 1 → No order → KEEP CUSTOMER
Customer 2 → Order 10308 → MATCH
Customer 3 → Order 10309 → MATCH
Customer 4 → No order → KEEP CUSTOMER
```

Result:

| CustomerName        | OrderID |
| ------------------- | ------: |
| Alfreds Futterkiste |    NULL |
| Ana Trujillo        |   10308 |
| Antonio Moreno      |   10309 |
| Around the Horn     |    NULL |

This is the key idea of `LEFT JOIN`.

---

# 12. Why Does NULL Appear?

For:

```text
Alfreds Futterkiste
```

there is no matching order.

But because `Customers` is the left table, the customer must still appear.

Therefore:

```text
CustomerName          OrderID
Alfreds Futterkiste   NULL
```

`NULL` means:

> There is no matching value from the right table.

It does **not** mean:

```text
0
```

It does **not** mean:

```text
empty string
```

It means:

```text
unknown / missing / no matching value
```

---

# 13. The Most Important LEFT JOIN Rule

Remember:

> **LEFT JOIN never removes a row from the LEFT table merely because there is no match in the RIGHT table.**

For example:

```text
Customers = 91 rows
Orders    = 196 rows
```

If `Customers` is the left table:

```sql
FROM Customers
LEFT JOIN Orders
```

all 91 customers remain represented in the result.

However, customers with multiple orders can appear multiple times.

---

# 14. One Customer Can Have Many Orders

Suppose:

### Customers

| CustomerID | CustomerName |
| ---------: | ------------ |
|         10 | Customer A   |

### Orders

| OrderID | CustomerID |
| ------: | ---------: |
|    1001 |         10 |
|    1002 |         10 |
|    1003 |         10 |

LEFT JOIN:

```sql
SELECT C.CustomerName,
       O.OrderID
FROM Customers AS C
LEFT JOIN Orders AS O
ON C.CustomerID = O.CustomerID;
```

Result:

| CustomerName | OrderID |
| ------------ | ------: |
| Customer A   |    1001 |
| Customer A   |    1002 |
| Customer A   |    1003 |

The customer appears three times.

Why?

Because:

```text
1 Customer
    ↓
3 Orders
```

This is a normal one-to-many relationship.

---

# 15. LEFT JOIN With a Customer Having No Orders

Suppose:

### Customers

| CustomerID | CustomerName |
| ---------: | ------------ |
|         10 | Customer A   |
|         20 | Customer B   |

### Orders

| OrderID | CustomerID |
| ------: | ---------: |
|    1001 |         10 |
|    1002 |         10 |

Customer B has no orders.

LEFT JOIN:

```sql
SELECT C.CustomerName,
       O.OrderID
FROM Customers AS C
LEFT JOIN Orders AS O
ON C.CustomerID = O.CustomerID;
```

Result:

| CustomerName | OrderID |
| ------------ | ------: |
| Customer A   |    1001 |
| Customer A   |    1002 |
| Customer B   |    NULL |

Customer B is still present.

This is the major difference from `INNER JOIN`.

---

# 16. LEFT JOIN vs INNER JOIN — Same Data

Suppose:

### Customers

| CustomerID | CustomerName |
| ---------: | ------------ |
|          1 | A            |
|          2 | B            |
|          3 | C            |

### Orders

| OrderID | CustomerID |
| ------: | ---------: |
|     101 |          1 |
|     102 |          2 |

## INNER JOIN

```sql
SELECT C.CustomerName,
       O.OrderID
FROM Customers AS C
INNER JOIN Orders AS O
ON C.CustomerID = O.CustomerID;
```

Result:

| CustomerName | OrderID |
| ------------ | ------: |
| A            |     101 |
| B            |     102 |

Customer C disappears.

---

## LEFT JOIN

```sql
SELECT C.CustomerName,
       O.OrderID
FROM Customers AS C
LEFT JOIN Orders AS O
ON C.CustomerID = O.CustomerID;
```

Result:

| CustomerName | OrderID |
| ------------ | ------: |
| A            |     101 |
| B            |     102 |
| C            |    NULL |

Customer C remains.

---

# 17. Visual Comparison

```text
INNER JOIN

Customers       Orders
    |              |
    +--- MATCH ----+
          ↓
       RESULT
```

Only matches.

```text
LEFT JOIN

Customers       Orders
    |              |
    +--- MATCH ----+
    |
    +--- NO MATCH
          ↓
       RESULT
```

All customers remain.

---

# 18. LEFT JOIN with ORDER BY

The W3Schools-style example can be written:

```sql
SELECT Customers.CustomerName,
       Orders.OrderID
FROM Customers
LEFT JOIN Orders
ON Customers.CustomerID = Orders.CustomerID
ORDER BY Customers.CustomerName;
```

This means:

1. Start with all customers.
2. Match their orders.
3. Keep customers without orders.
4. Sort by customer name.

---

# 19. Using Table Aliases

Instead of:

```sql
SELECT Customers.CustomerName,
       Orders.OrderID
FROM Customers
LEFT JOIN Orders
ON Customers.CustomerID = Orders.CustomerID;
```

we can write:

```sql
SELECT C.CustomerName,
       O.OrderID
FROM Customers AS C
LEFT JOIN Orders AS O
ON C.CustomerID = O.CustomerID;
```

Here:

```text
C = Customers
O = Orders
```

This is cleaner and especially useful with multiple tables.

---

# 20. Finding Customers Who Have No Orders

One of the most useful applications of `LEFT JOIN` is finding records that **do not have a match**.

Question:

> Which customers have never placed an order?

Query:

```sql
SELECT C.CustomerName,
       O.OrderID
FROM Customers AS C
LEFT JOIN Orders AS O
ON C.CustomerID = O.CustomerID
WHERE O.CustomerID IS NULL;
```

The result contains only customers with no matching order.

---

# 21. Why `IS NULL`?

We cannot normally write:

```sql
WHERE O.CustomerID = NULL
```

This is incorrect.

Use:

```sql
WHERE O.CustomerID IS NULL
```

For checking NULL values, SQL provides:

```sql
IS NULL
```

and:

```sql
IS NOT NULL
```

---

# 22. LEFT JOIN + IS NULL

This pattern is extremely important:

```sql
SELECT ...
FROM TableA AS A
LEFT JOIN TableB AS B
ON A.ID = B.ID
WHERE B.ID IS NULL;
```

Meaning:

> Give me rows from A that do not have a matching row in B.

Think of it as:

```text
LEFT JOIN
    +
IS NULL
    =
UNMATCHED LEFT ROWS
```

---

# 23. Finding Customers Who DID Place Orders

We can reverse the condition:

```sql
SELECT C.CustomerName,
       O.OrderID
FROM Customers AS C
LEFT JOIN Orders AS O
ON C.CustomerID = O.CustomerID
WHERE O.CustomerID IS NOT NULL;
```

This returns customers for whom a matching order exists.

However, for simply finding matching records, an `INNER JOIN` is usually clearer.

---

# 24. NULL vs NOT NULL

### No matching order

```sql
WHERE O.CustomerID IS NULL
```

means:

```text
No matching order
```

### Matching order

```sql
WHERE O.CustomerID IS NOT NULL
```

means:

```text
A matching order exists
```

---

# 25. LEFT JOIN With Three Tables

We can join:

```text
Customers
Orders
Shippers
```

Query:

```sql
SELECT C.CustomerName,
       O.OrderID,
       S.ShipperName
FROM Customers AS C
LEFT JOIN Orders AS O
ON C.CustomerID = O.CustomerID
LEFT JOIN Shippers AS S
ON O.ShipperID = S.ShipperID;
```

This starts with:

```text
Customers
```

and keeps all customers.

If a customer has an order, the order information is shown.

If that order has a matching shipper, the shipper information is shown.

---

# 26. Understanding LEFT JOIN With Multiple Tables

Conceptually:

```text
Customers
    |
    | LEFT JOIN
    ↓
Orders
    |
    | LEFT JOIN
    ↓
Shippers
```

The important point is that the first table remains the preserved table.

```text
Customers
```

is the starting point.

---

# 27. LEFT JOIN Products and Categories

Suppose we want:

> Show every product and its category.

Query:

```sql
SELECT P.ProductID,
       P.ProductName,
       C.CategoryName
FROM Products AS P
LEFT JOIN Categories AS C
ON P.CategoryID = C.CategoryID;
```

Because:

```text
Products = LEFT TABLE
Categories = RIGHT TABLE
```

every product is retained.

If a product has no matching category:

```text
CategoryName = NULL
```

---

# 28. LEFT JOIN Products and Suppliers

Relationship:

```text
Products.SupplierID
        =
Suppliers.SupplierID
```

Query:

```sql
SELECT P.ProductID,
       P.ProductName,
       S.SupplierName
FROM Products AS P
LEFT JOIN Suppliers AS S
ON P.SupplierID = S.SupplierID;
```

This means:

> Show every product, even if its supplier information is missing.

---

# 29. LEFT JOIN Orders and Employees

Relationship:

```text
Orders.EmployeeID
        =
Employees.EmployeeID
```

Query:

```sql
SELECT O.OrderID,
       O.OrderDate,
       E.FirstName,
       E.LastName
FROM Orders AS O
LEFT JOIN Employees AS E
ON O.EmployeeID = E.EmployeeID;
```

Every order is retained because:

```text
Orders = LEFT TABLE
```

---

# 30. LEFT JOIN Orders and Shippers

Relationship:

```text
Orders.ShipperID
        =
Shippers.ShipperID
```

Query:

```sql
SELECT O.OrderID,
       O.OrderDate,
       S.ShipperName
FROM Orders AS O
LEFT JOIN Shippers AS S
ON O.ShipperID = S.ShipperID;
```

Every order remains in the result.

If no matching shipper exists:

```text
ShipperName = NULL
```

---

# 31. LEFT JOIN OrderDetails and Products

Relationship:

```text
OrderDetails.ProductID
        =
Products.ProductID
```

Query:

```sql
SELECT OD.OrderID,
       OD.ProductID,
       P.ProductName,
       OD.Quantity
FROM OrderDetails AS OD
LEFT JOIN Products AS P
ON OD.ProductID = P.ProductID;
```

This keeps every `OrderDetails` row.

If a product cannot be matched:

```text
ProductName = NULL
```

---

# 32. LEFT JOIN With Our Database Relationships

Our database relationships include:

```text
Customers
    |
    | CustomerID
    ↓
Orders
```

```text
Orders
    |
    | OrderID
    ↓
OrderDetails
```

```text
OrderDetails
    |
    | ProductID
    ↓
Products
```

```text
Products
    |
    | CategoryID
    ↓
Categories
```

```text
Products
    |
    | SupplierID
    ↓
Suppliers
```

```text
Orders
    |
    | EmployeeID
    ↓
Employees
```

```text
Orders
    |
    | ShipperID
    ↓
Shippers
```

LEFT JOIN allows us to preserve the table on the left while optionally bringing information from related tables.

---

# 33. Practical Example — Every Customer and Order

Question:

> Show all 91 customers and their orders, including customers who have never ordered.

```sql
SELECT C.CustomerID,
       C.CustomerName,
       O.OrderID,
       O.OrderDate
FROM Customers AS C
LEFT JOIN Orders AS O
ON C.CustomerID = O.CustomerID
ORDER BY C.CustomerName;
```

The important part is:

```sql
LEFT JOIN
```

because we want:

```text
ALL CUSTOMERS
```

not only customers who have orders.

---

# 34. Practical Example — Customers Without Orders

Question:

> Find customers who have never placed an order.

```sql
SELECT C.CustomerID,
       C.CustomerName
FROM Customers AS C
LEFT JOIN Orders AS O
ON C.CustomerID = O.CustomerID
WHERE O.CustomerID IS NULL;
```

This is a very common SQL interview pattern.

---

# 35. Practical Example — Every Product and Category

Question:

> Show every product, even products that don't have a category.

```sql
SELECT P.ProductID,
       P.ProductName,
       C.CategoryName
FROM Products AS P
LEFT JOIN Categories AS C
ON P.CategoryID = C.CategoryID;
```

If category exists:

```text
Product → Category
```

If category doesn't exist:

```text
Product → NULL
```

But the product remains.

---

# 36. Practical Example — Every Product and Supplier

```sql
SELECT P.ProductID,
       P.ProductName,
       S.SupplierName
FROM Products AS P
LEFT JOIN Suppliers AS S
ON P.SupplierID = S.SupplierID;
```

All products are retained.

---

# 37. Practical Example — Every Order and Customer

```sql
SELECT O.OrderID,
       O.OrderDate,
       C.CustomerName
FROM Orders AS O
LEFT JOIN Customers AS C
ON O.CustomerID = C.CustomerID;
```

Here:

```text
Orders = LEFT TABLE
Customers = RIGHT TABLE
```

Therefore:

> Every order is retained, even if customer information is missing.

This is different from:

```sql
FROM Customers
LEFT JOIN Orders
```

because changing the table order changes which rows are guaranteed to remain.

---

# 38. The LEFT Table Matters

Compare:

### Query 1

```sql
SELECT *
FROM Customers
LEFT JOIN Orders
ON Customers.CustomerID = Orders.CustomerID;
```

Guarantees:

```text
ALL CUSTOMERS
```

### Query 2

```sql
SELECT *
FROM Orders
LEFT JOIN Customers
ON Orders.CustomerID = Customers.CustomerID;
```

Guarantees:

```text
ALL ORDERS
```

This is extremely important.

---

# 39. LEFT JOIN Is Directional

LEFT JOIN is directional.

```text
FROM A
LEFT JOIN B
```

means:

```text
A = preserved table
B = optional matching table
```

So:

```text
A → Always keep
B → Keep only matches
```

Remember:

```text
LEFT = table written before LEFT JOIN
```

---

# 40. LEFT JOIN and NULL

Suppose:

```text
Customers

CustomerID
1
2
3
```

and:

```text
Orders

CustomerID
1
2
```

Query:

```sql
SELECT C.CustomerID,
       O.OrderID
FROM Customers AS C
LEFT JOIN Orders AS O
ON C.CustomerID = O.CustomerID;
```

Result:

```text
CustomerID | OrderID
-----------|--------
1          | 101
2          | 102
3          | NULL
```

The `NULL` tells us:

```text
Customer 3
    ↓
No matching order
```

---

# 41. LEFT JOIN + WHERE — Important Warning

Consider:

```sql
SELECT C.CustomerName,
       O.OrderID
FROM Customers AS C
LEFT JOIN Orders AS O
ON C.CustomerID = O.CustomerID
WHERE O.OrderDate >= '1996-01-01';
```

Be careful.

The `WHERE` condition removes rows where:

```text
O.OrderDate = NULL
```

Therefore, customers without orders may disappear.

The query can effectively behave more like an INNER JOIN for that condition.

---

# 42. Filtering in ON vs WHERE

Consider:

```sql
FROM Customers AS C
LEFT JOIN Orders AS O
ON C.CustomerID = O.CustomerID
AND O.OrderDate >= '1996-01-01';
```

Here, all customers remain.

The condition controls which orders are matched.

Compare with:

```sql
FROM Customers AS C
LEFT JOIN Orders AS O
ON C.CustomerID = O.CustomerID
WHERE O.OrderDate >= '1996-01-01';
```

Here, customers with no matching orders can be filtered out.

This distinction is very important when working with `LEFT JOIN`.

---

# 43. LEFT JOIN and WHERE IS NULL — Anti-Join Pattern

This pattern:

```sql
SELECT C.*
FROM Customers AS C
LEFT JOIN Orders AS O
ON C.CustomerID = O.CustomerID
WHERE O.CustomerID IS NULL;
```

is commonly called an:

```text
ANTI-JOIN
```

It means:

> Find records in the left table that do not have a matching record in the right table.

Conceptually:

```text
Customers
    |
    +---- Has Order → Exclude
    |
    +---- No Order  → Include
```

---

# 44. LEFT JOIN vs INNER JOIN — Comparison Table

| Feature                     | INNER JOIN          | LEFT JOIN                 |
| --------------------------- | ------------------- | ------------------------- |
| Matching rows               | Yes                 | Yes                       |
| All left rows               | No                  | Yes                       |
| Unmatched left rows         | Removed             | Kept                      |
| Right-side unmatched values | Not shown           | NULL                      |
| Common use                  | Get related records | Preserve all left records |
| Find missing relationships  | Less convenient     | Very useful               |
| `IS NULL` pattern           | Usually not         | Very common               |

---

# 45. LEFT JOIN — Simple Example

### Table A

| ID | Name |
| -: | ---- |
|  1 | A    |
|  2 | B    |
|  3 | C    |

### Table B

| ID | Order |
| -: | ----- |
|  1 | X     |
|  3 | Y     |

LEFT JOIN:

```sql
SELECT A.ID,
       A.Name,
       B.Order
FROM A
LEFT JOIN B
ON A.ID = B.ID;
```

Result:

| ID | Name | Order |
| -: | ---- | ----- |
|  1 | A    | X     |
|  2 | B    | NULL  |
|  3 | C    | Y     |

Why is B present?

Because B belongs to the left table.

---

# 46. LEFT JOIN Formula

Remember this formula:

```text
LEFT JOIN

ALL LEFT ROWS
        +
MATCHING RIGHT ROWS
        +
NULL FOR UNMATCHED RIGHT DATA
```

Or even shorter:

```text
LEFT JOIN = ALL LEFT + MATCH RIGHT
```

---

# 47. How to Decide When to Use LEFT JOIN

Ask yourself:

> **Do I want every row from my main table, even if there is no related record?**

If the answer is:

```text
YES
```

consider:

```sql
LEFT JOIN
```

Examples:

### Every customer, even without orders

```sql
Customers
LEFT JOIN Orders
```

### Every product, even without category

```sql
Products
LEFT JOIN Categories
```

### Every product, even without supplier

```sql
Products
LEFT JOIN Suppliers
```

### Every order, even without customer information

```sql
Orders
LEFT JOIN Customers
```

---

# 48. How to Find the Correct LEFT Table

A useful technique is to ask:

> **What must never disappear from my result?**

That table should normally be on the left.

Example:

> Show every customer and their orders.

What must never disappear?

```text
Customers
```

Therefore:

```sql
FROM Customers
LEFT JOIN Orders
```

---

Another example:

> Show every order and its customer.

What must never disappear?

```text
Orders
```

Therefore:

```sql
FROM Orders
LEFT JOIN Customers
```

---

# 49. LEFT JOIN With Aggregation

LEFT JOIN is especially useful with `COUNT()`.

Question:

> Show every customer and the number of orders they have placed.

```sql
SELECT C.CustomerID,
       C.CustomerName,
       COUNT(O.OrderID) AS OrderCount
FROM Customers AS C
LEFT JOIN Orders AS O
ON C.CustomerID = O.CustomerID
GROUP BY C.CustomerID,
         C.CustomerName;
```

Why use LEFT JOIN?

Because we want customers with:

```text
0 orders
```

to appear too.

Their result can be:

| CustomerID | CustomerName        | OrderCount |
| ---------: | ------------------- | ---------: |
|          1 | Alfreds Futterkiste |          0 |
|          2 | Ana Trujillo        |          3 |
|          3 | Antonio Moreno      |          2 |

The `LEFT JOIN` ensures that a customer with no orders is still present.

---

# 50. LEFT JOIN + COUNT — Important

Consider:

```sql
COUNT(O.OrderID)
```

For a customer with no order:

```text
O.OrderID = NULL
```

`COUNT(column)` does not count NULL values.

Therefore:

```text
No Orders → COUNT(O.OrderID) = 0
```

This makes the pattern very useful for reporting.

---

# 51. Example — Every Category and Product Count

We can use:

```sql
SELECT C.CategoryID,
       C.CategoryName,
       COUNT(P.ProductID) AS ProductCount
FROM Categories AS C
LEFT JOIN Products AS P
ON C.CategoryID = P.CategoryID
GROUP BY C.CategoryID,
         C.CategoryName;
```

This shows every category, including categories that have zero products.

---

# 52. LEFT JOIN and Data Analysis

LEFT JOIN is commonly used for questions such as:

```text
Which customers have no orders?

Which products have no category?

Which products have no supplier?

Which employees have no assigned records?

Which categories contain zero products?

Which customers have zero purchases?
```

The general pattern is:

```sql
LEFT JOIN
+
IS NULL
```

for finding missing relationships.

---

# 53. Real-World Business Example

Imagine an e-commerce database.

You want to find:

> Customers who registered but never purchased anything.

Tables:

```text
Customers
Orders
```

Relationship:

```text
Customers.CustomerID
        =
Orders.CustomerID
```

Query:

```sql
SELECT C.CustomerID,
       C.CustomerName
FROM Customers AS C
LEFT JOIN Orders AS O
ON C.CustomerID = O.CustomerID
WHERE O.CustomerID IS NULL;
```

This is a real business use case for `LEFT JOIN`.

---

# 54. Real-World Inventory Example

Question:

> Find products that are not assigned to any category.

```sql
SELECT P.ProductID,
       P.ProductName
FROM Products AS P
LEFT JOIN Categories AS C
ON P.CategoryID = C.CategoryID
WHERE C.CategoryID IS NULL;
```

The logic is:

```text
Products
    ↓
LEFT JOIN Categories
    ↓
No category match?
    ↓
IS NULL
    ↓
Return product
```

---

# 55. Real-World Supplier Example

Question:

> Find products that don't have a matching supplier.

```sql
SELECT P.ProductID,
       P.ProductName
FROM Products AS P
LEFT JOIN Suppliers AS S
ON P.SupplierID = S.SupplierID
WHERE S.SupplierID IS NULL;
```

---

# 56. LEFT JOIN — Complete Pattern

### Retrieve all left records

```sql
SELECT A.*
FROM TableA AS A
LEFT JOIN TableB AS B
ON A.ID = B.ID;
```

### Retrieve matching information too

```sql
SELECT A.Name,
       B.Description
FROM TableA AS A
LEFT JOIN TableB AS B
ON A.ID = B.ID;
```

### Find unmatched left records

```sql
SELECT A.*
FROM TableA AS A
LEFT JOIN TableB AS B
ON A.ID = B.ID
WHERE B.ID IS NULL;
```

### Count matching records

```sql
SELECT A.ID,
       COUNT(B.ID)
FROM TableA AS A
LEFT JOIN TableB AS B
ON A.ID = B.ID
GROUP BY A.ID;
```

---

# 57. LEFT JOIN — Interview Questions

## Question 1

What does LEFT JOIN return?

**Answer:**

All rows from the left table and matching rows from the right table. Unmatched right-side columns contain NULL.

---

## Question 2

What is the difference between LEFT JOIN and INNER JOIN?

**Answer:**

`INNER JOIN` returns only matching rows.

`LEFT JOIN` returns all rows from the left table, including rows that have no match in the right table.

---

## Question 3

Is `LEFT JOIN` the same as `LEFT OUTER JOIN`?

**Answer:**

Yes.

```text
LEFT JOIN = LEFT OUTER JOIN
```

The `OUTER` keyword is optional.

---

## Question 4

How do you find customers with no orders?

```sql
SELECT C.CustomerName
FROM Customers AS C
LEFT JOIN Orders AS O
ON C.CustomerID = O.CustomerID
WHERE O.CustomerID IS NULL;
```

---

## Question 5

Why does NULL appear in a LEFT JOIN?

Because there is no matching row in the right table, but the left row must still be retained.

---

# 58. LEFT JOIN — Common Mistakes

## Mistake 1 — Putting the wrong table on the left

If you need all customers:

Correct:

```sql
FROM Customers
LEFT JOIN Orders
```

Not:

```sql
FROM Orders
LEFT JOIN Customers
```

The second query guarantees all orders, not all customers.

---

## Mistake 2 — Using `= NULL`

Incorrect:

```sql
WHERE O.CustomerID = NULL;
```

Correct:

```sql
WHERE O.CustomerID IS NULL;
```

---

## Mistake 3 — Forgetting one-to-many relationships

A customer with five orders can appear five times.

This is normal.

---

## Mistake 4 — Accidentally removing NULL rows with WHERE

For example:

```sql
LEFT JOIN Orders O
...
WHERE O.OrderDate > '1996-01-01'
```

can remove customers with no orders.

Always understand how the `WHERE` condition interacts with NULL values.

---

# 59. LEFT JOIN Decision Tree

When writing a JOIN, ask:

```text
What records do I need?
          |
          ↓
Do I need ALL records from one table?
          |
       YES
          |
          ↓
Put that table on the LEFT
          |
          ↓
Use LEFT JOIN
          |
          ↓
Find the related table
          |
          ↓
Write ON condition
```

Example:

```text
Need all Customers
       ↓
Customers goes LEFT
       ↓
LEFT JOIN Orders
       ↓
ON CustomerID
```

---

# 60. INNER JOIN vs LEFT JOIN — Visual

```text
INNER JOIN

Customers              Orders
   ○                     ○
   |                     |
   |      MATCH          |
   +-------●-------------+
           |
         RESULT
```

Only matching portion.

---

```text
LEFT JOIN

Customers              Orders
   ○                     ○
   |                     |
   +-------●-------------+
   |
   |  ALL LEFT ROWS
   |
   +----------------
```

All customers remain.

---

# 61. The Three Most Important LEFT JOIN Patterns

## Pattern 1 — All left rows

```sql
SELECT ...
FROM A
LEFT JOIN B
ON A.ID = B.ID;
```

Meaning:

```text
ALL A
+
MATCHING B
```

---

## Pattern 2 — All left rows with related information

```sql
SELECT A.Name,
       B.Description
FROM A
LEFT JOIN B
ON A.ID = B.ID;
```

Meaning:

```text
Every A
+
B information when available
```

---

## Pattern 3 — Only unmatched left rows

```sql
SELECT A.*
FROM A
LEFT JOIN B
ON A.ID = B.ID
WHERE B.ID IS NULL;
```

Meaning:

```text
A records
WITHOUT
a matching B record
```

---

# 62. LEFT JOIN With Our Northwind Database

### All Customers + Orders

```sql
SELECT C.CustomerID,
       C.CustomerName,
       O.OrderID,
       O.OrderDate
FROM Customers AS C
LEFT JOIN Orders AS O
ON C.CustomerID = O.CustomerID;
```

### Customers Without Orders

```sql
SELECT C.CustomerID,
       C.CustomerName
FROM Customers AS C
LEFT JOIN Orders AS O
ON C.CustomerID = O.CustomerID
WHERE O.CustomerID IS NULL;
```

### All Products + Categories

```sql
SELECT P.ProductID,
       P.ProductName,
       C.CategoryName
FROM Products AS P
LEFT JOIN Categories AS C
ON P.CategoryID = C.CategoryID;
```

### Products Without Categories

```sql
SELECT P.ProductID,
       P.ProductName
FROM Products AS P
LEFT JOIN Categories AS C
ON P.CategoryID = C.CategoryID
WHERE C.CategoryID IS NULL;
```

### All Products + Suppliers

```sql
SELECT P.ProductID,
       P.ProductName,
       S.SupplierName
FROM Products AS P
LEFT JOIN Suppliers AS S
ON P.SupplierID = S.SupplierID;
```

### Products Without Suppliers

```sql
SELECT P.ProductID,
       P.ProductName
FROM Products AS P
LEFT JOIN Suppliers AS S
ON P.SupplierID = S.SupplierID
WHERE S.SupplierID IS NULL;
```

---

# 63. LEFT JOIN — Final Cheat Sheet

```text
LEFT JOIN
    ↓
Keep ALL rows from LEFT table
    ↓
Find matching rows in RIGHT table
    ↓
If match exists
    → show right-side data
    ↓
If match doesn't exist
    → show NULL for right-side columns
```

### Syntax

```sql
SELECT columns
FROM LeftTable AS L
LEFT JOIN RightTable AS R
ON L.Key = R.Key;
```

### Find unmatched records

```sql
SELECT L.*
FROM LeftTable AS L
LEFT JOIN RightTable AS R
ON L.Key = R.Key
WHERE R.Key IS NULL;
```

---

# 64. Final Summary

The most important concept is:

> **LEFT JOIN preserves the entire LEFT table.**

For:

```sql
FROM Customers AS C
LEFT JOIN Orders AS O
ON C.CustomerID = O.CustomerID;
```

think:

```text
Customers
   ↓
KEEP EVERY CUSTOMER
   ↓
Look for matching Orders
   ↓
Match found?
   ├── YES → show Order information
   └── NO  → show NULL
```

The key formula is:

```text
LEFT JOIN
=
ALL LEFT ROWS
+
MATCHING RIGHT ROWS
+
NULL FOR UNMATCHED RIGHT ROWS
```

And the most useful missing-data pattern is:

```sql
LEFT JOIN
...
WHERE RightTable.Key IS NULL;
```

which means:

> **Find records in the left table that have no matching record in the right table.**

---

# 65. One-Minute Revision

```text
INNER JOIN
→ Only matches

LEFT JOIN
→ All LEFT + matches from RIGHT

LEFT OUTER JOIN
→ Same as LEFT JOIN

ON
→ Defines relationship

IS NULL
→ Finds missing/unmatched right-side records

LEFT JOIN + IS NULL
→ Find records with NO matching record

LEFT table
→ The table whose rows must be preserved
```

### Remember this example:

```sql
SELECT C.CustomerName,
       O.OrderID
FROM Customers AS C
LEFT JOIN Orders AS O
ON C.CustomerID = O.CustomerID;
```

Read it as:

> **Give me every customer, and if that customer has an order, show the order. If there is no order, still show the customer and put NULL for the order.**

That is the essence of `LEFT JOIN`.
