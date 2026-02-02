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
Create a table named Orders with the following constraints:
OrderID as INTEGER should be the primary key.
OrderDate as DATE should be not NULL.
CustomerID as INTEGER should be a foreign key referencing Customers(CustomerID).

```sql
create table Orders(
OrderID int primary key,
OrderDate date not null,
CustomerID int,
foreign key (CustomerID) references Customers(CustomerID)
);
```

**Output:**

<img width="1314" height="629" alt="image" src="https://github.com/user-attachments/assets/f13a1b5e-e6bf-49d1-bc95-2621f222cf79" />


**Question 2**
---
Create a new table named contacts with the following specifications:
contact_id as INTEGER and primary key.
first_name as TEXT and not NULL.
last_name as TEXT and not NULL.
email as TEXT.
phone as TEXT and not NULL with a check constraint to ensure the length of phone is at least 10 characters.

```sql
create table contacts(
contact_id int primary key,
first_name text not null,
last_name text not null,
email text,
phone text not null check(length(phone)>=10)
);
```

**Output:**

<img width="1305" height="664" alt="image" src="https://github.com/user-attachments/assets/5cf29697-de20-4838-82fc-7a117b49e48c" />


**Question 3**
---
Insert the below data into the Student_details table, allowing the Subject and MARKS columns to take their default values.

RollNo      Name          Gender      
----------  ------------  ----------  
204         Samuel Black  M          

Note: The Subject and MARKS columns will use their default values.
 

```sql
insert into Student_details (RollNo,Name,Gender)
values
(204,'Samuel Black','M')
```

**Output:**

<img width="798" height="645" alt="image" src="https://github.com/user-attachments/assets/f30ede1e-6a85-40d1-96b9-ef1e10ed969d" />


**Question 4**
---
Write a SQL query to add birth_date attribute as timestamp (datatype) in the table customer 

Sample table: customer

 customer_id |   cust_name    |    city    | grade | salesman_id 
-------------+----------------+------------+-------+-------------
        3002 | Nick Rimando   | New York   |   100 |        5001
        3007 | Brad Davis     | New York   |   200 |        5001
        3005 | Graham Zusi    | California |   200 |        5002
 

```sql
alter table customer add birth_date timestamp;
```

**Output:**
<img width="1068" height="491" alt="image" src="https://github.com/user-attachments/assets/85890195-279c-4fbd-9479-6d3304f0ca99" />


**Question 5**
---
Write a SQL Query for inserting the below values in the table Customers

ID               NAME             AGE  ADDRESS     SALARY      
---------------  ---------------  ---  ----------  ----------  
1                Ramesh           32   Ahmedabad   2000
2                Khilan           25   Delhi       1500
3                Kaushik          23   Kota        2000

```sql
insert into Customers
values
(1,'Ramesh','32','Ahmedabad','2000'),
(2,'Khilan','25','Delhi','1500'),
(3,'Kaushik','23','Kota','2000')
```

**Output:**



**Question 6**
---
-- Paste Question 6 here

```sql
alter table Student_details add Country TEXT;
```

**Output:**

<img width="934" height="509" alt="image" src="https://github.com/user-attachments/assets/8f7cd56e-8d2c-4081-8607-aaf961efb53a" />


**Question 7**
---
Write a SQL query to Add a new column Country as text in the Student_details table.

Sample table: Student_details

 cid              name             type   notnull     dflt_value  pk
---------------  ---------------  -----  ----------  ----------  ----------
0                RollNo           int    0                       1
1                Name             VARCH  1                       0
2                Gender           TEXT   1                       0
3                Subject          VARCH  0                       0
4                MARKS            INT (  0                       0

```sql
create table Products(
ProductID INTEGER,
ProductName TEXT,
Price REAL,
Stock INTEGER
);
```

**Output:**

<img width="1084" height="622" alt="image" src="https://github.com/user-attachments/assets/3adb6b49-9eba-47fc-8dff-d1f601450e8a" />


**Question 8**
---
Create a table named Invoices with the following constraints:

InvoiceID as INTEGER should be the primary key.
InvoiceDate as DATE.
DueDate as DATE should be greater than the InvoiceDate.
Amount as REAL should be greater than 0.

```sql
create table Invoices(
InvoiceID INTEGER PRIMARY KEY,
InvoiceDate DATE,
DueDate DATE check (DueDate>InvoiceDate),
Amount REAL check(Amount>0)
);
```

**Output:**

<img width="1005" height="626" alt="image" src="https://github.com/user-attachments/assets/0c68ad95-3c1c-470c-846b-6607d3f97e44" />



**Question 9**
---
Create a table named ProjectAssignments with the following constraints:
AssignmentID as INTEGER should be the primary key.
EmployeeID as INTEGER should be a foreign key referencing Employees(EmployeeID).
ProjectID as INTEGER should be a foreign key referencing Projects(ProjectID).
AssignmentDate as DATE should be NOT NULL.

```sql
create table ProjectAssignments(
AssignmentID INTEGER PRIMARY KEY,
EmployeeID INTEGER,
ProjectID INTEGER,
AssignmentDate DATE not null,
foreign key (EmployeeID) references Employees(EmployeeID),
foreign key (ProjectID) references Projects(ProjectID)
);
```

**Output:**
<img width="1099" height="459" alt="image" src="https://github.com/user-attachments/assets/33f7d3f3-b84b-41b4-a429-3c834ee2db90" />


**Question 10**
---
Insert all employees from Former_employees into Employee

Table attributes are EmployeeID, Name, Department, Salary



```sql
insert into Employee(EmployeeID,Name,Department,Salary) select EmployeeID,Name,Department,Salary from Former_employees
```

**Output:**

<img width="626" height="463" alt="image" src="https://github.com/user-attachments/assets/db214b74-b54c-44da-be49-0a192c32843f" />



## RESULT
Thus, the SQL queries to implement different types of constraints and DDL commands have been executed successfully.


