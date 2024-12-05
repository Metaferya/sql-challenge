# Database Schema for Employee Management System

This README file provides an overview of the SQL tables and queries used to create and manage the database schema for an Employee Management System.

## Table of Contents

    #Tables#
    
    Titles
    
    Employees
    
    Departments
    
    Department Managers
    
    Department Employees
    
    Salaries
    
    Queries
    
    Usage

**Tables**

***Titles***

    CREATE TABLE titles(
        title_id VARCHAR NOT NULL,
        title VARCHAR NOT NULL,
        PRIMARY KEY (title_id)
    );

***Employees***

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


***Departments***

    CREATE TABLE departments(
        dept_no VARCHAR NOT NULL,
        dept_name VARCHAR NOT NULL,
        PRIMARY KEY (dept_no)
    );
    

***Department Managers***

    CREATE TABLE dept_manager(
        dept_no VARCHAR NOT NULL,
        emp_no INT NOT NULL,
        FOREIGN KEY (emp_no) REFERENCES employees(emp_no),
        FOREIGN KEY (dept_no) REFERENCES departments(dept_no),
        PRIMARY KEY (dept_no, emp_no)
    );


***Department Employees***

    CREATE TABLE dept_emp(
        emp_no INT NOT NULL,
        dept_no VARCHAR NOT NULL,
        FOREIGN KEY (emp_no) REFERENCES employees(emp_no),
        FOREIGN KEY (dept_no) REFERENCES departments(dept_no),
        PRIMARY KEY (emp_no, dept_no)
    );


***Salaries***

    CREATE TABLE salaries(
        emp_no INT NOT NULL,
        salary INT NOT NULL,
        FOREIGN KEY (emp_no) REFERENCES employees(emp_no),
        PRIMARY KEY (emp_no)
    );


***Usage***

   1. Create Tables: Execute the CREATE TABLE statements to set up the database schema.
    
   2.Insert Data: Insert relevant data into the tables as required.
    
   3.Query Data: Use the provided SELECT statements to retrieve data from the tables.


