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

Create a table named Events with the following columns: EventID as INTEGER,EventName as TEXT,EventDate as DATE

<img width="965" height="238" alt="Screenshot 2025-09-27 082653" src="https://github.com/user-attachments/assets/58c5840e-4ded-4fca-99c6-a873434fb8c8" />

**Query:**
```sql
create table Events(
EventID INTEGER,
EventName TEXT,
EventDate DATE
);
```

**Output:**

<img width="1228" height="468" alt="Screenshot 2025-09-27 082801" src="https://github.com/user-attachments/assets/b44690c1-ee5c-4635-a3af-1f61a206ac3f" />


**Question 2**

Write a SQL query to Rename the "city" column to "location" in the "customer" table.

Sample table: customer

 customer_id |   cust_name    |    city    | grade | salesman_id 
-------------+----------------+------------+-------+-------------
        3002 | Nick Rimando   | New York   |   100 |        5001
        3007 | Brad Davis     | New York   |   200 |        5001
        3005 | Graham Zusi    | California |   200 |        5002
        
<img width="1195" height="313" alt="Screenshot 2025-09-27 083019" src="https://github.com/user-attachments/assets/28509651-ebfa-4a18-b3df-cfcd05580b30" />

**Query:**
```sql
Alter table customer Rename city to location;
```

**Output:**

<img width="1236" height="416" alt="Screenshot 2025-09-27 083132" src="https://github.com/user-attachments/assets/795900be-3805-4026-9040-2bf248a56c21" />


**Question 3**

Create a new table named item with the following specifications and constraints:
item_id as TEXT and as primary key.
item_desc as TEXT.
rate as INTEGER.
icom_id as TEXT with a length of 4.
icom_id is a foreign key referencing com_id in the company table.
The foreign key should cascade updates and deletes.
item_desc and rate should not accept NULL.

<img width="1048" height="200" alt="Screenshot 2025-09-27 083218" src="https://github.com/user-attachments/assets/2d4789b6-6ee6-4917-bd70-4752b2a9d9d0" />

**Query:**
```sql
Create table item(
item_id TEXT primary key,
item_desc TEXT NOT NULL,
rate INTEGER NOT NULL,
icom_id TEXT CHECK(length(icom_id)=4),
foreign key(icom_id) references company(com_id)
ON UPDATE CASCADE 
ON DELETE CASCADE
);
```

**Output:**

<img width="1221" height="426" alt="Screenshot 2025-09-27 083318" src="https://github.com/user-attachments/assets/05bf0a2e-48bd-4b4a-9695-240265e43b7d" />


**Question 4**

Write an SQL query to add two new columns, designation and net_salary, to the table Companies. The designation column should have a data type of varchar(50), and the net_salary column should have a data type of number.

<img width="991" height="344" alt="Screenshot 2025-09-27 083422" src="https://github.com/user-attachments/assets/19beeb37-ede5-4fe2-ac72-8800c3c1805c" />

**Query:**
```sql
Alter table Companies add designation varchar(50);
Alter table Companies add net_salary number;
```

**Output:**

<img width="1223" height="475" alt="Screenshot 2025-09-27 083520" src="https://github.com/user-attachments/assets/820df652-d26f-4207-a9b6-d6d2cb9d32b0" />


**Question 5**

Insert a book with ISBN 978-1234567890, Title Data Science Essentials, Author Jane Doe, Publisher TechBooks, and Year 2024 into the Books table.

<img width="921" height="206" alt="Screenshot 2025-09-27 083558" src="https://github.com/user-attachments/assets/5e68f5b2-cd31-4746-9a36-2a8c93508e4f" />

**Query:**
```sql
Insert into Books(ISBN,Title,Author,Publisher,Year)
Values('978-1234567890', 'Data Science Essentials', 'Jane Doe', 'TechBooks', 2024);
```

**Output:**

<img width="1230" height="313" alt="Screenshot 2025-09-27 083649" src="https://github.com/user-attachments/assets/0a79b930-bb42-4295-930b-bc90b68208f1" />


**Question 6**

create a table named jobs including columns job_id, job_title, min_salary and max_salary, and make sure that, the default value for job_title is blank and min_salary is 8000 and max_salary is NULL will be entered automatically at the time of insertion if no value assigned for the specified columns.

<img width="1213" height="189" alt="Screenshot 2025-09-27 083819" src="https://github.com/user-attachments/assets/45cc3458-2724-48b5-9ec4-e14cb752731e" />

**Query:**
```sql
CREATE TABLE jobs(
job_id INT,
job_title BLANK,
min_salary INTEGER DEFAULT 8000,
max_salary INTEGER DEFAULT NULL
);
```

**Output:**

<img width="1226" height="405" alt="Screenshot 2025-09-27 084002" src="https://github.com/user-attachments/assets/2a40a428-62f7-4759-a997-c9944158f204" />


**Question 7**

Create a table named Shipments with the following constraints:
ShipmentID as INTEGER should be the primary key.
ShipmentDate as DATE.
SupplierID as INTEGER should be a foreign key referencing Suppliers(SupplierID).
OrderID as INTEGER should be a foreign key referencing Orders(OrderID).

<img width="1220" height="146" alt="Screenshot 2025-09-27 084124" src="https://github.com/user-attachments/assets/62fca1b1-f966-40e1-947b-1315e8d7d0d5" />

**Query:**
```sql
CREATE TABLE Shipments(
ShipmentID INTEGER primary key,
ShipmentDate DATE,
SupplierID INTEGER,
OrderID INTEGER,
foreign key(SupplierID) references Suppliers(SupplierID)
foreign key(OrderID) references Orders(OrderID)
);
```

**Output:**

<img width="1227" height="319" alt="Screenshot 2025-09-27 084245" src="https://github.com/user-attachments/assets/a3bd7b4a-d465-4a11-8203-d39b41888419" />


**Question 8**

Insert the following customers into the Customers table:

CustomerID  Name         Address     City        ZipCode
----------  -----------  ----------  ----------  ----------
302         Laura Croft  456 Elm St  Seattle     98101
303         Bruce Wayne  789 Oak St  Gotham      10001

<img width="849" height="237" alt="Screenshot 2025-09-27 084427" src="https://github.com/user-attachments/assets/0028ef7c-4285-4335-8646-f2bdd3a4c504" />

**Query:**
```sql
INSERT INTO Customers(CustomerID, Name, Address, City, ZipCode)
VALUES(302, 'Laura Croft', '456 Elm St', 'Seattle', 98101);
INSERT INTO Customers(CustomerID, Name, Address, City, ZipCode)
VALUES(303,'Bruce Wayne', '789 Oak St',  'Gotham', 10001);
```

**Output:**

<img width="1227" height="444" alt="Screenshot 2025-09-27 084353" src="https://github.com/user-attachments/assets/3f437d84-7716-4986-b5d2-5c02b584c7b3" />


**Question 9**

Insert all students from Archived_students table into the Student_details table.

cid         name        type        notnull     dflt_value  pk
----------  ----------  ----------  ----------  ----------  ----------
0           RollNo      INT           0                       1
1           Name        VARCHAR(100)  0                       0
2           Gender      VARCHAR(10)   0                       0
3           Subject     VARCHAR(50)   0                       0
4           MARKS       INT           0                       0

<img width="905" height="244" alt="Screenshot 2025-09-27 084507" src="https://github.com/user-attachments/assets/8be0c50a-9ad5-4c2b-8005-0a15db1c4a21" />

**Query:**
```sql
INSERT INTO Student_details(RollNo,Name,Gender,Subject,MARKS)
SELECT RollNo,Name,Gender,Subject,MARKS
FROM Archived_students;
```

**Output:**

<img width="1227" height="375" alt="Screenshot 2025-09-27 084559" src="https://github.com/user-attachments/assets/b0df5c8b-3cb0-4655-9b8f-803219fd5bb3" />


**Question 10**

Create a new table named contacts with the following specifications:
contact_id as INTEGER and primary key.
first_name as TEXT and not NULL.
last_name as TEXT and not NULL.
email as TEXT.
phone as TEXT and not NULL with a check constraint to ensure the length of phone is at least 10 characters.

<img width="1212" height="188" alt="Screenshot 2025-09-27 084639" src="https://github.com/user-attachments/assets/fc1cf1ef-0f62-4320-beca-33a9f940f1ee" />

**Query:**
```sql
CREATE table contacts(
contact_id INTEGER primary key,
first_name TEXT NOT NULL,
last_name TEXT NOT NULL,
email TEXT,
phone TEXT NOT NULL,
CHECK(length(phone)>=10)
);
```

**Output:**

<img width="1232" height="383" alt="Screenshot 2025-09-27 084744" src="https://github.com/user-attachments/assets/0c1a005a-435f-4e4b-bca2-f410b5be4050" />

## Module 1 Home Challenge-Grade

<img width="1325" height="70" alt="Screenshot 2025-09-27 084900" src="https://github.com/user-attachments/assets/a1f9ff55-9f39-4183-a21f-4ab3191a7902" />

## RESULT
Thus, the SQL queries to implement different types of constraints and DDL commands have been executed successfully.
