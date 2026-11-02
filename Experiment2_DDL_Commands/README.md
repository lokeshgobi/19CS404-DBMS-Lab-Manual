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
--
Insert a book with ISBN 978-1234567890, Title Data Science Essentials, Author Jane Doe, Publisher TechBooks, and Year 2024 into the Books table.

For example:

Test	                  Result
SELECT * FROM Books;    ISBN            Title                    Author      Publisher   Year
                        --------------  -----------------------  ----------  ----------  ----------
                        978-1234567890  Data Science Essentials  Jane Doe    TechBooks   2024


```sql
INSERT INTO Books (ISBN, Title, Author, Publisher, Year)
VALUES ('978-1234567890', 'Data Science Essentials', 'Jane Doe', 'TechBooks', 2024);
```

**Output:**

<img width="1277" height="347" alt="image" src="https://github.com/user-attachments/assets/4d183d43-fd1c-460b-8301-c472a0cefd58" />

**Question 2**
---
Create a new table named products with the following specifications:
* product_id as INTEGER and primary key.
* product_name as TEXT and not NULL.
* list_price as DECIMAL (10, 2) and not NULL.
* discount as DECIMAL (10, 2) with a default value of 0 and not NULL.
* A CHECK constraint at the table level to ensure:
   - list_price is greater than or equal to discount
   - discount is greater than or equal to 0
   - list_price is greater than or equal to 0
For example:

Test	                                                                                        Result
INSERT INTO products (product_id, product_name, list_price) VALUES (2, 'Product B', 50.00);   product_id  product_name  list_price  discount
SELECT * FROM products;                                                                       ----------  ------------  ----------  ----------
                                                                                              2           Product B     50          0




```sql
CREATE TABLE products (
    product_id INTEGER PRIMARY KEY,
    product_name TEXT NOT NULL,
    list_price DECIMAL(10, 2) NOT NULL,
    discount DECIMAL(10, 2) NOT NULL DEFAULT 0,
    CHECK (
        list_price >= discount
        AND discount >= 0
        AND list_price >= 0
    )
);
```

**Output:**

<img width="1277" height="388" alt="image" src="https://github.com/user-attachments/assets/e09d9e07-2bff-4b9e-bca8-0e5a3842b609" />


**Question 3**
---
Create a table named Members with the following columns:

* MemberID as INTEGER
* MemberName as TEXT
* JoinDate as DATE
For example:

Test	                               Result:
pragma table_info('Members');        cid         name        type        notnull     dflt_value  pk
                                     ----------  ----------  ----------  ----------  ----------  ----------
                                     0           MemberID    INTEGER     0                       0
                                     1           MemberName  TEXT        0                       0
                                     2           JoinDate    DATE        0                       0


```sql
CREATE TABLE Members (
    MemberID INTEGER,
    MemberName TEXT,
    JoinDate DATE
);
```

**Output:**

<img width="1275" height="490" alt="image" src="https://github.com/user-attachments/assets/90cfddd4-d636-4736-ab90-0c78912f6289" />


**Question 4**
---
Create a new table named contacts with the following specifications:
* contact_id as INTEGER and primary key.
* first_name as TEXT and not NULL.
* last_name as TEXT and not NULL.
* email as TEXT.
* phone as TEXT and not NULL with a check constraint to ensure the length of phone is at least 10 characters.
For example:

Test	                                                                      Result :
INSERT INTO contacts (contact_id, first_name, last_name, email, phone)      contact_id  first_name  last_name   email                 phone
VALUES (1, 'John', 'Doe', 'john.doe@example.com', '1234567890');            ----------  ----------  ----------  --------------------  ----------
SELECT * FROM contacts;                                                     1           John        Doe         john.doe@example.com  1234567890


```sql
CREATE TABLE contacts (
    contact_id INTEGER PRIMARY KEY,
    first_name TEXT NOT NULL,
    last_name TEXT NOT NULL,
    email TEXT,
    phone TEXT NOT NULL CHECK (LENGTH(phone) >= 10)
);
```

**Output:**

<img width="1262" height="447" alt="image" src="https://github.com/user-attachments/assets/74d972f5-d4c4-4dce-8687-d4eef7f720a3" />


**Question 5**
---
Insert the following students into the Student_details table:
RollNo      Name        Gender      Subject     MARKS
----------  ----------  ----------  ----------  ----------
202            Ella King         F           Chemistry   87
203            James Bond   M          Literature    78

 

 

For example:

Test                                             Result :
SELECT * FROM Student_details;                   RollNo      Name        Gender      Subject     MARKS
                                                 ----------  ----------  ----------  ----------  ----------
                                                 202         Ella King   F           Chemistry   87
                                                 203         James Bond  M           Literature  78


```sql
INSERT INTO Student_details (RollNo, Name, Gender, Subject, MARKS)
VALUES
(202, 'Ella King', 'F', 'Chemistry', 87),
(203, 'James Bond', 'M', 'Literature', 78);
```

**Output:**

<img width="1243" height="382" alt="image" src="https://github.com/user-attachments/assets/3ffc1457-27d4-4f09-ba5a-576733466575" />


**Question 6**
---
Write an SQL Query to add the attributes designation, net_salary, and dob to the Companies table with the following data types:
* designation as VARCHAR(50)
* net_salary as NUMBER
* dob as DATE
 

 

For example:

Test	                                    Result :
pragma table_info('Companies');           cid         name        type        notnull     dflt_value  pk
                                          ----------  ----------  ----------  ----------  ----------  ----------
                                          0           id          int         0                       0
                                          1           name        varchar(50  0                       0
                                          2           address     text        0                       0
                                          3           email       varchar(50  0                       0
                                          4           phone       varchar(10  0                       0
                                          5           designatio  varchar(50  0                       0
                                          6           net_salary  number      0                       0
                                          7           dob         date        0                       0

```sql
ALTER TABLE Companies ADD COLUMN designation varchar(50);
ALTER TABLE Companies ADD COLUMN net_salary number;
ALTER TABLE Companies ADD COLUMN dob date;
```

**Output:**

<img width="1268" height="535" alt="image" src="https://github.com/user-attachments/assets/39021343-bc52-45dd-b660-f9eed09a39cc" />


**Question 7**
---
Write a SQL query to Add a new column named "discount" with the data type DECIMAL(5,2) to the "customer" table.

Sample table: customer

 customer_id |   cust_name    |    city    | grade | salesman_id 
-------------+----------------+------------+-------+-------------
        3002 | Nick Rimando   | New York   |   100 |        5001
        3007 | Brad Davis     | New York   |   200 |        5001
        3005 | Graham Zusi    | California |   200 |        5002
 

For example:

Test	                                   Result :
pragma table_info('customer');           cid         name         type                               notnull     dflt_value  pk
                                         ----------  -----------  ---------------------------------  ----------  ----------  ----------
                                         0           customer_id  integer primarykey auto increment  0                       0
                                         1           cust_name    varchar2(30)                       0                       0
                                         2           city         varchar(30)                        0                       0
                                         3           grade        number                             0                       0
                                         4           salesman_id  number                             0                       0
                                         5           discount     DECIMAL(5,2)                       0                       0


```sql
ALTER TABLE customer
ADD COLUMN discount DECIMAL(5,2);
```

**Output:**

<img width="1282" height="475" alt="image" src="https://github.com/user-attachments/assets/a176b9bf-c224-49da-a49e-a6a2eaad1745" />


**Question 8**
---
Create a new table named item with the following specifications and constraints:
  1. item_id as TEXT and as primary key.
  2. item_desc as TEXT.
  3. rate as INTEGER.
  4. icom_id as TEXT with a length of 4.
  5. icom_id is a foreign key referencing com_id in the company table.
  6. The foreign key should set NULL on updates and deletes.
  7. item_desc and rate should not accept NULL.
For example:

Test	                                                       Result :
INSERT INTO item VALUES("ITM5","Charlie Gold",700,"COM4");   item_id     item_desc     rate        icom_id
UPDATE company SET com_id='COM5' WHERE com_id='COM4';        ----------  ------------  ----------  ----------
SELECT * FROM item;                                          ITM5        Charlie Gold  700

```sql
CREATE TABLE item (
    item_id TEXT PRIMARY KEY,
    item_desc TEXT NOT NULL,
    rate INTEGER NOT NULL,
    icom_id TEXT(4),
    FOREIGN KEY (icom_id)
        REFERENCES company(com_id)
        ON UPDATE SET NULL
        ON DELETE SET NULL
);
```

**Output:**

<img width="1248" height="467" alt="image" src="https://github.com/user-attachments/assets/33c6c315-7fee-4325-9b57-ca645a822883" />


**Question 9**
---
Insert all employees from Former_employees into Employee

Table attributes are EmployeeID, Name, Department, Salary

For example:

Test	                      Result :
select * from Employee;     EmployeeID  Name        Department  Salary
                            ----------  ----------  ----------  ----------
                            201         John Doe    HR          50000
                            202         Jane Smith  Engineerin  75000
                            203         Emily Davi  Marketing   60000


```sql
INSERT INTO Employee (EmployeeID, Name, Department, Salary)
SELECT EmployeeID, Name, Department, Salary
FROM Former_employees;
```

**Output:**

<img width="1255" height="402" alt="image" src="https://github.com/user-attachments/assets/edf10110-81f8-4295-a42d-dd4dc83d65dd" />


**Question 10**
---
Create a table named Employees with the following constraints:

 * EmployeeID should be the primary key.
 * FirstName and LastName should be NOT NULL.
 * Email should be unique.
 * Salary should be greater than 0.
 * DepartmentID should be a foreign key referencing the Departments table.
For example:

Test	                                                                                 Result : 
-- Attempt to insert a record with NULL FirstName                                      Error: NOT NULL constraint failed: Employees.FirstName
INSERT INTO Employees (EmployeeID, FirstName, LastName, Email, Salary, DepartmentID)
VALUES (1, NULL, 'Doe', 'john.doe@example.com', 50000, 1);


```sql
CREATE TABLE Employees (
    EmployeeID INTEGER PRIMARY KEY,
    FirstName TEXT NOT NULL,
    LastName TEXT NOT NULL,
    Email TEXT UNIQUE,
    Salary REAL CHECK (Salary > 0),
    DepartmentID INTEGER,
    FOREIGN KEY (DepartmentID) REFERENCES Departments(DepartmentID)
);
```

**Output:**

<img width="1272" height="557" alt="image" src="https://github.com/user-attachments/assets/191dbfb6-c646-484c-9dd1-25a35bf65373" />



## RESULT
Thus, the SQL queries to implement different types of constraints and DDL commands have been executed successfully.
