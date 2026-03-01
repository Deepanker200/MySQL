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

    Q. Imp: Having name from R and S
        select * from employees where name like "R%" or name like "S%";

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

    -> IN : For selecting multiple data
        Select * from employees where dept In('Accounts','IT','Loan');

    -> Not IN
    Select * from employees where dept Not In('Accounts','IT','Loan');

# Between (Inclusive In Nature)
    - One Way
        select * from employees where salary>=40000 and salary<=65000;

    - In clean way
        select * from employees where salary between 40000 and 65000;

# CASE Statements
    1. select name,salary,
     Case
     When salary>=50000 Then 'Higher Salary'
     Else 'Low Salary'
     End As 'Salary Category'
     from employees;

    2. Multiple Cases
    select name,salary,
    -> case
    -> when salary<=40000 then 'Low Salary'
    -> when salary>40000 And salary<=50000 then 'Mid Salary'
    -> else 'High Salary'
    -> end as 'Salary Category'
    -> from employees;


# IS Null 
    select * from person where jt is Null;

# Not Like
    select * from employees where name not like "A%";
    // Not give names starting from A

Q.  Salary in Dollars

    SELECT name, salary, (salary/80) AS sal_in_dollars FROM employees;

# Unique Constraint: For storing unique values

    create table contact(
     mob varchar(50) unique
     );

# Check Contraint: Checking condition
    create table contact1(
     mob varchar(15) unique check (length(mob)>=10)
     );

     -> Error with name (Named Constraint)

      create table contact2(
        mob varchar(15) unique,
        constraint mobno_less_than_10digits check(Length(mob)>=10)
        );

        also we can replace
        CHECK (CHAR_LENGTH(mob) BETWEEN 10 AND 15)


# Alter Table Commands
 -> Adding new column in table
    alter table contact
    add column name varchar(50);

 -> Drop Column
    alter table contact
    drop column name;

 -> Rename a Column name
    alter table contact
    rename column mob to mobile_no;

 -> Rename a Table name
    alter table contact
    rename to mycontact;
 
 -> How to add/modify column name (also how to add default values to a column)
    alter table mycontact
    modify column mobile_no varchar(20) default "Unknown";
    or
    modify mobile_no varchar(20) default "Unknown";


# MySQL Relationships

    1. One to One (Employee to Employee Details)
    2. One to Many (Employee to Employee Task )
    3. Many to Many (Authors to Books and Books to Authors)

# One to Many Relation
    1. Creating 1st table
    create table customers(
     cust_id INT Auto_Increment Primary key,
     name varchar(50),
     email varchar(5)
     );

     2. Creating 2nd table
    create table orders(
     ord_id int auto_increment primary key,
     date Date,
     amount decimal(10,2),
     cust_id int,
     foreign key (cust_id) references customers(cust_id)
    );

    -> For checking whether the foreign key exists or not 
     select constraint_name, column_name, referenced_table_name from information_schema.key_column_usage where table_name='orders';

# Join: It is used to combine rows from two or more tables based on a related column between them

# Types of Join
    1. Cross Join: Every row from one table is combined with every row from another table

    -  select * from customers,orders;

    2. Inner Join: Returns only the rows where there is a match between the specified columns in both the left(or first) and right(or second) tables

    select * from customers
     inner join
     orders
     on orders.cust_id=customers.cust_id;
  
    -> Inner Join by using group by

    select name, SUM(amount) from customers 
     inner join 
     orders 
     on customers.cust_id=orders.cust_id 
     group by name;

    3. Left Join: Returns all rows from the left(or first) table and the matchibg rows from the right (or second) table

    select * from customers
     left join
     orders
     on orders.cust_id=customers.cust_id;

    -> Using Group By
        select name,sum(amount) from customers
        left join
        orders
        on customers.cust_id=orders.cust_id
        group by name;
    
     Condition: If 0 value in order

      select name,ifnull(sum(amount),0) as Total from customers left join orders on customers.cust_id=orders.cust_id group by name;


    4. Right Join: Just invers of Left Join

    select * from orders right join customers on customers.cust_id=orders.cust_id;

# Delete on Cascade
 -  ALTER TABLE orders
    MODIFY COLUMN cust_id INT,
    ADD FOREIGN KEY (cust_id) REFERENCES customers(cust_id) ON DELETE CASCADE;

    For deleting foreign key

    - ALTER TABLE orders
        DROP FOREIGN KEY orders_ibfk_1;

    
    Q. For 2 null values

     select author_name,ifnull(title,"Not found"),ifnull(ratings,0) from authors
     left join
     books
     on
     books.au_id=authors.author_id;

     Q. IMP Topic

     select author_name,ratings,
     case
     when ifnull(ratings,0)>=3 then 'Good'
     else 'Average'
     end as remark
     from authors
     inner join books
     on books.au_id=authors.author_id;


# Many To Many Relationship

    Table 1:
    create table students(
     id int auto_increment primary key,
     student_name varchar(250)
     );

    Table 2:
    create table courses(
     id int auto_increment primary key,
     course_name varchar(250),
     fees int
     );

     Table 3: Junction Table/Bridge Table

    create table student_course(
     student_id int,
     course_id int,
     foreign key(student_id) references students(id),
     foreign key(course_id) references courses(id)
    );

    Join Query:

    select student_name,course_name from students
     join
     student_course on student_course.student_id=students.id
     join
     courses on student_course.course_id=courses.id;


    Q. Count No of Students
     SELECT course_name, COUNT(student_id)
    -> FROM students
    -> JOIN student_course
    -> ON student_course.student_id = students.id
    -> JOIN courses
    -> ON courses.id = student_course.course_id 
    -> group by course_name;

    Q. Count no of courses taken by each student

    select student_name, count(course_id) from students
     join
     student_course on student_course.student_id=students.id
     join
     courses on student_course.course_id=courses.id

     Q. Total Fees by each student

    select student_name, sum(fees) from students
     join
     student_course on student_course.student_id=students.id
     join
     courses on student_course.course_id=courses.id


# Views to Create Virtual Table

    //It creates another table(view) so that we don't need to write large and complex queries

    create view inst_info AS
     select student_name,course_name,fees from students
          join
          student_course on student_course.student_id=students.id
          join
          courses on student_course.course_id=courses.id;

    - show tables;
    - select * from view inst_info;
    - drop view inst_info;


# Having Clause: Where clause does'nt work with group by clause so we have to use Having clause

    select student_name,sum(fees) from inst_info
     group by student_name having sum(fees)>10000;

# Roll up: It is used with group by. It is to generate subtotals and a grand total in the result

    select ifnull(student_name,"Total Fees"),sum(fees) from inst_info group by student_name
     with rollup;

# Stored Routine: An SQL statement or a set of SQL statement that can be stored on database server which can be call no. of times.

    - Types of Stored Routine
    1. Stored Procedure
    2. User Defined Functions

    1. Stored Procedure
    These are routines that contain a series of SQL Statement and procedural logic

    - Delimiter: By which the statement ends

     DELIMITER $$

    create procedure emp_info()
     Begin
     Select * from employees order by salary;
     End $$

    Delimiter ;

    -> Use: For calling
    call bank_db.emp_info();

    Works best with workbench we easily see

    Q. Using dynamic value

    DELIMITER $$

    create procedure get_empid(IN p_name varchar(100))
    
    Begin
	    Select emp_id from employees
	    where name=p_name;
    End $$

    Delimiter ;

    ->Use: For calling:
    call get_empid('Raju');


    -> Returning output in a variable in stored procedure

    DELIMITER $$

    create procedure get_sum_by_dept(IN p_dept varchar(100),OUT p_sum Decimal(10,2))
    
    Begin
	    Select sum(salary) into p_sum from employees
	    where dept=p_dept;
    End $$

    Delimiter ;

    -> For calling in mysql command line
    set @p_sum = 0;     //setting variable
    call bank_db.get_sum_by_dept('Loan', @p_sum);
    select @p_sum;

    2. User Defined Functions

    DELIMITER $$

    CREATE FUNCTION emp_name_max_salary(p_name VARCHAR(50)) RETURNS VARCHAR(50)
    DETERMINISTIC NO SQL READS SQL DATA

    BEGIN
        DECLARE v_max INT;
        DECLARE v_name VARCHAR(50);

        Select MAX(salary) INTO v_max from employees;
        Select name into v_name from employees
            where salary = v_max;

        return v_name;
    END$$

    DELIMITER ;


    -> For calling Input: select bank_db.   emp_name_max_salary('john');

# Window Functions: Only used in version 8.0 or upper. Also known as analytic functions allow us to perform calculations across a set of rows related to the current row.
    
    - Defined by an OVER() clause

    select emp_id,name,salary, sum(salary) 
    over(partition by dept) as sum_salary 
    from employees;

    -> Row_Number() 1st use case
    select 
    Row_number() over() as row_no,
    emp_id,name,salary
    from employees;
    
    -> 2nd use case
    
    select 
    Row_number() over(order by salary) as row_no,
    emp_id,name,salary
    from employees;

    ->3rd use case
    
    select 
    Row_number() over(partition by salary) as row_no,
    emp_id,dept
    from employees;

    ->Rank(): For ranking purpose

    select 
    emp_id,dept,salary,
    Rank() over(order by salary) as rank_sal
    from employees;

    -> Dense_Rank(): For more accurate rank 1,2,3...

    -> Lag(): Lag(salary)- For differences of next salary  , Like cummulative freq

    -> Lead(): Lead(salary), Like cummulative freq