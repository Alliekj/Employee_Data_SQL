# Employee Data Analysis with SQL

## Objective

This project is an analysis of employee data from the 1980s and 1990s. It involves database reconstruction using SQL, data modeling to design an tale schema for each of the csv files, and data analysis to derive insights about the company’s workforce during this time period.

## Project Overview

In this project, you will:

1. **Design and implement the database schema** for the CSV files.
2. **Import the data** into the database.
3. **Perform data analysis** using SQL queries to answer specific questions.

---

## Project Structure

1. **Data Modeling**: Inspect the CSV files and design an Entity Relationship Diagram (ERD) to map the relationships between tables. (Refer to the ERD diagram included in this repository.)

2. **Data Engineering**: Create a table schema based on the ERD, specifying the correct data types, primary keys, foreign keys, and other constraints. Import the CSV data into the corresponding SQL tables.

3. **Data Analysis**: Execute various SQL queries to extract insights about the employees from the data.

---

## Files in the Repository

- **schema.sql**: SQL file containing table creation statements with primary and foreign key relationships.
- **queries.sql**: SQL file containing the queries for data analysis.
- **CSV files**: Employee data files used for import.
- **Entity Relationship Diagram (ERD)**: Visual representation of the database schema.

---

## Instructions

### Step 1: Data Modeling

1. Download and inspect the CSV files.
2. Use a tool like QuickDBD to sketch the ERD.
3. Review the relationships between the entities and finalize your schema.

### Step 2: Data Engineering

1. Create SQL tables based on your schema.
2. Specify data types for each column.
   - Use `INT` for numerical fields such as `emp_no`.
   - Use `VARCHAR` for text fields like `dept_name` and `title`.
   - Use `DATE` for date fields like `hire_date` and `birth_date`.
3. Establish relationships using primary and foreign keys.
   - Example: Link the `employees` table to the `salaries` and `titles` tables via `emp_no` and `emp_title_id`, respectively.
4. Import the CSV files into the corresponding SQL tables.

#### Sample Table Schema:

```sql
CREATE TABLE departments (
    dept_no INT PRIMARY KEY,
    dept_name VARCHAR NOT NULL
);

CREATE TABLE titles (
    title_id VARCHAR PRIMARY KEY,
    title VARCHAR NOT NULL
);

CREATE TABLE employees (
    emp_no INT PRIMARY KEY,
    emp_title_id VARCHAR,
    birth_date DATE NOT NULL,
    first_name VARCHAR NOT NULL,
    last_name VARCHAR NOT NULL,
    sex VARCHAR CHECK (sex IN ('F', 'M')),
    hire_date DATE NOT NULL,
    FOREIGN KEY (emp_title_id) REFERENCES titles(title_id)
);

CREATE TABLE salaries (
    emp_no INT PRIMARY KEY,
    salary INT NOT NULL,
    FOREIGN KEY (emp_no) REFERENCES employees(emp_no)
);

CREATE TABLE dept_emp (
    emp_no INT,
    dept_no INT,
    PRIMARY KEY (emp_no, dept_no),
    FOREIGN KEY (emp_no) REFERENCES employees(emp_no),
    FOREIGN KEY (dept_no) REFERENCES departments(dept_no)
);

CREATE TABLE dept_manager (
    emp_no INT,
    dept_no INT,
    PRIMARY KEY (emp_no, dept_no),
    FOREIGN KEY (emp_no) REFERENCES employees(emp_no),
    FOREIGN KEY (dept_no) REFERENCES departments(dept_no)
);

### Step 3: Data Analysis

Use SQL queries to explore the data and answer the following questions:

1. List the employee number, last name, first name, sex, and salary of each employee.

    ```sql
    SELECT e.emp_no, e.last_name, e.first_name, e.sex, s.salary
    FROM employees e
    JOIN salaries s ON e.emp_no = s.emp_no;
    ```

2. Find the employees hired in 1986.

    ```sql
    SELECT first_name, last_name, hire_date
    FROM employees
    WHERE hire_date BETWEEN '1986-01-01' AND '1986-12-31';
    ```

3. List the managers for each department along with their department number, department name, employee number, last name, and first name.

    ```sql
    SELECT dm.dept_no, d.dept_name, dm.emp_no, e.last_name, e.first_name
    FROM dept_manager dm
    JOIN employees e ON dm.emp_no = e.emp_no
    JOIN departments d ON dm.dept_no = d.dept_no;
    ```

4. Get the department number for each employee along with their employee number, last name, first name, and department name.

    ```sql
    SELECT de.dept_no, e.emp_no, e.last_name, e.first_name, d.dept_name
    FROM dept_emp de
    JOIN employees e ON de.emp_no = e.emp_no
    JOIN departments d ON de.dept_no = d.dept_no;
    ```

5. List the first name, last name, and sex of employees named Hercules, whose last name begins with 'B'.

    ```sql
    SELECT first_name, last_name, sex
    FROM employees
    WHERE first_name = 'Hercules' AND last_name LIKE 'B%';
    ```

6. Find all employees in the Sales department.

    ```sql
    SELECT e.emp_no, e.last_name, e.first_name
    FROM employees e
    JOIN dept_emp de ON e.emp_no = de.emp_no
    JOIN departments d ON de.dept_no = d.dept_no
    WHERE d.dept_name = 'Sales';
    ```

7. List all employees in the Sales and Development departments.

    ```sql
    SELECT e.emp_no, e.last_name, e.first_name, d.dept_name
    FROM employees e
    JOIN dept_emp de ON e.emp_no = de.emp_no
    JOIN departments d ON de.dept_no = d.dept_no
    WHERE d.dept_name IN ('Sales', 'Development');
    ```

8. Find the frequency count of all employee last names.

    ```sql
    SELECT last_name, COUNT(*) as frequency
    FROM employees
    GROUP BY last_name
    ORDER BY frequency DESC;
    ```

---

## How to Use

1. Clone the repository: `git clone https://github.com/your-username/sql-challenge.git`
2. Create and populate the SQL database using the schema and data files.
3. Run the SQL queries from the `queries.sql` file to analyze the employee data.

---

## Entity Relationship Diagram

![Entity Relationship Diagram](QuickDBD-export.png)

---

## Technologies Used

- SQL
- PostgreSQL (or another RDBMS)
- Entity Relationship Diagram tools (e.g., QuickDBD) (https://www.quickdatabasediagrams.com/) 

