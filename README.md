# SQL-Query-Language

Welcome to the SQL Training repository! This repository is dedicated to providing comprehensive training materials and resources for mastering the Structured Query Language (SQL).

## Topics Covered

- **Database Structure, DESCRIBE Query**: Explore the database structure and utilize the DESCRIBE query.

```
VARCHAR - Save lines (char)
INT - Save integers numbers
ENUM - Enumeration
DATETIME - date

SHOW DATABASES; 
USE [NAME];

DESCRIBE - describe
DESCRIBE [name]; or DESCRIBE [name]\G (with more details)
DESCRIBE courses;
DESCRIBE teachers;
DESCRIBE students;
DESCRIBE subscriptions;

```

- **Data Selection and Filtering, SELECT Query**: Learn the essentials of selecting and filtering data using the SELECT query.

```
a-SELECT b-FROM c-WHERE d-ORDERBY e-LIMIT
SELECT name, type FROM courses; or \G  or SELECT name FROM Courses;
SELECT * FROM students; or \G (from all records)
SELECT * FROM courses WHERE type = "PROGRAMMING"; or \G
SELECT name FROM students WHERE age > 35;
SELECT * FROM teachers WHERE salary > 20000;
SELECT * FROM teachers WHERE salary > 20000 AND age < 30;
SELECT * FROM students ORDER BY age;
SELECT * FROM students ORDER BY age DESC;
SELECT * FROM teachers ORDER BY age DESC, salary ASC;
SELECT * FROM teachers ORDER BY age LIMIT 3;
SELECT name, duration, students_count FROM courses WHERE type="PROGRAMMING" ORDER BY price LIMIT 3;
SELECT type FROM courses;
SELECT DISTINCT type FROM courses;
SELECT DISTINCT type, duration FROM courses;
mysql> SELECT name FROM students
    -> UNION
    -> SELECT name FROM teachers;
SELECT age, name FROM Teachers UNION ALL Select age, name FROM students;
```

- **Functions and Expressions, Data Aggregation**: Dive into functions, expressions, and data aggregation techniques.

```
SELECT salary, salary * 12 FROM teachers LIMIT 10;
SELECT salary AS monthly_salary, salary * 12 AS annual_salary FROM teachers LIMIT 10;
SELECT DATEDIFF(NOW(), registration_date) AS days_since_registration FROM students LIMIT 10;
SELECT registration_date, DATEDIFF(NOW(), registration_date) AS days_since_registration FROM students LIMIT 10;
SELECT name, IF(students_count > 500, "FULL", "NOT FULL") AS status FROM courses LIMIT 10;
SELECT name, IF(students_count > 100, "FULL", "NOT FULL") AS Status FROM courses LIMIT 10;
SELECT CONCAT("Please buy our new course '", name , "' it's only " , duration , " hours long, and the price as low ", price, " rub.") FROM courses LIMIT 3;
SELECT COUNT(*) FROM students;
SELECT AVG(age) FROM students;
SELECT AVG(duration), MAX(students_count), MAX(price) FROM courses;
SELECT SUM(duration) AS total_duration FROM courses WHERE type = "MARKETING";
```

- **Relationships and Table Joins**: Understand relationships and perform table joins for comprehensive data retrieval.

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

- **Grouping**: Master data grouping techniques for effective analysis.

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

- **Data Modification**: Explore data modification operations to update and manipulate database content.

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

- **Subqueries**: Learn the concept of subqueries for advanced data retrieval.

```
SELECT name, (SELECT COUNT(*) FROM Teachers WHERE Teachers.age > Students.age) AS older_count FROM Students ORDER BY older_count DESC LIMIT 10;
```

- **Declaration and Modification of Data Structure**: Understand data structure declaration and modification.

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

