# Experiment 4: Aggregate Functions, Group By and Having Clause

## AIM
To study and implement aggregate functions, GROUP BY, and HAVING clause with suitable examples.

## THEORY

### Aggregate Functions
These perform calculations on a set of values and return a single value.

- **MIN()** – Smallest value  
- **MAX()** – Largest value  
- **COUNT()** – Number of rows  
- **SUM()** – Total of values  
- **AVG()** – Average of values

**Syntax:**
```sql
SELECT AGG_FUNC(column_name) FROM table_name WHERE condition;
```
### GROUP BY
Groups records with the same values in specified columns.
**Syntax:**
```sql
SELECT column_name, AGG_FUNC(column_name)
FROM table_name
GROUP BY column_name;
```
### HAVING
Filters the grouped records based on aggregate conditions.
**Syntax:**
```sql
SELECT column_name, AGG_FUNC(column_name)
FROM table_name
GROUP BY column_name
HAVING condition;
```

**Question 1**
--
Write a SQL query to find the number of employees who are having the same age removing the duplicate values.

Sample table: employee

id  name  age  address     salary
1   Paul  32   California  20000
4   Mark  25   Richtown    65000
5   David 27   Texas       85000

For example:

Result

COUNT
----------
4



```sql
SELECT COUNT(DISTINCT age) AS COUNT
FROM employee;
```

**Output:**
<img width="1347" height="445" alt="image" src="https://github.com/user-attachments/assets/0cf9d57f-e3a9-459e-8ea2-c5c7442ac366" />


**Question 2**
---
Write a SQL query to find the total income of employees aged 40 or above.

Table: employee

name        type
----------  ----------
id          INTEGER
name        TEXT
age         INTEGER
city        TEXT
income      INTEGER
For example:

Result
total_income
------------
1800000


```sql
SELECT SUM(income) AS total_income
FROM employee
WHERE age >= 40;
```

**Output:**
<img width="1317" height="443" alt="image" src="https://github.com/user-attachments/assets/1b9c7c44-e080-45ad-a7ba-e4188a5cc771" />


**Question 3**
---

Write a SQL query to find What is the age difference between the youngest and oldest employee in the company.

Table: employee

name        type
----------  ----------
id          INTEGER
name        TEXT
age         INTEGER
city        TEXT
income      INTEGER
For example:

Result
age_difference
--------------
13

```sql
SELECT MAX(age) - MIN(age) AS age_difference
FROM employee;
```

**Output:**


<img width="1313" height="428" alt="image" src="https://github.com/user-attachments/assets/a6d09698-baa0-43a8-af13-ea6fad470b1b" />


**Question 4**
---
Which cities (addresses) in the "customer1" table have an average salary lesser than Rs. 15000

Sample table: customer1

<img width="1342" height="233" alt="image" src="https://github.com/user-attachments/assets/db19960e-3363-41a3-9f19-5cba6b77c631" />

For example:

Result
address     AVG(salary)
----------  -----------
Ahmedabad   2000.0
Bhopal      8500.0
Delhi       1500.0
Hyderabad   4500.0
Indore      10000.0
Kota        2000.0
Mumbai      6500.0


```sql
SELECT address, AVG(salary)
FROM customer1
GROUP BY address
HAVING AVG(salary) < 15000
ORDER BY address;
```

**Output:**

<img width="1307" height="736" alt="image" src="https://github.com/user-attachments/assets/7e6cbac3-79c5-4e4b-8f04-9694a41dafdf" />


**Question 5**
---
Write the SQL query that achieves the grouping of data by occupation, calculates the average work hours for each occupation, and includes only those occupations where the average work hour falls between 10 and 12.

Sample table: employee1

<img width="1117" height="217" alt="image" src="https://github.com/user-attachments/assets/40d74b4c-a70f-4858-8c81-3bdb6b4b1a8d" />


For example:

Result
occupation  AVG(workhour)
----------  -------------
Business    10.0
Engineer    12.0


```sql
SELECT occupation, AVG(workhour)
FROM employee1
GROUP BY occupation
HAVING AVG(workhour) BETWEEN 10 AND 12;
```

**Output:**

<img width="1320" height="511" alt="image" src="https://github.com/user-attachments/assets/3412e334-0c41-4783-9ae2-614ce96070fe" />


## RESULT
Thus, the SQL queries to implement aggregate functions, GROUP BY, and HAVING clause have been executed successfully.
