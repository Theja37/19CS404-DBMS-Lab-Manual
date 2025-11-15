# Experiment 5: Subqueries and Views

## AIM
To study and implement subqueries and viewS.

## THEORY

### Subqueries
A subquery is a query inside another SQL query and is embedded in:
- WHERE clause
- HAVING clause
- FROM clause

**Types:**
- **Single-row subquery**:
  Sub queries can also return more than one value. Such results should be made use along with the operators in and any.
- **Multiple-row subquery**:
  Here more than one subquery is used. These multiple sub queries are combined by means of ‘and’ & ‘or’ keywords.
- **Correlated subquery**:
  A subquery is evaluated once for the entire parent statement whereas a correlated Sub query is evaluated once per row processed by the parent statement.

**Example:**
```sql
SELECT * FROM employees
WHERE salary > (SELECT AVG(salary) FROM employees);
```
### Views
A view is a virtual table based on the result of an SQL SELECT query.
**Create View:**
```sql
CREATE VIEW view_name AS
SELECT column1, column2 FROM table_name WHERE condition;
```
**Drop View:**
```sql
DROP VIEW view_name;
```

**Question 1**
--
![image](https://github.com/user-attachments/assets/88a40189-1c37-46f2-a17b-05be8863d0df)


```sql
SELECT student_name, grade
FROM GRADES g
WHERE grade = (
    SELECT MAX(grade)
    FROM GRADES
    WHERE subject = g.subject
);

```

**Output:**

![image](https://github.com/user-attachments/assets/233b3847-f3fc-4aba-9cac-41ca40ce7be7)


**Question 2**
---
![image](https://github.com/user-attachments/assets/48392dd7-9605-4f2e-a581-6671544614c5)


```sql
SELECT department_id, department_name
FROM Departments
WHERE LENGTH(department_name) > (
    SELECT AVG(LENGTH(department_name)) FROM Departments
);

```

**Output:**

![image](https://github.com/user-attachments/assets/e9120de9-feb3-4af4-98a6-ba0006a37b0d)


**Question 3**
---
![image](https://github.com/user-attachments/assets/0d538172-1fb3-4392-9e6e-aa0a2a4f1437)


```sql
SELECT medication_id, medication_name, dosage
FROM Medications
WHERE CAST(SUBSTR(dosage, 1, LENGTH(dosage) - 2) AS INT) = (
    SELECT MIN(CAST(SUBSTR(dosage, 1, LENGTH(dosage) - 2) AS INT))
    FROM Medications
);

```

**Output:**

![image](https://github.com/user-attachments/assets/54939113-1feb-4e78-8e8d-909bc85eeb9c)


**Question 4**
---
![image](https://github.com/user-attachments/assets/ea483a91-f965-4f5b-a2b6-6a371794ca64)


```sql
SELECT name
FROM customer
WHERE phone IN (
    SELECT phone
    FROM customer
    GROUP BY phone
    HAVING COUNT(*) = 1
);

```

**Output:**

![image](https://github.com/user-attachments/assets/b01928cc-8c21-4a01-ab4e-356f89a8d4f5)


**Question 5**
---
![image](https://github.com/user-attachments/assets/20c82144-3e21-4aba-b00c-2c7a9a94b006)


```sql
SELECT name, city
FROM customer
WHERE city IN (
    SELECT city
    FROM customer
    WHERE id IN (3, 7)
);

```

**Output:**

![image](https://github.com/user-attachments/assets/cd291f07-9f36-448c-ba98-3f17caf78693)


**Question 6**
---
![image](https://github.com/user-attachments/assets/b2d46683-5f7a-4d69-9055-ce50784025a2)


```sql
SELECT id, name, age, city, income
FROM Employee
WHERE age < (
    SELECT AVG(age)
    FROM Employee
    WHERE income > 250000
);

```

**Output:**

![image](https://github.com/user-attachments/assets/a0d2c4c8-ac09-4ca2-bdb3-319161dd7fb0)


**Question 7**
---
![image](https://github.com/user-attachments/assets/48666326-10be-48ed-8046-6d3a49cb2e26)


```sql
SELECT commission
FROM salesman
WHERE salesman_id IN
(SELECT salesman_id FROM customer WHERE city='Paris');
```

**Output:**

![image](https://github.com/user-attachments/assets/626a2880-134a-43ee-b4ad-84e61d6e85ce)


**Question 8**
---
![image](https://github.com/user-attachments/assets/fde8c7f8-f5d0-4b41-a35b-99522c58fda5)


```sql
SELECT ord_no, purch_amt, ord_date, customer_id, salesman_id
FROM ORDERS
WHERE purch_amt > (
    SELECT AVG(purch_amt)
    FROM ORDERS
    WHERE ord_date = '2012-10-10'
);
```

**Output:**

![image](https://github.com/user-attachments/assets/510460f5-4d53-445c-8532-892d8a2babdb)


**Question 9**
---
![image](https://github.com/user-attachments/assets/6eda3db2-9f9d-4abf-b54e-5de7ba245a35)


```sql
SELECT o.ord_no, o.purch_amt, o.ord_date, o.customer_id, o.salesman_id
FROM ORDERS o
JOIN SALESMAN s ON o.salesman_id = s.salesman_id
WHERE s.city = 'New York';
```

**Output:**

![image](https://github.com/user-attachments/assets/ec9fdd44-8505-43dd-bfc1-a30ab7afb8cc)


**Question 10**
---

![image](https://github.com/user-attachments/assets/652f0357-af5d-407f-a7e1-f13f1504aa2f)

```sql
SELECT *
FROM CUSTOMERS
WHERE SALARY < 2500;
```

**Output:**

![image](https://github.com/user-attachments/assets/f6cab633-780c-4363-931a-074c0e1308ae)



## RESULT
Thus, the SQL queries to implement subqueries and views have been executed successfully.
