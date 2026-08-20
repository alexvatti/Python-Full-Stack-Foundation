# Day 33 — Python + MySQL

## Two Related Tables — Primary Key, Foreign Key and JOIN

In this demo, we will use **Python programming** to work with two related MySQL tables:

```text
Customers
    │
    │ CustomerID
    ▼
Orders
```

We will learn:

```text
CREATE TABLE
INSERT MULTIPLE RECORDS
PRIMARY KEY
FOREIGN KEY
SELECT
JOIN
WHERE
ORDER BY
GROUP BY
COUNT
HAVING
```

---

# 1. Database Structure

We will create:

### Table 1 — Customers

| Column       | Description      |
| ------------ | ---------------- |
| CustomerID   | Primary Key      |
| CustomerName | Customer name    |
| ContactName  | Contact person   |
| City         | Customer city    |
| Country      | Customer country |

### Table 2 — Orders

| Column     | Description  |
| ---------- | ------------ |
| OrderID    | Primary Key  |
| CustomerID | Foreign Key  |
| OrderDate  | Order date   |
| Amount     | Order amount |
| Status     | Order status |

---

# 2. Project Structure

```text
Day-33/
│
├── database.py
├── create_tables.py
├── insert_customers.py
├── insert_orders.py
├── select_customers.py
├── join_customers_orders.py
└── questions.py
```

The important idea is:

```text
database.py
     │
     ├── create_tables.py
     ├── insert_customers.py
     ├── insert_orders.py
     ├── select_customers.py
     └── join_customers_orders.py
```

We keep the **database connection code in one module** and reuse it everywhere.

---

# 3. Install MySQL Connector

If it is not already installed:

```bash
pip install mysql-connector-python
```

---

# 4. Module 1 — Database Connection

Create:

```text
database.py
```

```python
import mysql.connector


def get_connection():

    connection = mysql.connector.connect(
        host="localhost",
        user="root",
        password="your_password",
        database="demo"
    )

    return connection
```

Every Python program will use:

```python
from database import get_connection
```

---

# 5. Module 2 — Create Customers and Orders Tables

Create:

```text
create_tables.py
```

## Question

Using Python:

1. Create the `Customers` table.
2. Create the `Orders` table.
3. Make `CustomerID` the Primary Key in `Customers`.
4. Make `OrderID` the Primary Key in `Orders`.
5. Make `Orders.CustomerID` a Foreign Key referencing `Customers.CustomerID`.

---

## Python Program

```python
from database import get_connection


def create_tables():

    connection = get_connection()

    cursor = connection.cursor()

    # Customers table

    cursor.execute("""
        CREATE TABLE IF NOT EXISTS Customers(

            CustomerID INT PRIMARY KEY,

            CustomerName VARCHAR(100),

            ContactName VARCHAR(100),

            City VARCHAR(50),

            Country VARCHAR(50)
        )
    """)

    # Orders table

    cursor.execute("""
        CREATE TABLE IF NOT EXISTS Orders(

            OrderID INT PRIMARY KEY,

            CustomerID INT,

            OrderDate DATE,

            Amount DECIMAL(10,2),

            Status VARCHAR(20),

            FOREIGN KEY (CustomerID)
                REFERENCES Customers(CustomerID)
        )
    """)

    connection.commit()

    print("Tables created successfully.")

    cursor.close()
    connection.close()


def main():

    create_tables()


if __name__ == "__main__":
    main()
```

---

# 6. Understand the Relationship

The important part is:

```python
FOREIGN KEY (CustomerID)
REFERENCES Customers(CustomerID)
```

This means:

```text
Customers.CustomerID
        ↑
        │
        │ Foreign Key
        │
Orders.CustomerID
```

Example:

```text
Customer
CustomerID = 1
     │
     ├──── OrderID = 101
     │
     └──── OrderID = 106
```

One customer can have multiple orders.

This is a:

> **One-to-Many Relationship**

---

# 7. Module 3 — Insert Multiple Customers

Create:

```text
insert_customers.py
```

We will insert **10 customers**.

## Question

Using Python, insert multiple customer records using `executemany()`.

---

## Python Program

```python
from database import get_connection


def insert_customers():

    connection = get_connection()

    cursor = connection.cursor()

    sql = """
        INSERT INTO Customers
        (
            CustomerID,
            CustomerName,
            ContactName,
            City,
            Country
        )
        VALUES (%s, %s, %s, %s, %s)
    """

    customers = [

        (
            1,
            "Alfreds Futterkiste",
            "Maria Anders",
            "Berlin",
            "Germany"
        ),

        (
            2,
            "Ana Trujillo Emparedados",
            "Ana Trujillo",
            "Mexico City",
            "Mexico"
        ),

        (
            3,
            "Antonio Moreno Taqueria",
            "Antonio Moreno",
            "Mexico City",
            "Mexico"
        ),

        (
            4,
            "Around the Horn",
            "Thomas Hardy",
            "London",
            "UK"
        ),

        (
            5,
            "Berglunds Snabbkop",
            "Christina Berglund",
            "Lulea",
            "Sweden"
        ),

        (
            6,
            "Blauer See Delikatessen",
            "Hanna Moos",
            "Mannheim",
            "Germany"
        ),

        (
            7,
            "Blondel Pere et Fils",
            "Frederique Citeaux",
            "Strasbourg",
            "France"
        ),

        (
            8,
            "Bolido Comidas",
            "Martin Sommer",
            "Madrid",
            "Spain"
        ),

        (
            9,
            "Bon App",
            "Laurence Lebihans",
            "Marseille",
            "France"
        ),

        (
            10,
            "Bottom-Dollar Markets",
            "Elizabeth Lincoln",
            "Tsawassen",
            "Canada"
        )
    ]

    cursor.executemany(sql, customers)

    connection.commit()

    print(len(customers), "customers inserted.")

    cursor.close()
    connection.close()


def main():

    insert_customers()


if __name__ == "__main__":
    main()
```

---

# 8. Customers Data

After running the program:

```text
10 customers inserted.
```

The table contains:

| CustomerID | CustomerName             | ContactName        | City        | Country |
| ---------: | ------------------------ | ------------------ | ----------- | ------- |
|          1 | Alfreds Futterkiste      | Maria Anders       | Berlin      | Germany |
|          2 | Ana Trujillo Emparedados | Ana Trujillo       | Mexico City | Mexico  |
|          3 | Antonio Moreno Taqueria  | Antonio Moreno     | Mexico City | Mexico  |
|          4 | Around the Horn          | Thomas Hardy       | London      | UK      |
|          5 | Berglunds Snabbkop       | Christina Berglund | Lulea       | Sweden  |
|          6 | Blauer See Delikatessen  | Hanna Moos         | Mannheim    | Germany |
|          7 | Blondel Pere et Fils     | Frederique Citeaux | Strasbourg  | France  |
|          8 | Bolido Comidas           | Martin Sommer      | Madrid      | Spain   |
|          9 | Bon App                  | Laurence Lebihans  | Marseille   | France  |
|         10 | Bottom-Dollar Markets    | Elizabeth Lincoln  | Tsawassen   | Canada  |

---

# 9. Module 4 — Insert Multiple Orders

Create:

```text
insert_orders.py
```

## Question

Using Python:

* Insert 10 orders.
* Use `executemany()`.
* Use existing `CustomerID` values.
* Maintain the Foreign Key relationship.

---

## Python Program

```python
from database import get_connection


def insert_orders():

    connection = get_connection()

    cursor = connection.cursor()

    sql = """
        INSERT INTO Orders
        (
            OrderID,
            CustomerID,
            OrderDate,
            Amount,
            Status
        )
        VALUES (%s, %s, %s, %s, %s)
    """

    orders = [

        (101, 1, "2026-01-10", 1200.00, "Completed"),

        (102, 2, "2026-01-12", 850.00, "Completed"),

        (103, 3, "2026-01-15", 450.00, "Pending"),

        (104, 4, "2026-01-18", 1500.00, "Completed"),

        (105, 5, "2026-01-20", 700.00, "Cancelled"),

        (106, 1, "2026-01-25", 950.00, "Completed"),

        (107, 6, "2026-02-01", 1100.00, "Pending"),

        (108, 7, "2026-02-05", 650.00, "Completed"),

        (109, 8, "2026-02-08", 900.00, "Completed"),

        (110, 10, "2026-02-10", 1250.00, "Pending")
    ]

    cursor.executemany(sql, orders)

    connection.commit()

    print(len(orders), "orders inserted.")

    cursor.close()
    connection.close()


def main():

    insert_orders()


if __name__ == "__main__":
    main()
```

---

# 10. Orders Data

| OrderID | CustomerID | OrderDate  |  Amount | Status    |
| ------: | ---------: | ---------- | ------: | --------- |
|     101 |          1 | 2026-01-10 | 1200.00 | Completed |
|     102 |          2 | 2026-01-12 |  850.00 | Completed |
|     103 |          3 | 2026-01-15 |  450.00 | Pending   |
|     104 |          4 | 2026-01-18 | 1500.00 | Completed |
|     105 |          5 | 2026-01-20 |  700.00 | Cancelled |
|     106 |          1 | 2026-01-25 |  950.00 | Completed |
|     107 |          6 | 2026-02-01 | 1100.00 | Pending   |
|     108 |          7 | 2026-02-05 |  650.00 | Completed |
|     109 |          8 | 2026-02-08 |  900.00 | Completed |
|     110 |         10 | 2026-02-10 | 1250.00 | Pending   |

---

# 11. Module 5 — Select Customers

Create:

```text
select_customers.py
```

## Question

Using Python, display all customers.

```python
from database import get_connection


def select_customers():

    connection = get_connection()

    cursor = connection.cursor()

    cursor.execute("""
        SELECT *
        FROM Customers
    """)

    rows = cursor.fetchall()

    print("Customers")
    print("--------------------------------")

    for row in rows:
        print(row)

    cursor.close()
    connection.close()


def main():

    select_customers()


if __name__ == "__main__":
    main()
```

---

# 12. Module 6 — Select Orders

## Question

Using Python, display all orders.

```python
from database import get_connection


def select_orders():

    connection = get_connection()

    cursor = connection.cursor()

    cursor.execute("""
        SELECT *
        FROM Orders
    """)

    rows = cursor.fetchall()

    print("Orders")
    print("--------------------------------")

    for row in rows:
        print(row)

    cursor.close()
    connection.close()


def main():

    select_orders()


if __name__ == "__main__":
    main()
```

---

# 13. Module 7 — Print Table Schema

## Question

Using Python, display the schema of both tables.

We can execute:

```sql
DESC Customers;
DESC Orders;
```

---

## Python Program

```python
from database import get_connection


def print_schema():

    connection = get_connection()

    cursor = connection.cursor()

    print("CUSTOMERS TABLE")
    print("--------------------------------")

    cursor.execute("DESC Customers")

    rows = cursor.fetchall()

    for row in rows:
        print(row)

    print()

    print("ORDERS TABLE")
    print("--------------------------------")

    cursor.execute("DESC Orders")

    rows = cursor.fetchall()

    for row in rows:
        print(row)

    cursor.close()
    connection.close()


def main():

    print_schema()


if __name__ == "__main__":
    main()
```

---

# 14. Expected Schema

## Customers

```text
CustomerID      INT              PRI
CustomerName    VARCHAR(100)
ContactName     VARCHAR(100)
City            VARCHAR(50)
Country         VARCHAR(50)
```

## Orders

```text
OrderID         INT              PRI
CustomerID      INT              MUL
OrderDate       DATE
Amount          DECIMAL(10,2)
Status          VARCHAR(20)
```

The important relationship is:

```text
Customers.CustomerID
        │
        │ PRIMARY KEY
        │
        ▼
Orders.CustomerID
        │
        │ FOREIGN KEY
        ▼
Customers.CustomerID
```

---

# 15. Module 8 — Basic INNER JOIN

Create:

```text
join_customers_orders.py
```

## Question

Using Python, display customer information together with order information.

We need:

* Customer name
* City
* Order ID
* Order date
* Amount
* Status

---

## SQL

```sql
SELECT
    Customers.CustomerName,
    Customers.City,
    Orders.OrderID,
    Orders.OrderDate,
    Orders.Amount,
    Orders.Status
FROM Customers
JOIN Orders
ON Customers.CustomerID = Orders.CustomerID;
```

---

## Python Program

```python
from database import get_connection


def customer_orders():

    connection = get_connection()

    cursor = connection.cursor()

    sql = """
        SELECT
            Customers.CustomerName,
            Customers.City,
            Orders.OrderID,
            Orders.OrderDate,
            Orders.Amount,
            Orders.Status

        FROM Customers

        JOIN Orders

        ON Customers.CustomerID = Orders.CustomerID
    """

    cursor.execute(sql)

    rows = cursor.fetchall()

    print("Customer Orders")
    print("--------------------------------")

    for row in rows:
        print(row)

    cursor.close()
    connection.close()


def main():

    customer_orders()


if __name__ == "__main__":
    main()
```

---

# 16. JOIN Result

| CustomerName             | City        | OrderID | OrderDate  |  Amount | Status    |
| ------------------------ | ----------- | ------: | ---------- | ------: | --------- |
| Alfreds Futterkiste      | Berlin      |     101 | 2026-01-10 | 1200.00 | Completed |
| Alfreds Futterkiste      | Berlin      |     106 | 2026-01-25 |  950.00 | Completed |
| Ana Trujillo Emparedados | Mexico City |     102 | 2026-01-12 |  850.00 | Completed |
| Antonio Moreno Taqueria  | Mexico City |     103 | 2026-01-15 |  450.00 | Pending   |
| Around the Horn          | London      |     104 | 2026-01-18 | 1500.00 | Completed |
| Berglunds Snabbkop       | Lulea       |     105 | 2026-01-20 |  700.00 | Cancelled |
| Blauer See Delikatessen  | Mannheim    |     107 | 2026-02-01 | 1100.00 | Pending   |
| Blondel Pere et Fils     | Strasbourg  |     108 | 2026-02-05 |  650.00 | Completed |
| Bolido Comidas           | Madrid      |     109 | 2026-02-08 |  900.00 | Completed |
| Bottom-Dollar Markets    | Tsawassen   |     110 | 2026-02-10 | 1250.00 | Pending   |

---

# 17. Module 9 — JOIN + WHERE

## Question 1

Using Python and `JOIN`, display customers from **Germany** and their orders.

### Python Program

```python
from database import get_connection


def german_customer_orders():

    connection = get_connection()

    cursor = connection.cursor()

    sql = """
        SELECT
            Customers.CustomerName,
            Customers.Country,
            Orders.OrderID,
            Orders.Amount,
            Orders.Status

        FROM Customers

        JOIN Orders

        ON Customers.CustomerID = Orders.CustomerID

        WHERE Customers.Country = %s
    """

    value = ("Germany",)

    cursor.execute(sql, value)

    rows = cursor.fetchall()

    print("German Customer Orders")
    print("--------------------------------")

    for row in rows:
        print(row)

    cursor.close()
    connection.close()


def main():

    german_customer_orders()


if __name__ == "__main__":
    main()
```

### Expected Result

| CustomerName            | Country | OrderID |  Amount | Status    |
| ----------------------- | ------- | ------: | ------: | --------- |
| Alfreds Futterkiste     | Germany |     101 | 1200.00 | Completed |
| Alfreds Futterkiste     | Germany |     106 |  950.00 | Completed |
| Blauer See Delikatessen | Germany |     107 | 1100.00 | Pending   |

---

# 18. Question 2 — JOIN + WHERE

## Question

Display all **Completed** orders with customer information.

### Python Program

```python
from database import get_connection


def completed_orders():

    connection = get_connection()

    cursor = connection.cursor()

    sql = """
        SELECT
            Customers.CustomerName,
            Customers.City,
            Orders.OrderID,
            Orders.Amount

        FROM Customers

        JOIN Orders

        ON Customers.CustomerID = Orders.CustomerID

        WHERE Orders.Status = %s
    """

    value = ("Completed",)

    cursor.execute(sql, value)

    rows = cursor.fetchall()

    print("Completed Orders")
    print("--------------------------------")

    for row in rows:
        print(row)

    cursor.close()
    connection.close()


def main():

    completed_orders()


if __name__ == "__main__":
    main()
```

---

# 19. Question 3 — JOIN + WHERE + ORDER BY

## Question

Display orders greater than `1000`.

Show:

* Customer name
* Country
* Order ID
* Amount

Sort by amount from highest to lowest.

### Python Program

```python
from database import get_connection


def high_value_orders():

    connection = get_connection()

    cursor = connection.cursor()

    sql = """
        SELECT
            Customers.CustomerName,
            Customers.Country,
            Orders.OrderID,
            Orders.Amount

        FROM Customers

        JOIN Orders

        ON Customers.CustomerID = Orders.CustomerID

        WHERE Orders.Amount > %s

        ORDER BY Orders.Amount DESC
    """

    value = (1000,)

    cursor.execute(sql, value)

    rows = cursor.fetchall()

    print("High Value Orders")
    print("--------------------------------")

    for row in rows:
        print(row)

    cursor.close()
    connection.close()


def main():

    high_value_orders()


if __name__ == "__main__":
    main()
```

---

# 20. Question 4 — JOIN + GROUP BY + COUNT

## Question

Find customers who have placed **more than one order**.

This introduces:

```text
JOIN
GROUP BY
COUNT()
HAVING
```

### Python Program

```python
from database import get_connection


def customers_with_multiple_orders():

    connection = get_connection()

    cursor = connection.cursor()

    sql = """
        SELECT
            Customers.CustomerID,
            Customers.CustomerName,
            COUNT(Orders.OrderID) AS TotalOrders

        FROM Customers

        JOIN Orders

        ON Customers.CustomerID = Orders.CustomerID

        GROUP BY
            Customers.CustomerID,
            Customers.CustomerName

        HAVING COUNT(Orders.OrderID) > %s
    """

    value = (1,)

    cursor.execute(sql, value)

    rows = cursor.fetchall()

    print("Customers With Multiple Orders")
    print("--------------------------------")

    for row in rows:
        print(row)

    cursor.close()
    connection.close()


def main():

    customers_with_multiple_orders()


if __name__ == "__main__":
    main()
```

### Expected Result

```text
(1, 'Alfreds Futterkiste', 2)
```

---

# 21. Question 5 — JOIN + SUM

## Question

Calculate the **total order amount for each customer**.

Display:

* Customer ID
* Customer name
* Total amount

Sort from highest total to lowest total.

### Python Program

```python
from database import get_connection


def customer_total_amount():

    connection = get_connection()

    cursor = connection.cursor()

    sql = """
        SELECT
            Customers.CustomerID,
            Customers.CustomerName,
            SUM(Orders.Amount) AS TotalAmount

        FROM Customers

        JOIN Orders

        ON Customers.CustomerID = Orders.CustomerID

        GROUP BY
            Customers.CustomerID,
            Customers.CustomerName

        ORDER BY TotalAmount DESC
    """

    cursor.execute(sql)

    rows = cursor.fetchall()

    print("Customer Total Order Amount")
    print("--------------------------------")

    for row in rows:
        print(row)

    cursor.close()
    connection.close()


def main():

    customer_total_amount()


if __name__ == "__main__":
    main()
```

---

# 22. Five Practice Questions

Now students can solve these without looking at the solutions.

## Question 1

Using Python, display:

```text
CustomerName
OrderID
Amount
```

for all customers and their orders.

---

## Question 2

Using Python + `JOIN`, display customers from:

```text
France
```

and their orders.

---

## Question 3

Using Python + `JOIN`, display orders with:

```text
Amount > 800
```

Sort by amount descending.

---

## Question 4

Using Python + `JOIN`, display only:

```text
Pending
```

orders along with customer names.

---

## Question 5

Using Python + `JOIN + GROUP BY + SUM`, calculate the total amount spent by each customer.

---

# 23. Important Python Pattern

Notice that every program follows almost the same structure:

```python
from database import get_connection


def operation():

    connection = get_connection()

    cursor = connection.cursor()

    sql = """
        SQL QUERY
    """

    cursor.execute(sql)

    rows = cursor.fetchall()

    for row in rows:
        print(row)

    cursor.close()
    connection.close()


def main():

    operation()


if __name__ == "__main__":
    main()
```

Only the **SQL query changes**.

---

# 24. What We Learned

```text
Python
   │
   ▼
mysql.connector
   │
   ▼
Connection
   │
   ▼
Cursor
   │
   ▼
SQL
   │
   ├── CREATE
   ├── INSERT
   ├── SELECT
   ├── JOIN
   ├── WHERE
   ├── ORDER BY
   ├── GROUP BY
   ├── COUNT
   ├── SUM
   └── HAVING
   │
   ▼
fetchall()
   │
   ▼
Python
```

## Database Relationship

```text
┌─────────────────────────────┐
│         Customers           │
├─────────────────────────────┤
│ PK CustomerID               │
│ CustomerName                │
│ ContactName                 │
│ City                        │
│ Country                     │
└──────────────┬──────────────┘
               │
               │ 1
               │
               │
               │ MANY
               ▼
┌─────────────────────────────┐
│           Orders            │
├─────────────────────────────┤
│ PK OrderID                  │
│ FK CustomerID               │
│ OrderDate                   │
│ Amount                      │
│ Status                      │
└─────────────────────────────┘
```

# Final Takeaway

> **Python manages the database connection and executes SQL.**

> **Primary Key uniquely identifies a record.**

> **Foreign Key connects records between tables.**

> **JOIN combines related data from multiple tables.**

> **`WHERE`, `ORDER BY`, `GROUP BY`, `COUNT()`, `SUM()` and `HAVING` allow us to perform useful operations on the joined data.**
