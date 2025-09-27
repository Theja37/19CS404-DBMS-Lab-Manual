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
Create a table named Orders with the following columns:
OrderID as INTEGER
OrderDate as TEXT
CustomerID as INTEGER

<img width="933" height="247" alt="image" src="https://github.com/user-attachments/assets/80cf1962-eded-45a6-9d81-b8fae281f575" />


```sql
Create table Orders(
OrderID INTEGER,
OrderDate TEXT,
CustomerID INTEGER
);
```

**Output:**

<img width="1211" height="441" alt="image" src="https://github.com/user-attachments/assets/6eba465b-8590-4c43-bce2-c95c8bcc57c1" />

**Question 2**
---
Insert all books from Out_of_print_books into Books

Table attributes are ISBN, Title, Author, Publisher, YearPublished
<img width="973" height="262" alt="image" src="https://github.com/user-attachments/assets/7d413e39-76fa-418a-9446-e1d31c76b840" />


```sql
INSERT INTO Books(ISBN, Title, Author, Publisher, YearPublished)
SELECT ISBN, Title, Author, Publisher, YearPublished 
FROM Out_of_print_books
```

**Output:**

<img width="1157" height="386" alt="image" src="https://github.com/user-attachments/assets/72eb5dbd-3541-49f9-bf6a-c57d8deef2e9" />


**Question 3**
---
Create a table named Invoices with the following constraints:
InvoiceID as INTEGER should be the primary key.
InvoiceDate as DATE.
Amount as REAL should be greater than 0.
DueDate as DATE should be greater than the InvoiceDate.
OrderID as INTEGER should be a foreign key referencing Orders(OrderID).
<img width="1225" height="200" alt="image" src="https://github.com/user-attachments/assets/c251bbee-3c69-4083-9ab0-d5643046dae5" />


```sql
CREATE table Invoices(
InvoiceID INTEGER primary key,
InvoiceDate DATE,
Amount REAL CHECK(Amount>0),
DueDate DATE CHECK(DueDate>InvoiceDate),
OrderID INTEGER,
foreign key(OrderID) references Orders(OrderID)
);
```

**Output:**

<img width="1205" height="358" alt="image" src="https://github.com/user-attachments/assets/81830ea1-3c6b-4ca1-971d-b21d6508ae71" />


**Question 4**
---
Write an SQL query to add a new column email of type TEXT to the Student_details table, and ensure that this column cannot contain NULL values and make default value as 'Invalid'
<img width="1089" height="195" alt="image" src="https://github.com/user-attachments/assets/b2a43866-05cd-4edc-88bd-e7f22cd99e35" />


```sql
ALTER table Student_details add email TEXT NOT NULL DEFAULT 'Invalid';
```

**Output:**

<img width="1192" height="313" alt="image" src="https://github.com/user-attachments/assets/e76ab166-d03e-47eb-9311-80e71dc14a59" />


**Question 5**
---
Insert the following students into the Student_details table:
RollNo      Name        Gender      Subject     MARKS
----------  ----------  ----------  ----------  ----------
202            Ella King         F           Chemistry   87
203            James Bond   M          Literature    78
<img width="866" height="234" alt="image" src="https://github.com/user-attachments/assets/3ae7a799-cd7f-4ce7-86a7-2df114dd97f8" />


```sql
INSERT INTO Student_details
Values(202,'Ella King','F','Chemistry',87);
INSERT INTO Student_details
Values (203,'James Bond','M','Literature',78);
```

**Output:**

<img width="1208" height="321" alt="image" src="https://github.com/user-attachments/assets/e432ecde-679c-474d-9bc3-64c4544bd553" />


**Question 6**
---
Create a table named ProjectAssignments with the following constraints:
AssignmentID as INTEGER should be the primary key.
EmployeeID as INTEGER should be a foreign key referencing Employees(EmployeeID).
ProjectID as INTEGER should be a foreign key referencing Projects(ProjectID).
AssignmentDate as DATE should be NOT NULL.
<img width="1198" height="136" alt="image" src="https://github.com/user-attachments/assets/ebe2f007-f224-42c3-ad87-f145aa1941aa" />


```sql
Create table ProjectAssignments(
AssignmentID INTEGER primary key,
EmployeeID INTEGER,
ProjectID INTEGER,
AssignmentDate DATE NOT NULL,
foreign key(EmployeeID) references Employees(EmployeeID)
foreign key(ProjectID) references Projects(ProjectID)

);
```

**Output:**

<img width="1190" height="359" alt="image" src="https://github.com/user-attachments/assets/6635d045-5f29-4d25-adb6-c28e435305ba" />


**Question 7**
---
Write an SQL query to add two new columns, first_name and last_name, to the table employee. Both columns should have a data type of varchar(50).

<img width="960" height="263" alt="image" src="https://github.com/user-attachments/assets/bb597dc9-f741-4adb-8865-0726ee19f72d" />


```sql
ALTER table employee ADD first_name varchar(50);
ALTER table employee ADD last_name varchar(50);
```

**Output:**

<img width="1204" height="383" alt="image" src="https://github.com/user-attachments/assets/e0bb7e12-bcc8-4787-9afe-11cd4722046a" />


**Question 8**
---
Insert the below data into the Books table, allowing the Publisher and Year columns to take their default values.

ISBN             Title                 Author
---------------  --------------------  ---------------
978-6655443321   Big Data Analytics    Karen Adams

Note: The Publisher and Year columns will use their default values.

<img width="792" height="213" alt="image" src="https://github.com/user-attachments/assets/6421bd49-2a32-436a-a84f-ef5e66b722b5" />


```sql
INSERT INTO Books(ISBN, Title, Author)
values('978-6655443321','Big Data Analytics','Karen Adams');
```

**Output:**

<img width="1208" height="387" alt="image" src="https://github.com/user-attachments/assets/4eb7a2aa-9190-4661-8fb1-1b3dbd4e9ab8" />


**Question 9**
---
create a table named jobs including columns job_id, job_title, min_salary and max_salary, and make sure that, the default value for job_title is blank and min_salary is 8000 and max_salary is NULL will be entered automatically at the time of insertion if no value assigned for the specified columns.

<img width="1214" height="222" alt="image" src="https://github.com/user-attachments/assets/a5cc670d-a4e6-4240-9671-671888b9b7d8" />

```sql
CREATE table jobs(
job_id INTEGER,
job_title blank,
min_salary INTEGER DEFAULT 8000,
max_salary INTEGER DEFAULT NULL
);
```

**Output:**

<img width="1202" height="401" alt="image" src="https://github.com/user-attachments/assets/4fbfdb1b-19c7-4237-a526-edac3705d294" />


**Question 10**
---
Create a table named Products with the following constraints:
ProductID as INTEGER should be the primary key.
ProductName as TEXT should be unique and not NULL.
Price as REAL should be greater than 0.
StockQuantity as INTEGER should be non-negative.

<img width="1212" height="182" alt="image" src="https://github.com/user-attachments/assets/fab9870b-49cf-4b8e-a00d-108681a3e4aa" />


```sql
CREATE table Products(
ProductID INTEGER primary key,
ProductName TEXT unique NOT NULL,
Price REAL CHECK(Price>0),
StockQuantity INTEGER CHECK(StockQuantity>0)
);
```

**Output:**

<img width="1194" height="332" alt="image" src="https://github.com/user-attachments/assets/d0c8688b-b57b-4383-a96f-d7110e23b3d4" />



## RESULT
Thus, the SQL queries to implement different types of constraints and DDL commands have been executed successfully.
