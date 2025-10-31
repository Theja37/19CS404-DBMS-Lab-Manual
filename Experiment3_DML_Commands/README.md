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
Increase the reorder level by 30% for products from 'Food' category having quantity in stock less than 50% of existing reorder level in the products table
name               type
--------------  ----------
product_id         INT
product_name       VARCHAR(10)
category           VARCHAR(50)
cost_price         DECIMAL(10)
sell_price         DECIMAL(10)
reorder_lvl        INT
quantity              INT
supplier_id           INT

```sql
UPDATE products
SET reorder_lvl = reorder_lvl*1.30
WHERE category = 'Food' and quantity < 0.5*reorder_lvl;
```

**Output:**

<img width="1185" height="486" alt="image" src="https://github.com/user-attachments/assets/880f4eb8-59d4-4108-8eea-f9d5ec901db5" />


**Question 2**
---
Write a SQL statement to double the availability of the product with product_id 1.

products table

---------------
product_id
product_name
category_id
availability

```sql
UPDATE products
SET availability = 2*availability
WHERE product_id=1;
```

**Output:**

<img width="1220" height="342" alt="image" src="https://github.com/user-attachments/assets/80fd2d34-7014-4d12-a695-1d45fdf3781a" />


**Question 3**
---
 Update the total selling price to quantity sold multiplied by updated selling price per unit where product id is 10 in the sales table.

SALES TABLE
name               type
-----------------  ---------------
sale_id            INT
sale_date          DATE
product_id         INT
quantity           INT
sell_price         DECIMAL(10,2)
total_sell_price   DECIMAL(10,2)

```sql
UPDATE sales
SET total_sell_price = quantity*sell_price
WHERE product_id = 10;
```

**Output:**

<img width="1170" height="552" alt="image" src="https://github.com/user-attachments/assets/bde4d550-66a7-425d-a086-c9e465ea9641" />


**Question 4**
---
Write a SQL statement to change the email column of employees table with 'Unavailable' for all employees in employees table.

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

```sql
UPDATE employees
SET email='Unavailable';
```

**Output:**

<img width="1211" height="509" alt="image" src="https://github.com/user-attachments/assets/8b79c4b9-be34-440a-ac70-cf805d8914ad" />


**Question 5**
---
Write a SQL query to Delete customers with 'GRADE' 3 or 'AGENT_CODE' 'A008' whose 'OUTSTANDING_AMT' is less than 5000

Sample table: Customer

```sql
DELETE FROM Customer
WHERE (GRADE=3 OR AGENT_CODE='A008') AND OUTSTANDING_AMT<5000
```

**Output:**
<img width="1177" height="496" alt="image" src="https://github.com/user-attachments/assets/f0220a6f-91ee-48e0-96ac-935c3afb5f05" />


**Question 6**
---
Write a SQL query to Delete customers with following conditions

'CUST_COUNTRY' is not in a list of specified countries ('UK', 'USA', 'Canada')
'GRADE' is greater than or equal to 3
```sql
DELETE from Customer
WHERE CUST_COUNTRY NOT IN ('UK', 'USA', 'Canada') AND GRADE>=3;
```

**Output:**

<img width="1214" height="505" alt="image" src="https://github.com/user-attachments/assets/7c6a35ba-067e-4831-aebf-fced42fce634" />


**Question 7**
---
Write a SQL query to Delete customers from 'customer' table where 'GRADE' is less than 2.

 
Sample table: Customer

```sql
DELETE from Customer
WHERE Grade<2;
```

**Output:**

<img width="773" height="639" alt="image" src="https://github.com/user-attachments/assets/53833ec4-fe90-47ef-bb2e-e7b47685ef02" />


**Question 8**
---
Write a SQL statement to retrieve city(column name) of all customers from customers table without any repeats.

```sql
SELECT DISTINCT city
FROM customers;
```

**Output:**

<img width="510" height="584" alt="image" src="https://github.com/user-attachments/assets/8c52a794-4881-487f-a1a7-286785201221" />


**Question 9**
---
Write a query to find all the employees whose salary is between 50000 to 100000 from employeeposition table.

```sql
SELECT *
FROM employeeposition
WHERE Salary BETWEEN 50000 and 100000;
```

**Output:**

<img width="1122" height="332" alt="image" src="https://github.com/user-attachments/assets/7d2c8807-aa82-4e64-962b-b62701f13ac9" />


**Question 10**
---
Write a SQL query to classify value2 in the Calculations table as 'Small', 'Medium', or 'Large' based on whether it is less than 10, between 10 and 50, or greater than 50, respectively.

```sql
SELECT id,
    value2,
    CASE
        WHEN value2<10 THEN 'Small'
        WHEN value2>=10 AND value2<=50 THEN 'Medium'
        WHEN value2>50 THEN 'Large'
    END AS size_category
FROM Calculations;
```

**Output:**

<img width="982" height="563" alt="image" src="https://github.com/user-attachments/assets/a491f653-b7b8-44fd-bc6e-12a2449bed24" />


## RESULT
Thus, the SQL queries to implement DML commands have been executed successfully.
