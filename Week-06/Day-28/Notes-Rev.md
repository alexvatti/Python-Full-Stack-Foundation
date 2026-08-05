# SQLite CRUD Operations Using Python (Menu Driven)

```python
import sqlite3


# ======================================
# Database Connection
# ======================================

def db_connect():
    conn = sqlite3.connect("college.db")
    cursor = conn.cursor()
    return conn, cursor


# ======================================
# Database Close
# ======================================

def db_close(conn):
    conn.close()


# ======================================
# Select Table
# ======================================

def select_table():

    print("\nSelect Table")
    print("1. Student")
    print("2. Employee")
    print("3. Product")
    print("4. Book")
    print("5. Patient")

    choice = input("Enter Choice : ")

    tables = {
        "1": "Student",
        "2": "Employee",
        "3": "Product",
        "4": "Book",
        "5": "Patient"
    }

    return tables.get(choice)
```

---

# Insert Sample Data

```python
def insert_sample_data(conn, cursor):

    table = select_table()

    if table == "Student":

        data = [
            (1, "Rahul", 20, "CSE", 88),
            (2, "Priya", 21, "ECE", 91),
            (3, "Kiran", 19, "IT", 79),
            (4, "Sneha", 22, "EEE", 85),
            (5, "Arjun", 20, "MECH", 73)
        ]

        cursor.executemany(
            "INSERT INTO Student VALUES(?,?,?,?,?)", data
        )

    elif table == "Employee":

        data = [
            (1, "Ramesh", "HR", 35000),
            (2, "Suresh", "IT", 55000),
            (3, "Mahesh", "Sales", 42000),
            (4, "Anitha", "Finance", 60000),
            (5, "Divya", "Admin", 30000)
        ]

        cursor.executemany(
            "INSERT INTO Employee VALUES(?,?,?,?)", data
        )

    elif table == "Product":

        data = [
            (1, "Laptop", 65000, 10),
            (2, "Mouse", 500, 50),
            (3, "Keyboard", 1200, 25),
            (4, "Monitor", 12000, 15),
            (5, "Printer", 9000, 8)
        ]

        cursor.executemany(
            "INSERT INTO Product VALUES(?,?,?,?)", data
        )

    elif table == "Book":

        data = [
            (1, "Python", "Guido", 550),
            (2, "Java", "James", 650),
            (3, "C Programming", "Dennis", 450),
            (4, "DBMS", "Navathe", 700),
            (5, "AI Basics", "Andrew", 850)
        ]

        cursor.executemany(
            "INSERT INTO Book VALUES(?,?,?,?)", data
        )

    elif table == "Patient":

        data = [
            (1, "Ravi", 35, "Fever"),
            (2, "Sita", 28, "Diabetes"),
            (3, "John", 42, "BP"),
            (4, "Mary", 31, "Cold"),
            (5, "Krishna", 55, "Asthma")
        ]

        cursor.executemany(
            "INSERT INTO Patient VALUES(?,?,?,?)", data
        )

    conn.commit()

    print("Sample Data Inserted Successfully.")
```

---

# Insert Record

```python
def insert_record(conn, cursor):

    table = select_table()

    if table == "Student":

        id = int(input("ID : "))
        name = input("Name : ")
        age = int(input("Age : "))
        branch = input("Branch : ")
        marks = float(input("Marks : "))

        cursor.execute(
            "INSERT INTO Student VALUES(?,?,?,?,?)",
            (id, name, age, branch, marks)
        )

    elif table == "Employee":

        id = int(input("ID : "))
        name = input("Name : ")
        dept = input("Department : ")
        salary = float(input("Salary : "))

        cursor.execute(
            "INSERT INTO Employee VALUES(?,?,?,?)",
            (id, name, dept, salary)
        )

    elif table == "Product":

        id = int(input("ID : "))
        pname = input("Product Name : ")
        price = float(input("Price : "))
        qty = int(input("Quantity : "))

        cursor.execute(
            "INSERT INTO Product VALUES(?,?,?,?)",
            (id, pname, price, qty)
        )

    elif table == "Book":

        id = int(input("ID : "))
        title = input("Title : ")
        author = input("Author : ")
        price = float(input("Price : "))

        cursor.execute(
            "INSERT INTO Book VALUES(?,?,?,?)",
            (id, title, author, price)
        )

    elif table == "Patient":

        id = int(input("ID : "))
        name = input("Name : ")
        age = int(input("Age : "))
        disease = input("Disease : ")

        cursor.execute(
            "INSERT INTO Patient VALUES(?,?,?,?)",
            (id, name, age, disease)
        )

    conn.commit()

    print("Record Inserted Successfully.")
```

---

# Select Records

```python
def select_records(cursor):

    table = select_table()

    cursor.execute(f"SELECT * FROM {table}")

    rows = cursor.fetchall()

    print("\nRecords\n")

    for row in rows:
        print(row)
```

---

# Update Record

```python
def update_record(conn, cursor):

    table = select_table()

    if table == "Student":

        id = int(input("Student ID : "))
        marks = float(input("New Marks : "))

        cursor.execute(
            "UPDATE Student SET marks=? WHERE id=?",
            (marks, id)
        )

    elif table == "Employee":

        id = int(input("Employee ID : "))
        salary = float(input("New Salary : "))

        cursor.execute(
            "UPDATE Employee SET salary=? WHERE id=?",
            (salary, id)
        )

    elif table == "Product":

        id = int(input("Product ID : "))
        qty = int(input("New Quantity : "))

        cursor.execute(
            "UPDATE Product SET quantity=? WHERE id=?",
            (qty, id)
        )

    elif table == "Book":

        id = int(input("Book ID : "))
        price = float(input("New Price : "))

        cursor.execute(
            "UPDATE Book SET price=? WHERE id=?",
            (price, id)
        )

    elif table == "Patient":

        id = int(input("Patient ID : "))
        disease = input("New Disease : ")

        cursor.execute(
            "UPDATE Patient SET disease=? WHERE id=?",
            (disease, id)
        )

    conn.commit()

    print("Record Updated Successfully.")
```

---

# Delete Record

```python
def delete_record(conn, cursor):

    table = select_table()

    id = int(input("Enter ID : "))

    cursor.execute(
        f"DELETE FROM {table} WHERE id=?",
        (id,)
    )

    conn.commit()

    print("Record Deleted Successfully.")
```

---

# Show Tables

```python
def show_tables(cursor):

    cursor.execute("""
        SELECT name
        FROM sqlite_master
        WHERE type='table'
        ORDER BY name
    """)

    tables = cursor.fetchall()

    print("\nAvailable Tables\n")

    for table in tables:
        print(table[0])
```

---

# Menu

```python
def menu():

    conn, cursor = db_connect()

    while True:

        print("\n========== MENU ==========")
        print("1. Insert Sample Data")
        print("2. Insert Record")
        print("3. Select Records")
        print("4. Update Record")
        print("5. Delete Record")
        print("6. Show Tables")
        print("7. Exit")
        print("==========================")

        choice = input("Enter Choice : ")

        if choice == "1":
            insert_sample_data(conn, cursor)

        elif choice == "2":
            insert_record(conn, cursor)

        elif choice == "3":
            select_records(cursor)

        elif choice == "4":
            update_record(conn, cursor)

        elif choice == "5":
            delete_record(conn, cursor)

        elif choice == "6":
            show_tables(cursor)

        elif choice == "7":
            db_close(conn)
            print("Thank You...")
            break

        else:
            print("Invalid Choice")


menu()
```
