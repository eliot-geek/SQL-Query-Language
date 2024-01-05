# SQL Structured Query Language

Welcome to the SQL Training repository! This repository is dedicated to providing comprehensive training materials and resources for mastering the Structured Query Language (SQL).

## Topics Covered

### **Database Structure, DESCRIBE Query**: Explore the database structure and utilize the DESCRIBE query.

```
VARCHAR     - Variable-length text.
INT         - Integer.
ENUM        - Enumeration (Predefined options)
DATETIME    - Date and time.

SHOW DATABASES;         - Lists available databases.
USE [NAME DATABASE];    - Selects a specific database.
SHOW TABLES;            - Lists tables in the selected database.

DESCRIBE - describe : Provides information about the structure of a database table
DESCRIBE [table_name]; or DESCRIBE [table_name]\G (with more details)
DESCRIBE courses;
DESCRIBE teachers;
DESCRIBE students;
DESCRIBE subscriptions;

```

### **Data Selection and Filtering, SELECT Query**: Learn the essentials of selecting and filtering data using the SELECT query.

```
a-SELECT b-FROM c-WHERE d-ORDERBY e-LIMIT

SELECT column1, column2, ...
FROM table
WHERE condition
ORDER BY column1 [ASC | DESC], column2 [ASC | DESC], ...
LIMIT number;

```

- `SELECT`: Specifies the columns you want to retrieve data from.
- `FROM`: Specifies the table from which to retrieve the data.
- `WHERE`: Optional clause for filtering the results based on a specified condition.
- `ORDER BY`: Optional clause for sorting the results. It can be ascending (`ASC`) or descending (`DESC`).
- `LIMIT`: Optional clause for restricting the number of rows returned.

- The \G is specific to MySQL and isn't part of standard SQL. It's a helpful tool for more detailed, vertical display of the results. 
- Selecting specific columns (name and type) from the "courses" table
```
SELECT name, type FROM courses; or
SELECT name, type FROM courses \G; or
SELECT name FROM Courses;
```
- Selecting all columns from the "students" table
```
SELECT * FROM students; or with \G
```
- Selecting all columns from the "courses" table where type is "PROGRAMMING" with detailed output
```
SELECT * FROM courses WHERE type = 'PROGRAMMING'; or with \G
```
- Selecting the names of students whose age is greater than 35
```
SELECT name FROM students WHERE age > 35;
```
- Selecting all columns from the "teachers" table where the salary is greater than 20000
```
SELECT * FROM teachers WHERE salary > 20000;
```
- Selecting all columns from the "teachers" table where the salary is greater than 20000 and the age is less than 30
```
SELECT * FROM teachers WHERE salary > 20000 AND age < 30;
```
- Selecting all columns from the "students" table and ordering the results by age in ascending order
```
SELECT * FROM students ORDER BY age;
```
- Selecting all columns from the "students" table and ordering the results by age in descending order
```
SELECT * FROM students ORDER BY age DESC;
```
- Selecting all columns from the "teachers" table and ordering the results by age in descending order
```
SELECT * FROM teachers ORDER BY age DESC;
```
- Selecting all columns from the "teachers" table, ordering the results by age in descending order, and limiting the output to the first 3 rows
```
SELECT * FROM teachers ORDER BY age LIMIT 3;
```
- Selecting the name, duration, price and students_count from courses where the type is "PROGRAMMING," ordering by price, and limiting to 3 rows:
```
SELECT name, duration, price, students_count FROM courses WHERE type="PROGRAMMING" ORDER BY price LIMIT 3;
```
- Selecting all values from the "type" column in the "courses" table without removing duplicates. If there are duplicate values in the "type" column, this query will display each occurrence.
```
SELECT type FROM courses;
```
### **DISTINCT Query**: Retrieves unique values from a specified column in a table, eliminating duplicates and providing a distinct list of values.
  
- Displays unique values from the "type" column in "courses," removing duplicates.
```
SELECT DISTINCT type FROM courses;
```
- Displays unique values from the "duration" column in "courses," removing duplicates.

```
SELECT DISTINCT duration FROM courses;
```

### **UNION Query**: is used to combine the result sets of two or more SELECT statements. It is used to merge the rows from different tables or queries into a single result set.  
- It's important to note that `UNION` eliminates duplicate rows from the final result set. If you want to include duplicate rows, you can use the `UNION ALL` operator instead.
- `UNION ALL` includes all rows, even if they are duplicates.

The basic syntax for a `UNION` operation looks like this:

```
SELECT column1, column2, ...
FROM table1
WHERE condition
UNION
SELECT column1, column2, ...
FROM table2
WHERE condition;
```

- Combines and displays unique names from the "students" and "teachers" tables, removing duplicates.
```
mysql> SELECT name FROM students
    -> UNION
    -> SELECT name FROM teachers;
```
- Retrieves and combines age and name information from the "Teachers" and "students" tables, including duplicates using UNION ALL.
```
SELECT age, name FROM Teachers UNION ALL SELECT age, name FROM students;
```

### **Functions and Expressions, Data Aggregation**: Dive into functions, expressions, and data aggregation techniques.

- Selects the salary and the calculated annual salary (salary * 12) from the "Teachers" table for the first 10 records.
```
SELECT salary, salary * 12 FROM teachers LIMIT 10;
```
- Selects the salary as monthly_salary and the calculated annual salary (salary * 12) as annual_salary from the "Teachers" table for the first 10 records.
```
SELECT salary AS monthly_salary, salary * 12 AS annual_salary FROM teachers LIMIT 10;
```

- The `AS` keyword is used to alias or rename a column or a table. 
- `AS monthly_salary`: Renames the "salary" column as "monthly_salary."
- `AS annual_salary`: Renames the result of the expression `salary * 12` as "annual_salary."

- Selects the difference in days between the current date and the registration date as days_since_registration for the first 10 records from the "Students" table.
```
SELECT DATEDIFF(NOW(), registration_date) AS days_since_registration FROM students LIMIT 10;
```
- The `DATEDIFF` function in SQL is used to calculate the difference between two dates.
- `DATEDIFF(NOW(), registration_date)`: Calculates the difference in days between the current date (`NOW()`) and the "registration_date" column for each record in the "students" table.

- Selects the registration date and the difference in days between the current date and the registration date as days_since_registration for the first 10 records from the "Students" table.
```
SELECT registration_date, DATEDIFF(NOW(), registration_date) AS days_since_registration FROM students LIMIT 10;
```
- Selects the name and assigns a status ("FULL" or "NOT FULL") based on the students_count from the "Courses" table for the first 10 records.
```
SELECT name, IF(students_count > 500, "FULL", "NOT FULL") AS status FROM courses LIMIT 10;
```

- The `IF` function is a conditional expression. It works as follows:
- `IF(students_count > 500, "FULL", "NOT FULL")`: This expression checks if the value in the "students_count" column for each record is greater than 500.
  - If the condition is true, it returns the string "FULL."
  - If the condition is false, it returns the string "NOT FULL."
- The result of this conditional expression is then aliased as "status" in the output.

- Selects the name and assigns a status ("FULL" or "NOT FULL") based on the students_count from the "Courses" table for the first 10 records.
```
SELECT name, IF(students_count > 100, "FULL", "NOT FULL") AS Status FROM courses LIMIT 10;
```

- Concatenates a message about a new course, including its name, duration, and price from the "Courses" table for the first 3 records.
```
SELECT CONCAT("Please buy our new course '", name , "' it's only " , duration , " hours long, and the price as low ", price, " rub.") FROM courses LIMIT 3;
```
- The `CONCAT` function is used to concatenate or combine multiple strings into a single string.

- Counts the total number of records in the "Students" table.
```
SELECT COUNT(*) FROM students;
```
- The `COUNT(*)` function is used to count the number of rows in a table.
- The `COUNT(*)` function is commonly used to retrieve the total count of records in a table. If you want to count the number of non-null values in a specific column, you can use `COUNT(column_name)` instead, where `column_name` is the name of the column you want to count.
- However, when `COUNT(*)` is used, it counts all rows, regardless of the values in any specific column.

- Calculates the average age of students from the "Students" table.
```
SELECT AVG(age) FROM students;
```
- The `AVG` function is used to calculate the average (mean) value of a numeric column.
- The `AVG` function is commonly used to obtain the average value of a numeric column, such as age, salary, or any other numerical attribute in a dataset.
- It helps in analyzing the central tendency of the data, providing a single value that represents the "typical" or "average" value of the specified numeric column across all records in the table.

- Calculates the average duration, maximum students_count, and maximum price from the "Courses" table.
```s
SELECT AVG(duration), MAX(students_count), MAX(price) FROM courses;
```
- `MAX(students_count)`: This part of the query calculates the maximum value in the "students_count" column of the "courses" table.
- `MAX(price)`: This part calculates the maximum value in the "price" column of the "courses" table.
- So, it is calculating the maximum value for both the "students_count" and "price" columns independently. It is not calculating the sum of all prices; rather, it identifies the highest value present in the "price" column.

- Calculates the total duration of courses with the type "MARKETING" from the "Courses" table.
```
SELECT SUM(duration) AS total_duration FROM courses WHERE type = "MARKETING";
```

### **Relationships and Table Joins**: Understand relationships and perform table joins for comprehensive data retrieval.

```
SELECT * FROM courses LIMIT 1\G
SELECT * FROM teachers WHERE id = 1;

mysql> SELECT price,
    -> Courses.name AS course_name,
    -> Teachers.name AS teacher_name
    -> FROM Courses
    -> JOIN Teachers ON Teachers.id = Courses.teacher_id
    -> WHERE type="MANAGEMENT"
    -> ORDER BY price LIMIT 4;

mysql> SELECT Courses.name AS course_name,
    -> Students.name AS student_name
    -> FROM Courses
    -> JOIN Subscriptions ON Courses.id = Subscriptions.course_id
    -> JOIN Students ON Students.id = Subscriptions.student_id
    -> WHERE type = "DESIGN"
    -> ORDER BY subscription_date LIMIT 10;
```

### **Grouping**: Master data grouping techniques for effective analysis.

```
SELECT type, AVG(price) FROM Courses GROUP BY type;

mysql> SELECT Teachers.name AS teacher_name, COUNT(*) AS course_count FROM Courses
    -> JOIN Teachers ON Teachers.id = Courses.teacher_id
    -> GROUP BY Teachers.id;


mysql> SELECT Teachers.name AS teacher_name, COUNT(*) AS course_count FROM Courses
    -> JOIN Teachers ON Teachers.id = Courses.teacher_id
    -> GROUP BY Teachers.id
    -> ORDER BY COUNT(*) DESC LIMIT 5;
```

### **Data Modification**: Explore data modification operations to update and manipulate database content.

```
INSERT INTO Courses (name, duration, price, teacher_id) VALUES("SQL", 2, 99999, 2);
SELECT * FROM Courses WHERE name = "SQL";
UPDATE Courses SET price = 90000 WHERE id = 46;
SELECT * FROM Courses WHERE name = "SQL";
SELECT type, AVG(price) FROM Courses GROUP BY type;

UPDATE Courses SET price = price * 0.95 WHERE type = "DESIGN";
Query OK, 16 rows affected (0.01 sec)
Rows matched: 16  Changed: 16  Warnings: 0

SELECT type, AVG(price) FROM Courses GROUP BY type;

```

### **Subqueries**: Learn the concept of subqueries for advanced data retrieval.

```
SELECT name, (SELECT COUNT(*) FROM Teachers WHERE Teachers.age > Students.age) AS older_count FROM Students ORDER BY older_count DESC LIMIT 10;
```

### **Declaration and Modification of Data Structure**: Understand data structure declaration and modification.

```
mysql> CREATE TABLE PurchaseList (
    -> student_name VARCHAR(500),
    -> course_name VARCHAR(500),
    -> price INT,
    -> subscription_date DATETIME);

show tables;


mysql> SELECT Students.name AS student_name, Courses.name AS course_name,
    -> Subscription_date, price FROM Courses
    -> JOIN Subscriptions ON Subscriptions.course_id = Courses.id
    -> JOIN Students ON Students.id = Subscriptions.student_id;

mysql> INSERT INTO PurchaseList(student_name, course_name, subscription_date, price)
    -> SELECT Students.name AS student_name, Courses.name AS course_name,
    -> Subscription_date, price FROM Courses
    -> JOIN Subscriptions ON Subscriptions.course_id = Courses.id
    -> JOIN Students ON Students.id = Subscriptions.student_id;
Query OK, 271 rows affected (0.01 sec)
Records: 271  Duplicates: 0  Warnings: 0

SELECT COUNT(*) FROM PurchaseList;
SELECT * FROM PurchaseList LIMIT 10;
DESCRIBE Courses;
ALTER TABLE Courses ADD COLUMN price_per_hour FLOAT;
DESCRIBE Courses;

UPDATE Courses SET price_per_hour = price/duration;
Query OK, 31 rows affected (0.00 sec)
Rows matched: 47  Changed: 31  Warnings: 0

SELECT * FROM Courses LIMIT 10\G

```

