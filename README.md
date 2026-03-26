# Library Management System using SQL Project --P2

## Project Overview

**Project Title**: Library Management System  
**Level**: Intermediate  
**Database**: `library_db`

This project demonstrates the implementation of a Library Management System using SQL. It includes creating and managing tables, performing CRUD operations, and executing advanced SQL queries. The goal is to showcase skills in database design, manipulation, and querying.

![Library_project](https://github.com/tanish-6126/Library_Management_P2/blob/main/library.jpg)

## Objectives

1. **Set up the Library Management System Database**: Create and populate the database with tables for branches, employees, members, books, issued status, and return status.
2. **CRUD Operations**: Perform Create, Read, Update, and Delete operations on the data.
3. **CTAS (Create Table As Select)**: Utilize CTAS to create new tables based on query results.
4. **Advanced SQL Queries**: Develop complex queries to analyze and retrieve specific data.

## Project Structure

### 1. Database Setup

![ERD](https://github.com/tanish-6126/Library_Management_P2/blob/main/EER_Diagram.png)

- **Database Creation**: Created a database named `library_db`.
- **Table Creation**: Created tables for branches, employees, members, books, issued status, and return status. Each table includes relevant columns and relationships.

```sql
CREATE DATABASE library;

CREATE TABLE branch
(
branch_id VARCHAR(10) PRIMARY KEY,
manager_id VARCHAR(10),
branch_address VARCHAR(55),
contact_no VARCHAR(20) 
);


-- Create table "Employee" --

CREATE TABLE employees
(
emp_id VARCHAR(10) PRIMARY KEY,
emp_name VARCHAR(25),
position VARCHAR(15),
salary INT,
branch_id VARCHAR(25) --  FK
);


-- Create table "Members" --

CREATE TABLE members
(
member_id VARCHAR(10) PRIMARY KEY,
member_name VARCHAR(25),
member_address VARCHAR(75),
reg_date DATE
);

-- Create table "Books"

CREATE TABLE books
(
isbn VARCHAR(20) PRIMARY KEY,
book_title VARCHAR(75),
category VARCHAR(20),
rental_price FLOAT,
status VARCHAR(15),
author VARCHAR(35),
publisher varchar(55)
);

-- Create table "IssueStatus"

CREATE TABLE issued_status
(
issued_id VARCHAR(10) PRIMARY KEY,
issued_member_id VARCHAR(10),-- FK
issued_book_name VARCHAR(75),
issued_date DATE,
issued_book_isbn VARCHAR(25) , -- FK
issued_emp_id VARCHAR(10) -- FK
);

-- Create table "ReturnStatus"

CREATE TABLE return_status
(
return_id VARCHAR(10) PRIMARY KEY,
issued_id VARCHAR(10),
return_book_name VARCHAR(75),
return_date DATE,
return_book_isbn VARCHAR(20)
) ;

-- Adding Data of Issued_status and Return_status --

INSERT INTO issued_status(issued_id, issued_member_id, issued_book_name, issued_date, issued_book_isbn, issued_emp_id) 
VALUES
('IS106', 'C106', 'Animal Farm', '2024-03-10', '978-0-330-25864-8', 'E104'),
('IS107', 'C107', 'One Hundred Years of Solitude', '2024-03-11', '978-0-14-118776-1', 'E104'),
('IS108', 'C108', 'The Great Gatsby', '2024-03-12', '978-0-525-47535-5', 'E104'),
('IS109', 'C109', 'Jane Eyre', '2024-03-13', '978-0-141-44171-6', 'E105'),
('IS110', 'C110', 'The Alchemist', '2024-03-14', '978-0-307-37840-1', 'E105'),
('IS111', 'C109', 'Harry Potter and the Sorcerers Stone', '2024-03-15', '978-0-679-76489-8', 'E105'),
('IS112', 'C109', 'A Game of Thrones', '2024-03-16', '978-0-09-957807-9', 'E106'),
('IS113', 'C109', 'A Peoples History of the United States', '2024-03-17', '978-0-393-05081-8', 'E106'),
('IS114', 'C109', 'The Guns of August', '2024-03-18', '978-0-19-280551-1', 'E106'),
('IS115', 'C109', 'The Histories', '2024-03-19', '978-0-14-044930-3', 'E107'),
('IS116', 'C110', 'Guns, Germs, and Steel: The Fates of Human Societies', '2024-03-20', '978-0-393-91257-8', 'E107'),
('IS117', 'C110', '1984', '2024-03-21', '978-0-679-64115-3', 'E107'),
('IS118', 'C101', 'Pride and Prejudice', '2024-03-22', '978-0-14-143951-8', 'E108'),
('IS119', 'C110', 'Brave New World', '2024-03-23', '978-0-452-28240-7', 'E108'),
('IS120', 'C110', 'The Road', '2024-03-24', '978-0-670-81302-4', 'E108'),
('IS121', 'C102', 'The Shining', '2024-03-25', '978-0-385-33312-0', 'E109'),
('IS122', 'C102', 'Fahrenheit 451', '2024-03-26', '978-0-451-52993-5', 'E109'),
('IS123', 'C103', 'Dune', '2024-03-27', '978-0-345-39180-3', 'E109'),
('IS124', 'C104', 'Where the Wild Things Are', '2024-03-28', '978-0-06-025492-6', 'E110'),
('IS125', 'C105', 'The Kite Runner', '2024-03-29', '978-0-06-112241-5', 'E110'),
('IS126', 'C105', 'Charlotte''s Web', '2024-03-30', '978-0-06-440055-8', 'E110'),
('IS127', 'C105', 'Beloved', '2024-03-31', '978-0-679-77644-3', 'E110'),
('IS128', 'C105', 'A Tale of Two Cities', '2024-04-01', '978-0-14-027526-3', 'E110'),
('IS129', 'C105', 'The Stand', '2024-04-02', '978-0-7434-7679-3', 'E110'),
('IS130', 'C106', 'Moby Dick', '2024-04-03', '978-0-451-52994-2', 'E101'),
('IS131', 'C106', 'To Kill a Mockingbird', '2024-04-04', '978-0-06-112008-4', 'E101'),
('IS132', 'C106', 'The Hobbit', '2024-04-05', '978-0-7432-7356-4', 'E106'),
('IS133', 'C107', 'Angels & Demons', '2024-04-06', '978-0-7432-4722-5', 'E106'),
('IS134', 'C107', 'The Diary of a Young Girl', '2024-04-07', '978-0-375-41398-8', 'E106'),
('IS135', 'C107', 'Sapiens: A Brief History of Humankind', '2024-04-08', '978-0-307-58837-1', 'E108'),
('IS136', 'C107', '1491: New Revelations of the Americas Before Columbus', '2024-04-09', '978-0-7432-7357-1', 'E102'),
('IS137', 'C107', 'The Catcher in the Rye', '2024-04-10', '978-0-553-29698-2', 'E103'),
('IS138', 'C108', 'The Great Gatsby', '2024-04-11', '978-0-525-47535-5', 'E104'),
('IS139', 'C109', 'Harry Potter and the Sorcerers Stone', '2024-04-12', '978-0-679-76489-8', 'E105'),
('IS140', 'C110', 'Animal Farm', '2024-04-13', '978-0-330-25864-8', 'E102');

INSERT INTO return_status(return_id, issued_id, return_date) 
VALUES
('RS105', 'IS107', '2024-05-03'),
('RS106', 'IS108', '2024-05-05'),
('RS107', 'IS109', '2024-05-07'),
('RS108', 'IS110', '2024-05-09'),
('RS109', 'IS111', '2024-05-11'),
('RS110', 'IS112', '2024-05-13'),
('RS111', 'IS113', '2024-05-15'),
('RS112', 'IS114', '2024-05-17'),
('RS113', 'IS115', '2024-05-19'),
('RS114', 'IS116', '2024-05-21'),
('RS115', 'IS117', '2024-05-23'),
('RS116', 'IS118', '2024-05-25'),
('RS117', 'IS119', '2024-05-27'),
('RS118', 'IS120', '2024-05-29');

-- Adding Constraints --
--  Adding Foreign Key in issued status..
-- 1.
ALTER TABLE issued_status
ADD CONSTRAINT fk_members
FOREIGN KEY (issued_member_id)
REFERENCES members(member_id);

-- 2.
ALTER TABLE issued_status
ADD CONSTRAINT fk_books
FOREIGN KEY (issued_book_isbn)
REFERENCES books(isbn);

-- 3.
ALTER TABLE issued_status
ADD CONSTRAINT fk_employees
FOREIGN KEY (issued_emp_id)
REFERENCES employees(emp_id);

-- return_status
-- 1.
ALTER TABLE return_status
ADD CONSTRAINT fk_issued_status
FOREIGN KEY (issued_id)
REFERENCES issued_status(issued_id);

-- employees
-- 1.
ALTER TABLE employees
ADD CONSTRAINT fk_branch
FOREIGN KEY (branch_id)
REFERENCES branch(branch_id);

```

### 2. CRUD Operations

- **Create**: Inserted sample records into the `books` table.
- **Read**: Retrieved and displayed data from various tables.
- **Update**: Updated records in the `employees` table.
- **Delete**: Removed records from the `members` table as needed.

**Task 1. Create a New Book Record
-- "978-1-60129-456-2', 'To Kill a Mockingbird', 'Classic', 6.00, 'yes', 'Harper Lee', 'J.B. Lippincott & Co.')"**

```sql
Insert into books Values(
'978-1-60129-456-2','To Kill a Mockingbird','Classic', 6.00, 'yes', 'Harper
Lee','J.B. Lippincott & Co.');
SELECT * FROM books;
```
**Task 2: Update an Existing Member's Address**

```sql
Update members set member_address ='780 Oak St.' where member_id ='C103';
select * from members;
```

**Task 3: Delete a Record from the Issued Status Table -- Objective: Delete the record with issued_id = 'IS104' from the issued_status table.**

```sql
delete from issued_status where issued_id = 'IS104';
select * from issued_status;
```

**Task 4:Retrieve All Books names Issued by a Specific Employee -- Objective: Select all books name issued by the employee with emp_id = 'E101'**

```sql
select issued_book_name from issued_status
where issued_emp_id ='E104';
```

**Task 5:  List Members Who Have Issued More Than One Book -- Objective: Use GROUP BY to find members who
-- have issued more than one book.**

```sql
select issued_member_id ,count(issued_member_id )cnt
 from issued_status
group by issued_member_id
having cnt > 1;
```

### 3. CTAS (Create Table As Select)

- **Task 6: Create Summary Tables: Used CTAS to generate new tables based on query results - each book and total book_issued_cnt**

```sql
Create table book_issued_cnt as 
SELECT b.isbn, b.book_title, COUNT(ist.issued_id) AS issue_count
FROM issued_status as ist
JOIN books as b
ON ist.issued_book_isbn = b.isbn
GROUP BY b.isbn, b.book_title;
select * from book_issued_cnt;
```

### 4. Data Analysis & Findings

The following SQL queries were used to address specific questions:

Task 7. **Retrieve All Books in a Specific Category**:

```sql
SELECT * FROM books
WHERE category = 'Classic';
```

Task 8: **Find Total Rental Income by Category**:

```sql
select b.category,sum(rental_price)as total_rent 
from issued_status a 
join 
books b
on a.issued_book_isbn = b.isbn
group by b.category;

```

9. **List members who registered in the last 1180 days..**:
```sql
select * from members
where datediff(curdate(),reg_date ) < 1180;
```

10. **List Employees with Their Branch Manager's Name and their branch details**:

```sql
select c.emp_name as manager_name,d.* from employees c
 join
(select a.branch_id,b.emp_id,b.emp_name,a.manager_id,a.branch_address from branch a join employees b
on a.branch_id = b.branch_id) d
on c.emp_id= d.manager_id;
```

Task 11. **Create a Table of Books with Rental Price Above a Certain Threshold 7USD**:
```sql
Create table price_greater_than_7 as
select * from books 
where 
rental_price > 7;
```

Task 12: **Retrieve the List of Books Not Yet Returned**
```sql
select * from (
select a.issued_id,a.issued_book_name,b.return_id,b.return_date
from issued_status a
left join
return_status b 
on a.issued_id = b.issued_id) c
where c.return_date is null;
```
-- Before Performing advance tasks ,we are adding some more details..

```sql
INSERT INTO issued_status
(issued_id, issued_member_id, issued_book_name, issued_date, issued_book_isbn, issued_emp_id)
VALUES
('IS151', 'C118', 'The Catcher in the Rye', CURRENT_DATE - INTERVAL 24 DAY, '978-0-553-29698-2', 'E108'),
('IS152', 'C119', 'The Catcher in the Rye', CURRENT_DATE - INTERVAL 13 DAY, '978-0-553-29698-2', 'E109'),
('IS153', 'C106', 'Pride and Prejudice', CURRENT_DATE - INTERVAL 7 DAY,  '978-0-14-143951-8', 'E107'),
('IS154', 'C105', 'The Road',CURRENT_DATE - INTERVAL 32 DAY, '978-0-375-50167-0', 'E101');

```

-- Adding new column in return_status

```sql
ALTER TABLE return_status
ADD Column book_quality VARCHAR(15) DEFAULT('Good');

UPDATE return_status
SET book_quality = 'Damaged'
WHERE issued_id 
    IN ('IS112', 'IS117', 'IS118');
```
    
## Advanced SQL Operations

**Task 13: Identify Members with Overdue Books**  
Write a query to identify members who have overdue books (assume a 30-day return period). Display the member's_id, member's name, book title, issue date, and days overdue.

```sql
select * from (
select *,datediff(ifnull(return_date,current_date), issued_date)overdue from (
select a.issued_id,a.issued_member_id,a.issued_book_name,a.issued_date,b.return_date from 
issued_status a 
left Join 
return_status b 
on a.issued_id = b.issued_id) c )d 
where overdue >30;
```

**Task 14: Branch Performance Report**  
Create a query that generates a performance report for each branch, showing the number of books issued, the number of books returned, and the total revenue generated from book rentals.

```sql
select branch_id,
count(distinct issued_id)no_issued,
sum(rental_price)total_revenue ,
count(distinct return_id)books_returned 
from(
select e.*,f.return_id from(
select d.*,c.rental_price from 
books c
inner join 
(select a.issued_emp_id,a.issued_book_isbn,a.issued_id,b.branch_id from 
issued_status a
left Join 
employees b
on a.issued_emp_id = b.emp_id)d
on c.isbn = d.issued_book_isbn) e
left join
return_status f 
on e.issued_id = f.issued_id)g
group by branch_id;

```

**Task 16: CTAS: Create a Table of Active Members**  
Use the CREATE TABLE AS (CTAS) statement to create a new table active_members containing members who have issued at least one book in the last 1 Year.

```sql

Create table active_members As 
select * from members where member_id in(
select distinct issued_member_id from issued_status 
where issued_date >= current_date - interval 1 year); 

```

**Task 17: Find Employees with the Most Book Issues Processed**  
Write a query to find the top 3 employees who have processed the most book issues. Display the employee name, number of books processed, and their branch.

```sql

select a.emp_id,a.emp_name,a.branch_id,count(*) from 
employees a
inner Join 
issued_status b
on a.emp_id = b. issued_emp_id 
group by a.emp_id
order by count(*) desc
 Limit 3;

```

## Reports

- **Database Schema**: Detailed table structures and relationships.
- **Data Analysis**: Insights into book categories, employee salaries, member registration trends, and issued books.
- **Summary Reports**: Aggregated data on high-demand books and employee performance.

## Conclusion

This project demonstrates the application of SQL skills in creating and managing a library management system. It includes database setup, data manipulation, and advanced querying, providing a solid foundation for data management and analysis.

## Author - Tanish

                   ------------------------End Of Project ------------------------------
