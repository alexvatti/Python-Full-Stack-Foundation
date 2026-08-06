# Python Full Stack Foundation

# Week-07 – Day-32

# MySQL CRUD Operations using Modular Programming

In the previous session, we created two common files.

```
config.py
database.py
```

Every program below uses the common database connection.

There is **no need to write the MySQL connection code again**.

Simply import the connection function.

```python
from database import get_connection
```

---

# Program-1

# Create Student Table

```python
from database import get_connection


def create_table():

    connection = get_connection()

    cursor = connection.cursor()

    cursor.execute("""
    CREATE TABLE IF NOT EXISTS Student(
        id INT AUTO_INCREMENT PRIMARY KEY,
        name VARCHAR(50),
        department VARCHAR(30),
        marks INT
    )
    """)

    connection.commit()

    print("Student table created successfully.")

    cursor.close()
    connection.close()


def main():

    create_table()


if __name__ == "__main__":
    main()
```

---

# Program-2

# Insert One Record

```python
from database import get_connection


def insert_record():

    connection = get_connection()

    cursor = connection.cursor()

    sql = """
    INSERT INTO Student(name, department, marks)
    VALUES(%s, %s, %s)
    """

    values = ("Alex", "CSE", 91)

    cursor.execute(sql, values)

    connection.commit()

    print("One record inserted successfully.")

    cursor.close()
    connection.close()


def main():

    insert_record()


if __name__ == "__main__":
    main()
```

---

# Program-3

# Insert Multiple Records

```python
from database import get_connection


def insert_multiple_records():

    connection = get_connection()

    cursor = connection.cursor()

    sql = """
    INSERT INTO Student(name, department, marks)
    VALUES(%s, %s, %s)
    """

    students = [
        ("John", "ECE", 88),
        ("Priya", "CSE", 95),
        ("Neha", "IT", 84),
        ("Ravi", "EEE", 79)
    ]

    cursor.executemany(sql, students)

    connection.commit()

    print("Multiple records inserted successfully.")

    cursor.close()
    connection.close()


def main():

    insert_multiple_records()


if __name__ == "__main__":
    main()
```

---

# Program-4

# Select All Records

```python
from database import get_connection


def select_records():

    connection = get_connection()

    cursor = connection.cursor()

    cursor.execute("SELECT * FROM Student")

    rows = cursor.fetchall()

    print("Student Records")
    print("------------------------------")

    for row in rows:
        print(row)

    cursor.close()
    connection.close()


def main():

    select_records()


if __name__ == "__main__":
    main()
```

---

# Program-5

# Search Records using WHERE

```python
from database import get_connection


def search_records():

    connection = get_connection()

    cursor = connection.cursor()

    sql = """
    SELECT *
    FROM Student
    WHERE department=%s
    """

    value = ("CSE",)

    cursor.execute(sql, value)

    rows = cursor.fetchall()

    print("CSE Students")
    print("----------------")

    for row in rows:
        print(row)

    cursor.close()
    connection.close()


def main():

    search_records()


if __name__ == "__main__":
    main()
```

---

# Program-6

# ORDER BY

```python
from database import get_connection


def order_by_marks():

    connection = get_connection()

    cursor = connection.cursor()

    cursor.execute("""
    SELECT *
    FROM Student
    ORDER BY marks DESC
    """)

    rows = cursor.fetchall()

    print("Students Sorted by Marks")
    print("----------------------------")

    for row in rows:
        print(row)

    cursor.close()
    connection.close()


def main():

    order_by_marks()


if __name__ == "__main__":
    main()
```

---

# Program-7

# LIMIT

```python
from database import get_connection


def limit_records():

    connection = get_connection()

    cursor = connection.cursor()

    cursor.execute("""
    SELECT *
    FROM Student
    LIMIT 3
    """)

    rows = cursor.fetchall()

    print("Top 3 Records")
    print("----------------")

    for row in rows:
        print(row)

    cursor.close()
    connection.close()


def main():

    limit_records()


if __name__ == "__main__":
    main()
```

---

# Program-8

# Update Record

```python
from database import get_connection


def update_record():

    connection = get_connection()

    cursor = connection.cursor()

    sql = """
    UPDATE Student
    SET marks=%s
    WHERE id=%s
    """

    values = (95, 1)

    cursor.execute(sql, values)

    connection.commit()

    print("Record updated successfully.")

    cursor.close()
    connection.close()


def main():

    update_record()


if __name__ == "__main__":
    main()
```

---

# Program-9

# Delete Record

```python
from database import get_connection


def delete_record():

    connection = get_connection()

    cursor = connection.cursor()

    sql = """
    DELETE FROM Student
    WHERE id=%s
    """

    value = (1,)

    cursor.execute(sql, value)

    connection.commit()

    print("Record deleted successfully.")

    cursor.close()
    connection.close()


def main():

    delete_record()


if __name__ == "__main__":
    main()
```

---

# Summary

In all the above programs:

- `config.py` stores the database credentials.
- `database.py` provides the reusable `get_connection()` function.
- Each program imports the common connection function.
- Only the SQL operation changes from one program to another.
- This modular approach avoids code duplication and follows industry-standard Python practices.
