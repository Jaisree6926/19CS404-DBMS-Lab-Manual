# Experiment 2: DDL Commands

## AIM
To study and implement DDL commands and different types of constraints.

## THEORY

### 1. CREATE
Used to create a new relation (table).

**Syntax:**
```sql
CREATE TABLE (
  field_1 data_type(size),
  field_2 data_type(size),
  ...
);
```
### 2. ALTER
Used to add, modify, drop, or rename fields in an existing relation.
(a) ADD
```sql
ALTER TABLE std ADD (Address CHAR(10));
```
(b) MODIFY
```sql
ALTER TABLE relation_name MODIFY (field_1 new_data_type(size));
```
(c) DROP
```sql
ALTER TABLE relation_name DROP COLUMN field_name;
```
(d) RENAME
```sql
ALTER TABLE relation_name RENAME COLUMN old_field_name TO new_field_name;
```
### 3. DROP TABLE
Used to permanently delete the structure and data of a table.
```sql
DROP TABLE relation_name;
```
### 4. RENAME
Used to rename an existing database object.
```sql
RENAME TABLE old_relation_name TO new_relation_name;
```
### CONSTRAINTS
Constraints are used to specify rules for the data in a table. If there is any violation between the constraint and the data action, the action is aborted by the constraint. It can be specified when the table is created (using CREATE TABLE) or after it is created (using ALTER TABLE).
### 1. NOT NULL
When a column is defined as NOT NULL, it becomes mandatory to enter a value in that column.
Syntax:
```sql
CREATE TABLE Table_Name (
  column_name data_type(size) NOT NULL
);
```
### 2. UNIQUE
Ensures that values in a column are unique.
Syntax:
```sql
CREATE TABLE Table_Name (
  column_name data_type(size) UNIQUE
);
```
### 3. CHECK
Specifies a condition that each row must satisfy.
Syntax:
```sql
CREATE TABLE Table_Name (
  column_name data_type(size) CHECK (logical_expression)
);
```
### 4. PRIMARY KEY
Used to uniquely identify each record in a table.
Properties:
Must contain unique values.
Cannot be null.
Should contain minimal fields.
Syntax:
```sql
CREATE TABLE Table_Name (
  column_name data_type(size) PRIMARY KEY
);
```
### 5. FOREIGN KEY
Used to reference the primary key of another table.
Syntax:
```sql
CREATE TABLE Table_Name (
  column_name data_type(size),
  FOREIGN KEY (column_name) REFERENCES other_table(column)
);
```
### 6. DEFAULT
Used to insert a default value into a column if no value is specified.

Syntax:
```sql
CREATE TABLE Table_Name (
  col_name1 data_type,
  col_name2 data_type,
  col_name3 data_type DEFAULT 'default_value'
);
```

**Question 1**

--Insert the below data into the Employee table, allowing the Department and Salary columns to take their default values.

      
        EmployeeID  Name         Position
        ----------  -----------  ----------
        4           Emily White  Analyst

```sql
-- INSERT INTO Employee (EmployeeID, Name, Position) VALUES (4, 'Emily White', 'Analyst');
```

**Output:**

<img width="1083" height="283" alt="Screenshot 2025-05-13 200015" src="https://github.com/user-attachments/assets/506055ca-4e5b-48f3-8373-fe49c538485a" />


**Question 2**

---In the Employee table, insert a record where some fields are NULL, another record where all fields are filled without any NULL values, and a third record where some fields are filled, and others are left as NULL.

-- 

    EmployeeID  Name          Position    Department  Salary
    ----------  ------------  ----------  ----------  ----------
    5           George Clark  Consultant
    7           Noah Davis    Manager     HR          60000
    8           Ava Miller    Consultant  IT


```sql
       INSERT INTO Employee VALUES (5, 'George Clark', 'Consultant', NULL, NULL);
       INSERT INTO Employee VALUES (7, 'Noah Davis', 'Manager', 'HR', 60000);
       INSERT INTO Employee VALUES (8, 'Ava Miller', 'Consultant', 'IT', NULL);
```
**Output:**

<img width="1161" height="194" alt="Screenshot 2025-05-13 200231" src="https://github.com/user-attachments/assets/187d679b-b293-4e9d-9a6a-b36c9d2c0f94" />


**Question 3**
---
-- Create a table named Department with the following constraints:

DepartmentID as INTEGER should be the primary key.
DepartmentName as TEXT should be unique and not NULL.
Location as TEXT.

```sql
-- CREATE TABLE Department (
    DepartmentID INTEGER PRIMARY KEY,
    DepartmentName TEXT NOT NULL,
    Location TEXT,
    UNIQUE(DepartmentName)
);
```

**Output:**

<img width="1196" height="126" alt="Screenshot 2025-05-13 200835" src="https://github.com/user-attachments/assets/823b840c-9576-4ad3-b74a-f9887d53be38" />


**Question 4**
---
-- Create a table named Invoices with the following constraints:

InvoiceID as INTEGER should be the primary key.
InvoiceDate as DATE.
Amount as REAL should be greater than 0.
DueDate as DATE should be greater than the InvoiceDate.
OrderID as INTEGER should be a foreign key referencing Orders(OrderID).

```sql
-- CREATE TABLE Invoices (
    InvoiceID INTEGER PRIMARY KEY,
    InvoiceDate DATE,
    Amount REAL CHECK (Amount > 0),
    DueDate DATE CHECK (DueDate > InvoiceDate),
    OrderID INTEGER,
    FOREIGN KEY (OrderID) REFERENCES Orders(OrderID)
);
```

**Output:**

<img width="1162" height="122" alt="Screenshot 2025-05-13 200607" src="https://github.com/user-attachments/assets/375f72be-7c8a-4e72-b0e4-fa505de06e0b" />


**Question 5**
---
--Create a table named jobs including columns job_id, job_title, min_salary and max_salary, and make sure that, the default value for job_title is blank and min_salary is 8000 and max_salary is NULL will be entered automatically at the time of insertion if no value assigned for the specified columns.

```sql
-- CREATE TABLE jobs (
    job_id INTEGER PRIMARY KEY,
    job_title TEXT DEFAULT '',
    min_salary INTEGER DEFAULT 8000,
    max_salary INTEGER DEFAULT NULL
);
```

**Output:**

<img width="1038" height="150" alt="Screenshot 2025-05-13 203519" src="https://github.com/user-attachments/assets/17ac070c-97c9-4255-a245-762e1d466f6e" />


**Question 6**
---
-- Create a table named Orders with the following constraints: OrderID as INTEGER should be the primary key. OrderDate as DATE should be not NULL. CustomerID as INTEGER should be a foreign key referencing Customers(CustomerID).



```sql
-- CREATE TABLE Orders (
    OrderID INTEGER PRIMARY KEY,
    OrderDate DATE NOT NULL,
    CustomerID INTEGER,
    FOREIGN KEY (CustomerID) REFERENCES Customers(CustomerID)
);
```

**Output:**

<img width="1279" height="169" alt="Screenshot 2025-05-13 203702" src="https://github.com/user-attachments/assets/e8e83fab-4763-4ff3-b1d4-e0a257629cb8" />


**Question 7**
---
-- Write a SQL query to Add a new column Mobilenumber as number in the Student_details table.

Sample table: Student_details

    cid              name             type             notnu  dflt_value  pk
    ---------------  ---------------  ---------------  -----  ----------  ----------
    0                RollNo           int              0                  1
    1                Name             VARCHAR(100)     1                  0
    2                Gender           TEXT             1                  0
    3                Subject          VARCHAR(30)      0                  0
    4                MARKS            INT (3)          0                  0
    ```

```sql
--ALTER TABLE Student_details ADD Mobilenumber number;
```

**Output:**

<img width="1170" height="217" alt="Screenshot 2025-05-13 203810" src="https://github.com/user-attachments/assets/78305ca1-ed31-4bb5-823c-0b1f468cac1d" />


**Question 8**
---
--Write a SQL query to add a new column MobileNumber of type NUMBER and a new column Address of type VARCHAR(100) to the Student_details table.

```sql
-- ALTER TABLE Student_details ADD MobileNumber NUMBER;
ALTER TABLE Student_details ADD Address VARCHAR(100);
```

**Output:**

<img width="1174" height="233" alt="Screenshot 2025-05-13 203901" src="https://github.com/user-attachments/assets/e282366d-23f6-4699-80f5-1f16a14b793b" />


**Question 9**
---
-- Create a table named Reviews with the following columns:
- ReviewID as INTEGER
- ProductID as INTEGER
- Rating as REAL
- ReviewText as TEXT
```sql
-- CREATE TABLE Reviews (
    ReviewID INTEGER,
    ProductID INTEGER,
    Rating REAL,
    ReviewText TEXT
);
```

**Output:**


<img width="992" height="190" alt="Screenshot 2025-05-13 204017" src="https://github.com/user-attachments/assets/19f4eef0-7759-4a87-be38-b345f269fc1c" />


**Question 10**
---
--Insert all books from Out_of_print_books into Books

Table attributes are ISBN, Title, Author, Publisher, YearPublished

```sql
-- INSERT INTO Books SELECT * FROM Out_of_print_books;
```

**Output:**

<img width="1186" height="165" alt="Screenshot 2025-05-13 204119" src="https://github.com/user-attachments/assets/d0426610-7c04-4cab-a82a-2a532b092853" />



## RESULT
Thus, the SQL queries to implement different types of constraints and DDL commands have been executed successfully.
