# Library Management System using SQL Project --P2

## Project Overview

**Project Title**: Library Management System  
**Level**: Intermediate  
**Database**: `library_db`

This project demonstrates the implementation of a Library Management System using SQL. It includes creating and managing tables, performing CRUD operations, and executing advanced SQL queries. The goal is to showcase skills in database design, manipulation, and querying.

## Objectives

1. **Set up the Library Management System Database**: Create and populate the database with tables for branches, employees, members, books, issued status, and return status.
2. **CRUD Operations**: Perform Create, Read, Update, and Delete operations on the data.
3. **CTAS (Create Table As Select)**: Utilize CTAS to create new tables based on query results.
4. **Advanced SQL Queries**: Develop complex queries to analyze and retrieve specific data.

## Project Structure

### 1. Database Setup
![ERD](https://github.com/najirh/Library-System-Management---P2/blob/main/library_erd.png)

- **Database Creation**: Created a database named `library_db`.
- **Table Creation**: Created tables for branches, employees, members, books, issued status, and return status. Each table includes relevant columns and relationships.

```sql
CREATE DATABASE library_db;

CREATE TABLE branches (
    branch_id INT PRIMARY KEY,
    branch_name VARCHAR(255),
    branch_location VARCHAR(255)
);

CREATE TABLE employees (
    emp_id INT PRIMARY KEY,
    emp_name VARCHAR(255),
    emp_position VARCHAR(255),
    emp_salary FLOAT,
    branch_id INT,
    FOREIGN KEY (branch_id) REFERENCES branches(branch_id)
);

CREATE TABLE members (
    member_id INT PRIMARY KEY,
    member_name VARCHAR(255),
    membership_date DATE
);

CREATE TABLE books (
    book_id INT PRIMARY KEY,
    book_title VARCHAR(255),
    book_author VARCHAR(255),
    category VARCHAR(255),
    available_copies INT
);

CREATE TABLE issued_status (
    issue_id INT PRIMARY KEY,
    member_id INT,
    book_id INT,
    issue_date DATE,
    return_date DATE,
    FOREIGN KEY (member_id) REFERENCES members(member_id),
    FOREIGN KEY (book_id) REFERENCES books(book_id)
);

CREATE TABLE return_status (
    return_id INT PRIMARY KEY,
    issue_id INT,
    return_date DATE,
    FOREIGN KEY (issue_id) REFERENCES issued_status(issue_id)
);
```

### 2. CRUD Operations

- **Create**: Inserted sample records into the `books` table.
- **Read**: Retrieved and displayed data from various tables.
- **Update**: Updated records in the `employees` table.
- **Delete**: Removed records from the `members` table as needed.

```sql
-- Insert Sample Records
INSERT INTO books (book_id, book_title, book_author, category, available_copies)
VALUES (1, 'To Kill a Mockingbird', 'Harper Lee', 'Fiction', 5);

-- Retrieve Data
SELECT * FROM books;

-- Update Records
UPDATE employees
SET emp_salary = 60000
WHERE emp_id = 1;

-- Delete Records
DELETE FROM members
WHERE member_id = 10;
```

### 3. CTAS (Create Table As Select)

- **Create Summary Tables**: Used CTAS to generate new tables based on query results.

```sql
CREATE TABLE high_demand_books AS
SELECT book_id, book_title, COUNT(issue_id) AS issue_count
FROM issued_status
JOIN books ON issued_status.book_id = books.book_id
GROUP BY book_id, book_title
HAVING COUNT(issue_id) > 10;
```

### 4. Data Analysis & Findings

The following SQL queries were used to address specific questions:

1. **Retrieve All Books in a Specific Category**:
```sql
SELECT * FROM books
WHERE category = 'Classic';
```

2. **Find Employees with a Salary Greater Than a Specific Amount**:
```sql
SELECT * FROM employees
WHERE emp_salary > 50000;
```

3. **List Members Who Registered in the Last 30 Days**:
```sql
SELECT * FROM members
WHERE membership_date >= CURRENT_DATE - INTERVAL '30 days';
```

4. **Count the Number of Books Issued by Each Employee**:
```sql
SELECT issued_emp_id, COUNT(*) AS number_of_books_issued
FROM issued_status
GROUP BY issued_emp_id;
```

5. **Create a Table of Books with Rental Price Above a Certain Threshold**:
```sql
CREATE TABLE expensive_books AS
SELECT * FROM books
WHERE rental_price > 7.00;
```

## Reports

- **Database Schema**: Detailed table structures and relationships.
- **Data Analysis**: Insights into book categories, employee salaries, member registration trends, and issued books.
- **Summary Reports**: Aggregated data on high-demand books and employee performance.

## Conclusion

This project demonstrates the application of SQL skills in creating and managing a library management system. It includes database setup, data manipulation, and advanced querying, providing a solid foundation for data management and analysis.

## How to Use

1. **Clone the Repository**: Clone this repository to your local machine.
   ```sh
   git clone https://github.com/your-username/library-management-system.git
   ```

2. **Set Up the Database**: Execute the SQL scripts in the `database_setup.sql` file to create and populate the database.
3. **Run the Queries**: Use the SQL queries in the `analysis_queries.sql` file to perform the analysis.
4. **Explore and Modify**: Customize the queries as needed to explore different aspects of the data or answer additional questions.

## Author - Zero Analyst

This project showcases SQL skills essential for database management and analysis. For more content on SQL and data analysis, connect with me through the following channels:

- **YouTube**: [Subscribe to my channel for tutorials and insights](https://www.youtube.com/@zero_analyst)
- **Instagram**: [Follow me for daily tips and updates](https://www.instagram.com/zero_analyst/)
- **LinkedIn**: [Connect with me professionally](https://www.linkedin.com/in/najirr)
- **Discord**: [Join our community for learning and collaboration](https://discord.gg/36h5f2Z5PK)

Thank you for your interest in this project!
