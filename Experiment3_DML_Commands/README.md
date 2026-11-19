# Experiment 3: DML Commands

## AIM
To study and implement DML (Data Manipulation Language) commands.

## THEORY

### 1. INSERT INTO
Used to add records into a relation.
These are three type of INSERT INTO queries which are as
A)Inserting a single record
**Syntax (Single Row):**
```sql
INSERT INTO table_name (field_1, field_2, ...) VALUES (value_1, value_2, ...);
```
**Syntax (Multiple Rows):**
```sql
INSERT INTO table_name (field_1, field_2, ...) VALUES
(value_1, value_2, ...),
(value_3, value_4, ...);
```
**Syntax (Insert from another table):**
```sql
INSERT INTO table_name SELECT * FROM other_table WHERE condition;
```
### 2. UPDATE
Used to modify records in a relation.
Syntax:
```sql
UPDATE table_name SET column1 = value1, column2 = value2 WHERE condition;
```
### 3. DELETE
Used to delete records from a relation.
**Syntax (All rows):**
```sql
DELETE FROM table_name;
```
**Syntax (Specific condition):**
```sql
DELETE FROM table_name WHERE condition;
```
### 4. SELECT
Used to retrieve records from a table.
**Syntax:**
```sql
SELECT column1, column2 FROM table_name WHERE condition;
```
**Question 1**
--
Write a SQL statement to Increase the salary by 500 and email as 'updated' for employees with job ID 'SA_REP' and commission percentage greater than 0.15

Employees table

---------------
employee_id
first_name
last_name
email
phone_number
hire_date
job_id
salary
commission_pct
manager_id
department_id

Test :
SELECT EMPLOYEE_ID, FIRST_NAME, EMAIL, SALARY, JOB_ID FROM EMPLOYEES 
WHERE job_id = 'SA_REP' AND EMAIL='updated' LIMIT 5;

Result :
EMPLOYEE_ID  FIRST_NAME  EMAIL       SALARY      JOB_ID
-----------  ----------  ----------  ----------  ----------
150          Peter       updated     10500       SA_REP
151          David       updated     10000       SA_REP
152          Peter       updated     9500        SA_REP
153          Christophe  updated     8500        SA_REP
154          Nanette     updated     8000        SA_REP
```sql
UPDATE Employees
SET salary = salary + 500,
    email = 'updated'
WHERE job_id = 'SA_REP'
  AND commission_pct > 0.15;
```

**Output:**
<img width="1287" height="653" alt="image" src="https://github.com/user-attachments/assets/a1d7f0e0-78cc-41ea-9338-8501ed1f10cf" />



**Question 2**
---
Write a SQL statement to Update the address to '58 Lakeview, Magnolia' where supplier ID is 5 in the suppliers table.

Suppliers Table 

name               type
-----------------  ---------------
supplier_id        INT
supplier_name      VARCHAR(100)
contact_person     VARCHAR(100)
phone_number       VARCHAR(20)
email              VARCHAR(100)
address            VARCHAR(250)
For example:

Test :
select changes();

Result:
changes()
----------
1


```sql
UPDATE suppliers
SET address = '58 Lakeview, Magnolia'
WHERE supplier_id = 5;
```

**Output:**

<img width="1286" height="522" alt="image" src="https://github.com/user-attachments/assets/435ce90b-5d28-4434-a3fc-7298f4ef408f" />


**Question 3**
---
Write a SQL statement to increase the salary of employees under the department 40, 90 and 110 according to the company rules.

Salary will be increased by 25% for the department 40, 15% for department 90 and 10% for the department 110 and the rest of the departments will remain same.

Employees table

---------------
employee_id
first_name
last_name
email
phone_number
hire_date
job_id
salary
commission_pct
manager_id
department_id
For example:

Test :
SELECT EMPLOYEE_ID, FIRST_NAME, SALARY, PHONE_NUMBER, EMAIL, JOB_ID FROM EMPLOYEES LIMIT 10;

Result :
EMPLOYEE_ID  FIRST_NAME  SALARY      PHONE_NUMBER  EMAIL       JOB_ID
-----------  ----------  ----------  ------------  ----------  ----------
100          Steven      27600       515.123.4567  SKING       AD_PRES
101          Neena       19550       515.123.4568  NKOCHHAR    AD_VP
102          Lex         19550       515.123.4569  LDEHAAN     AD_VP
103          Alexander   9000        590.423.4567  AHUNOLD     IT_PROG
104          Bruce       6000        590.423.4568  BERNST      IT_PROG
105          David       4800        590.423.4569  DAUSTIN     IT_PROG
106          Valli       4800        590.423.4560  VPATABAL    IT_PROG
107          Diana       4200        590.423.5567  DLORENTZ    IT_PROG
108          Nancy       12000       515.124.4569  NGREENBE    FI_MGR
109          Daniel      9000        515.124.4169  DFAVIET     FI_ACCOUNT


```sql
UPDATE Employees
SET salary = CASE
    WHEN department_id = 40 THEN ROUND(salary * 1.25)
    WHEN department_id = 90 THEN ROUND(salary * 1.15)
    WHEN department_id = 110 THEN ROUND(salary * 1.10)
    ELSE salary
END
WHERE department_id IN (40, 90, 110);
```

**Output:**
<img width="1330" height="577" alt="image" src="https://github.com/user-attachments/assets/8b1911fd-0987-4611-b4d2-980fda7213b8" />


**Question 4**
---
Write a SQL statement to update the product_name as 'Grapefruit' whose product_id is 4 in the products table.

products table

---------------
product_id
product_name
category_id
availability

```sql
UPDATE products
SET product_name = 'Grapefruit'
WHERE product_id = 4;
```

**Output:**

<img width="1293" height="366" alt="image" src="https://github.com/user-attachments/assets/ddcc46d4-cb19-443e-98ab-9f15af862984" />


**Question 5**
---
Write a SQL statement to Update the grade of all customers in Chennai city as  5. 

Customer table (customer_id,cust_name,city,grade,salesman_id)

```sql
UPDATE Customer
SET grade = 5
WHERE city = 'Chennai';
```

**Output:**

<img width="1298" height="601" alt="image" src="https://github.com/user-attachments/assets/b2c7d199-a8c5-46a2-a1b2-79fd791649b9" />

## RESULT
Thus, the SQL queries to implement DML commands have been executed successfully.
