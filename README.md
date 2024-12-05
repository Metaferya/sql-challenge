# Database Schema and Quereis for Employee Management System

This README file provides an overview of the SQL tables and queries used to create and manage the database schema for an Employee Management System.

## Table of Contents

    A-Schema
    
        1-Titles
        
        2-Employees
        
        3-Departments
        
        4-Department Managers
        
        5-Department Employees
        
        6-Salaries
    
    B-Queries
    
       1- Employee Details

       2- Employees Hired in 1986
        
       3- Department Managers
        
       4- Employee Departments
        
       5- Employees Named Hercules B
        
       6- Sales Department Employees
        
       7-  Sales and Development Employees
        
       8- Employee Last Name Frequency
    
    C-Usage
    D-Acknowledment

## A- Schemata

    1-Titles
    
        CREATE TABLE titles(
            title_id VARCHAR NOT NULL,
            title VARCHAR NOT NULL,
            PRIMARY KEY (title_id)
        );
    
    2-Employees
    
        CREATE TABLE employees(
            emp_no INT NOT NULL,
            emp_title_id VARCHAR NOT NULL,
            birth_date DATE NOT NULL,
            first_name VARCHAR NOT NULL,
            last_name VARCHAR NOT NULL,
            sex VARCHAR NOT NULL,
            hire_date DATE NOT NULL,
            FOREIGN KEY (emp_title_id) REFERENCES titles(title_id),
            PRIMARY KEY (emp_no)
        );
    
    3-Departments
    
        CREATE TABLE departments(
            dept_no VARCHAR NOT NULL,
            dept_name VARCHAR NOT NULL,
            PRIMARY KEY (dept_no)
        );
        
    
    4-Department Managers
    
        CREATE TABLE dept_manager(
            dept_no VARCHAR NOT NULL,
            emp_no INT NOT NULL,
            FOREIGN KEY (emp_no) REFERENCES employees(emp_no),
            FOREIGN KEY (dept_no) REFERENCES departments(dept_no),
            PRIMARY KEY (dept_no, emp_no)
        );
    
    
    5-Department Employees
    
        CREATE TABLE dept_emp(
            emp_no INT NOT NULL,
            dept_no VARCHAR NOT NULL,
            FOREIGN KEY (emp_no) REFERENCES employees(emp_no),
            FOREIGN KEY (dept_no) REFERENCES departments(dept_no),
            PRIMARY KEY (emp_no, dept_no)
        );
    
     6-Salaries
    
        CREATE TABLE salaries(
            emp_no INT NOT NULL,
            salary INT NOT NULL,
            FOREIGN KEY (emp_no) REFERENCES employees(emp_no),
            PRIMARY KEY (emp_no)
        );

## B- Query

    1- List the employee number, last name, first name, sex, and salary of each employee:
    
            SELECT e.emp_no, e.last_name, e.first_name, e.sex, s.salary
            FROM employees e
            JOIN salaries s ON e.emp_no = s.emp_no;

    2- List the first name, last name, and hire date for the employees who were hired in 1986:

            SELECT first_name, last_name, hire_date
            FROM employees
            WHERE hire_date BETWEEN '1986-01-01' AND '1986-12-31';

    3- List the manager of each department along with their department number, department name, employee number, last name, and first name:

            SELECT dm.dept_no, d.dept_name, dm.emp_no, e.last_name, e.first_name
            FROM dept_manager dm
            JOIN employees e ON dm.emp_no = e.emp_no
            JOIN departments d ON dm.dept_no = d.dept_no;
     
    4- List the department number for each employee along with that employee’s employee number, last name, first name, and department name:

            SELECT de.dept_no, de.emp_no, e.last_name, e.first_name, d.dept_name
            FROM dept_emp de
            JOIN employees e ON de.emp_no = e.emp_no
            JOIN departments d ON de.dept_no = d.dept_no;
    
    5- List first name, last name, and sex of each employee whose first name is Hercules and whose last name begins with the letter B:

            SELECT first_name, last_name, sex
            FROM employees
            WHERE first_name = 'Hercules' AND last_name LIKE 'B%';
    
    6- List each employee in the Sales department, including their employee number, last name, and first name:

            SELECT e.emp_no, e.last_name, e.first_name
            FROM dept_emp de
            JOIN employees e ON de.emp_no = e.emp_no
            JOIN departments d ON de.dept_no = d.dept_no
            WHERE d.dept_name = 'Sales';
    
    7- List each employee in the Sales and Development departments, including their employee number, last name, first name, and department name:

            SELECT e.emp_no, e.last_name, e.first_name, d.dept_name
            FROM dept_emp de
            JOIN employees e ON de.emp_no = e.emp_no
            JOIN departments d ON de.dept_no = d.dept_no
            WHERE d.dept_name IN ('Sales', 'Development');
    
    8- List the frequency counts, in descending order, of all the employee last names (that is, how many employees share each last name):

            SELECT last_name, COUNT(*) as frequency
            FROM employees
            GROUP BY last_name
            ORDER BY frequency DESC;



## C- Usage

   1. Create Tables: Execute the CREATE TABLE statements to set up the database schema.
    
   2.Insert Data: Insert relevant data into the tables as required.
    
   3.Run Queries: Execute the provided SQL queries in the pgAdmin Query Tool to retrieve the specific information from the database.

   4.Modify as Needed: Adjust the queries to fit any specific requirements or different conditions as necessary.

   5.Analyze Results: Use the query results for analysis, reporting, or further data processing as needed.
   
## D- Acknowledgements

**I would like to thank my instructor and Xpert for their guidance and support throughout this project.**


