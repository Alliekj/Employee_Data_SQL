# sql-challenge

Overview:
This project involves the design, creation, and manipulation of a relational database for a company's employee data. The main objectives include data modeling, data engineering, and data analysis using SQL and PostgreSQL. I used chatgpt to debug, establish foreign keys, and re-write my data analysis sql script.

Data Modeling:
The first step in this project is to inspect the provided CSV files and create an Entity Relationship Diagram (saved as QuickDBD-export.png within the Analysis folder). The ERD helps to visualize the relationships between different entities in the database.

The entities in this project include:

departments
dept_emp
dept_manager
employees
salaries
titles


Data Engineering:
-Table Creation
-The SQL scripts to create the necessary tables are included in the data_engineering.sql file. Each table is created with appropriate data types, primary keys, foreign keys, and other constraints.

Data Import:
CSV files are imported into their respective SQL tables using PostgreSQL's COPY command or the \copy command in psql for client-side execution.

Data Analysis:
After setting up the database and importing the data, various SQL queries are executed to analyze the data. This part includes:

-Retrieving employee details
-Analyzing salary distribution
-Identifying department managers
-Performing aggregate functions
-Files in the Repository
-data/: Contains the CSV files with employee data.
-departments.csv
-dept_emp.csv
-dept_manager.csv
-employees.csv
-salaries.csv
-titles.csv

Analysis/: Contains analysis files and SQL scripts.
data_engineering.sql: SQL script to create tables and constraints.
QuickDBD-export.png: ERD diagram for the database schema.
README.md: Project documentation.

Installation
Clone the repository to your local machine:

bash
Copy code
git clone git@github.com:Alliekj/sql-challenge.git
Navigate to the project directory:

bash
Copy code
cd sql-challenge
Set up the PostgreSQL database and import the data as described in the data_engineering.sql file.

Usage:
Launch pgAdmin or any SQL query tool connected to your PostgreSQL server.
Execute the SQL scripts in data_engineering.sql to create the database schema and import the data.
Run your SQL queries to analyze the employee data.
