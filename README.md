# This Repo consists of MySQL Commands

- Creating a Database(DB)
    - CREATE DATABASE store_db;
Note: system cls: For clearing the cmd

- Working in a particular DB
    - USE school_db;
    - For checking: select database();

- Show DBs
    - Show Databases;

- Drop DB
    - Drop Database test_db;

- Creating a Table
    Create Table students(
     id INT,
     name VARCHAR(100),
     class INT
     );

- Show Tables: Show tables;

- Describing the structure of DB: Desc students;

- Inserting Data into Table
    Insert into students
     Values(102,"Alex",8);

    - For inserting multiple data:  
    Insert into students
     Values(103,"Raju",10),(104,"Shyam",6);

- Reading data from a Table
    Select * from students;

- Reading  particular column
    Selct id,name from students;

# WHERE Clause
  - For selecting a particular record
    Select * from students where id=103;

# Modify Data
    Update students set class=12 where name="John";

# Deleting the data
    Delete from students where id=104;

# Drop Table
    Drop table students;

# Not Null in Table
    create table customers1(
     id INT NOT NULL,
     name VARCHAR(50) NOT NULL
     );

# Default Value
    create table customers3(
     id int not null,
     name varchar(50) not null,
     acc_type  varchar(50) not null default 'Savings'
     );

# Primary Key
    create table customers4(
     acc_no INT Primary Key,
     name varchar(50) not null,
     acc_type varchar(50) not null default 'Savings'
     );

# Auto_Increment
    create table customers5(
     acc_no INT Primary Key Auto_Increment,
     name varchar(50) not null,
     acc_type varchar(50) not null default "savings"
     );

    insert into customers5(name)
     values("Raju"),("Shyam");

# Alias
    select acc_no As 'Account No.', name As         'Customer Name' from customers5;

# String Functions
    - Concat
         Select emp_id,concat(name," ",desig) as "Full Name" from employees;
    
    - Concat_WS: With seperator
        select concat_ws(':',emp_id,name,desig) from employees;

    - Substring: can be -ve SUBSTRING(str, start, length_optional)
        select substring(emp_id,2) AS EmpID, name from employees;
    
    - Replace
        select replace(emp_id,10,'EMP') as NewEmpIDs, name from employees;

    - Reverse: For reversing the string
        select emp_id, Reverse(name) as rname from employees;

    - Uppercase/Lowercase
        - select Upper(name) from employees;
        - select lower(name) from employees;

        select ucase(name) from employees;
        - select lcase(name) from employees;

    - Char_length
    -   select char_length(name) as employee_length from employees;

    Note: We can use space in column name using backticks ``

    - Insert: Select Insert('Hey Wassup',5,0,'Kevin ');

    -> INSERT(str, pos, len, newstr)
    // If it were 3 instead of 0, it would delete 3 characters starting at position 5, then insert 'Kevin'.

    - Left: Select Left('Hey Buddy!',3);
    - Right: Select Right('Hey Buddy!',4);
    - Repeat: Select Repeat('hahah',5);
    - trim: Select Trim('  Alright  ');