# 🎓 Student Enrollment Management System — DBMS Project

A relational database project built with **PostgreSQL** that models a university's student enrollment system. The project demonstrates core database concepts including schema design, data manipulation, filtering, aggregation, and multi-table joins.

---

## 📌 Table of Contents

- [Overview](#overview)
- [Database Schema](#database-schema)
- [Features](#features)
- [Technologies Used](#technologies-used)
- [Setup & Installation](#setup--installation)
- [Sample Data](#sample-data)
- [Query Examples](#query-examples)
- [Screenshots](#screenshots)

---

## Overview

This project implements a three-table relational database for managing students, courses, and their enrollments at a university. It covers a wide range of SQL operations — from basic CRUD to advanced queries with joins and aggregate functions — making it an ideal reference for learning database management fundamentals.

---

## Database Schema

The database consists of three tables connected through foreign key relationships:

```
Students ──< Enrollments >── Courses
```

### `Students`
| Column       | Type           | Description              |
|--------------|----------------|--------------------------|
| student_id   | SERIAL (PK)    | Auto-incremented ID      |
| name         | VARCHAR(128)   | Full name of the student |
| email        | VARCHAR(128)   | Student email address    |
| department   | VARCHAR(128)   | Enrolled department      |
| cgpa         | DECIMAL(3,2)   | Cumulative GPA           |

### `Courses`
| Column      | Type         | Description                     |
|-------------|--------------|----------------------------------|
| course_id   | SERIAL (PK)  | Auto-incremented ID              |
| course_name | VARCHAR(128) | Name of the course               |
| credits     | INT          | Credit hours for the course      |
| department  | VARCHAR(128) | Offering department              |

### `Enrollments`
| Column        | Type         | Description                         |
|---------------|--------------|--------------------------------------|
| enrollment_id | SERIAL (PK)  | Auto-incremented ID                  |
| student_id    | INT (FK)     | References `Students.student_id`     |
| course_id     | INT (FK)     | References `Courses.course_id`       |
| grade         | VARCHAR(128) | Grade received in the course         |

---

## Features

- ✅ **Schema Design** — Normalized relational tables with primary and foreign keys
- ✅ **CRUD Operations** — INSERT, SELECT, UPDATE, DELETE
- ✅ **Filtering** — WHERE clause with AND, OR, NOT operators
- ✅ **Sorting** — ORDER BY (ascending/descending)
- ✅ **Grouping & Aggregation** — GROUP BY with COUNT, AVG, MAX, MIN, SUM
- ✅ **Having Clause** — Filter groups based on aggregate conditions
- ✅ **Joins** — INNER JOIN, LEFT JOIN, RIGHT JOIN, FULL OUTER JOIN
- ✅ **Multi-Table Queries** — Complex joins across all three tables

---

## Technologies Used

| Technology  | Purpose                          |
|-------------|----------------------------------|
| PostgreSQL  | Relational database engine       |
| SQL         | Query language for all operations |

---

## Setup & Installation

### Prerequisites

- [PostgreSQL](https://www.postgresql.org/download/) installed on your machine
- A PostgreSQL client (e.g., `psql`, pgAdmin, DBeaver)

### Steps

1. **Clone the repository**
   ```bash
   git clone https://github.com/muhammad-asif10/DBMS_Project.git
   cd DBMS_Project
   ```

2. **Create a new database**
   ```sql
   CREATE DATABASE dbms_project;
   ```

3. **Connect to the database**
   ```bash
   psql -U postgres -d dbms_project
   ```

4. **Run the SQL script**
   ```bash
   psql -U postgres -d dbms_project -f dbms_project.sql
   ```

---

## Sample Data

### Students

| student_id | name           | email                 | department              | cgpa |
|------------|----------------|-----------------------|-------------------------|------|
| 1          | Muhammad Asif  | masif@gmail.com       | Computer Science        | 2.80 |
| 2          | Shaziab        | CR@gmail.com          | Computer Science        | 3.60 |
| 3          | Abdul Rehman   | abdulR@gmail.com      | Cyber Security          | 3.30 |
| 4          | Abu Haraira    | huraira@gmail.com     | Data Science            | 2.70 |
| 5          | Bilal          | bila@gmail.com        | Artificial Intelligence | 3.50 |

### Courses

| course_id | course_name                    | credits | department              |
|-----------|--------------------------------|---------|-------------------------|
| 1         | Object Oriented Programming    | 4       | Computer Science        |
| 2         | Database Management System     | 4       | Computer Science        |
| 3         | Data Structure                 | 3       | Data Science            |
| 4         | Automating Things With AI      | 5       | Artificial Intelligence |
| 5         | Complex Threats                | 2       | Cyber Security          |

### Enrollments

| enrollment_id | student_id | course_id | grade |
|---------------|------------|-----------|-------|
| 1             | 1          | 1         | B     |
| 2             | 2          | 2         | A     |
| 3             | 3          | 3         | A     |
| 4             | 4          | 4         | B     |

---

## Query Examples

### Basic SELECT

```sql
SELECT * FROM Students;
```

### Update a Record

```sql
UPDATE Students
SET cgpa = 3.7
WHERE student_id = 2;
```

### Filter with WHERE

```sql
SELECT * FROM Students
WHERE department = 'Computer Science';
```

### AND / OR / NOT Operators

```sql
-- AND
SELECT * FROM Students
WHERE department = 'Computer Science' AND cgpa > 3.5;

-- OR
SELECT * FROM Students
WHERE department = 'Computer Science' OR department = 'Data Science';

-- NOT
SELECT * FROM Students
WHERE department != 'Computer Science';
```

### ORDER BY

```sql
SELECT * FROM Students
ORDER BY cgpa DESC;
```

### GROUP BY with Aggregation

```sql
SELECT department, ROUND(AVG(cgpa), 2) AS average_cgpa
FROM Students
GROUP BY department;
```

### HAVING Clause

```sql
SELECT department, AVG(CAST(cgpa AS float)) AS average_cgpa
FROM Students
GROUP BY department
HAVING AVG(cgpa) > 3.0;
```

### Aggregate Functions

```sql
SELECT COUNT(*) AS total_students FROM Students;
SELECT ROUND(AVG(cgpa), 3) AS average_cgpa FROM Students;
SELECT MAX(cgpa) AS max_cgpa FROM Students;
SELECT MIN(cgpa) AS min_cgpa FROM Students;
SELECT SUM(cgpa) AS sum_cgpa FROM Students;
```

### Joins

```sql
-- INNER JOIN
SELECT Students.name, Enrollments.course_id
FROM Students
INNER JOIN Enrollments ON Students.student_id = Enrollments.student_id;

-- LEFT JOIN
SELECT Enrollments.course_id, Students.name
FROM Students
LEFT JOIN Enrollments ON Students.student_id = Enrollments.student_id;

-- RIGHT JOIN
SELECT Enrollments.course_id, Students.name
FROM Students
RIGHT JOIN Enrollments ON Students.student_id = Enrollments.student_id;

-- FULL OUTER JOIN
SELECT Enrollments.course_id, Students.name
FROM Students
FULL OUTER JOIN Enrollments ON Students.student_id = Enrollments.student_id;
```

### Multi-Table Join

```sql
SELECT Enrollments.course_id, Students.name
FROM Students
LEFT JOIN Enrollments ON Students.student_id = Enrollments.student_id
INNER JOIN Courses ON Enrollments.course_id = Courses.course_id;
```

---

## Screenshots

### Database Tables & Schema

![Database Tables and Schema](https://github.com/user-attachments/assets/c69cd231-f142-46e9-b1ef-202f4b3106dc)

### CRUD Operations & WHERE Clause Queries

![CRUD Operations and Filtering](https://github.com/user-attachments/assets/d26a67e7-c9ca-4fa9-9db8-49805438fe17)

### Aggregation, GROUP BY & HAVING Queries

![Aggregation and Grouping Queries](https://github.com/user-attachments/assets/27b3cb3c-cb97-490a-b323-6fcd641366e3)

### JOIN Operations

![Join Operations](https://github.com/user-attachments/assets/8838e580-d777-4d55-9e20-d2141265077b)

---

## 👤 Author

**Muhammad Asif**
- GitHub: [@muhammad-asif10](https://github.com/muhammad-asif10)

---

## 📄 License

This project is open-source and available for educational use.
