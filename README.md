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

    **Note: If not using where then every value will be updated;
    
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

# Distinct: Gives distinct value
    select distinct dept from employees;

    - Combination fname,lname:
        Select distinct lname,fname from employees;

# Order By Asc, Desc
    - select * from employees order by name;

    - select * from employees order by name desc;

     select desig,name from employees order by desig,name;

# Like Keyword
    select * from employees
     where desig Like "%Cash%";

    Q. For 4 chars names
    
    select * from employees
     where name Like "____"; 

    Q. Name start with P having only 4 characters in name
    select * from employees
     where name Like "P___"; 

     Q. First name 'A'
     select * from employees where name like "A%";

     Q. Last name 'u'
     select * from employees where name like "%u";

# Limit
     select * from employees LIMIT 3;   //1st 3 employees

      select * from employees LIMIT 3,2;    //From 4 ownwards range

Q. For getting the maximum salary employee
    select * from employees 
     order by salary desc Limit 1;

# Count
    1. select count(*) from employees;
    2. select count(emp_id) from employees;

    Q. For getting unique departments
        select count(distinct dept) from employees;

    Q. Count no. of managers
     select count(emp_id) from employees
      where desig="Manager";


# Group By: It fetchs unique value from the table

    select dept from employees group by dept;

    - With Count
        select desig, count(name) from employees group by desig;

    Note: Group by should contain column from select list(Only aggregate function will run)

# Max and Min
    select max(salary) from employees;
    
    select min(salary) from employees;

    -> Sub Queries
    - select emp_id, name,salary from employees 
       where 
       salary=(Select max(salary) from employees);

# Sum and Avg
    - Sum
     select sum(salary) from employees;

     - Avg
      select avg(salary) from employees;

# Decimal
    Decimal(5,2)
    5 is total digit, 2 digits after decimal
    902.41 ✅
    7902.34 ❌

    -> It also round figures the decimal part

# Float and Double
    Float: upto ~7 digits, takes 4 bytes of memory
    Double: upto ~15 digits, takes 8 bytes of memory

    Note: We can store more than 15 digits using Decimal~ Decimal(50,2)

# Date, Time and DateTime

    create table person(
     jd Date,
     jt Time,
     jdt DateTime
     );

    insert into person
     values('2022-04-17','23:00:00','2023-05-16 22:05:02');
    
     yyyy-mm-dd

# Date Time Functions
    - Select curdate();
    - Select curtime();
    - Select now();: Date and time both

    - dayname, dayofmonth, dayofweek

    select dayname('2026-02-28');

    select dayofmonth(curdate());

    select dayofweek(curdate());

    select monthname('2026-02-28');

    select year('2026-02-28');

    select hour('10:05:03');
    
    select minute('10:05:03');

    select second('10:05:03');


# Date Format()

    select Date_Format(Now(),'%d/%m/%y');
    
    select Date_Format(Now(),'%D %a at %T');

# DateDiff(expr1,expr2)

    select datediff('2026-03-29', '2026-02-28');    //29

    -> select date_add('2026-02-28',Interval 1 Day);

    -> select date_sub('2026-02-28',Interval 1 Year);

# TimeDiff(expr1,expr2)
    select timediff('23:00:00', '20:00:00');


# Current TimeStamp
    create table blogs(
     blog varchar(150),
     ct DateTime default current_timestamp,
     ut datetime default current_timestamp
     );

      update blogs set blog="This is my personal blog";

      Note: It will update all blogs

# Relational Operators
    - <, >, <=, =>, =, !=

    Select * from employees where salary>60000;
    Select * from employees where salary>=60000;
    Select * from employees where salary!=75000;

# Logical Operators
    - AND, OR
    -> AND
        select * from employees where salary=45000 AND Dept="IT";
    
    -> OR
        select * from employees where salary=25000 or Dept="IT";    will give results for salary as well as for dept 'IT'

        select * from employees where salary=25000 or salary=75000 or salary=60000;