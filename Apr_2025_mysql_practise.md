
```bash
sudo mysql
[sudo] password for chinmay: 
Sorry, try again.
[sudo] password for chinmay: 
Welcome to the MySQL monitor.  Commands end with ; or \g.
Your MySQL connection id is 8
Server version: 8.0.41-0ubuntu0.24.04.1 (Ubuntu)

Copyright (c) 2000, 2025, Oracle and/or its affiliates.

Oracle is a registered trademark of Oracle Corporation and/or its
affiliates. Other names may be trademarks of their respective
owners.

Type 'help;' or '\h' for help. Type '\c' to clear the current input statement.

```
```mysql
 SHOW databases;
 ```
```bash
+--------------------+
| Database           |
+--------------------+
| boomi              |
| boomi_cert         |
| information_schema |
| mysql              |
| performance_schema |
| sys                |
+--------------------+
6 rows in set (0.01 sec)
```
```bash
show tables;
ERROR 1046 (3D000): No database selected
mysql> CREATE DATABASE mysql_prep;
Query OK, 1 row affected (0.03 sec)
```
```bash
mysql> SHOW databases;
+--------------------+
| Database           |
+--------------------+
| boomi              |
| boomi_cert         |
| information_schema |
| mysql              |
| mysql_prep         |
| performance_schema |
| sys                |
+--------------------+
7 rows in set (0.00 sec)
```
mysql> USE mysql_prep;
Database changed
mysql> show tables;
Empty set (0.00 sec)

id creates a new column, this type of field will assign a unique numberic ID to each record in the table(starts with 1 and no two ID's will be same)

Creating a table:
CREATE TABLE mytable
(
id           int unsigned NOT NULL auto_increment,
usernam      varchar(100) NOT NULL,
email        varchar(100) NOT NULL,
PRIMARY KEY  (ID)
);

Inserting a row into the table:
INSERT INTO mytable(username,email)
VALUES("bindu","bindu.gmail.com");]

Updating a row:
mysql> UPDATE mytable SET email="bindu@gmail.com" WHERE id=1;
Query OK, 1 row affected (0.02 sec)
Rows matched: 1  Changed: 1  Warnings: 0

mysql> SELECT * FROM mytable;
+----+---------+-----------------+
| id | usernam | email           |
+----+---------+-----------------+
|  1 | bindu   | bindu@gmail.com |
+----+---------+-----------------+
1 row in set (0.00 sec)

Altering a table:
ALTER TABLE mytable CHANGE usernam username VARCHAR(100);
mysql> SELECT * FROM mytable;
+----+----------+-----------------+
| id | username | email           |
+----+----------+-----------------+
|  1 | bindu    | bindu@gmail.com |
+----+----------+-----------------+
1 row in set (0.00 sec)

Data types:
1.CHAR(n)

CHAR vs. VARCHAR:
Feature	                 CHAR(n)	                                      VARCHAR(n)
Length	         Fixed-length (always n)	                       Variable-length (up to n)
Padding	         Pads with spaces if shorter	                   Stores only actual characters
Performance	     Slightly faster for fixed size	                   More efficient for varying lengths
Use Case	     Codes, fixed IDs (e.g., country codes)	           Names, emails, addresses

Implicit or Automatic casting:
mysql> select '123' * 2;
+-----------+
| '123' * 2 |
+-----------+
|       246 |
+-----------+
1 row in set (0.00 sec)

'123ABC' * 2
246

'ABC123' * 2
0

SELECT :
It is used to retrieve rows selected from one or more tables.

SELECT with DISTINCT:
DISTINCT clause after SELECT eliminates duplicate rows from the result set.

` is required when using reserved words in SQL.

CREATE TABLE `car` (
  `car_id` INT UNSIGNED NOT NULL PRIMARY KEY,
  `name` VARCHAR(20),
  `price` DECIMAL(8,2)
);

INSERT INTO `car`(`car_id`,`name`,`price`) VALUES (1,'Audi A1','200000');
INSERT INTO `car`(`car_id`,`name`,`price`) VALUES (2,'Audi A1','150000');
INSERT INTO `car`(`car_id`,`name`,`price`) VALUES (3,'Audi A2','400000');
INSERT INTO `car`(`car_id`,`name`,`price`) VALUES (4,'Audi A2','400000');

SELECT DISTINCT `name`,`price` FROM `car`;

+---------+-----------+
| name    | price     |
+---------+-----------+
| Audi A1 | 200000.00 |
| Audi A1 | 150000.00 |
| Audi A2 | 400000.00 |
+---------+-----------+
3 rows in set (0.02 sec)

SELECT all columns:
SELECT * FROM `car`;

+--------+---------+-----------+
| car_id | name    | price     |
+--------+---------+-----------+
|      1 | Audi A1 | 200000.00 |
|      2 | Audi A1 | 150000.00 |
|      3 | Audi A2 | 400000.00 |
|      4 | Audi A2 | 400000.00 |
+--------+---------+-----------+
4 rows in set (0.00 sec)

SELECT by column name:
SELECT car_id FROM car;

+--------+
| car_id |
+--------+
|      1 |
|      2 |
|      3 |
|      4 |
+--------+

SELECT with LIKE(%):
CREATE TABLE stack
(id INT AUTO_INCREMENT PRIMARY KEY,
username VARCHAR(100)NOT NULL
);

INSERT stack(username) VALUES ('admin'),('k admin'),('adm'),('a adm b'),('b XadmY c'),('adm now'),('not here');

mysql> SELECT * FROM stack;
+----+-----------+
| id | username  |
+----+-----------+
|  1 | admin     |
|  2 | k admin   |
|  3 | adm       |
|  4 | a adm b   |
|  5 | b XadmY c |
|  6 | adm now   |
|  7 | not here  |
+----+-----------+
7 rows in set (0.00 sec)

Getting rows when "adm" is anywhere in the username:
SELECT * FROM stack WHERE username LIKE "%adm%";

+----+-----------+
| id | username  |
+----+-----------+
|  1 | admin     |
|  2 | k admin   |
|  3 | adm       |
|  4 | a adm b   |
|  5 | b XadmY c |
|  6 | adm now   |
+----+-----------+

Begins with "adm":
SELECT * FROM stack WHERE username LIKE "adm%";

+----+----------+
| id | username |
+----+----------+
|  1 | admin    |
|  3 | adm      |
|  6 | adm now  |
+----+----------+

Ends with "adm":
SELECT * FROM stack WHERE username LIKE "%adm";

+----+----------+
| id | username |
+----+----------+
|  3 | adm      |
+----+----------+

% --> matches any no.of characters
_ --> matches just one character

SELECT * FROM stack WHERE username LIKE "adm_n";
+----+----------+
| id | username |
+----+----------+
|  1 | admin    |
+----+----------+

SELECT with CASE or IF:
CREATE TABLE `student` (
  `id` INT UNSIGNED NOT NULL AUTO_INCREMENT PRIMARY KEY,
  `name` VARCHAR(50) NOT NULL,
  `percentage` INT(2) NOT NULL
);

INSERT INTO student (`name`,`percentage`) VALUES ('Abhi',94);
INSERT INTO student (`name`,`percentage`) VALUES ('Bhanu',25);
INSERT INTO student (`name`,`percentage`) VALUES ('Akash',62);
INSERT INTO student (`name`,`percentage`) VALUES ('Anshu',90);
INSERT INTO student (`name`,`percentage`) VALUES ('yash',87);
INSERT INTO student (`name`,`percentage`) VALUES ('Nayak',35);

mysql> select * from student;
+----+-------+------------+
| id | name  | percentage |
+----+-------+------------+
|  1 | Abhi  |         94 |
|  2 | Bhanu |         25 |
|  3 | Akash |         62 |
|  4 | Anshu |         90 |
|  5 | yash  |         87 |
|  6 | Nayak |         35 |
+----+-------+------------+

SELECT st.name,st.percentage,
CASE WHEN st.percentage >= 35 THEN 'Pass' ELSE 'Fail' END AS `Remark`
FROM student AS st;

+-------+------------+--------+
| name  | percentage | Remark |
+-------+------------+--------+
| Abhi  |         94 | Pass   |
| Bhanu |         25 | Fail   |
| Akash |         62 | Pass   |
| Anshu |         90 | Pass   |
| yash  |         87 | Pass   |
| Nayak |         35 | Pass   |
+-------+------------+--------+

Or with IF:
SELECT st.name,st.percentage,
IF(st.percentage >= 35, 'Pass','Fail') AS `Remark`
FROM student AS st;

+-------+------------+--------+
| name  | percentage | Remark |
+-------+------------+--------+
| Abhi  |         94 | Pass   |
| Bhanu |         25 | Fail   |
| Akash |         62 | Pass   |
| Anshu |         90 | Pass   |
| yash  |         87 | Pass   |
| Nayak |         35 | Pass   |
+-------+------------+--------+

SELECT with Alias(AS):
Aliases are used to temporarily rename a table or a column

SELECT percentage AS per FROM student;
(or)
SELECT percentage per FROM student;

+-----+
| per |
+-----+
|  94 |
|  25 |
|  62 |
|  90 |
|  87 |
|  35 |
+-----+

SELECT with a LIMIT clause:
ALways use ORDER BY when using LIMIT.

SELECT * FROM student ORDER BY name LIMIT 4;

+----+-------+------------+
| id | name  | percentage |
+----+-------+------------+
|  1 | Abhi  |         94 |
|  3 | Akash |         62 |
|  4 | Anshu |         90 |
|  2 | Bhanu |         25 |
+----+-------+------------+

SELECT * FROM student ORDER BY name LIMIT 2,1;

LIMIT offset, count

So LIMIT 2,1 means:

    Skip the first 2 rows (offset = 2)

    Then return the next 1 row

In other words:

It returns the 3rd row only, because:

    Row 0 → skipped

    Row 1 → skipped

    Row 2 → returned (this is the 3rd row, since counting starts from 0)

+----+-------+------------+
| id | name  | percentage |
+----+-------+------------+
|  4 | Anshu |         90 |
+----+-------+------------+

SELECT with BETWEEN:
BETWEEN clause is used to replace a combination of "greater than equal and less than equal" conditions.
BETWEEN uses only <= and >= but not < and >.

For negative cases we can use NOT BETWEEN.
NOT BETWEEN uses only < and > but not <= and >=.

SELECT * FROM student WHERE percentage >= 35 and percentage <= 90;
(or)
SELECT * FROM student WHERE percentage BETWEEN 35 and 90;

+----+-------+------------+
| id | name  | percentage |
+----+-------+------------+
|  3 | Akash |         62 |
|  4 | Anshu |         90 |
|  5 | yash  |         87 |
|  6 | Nayak |         35 |
+----+-------+------------+

SELECT * FROM student WHERE percentage NOT BETWEEN 35 and 90;

NOT BETWEEN 35 and 90 is same as WHERE (percentage < 35 and percentage > 90).

+----+-------+------------+
| id | name  | percentage |
+----+-------+------------+
|  1 | Abhi  |         94 |
|  2 | Bhanu |         25 |
+----+-------+------------+

SELECT with WHERE:
SELECT * FROM student WHERE id = 1 AND percentage = 94;

+----+------+------------+
| id | name | percentage |
+----+------+------------+
|  1 | Abhi |         94 |
+----+------+------------+

SELECT with LIKE(_):
SELECT percentage FROM student WHERE name LIKE 'Ansh_';

+------------+
| percentage |
+------------+
|         90 |
+------------+

If we have multiple names with Ansh_ we will get the percentage of all those members.
example : Anshi,Anshu,Ansha...

NULL:
Uses for NULL:
1. Data not yet known - such as end_date,rating.
2.Optional data - such as middle_initial(though that might be better as the empty string).
3.0/0 - The result of certain computations, such as zero divided by zero.
4.NULL is not equal to "" (blank string) or 0 (in case of integer).

Testing NULLs:
--> IS NULL/IS NOT NULL = NULL does not work like you expect.

SELECT * FROM my_table WHERE (column IS NULL) = NULL;

You might expect this to return rows where column is null. But it doesn’t work because:

    column IS NULL returns a Boolean: TRUE or FALSE

    Comparing a Boolean to NULL with = results in... NULL (unknown)

    And in SQL, a condition that evaluates to NULL is treated as false

✅ Correct way:

WHERE column IS NULL

❌ Wrong way:

WHERE (column IS NULL) = NULL

--> x <=> y is a "null-safe" comparison.
x <=> y

This is the null-safe equality operator.

It returns:

    TRUE if x = y

    TRUE if both x and y are NULL

    FALSE otherwise

LIMIT and OFFSET:
LIMIT clause with one argument:
SELECT * FROM student ORDER BY id ASC LIMIT 2;

+----+-------+------------+
| id | name  | percentage |
+----+-------+------------+
|  1 | Abhi  |         94 |
|  2 | Bhanu |         25 |
+----+-------+------------+

LIMIT Clause with two arguments:
SELECT * FROM student ORDER BY id ASC LIMIT 2,3;

+----+-------+------------+
| id | name  | percentage |
+----+-------+------------+
|  3 | Akash |         62 |
|  4 | Anshu |         90 |
|  5 | yash  |         87 |
+----+-------+------------+

LIMIT offset, count

So LIMIT 2,3 means:

    Skip the first 2 rows (offset = 2)

    Then return the next 3 rows

Notice taht when the offset argument is 0, the result set will be equivalent to a one argument LIMIT clause.
SELECT * FROM student ORDER BY id ASC LIMIT 0,2;
SELECT * FROM student ORDER BY id ASC LIMIT 2;

Above 2 queries gives the same result.
+----+-------+------------+
| id | name  | percentage |
+----+-------+------------+
|  1 | Abhi  |         94 |
|  2 | Bhanu |         25 |
+----+-------+------------+


OFFSET keyword (alternative syntax):
SELECT * FROM student ORDER BY Id ASC LIMIT 2 OFFSET 3;

Skips 3 rows and returns the next 2 rows
+----+-------+------------+
| id | name  | percentage |
+----+-------+------------+
|  4 | Anshu |         90 |
|  5 | yash  |         87 |
+----+-------+------------+

Creating Databases:

Parameter                            Details
CREATE DATABASE           Creates a database with given name
CREATE SCHEMA             This is a synonym for CREATE DATABASE
IF NOT EXISTS             Used to avoid execution error,if specified database already exists
create_specification      If specify database characteristics such as CHARACTER SET and COLLATE(database collation)

💬 CHARACTER SET vs COLLATE

Aspect                 CHARACTER SET                                          COLLATE
What it does       Defines how characters are stored            Defines how text is compared and sorted
Examples           utf8, utf8mb4, latin1                        utf8_general_ci, utf8_bin, utf8mb4_unicode_ci
Sensitivity        N/A                                          Can be case-sensitive (cs) or insensitive (ci)
Binary or not      N/A                                          Collations like utf8_bin use binary comparison

CREATE DATABASE Baseball;

CREATE DATABASE IF NOT EXISTS Baseball;

The SQL engine checks if a database named Baseball already exists.
If it does not exist, it creates it.
If it already exists, it does nothing—no error is thrown.

Similarly, 
DROP DATABASE IF EXISTS Baseball;(drops the table if it exixts other wise it does nothing—no error is thrown.)
DROP DATABASE Baseball;(drops the table if it exixts other wise it throws error 1008)

CREATE DATABASE Baseball
    CHARACTER SET utf8
    COLLATE utf8_general_ci;

mysql> USE Baseball;
Database changed
mysql> SELECT @@character_set_database as cset, @@collation_database as col;
+---------+--------------------+
| cset    | col                |
+---------+--------------------+
| utf8mb3 | utf8mb3_general_ci |
+---------+--------------------+
The above shows the default CHARACTER SET and Collation for the database.

Using Variables:
Setting Variables:
1.You can set a variable to a specific string,number,date using SET.

SET @var_string = 'my_var';
SET @var_num = '2';
SET @var_date = '2025-04-18';

INSERT:
INSERT , ON DUPLICATE KEY UPDATE:

INSERT INTO table_name
    (index_field,other_field_1,other_field_2)
    VALUES
    (index_value,other_value_1,other_value_2)
ON DUPLICATE KEY UPDATE
    other_field_1 = update_value,
    other_field_2 = VALUES(other_field_2);

The ON DUPLICATE KEY UPDATE clause is a MySQL feature used in INSERT statements to handle conflicts that occur due to duplicate keys (like primary keys or unique constraints). It allows you to update existing rows instead of causing an error when a duplicate key is found.

🧠 How It Works
MySQL tries to insert the new row.
If no duplicate key conflict occurs (no unique or primary key collision), the row is inserted normally.
If a duplicate key conflict does occur:
   Instead of throwing an error, the ON DUPLICATE KEY UPDATE clause is triggered.
   The existing row with the duplicate key is updated with the values provided in the UPDATE part.

Inserting multiple rows:

INSERT INTO my_table (field_1,field_2)
    VALUES (data_1,data_2),
           (data_1,data_3),
           (data_4,data_5);

Ignoring existing rows:
INSERT IGNORE INTO my_table (field_1,field_2)
    VALUES (data_1,data_2),
           (data_1,data_3),
           (data_4,data_5);

Use case                                   Statement
Silently skip existing rows              INSERT IGNORE
Overwrite existing rows                  REPLACE INTO
Update existing rows            INSERT ... ON DUPLICATE KEY UPDATE

Basic Insert:
INSERT INTO my_table (field_1,field_2)
    VALUES (data_1,data_2),
           (data_1,data_3);

INSERT with AUTO_INCREEMNT+LAST_INSERT_ID():

CREATE TABLE iodku(
    id INT AUTO_INCREMENT NOT NULL,
    name VARCHAR(20) NOT NULL,
    misc INT NOT NULL,
    PRIMARY KEY(id),
    UNIQUE(name)
    )ENGINE=InnoDB;

INSERT INTO iodku(name,misc)
 VALUES('Leslie',123),
       ('Sally',456);

In MySQL, the clause ENGINE=InnoDB at the end of a CREATE TABLE statement specifies the storage engine used for that table.
A storage engine is the backend component responsible for storing, managing, and retrieving data in a MySQL table. Different engines have different features.
ENGINE=InnoDB:It tells MySQL to use InnoDB, which is the default and most powerful storage engine.

Case 1: IODKU performing an update and LAST_INSERT_ID() retrieving the relevant id:

INSERT INTO iodku(name,misc)
    VALUES ('Sally',333)
    ON DUPLICATE KEY UPDATE
    id = LAST_INSERT_ID(id),
    misc = VALUES(misc);

SELECT LAST_INSERT_ID();

+------------------+
| LAST_INSERT_ID() |
+------------------+
|                2 |
+------------------+

Case 2: IODKU performs an insert and LAST_INSERT_ID() retrieves the new id:

INSERT INTO iodku(name,misc)
    VALUES ('Dolly',789)
    ON DUPLICATE KEY UPDATE
    id = LAST_INSERT_ID(id),
    misc = VALUES(misc);

SELECT LAST_INSERT_ID();

+------------------+
| LAST_INSERT_ID() |
+------------------+
|                4 |
+------------------+

mysql> SELECT * FROM iodku;
+----+--------+------+
| id | name   | misc |
+----+--------+------+
|  1 | Leslie |  123 |
|  2 | Sally  |  333 |
|  4 | Dolly  |  789 |
+----+--------+------+

INSERT SELECT (inserting data from another table):

INSERT INTO tableA(field_1,field_2)
   SELECT tableB.field_1, tableB.field_2
   FROM tableB
   WHERE tableB.clmn <> somevalue
   ORDER BY tableB.sorting_clmn;

We can use SELECT * FROM , but for that we need to have matching column count and corresponding datatypes for two tables.

Lost AUTO_INCREMENT id's:

CREATE TABLE Burn(
    id SMALLINT UNSIGNED AUTO_INCREMENT NOT NULL,
    name VARCHAR(20) NOT NULL,
    PRIMARY KEY(id),
    UNIQUE(name)
    )ENGINE=InnoDB;

INSERT IGNORE INTO Burn(name) VALUES('first'),('second');

SELECT LAST_INSERT_ID();

+------------------+
| LAST_INSERT_ID() |
+------------------+
|                1 |
+------------------+

SELECT * FROM Burn ORDER BY id;

+----+--------+
| id | name   |
+----+--------+
|  1 | first  |
|  2 | second |
+----+--------+

INSERT IGNORE INTO Burn(name) VALUES ('second');

SELECT LAST_INSERT_ID();

+------------------+
| LAST_INSERT_ID() |
+------------------+
|                4 |
+------------------+

SELECT * FROM Burn ORDER BY id;

+----+--------+
| id | name   |
+----+--------+
|  1 | first  |
|  2 | second |
|  4 | third  |
+----+--------+

DELETE:

Parameter -> Details
LOW_PRIORITY -> If LOW_PRIORITY is provided, the delete will be delayed until there are no processes reading from the table.
IGNORE -> If IGNORE is provided, all errors encountered during the delete are ignored.      
WHERE conditions -> The conditions that must be met for the records to be deleted. If no conditions are provided, then all records will be deleted from the table.
ORDER BY expression -> If ORDER BY is provided, the records will be deleted in the given order.
LIMIT -> It controls the maximum no.of records to delete from the table. Given number_rows wil be deleted.

Multi-Table Deletes:
MySQL's DELETE statement can use JOIN construct, allowing also to specify which tables to detele from. This is useful to avoid nested queries.

CREATE TABLE people
(  id INT PRIMARY KEY,
   name VARCHAR(20) NOT NULL,
   gender CHAR(1) NOT NULL
);

INSERT people (id,name,gender) VALUES (1,'Kathy','F'),(2,'John','M'),(3,'Paul','M'),(4,'Kim','M');

SELECT * FROM people;
+----+-------+--------+
| id | name  | gender |
+----+-------+--------+
|  1 | Kathy | F      |
|  2 | John  | M      |
|  3 | Paul  | M      |
|  4 | Kim   | M      |
+----+-------+--------+

CREATE TABLE pets
(  id INT AUTO_INCREMENT PRIMARY KEY,
   ownerId INT NOT NULL,
   name VARCHAR(20) NOT NULL,
   color VARCHAR(20) NOT NULL
);

INSERT pets (ownerId,name,color) VALUES (1,'Rover','beige'),(2,'Bubbles','purple'),(3,'Spot','black and white'),(1,'Rover2','white');

SELECT * FROM pets;
+----+---------+---------+-----------------+
| id | ownerId | name    | color           |
+----+---------+---------+-----------------+
|  1 |       1 | Rover   | beige           |
|  2 |       2 | Bubbles | purple          |
|  3 |       3 | Spot    | black and white |
|  4 |       1 | Rover2  | white           |
+----+---------+---------+-----------------+

If we want to remove Paul's pets:

DELETE p2
FROM people p1
JOIN pets p2
ON p2.ownerId = p1.id
WHERE p1.name = 'Paul';

+----+---------+---------+--------+
| id | ownerId | name    | color  |
+----+---------+---------+--------+
|  1 |       1 | Rover   | beige  |
|  2 |       2 | Bubbles | purple |
|  4 |       1 | Rover2  | white  |
+----+---------+---------+--------+

If we want to remove both person and pet:

DELETE p1,p2
FROM people p1
JOIN pets p2
ON p2.ownerId = p1.id
WHERE p1.name = 'Paul';

INSERT pets (ownerId,name,color) VALUES (3,'Spot','black and white');

SELECT * FROM people;
+----+-------+--------+
| id | name  | gender |
+----+-------+--------+
|  1 | Kathy | F      |
|  2 | John  | M      |
|  4 | Kim   | M      |
+----+-------+--------+

TRUNCATE :
In MySQL, TRUNCATE is a Data Definition Language (DDL) command used to quickly delete all rows from a table, resetting it to empty — but more efficient than DELETE FROM table_name.

syntax:TRUNCATE TABLE table_name;

Important points about TRUNCATE:
It removes all rows from the table very quickly.
It resets AUTO_INCREMENT counters (if the table has an AUTO_INCREMENT primary key).
You cannot truncate a table that is referenced by a foreign key constraint (unless you first drop or disable the constraint).
TRUNCATE is often faster than DELETE because it does not log individual row deletions (it just logs the operation).
You cannot use WHERE clauses with TRUNCATE. If you want to delete specific rows, use DELETE.
In most storage engines (like InnoDB and MyISAM), it is essentially a drop and recreate table internally.

TRUNCATE vs DELETE
Feature               TRUNCATE                                                      DELETE
Removes all rows        Yes                                                 Yes (can use WHERE to filter)
Auto_increment reset    Yes                                                           No
Can use WHERE           No                                                            Yes
Logging                 Minimal (only the table operation)                    Row-by-row logging
Speed                   Faster                                               Slower for large tables

Multi-table DELETE:
This lets you delete rows from multiple tables at once, using a single DELETE query, often based on joins.

    You list the tables you want to delete from right after DELETE.
    Then use a JOIN to link the tables.
    The WHERE clause specifies which rows to delete.

remove only the employees
DELETE e
FROM Employees e JOIN Department d ON e.department_id = d.department_id
WHERE d.name = 'Sales'

-- remove employees and department
DELETE e, d
FROM Employees e JOIN Department d ON e.department_id = d.department_id
WHERE d.name = 'Sales'

-- remove from all tables (in this case same as previous)
DELETE
FROM Employees e JOIN Department d ON e.department_id = d.department_id
WHERE d.name = 'Sales'

Basic DELETE:
DELETE FROM mytable WHERE somecolumn = something

Delete all rows from a table:
DELETE FROM table_name;

LIMITing DELETE:
DELETE FROM table_name WHERE field_one = value_one LIMIT 1

UPDATE
Basic Update:

Creating a table:
CREATE TABLE mytable
(
id           int unsigned NOT NULL auto_increment,
usernam      varchar(100) NOT NULL,
email        varchar(100) NOT NULL,
PRIMARY KEY  (ID)
);

Inserting a row into the table:
INSERT INTO mytable(username,email)
VALUES("bindu","bindu.gmail.com");

Updating a row:
mysql> UPDATE mytable SET email="bindu@gmail.com" WHERE id=1;
Query OK, 1 row affected (0.02 sec)
Rows matched: 1  Changed: 1  Warnings: 0

mysql> SELECT * FROM mytable;
+----+---------+-----------------+
| id | usernam | email           |
+----+---------+-----------------+
|  1 | bindu   | bindu@gmail.com |
+----+---------+-----------------+

UPDATE all rows:
UPDATE mytable SET email="bindu@gmail.com";

mysql> INSERT INTO mytable(username,email)
    -> VALUES("mouni","bindu.gmail.com");
Query OK, 1 row affected (0.02 sec)

mysql> SELECT * FROM mytable;
+----+----------+-----------------+
| id | username | email           |
+----+----------+-----------------+
|  1 | bindu    | bindu@gmail.com |
|  2 | mouni    | bindu.gmail.com |
+----+----------+-----------------+
2 rows in set (0.01 sec)

mysql> UPDATE mytable SET email="bindu@gmail.com";
Query OK, 1 row affected (0.01 sec)
Rows matched: 2  Changed: 1  Warnings: 0

mysql> SELECT * FROM mytable;
+----+----------+-----------------+
| id | username | email           |
+----+----------+-----------------+
|  1 | bindu    | bindu@gmail.com |
|  2 | mouni    | bindu@gmail.com |
+----+----------+-----------------+

Bulk UPDATE:
SELECT * FROM car;
+--------+---------+-----------+
| car_id | name    | price     |
+--------+---------+-----------+
|      1 | Audi A1 | 200000.00 |
|      2 | Audi A1 | 150000.00 |
|      3 | Audi A2 | 400000.00 |
|      4 | Audi A2 | 400000.00 |
+--------+---------+-----------+
UPDATE car
SET name = 
       (case car_id WHEN 1 THEN 'R8 SPYDER'
                WHEN 2 THEN 'TTRS Coupe'
                WHEN 3 THEN 'RS6'
                WHEN 4 THEN 'R7'
        END)
    WHERE car_id IN (1,2,3,4);

SELECT * FROM car;
+--------+------------+-----------+
| car_id | name       | price     |
+--------+------------+-----------+
|      1 | R8 SPYDER  | 200000.00 |
|      2 | TTRS Coupe | 150000.00 |
|      3 | RS6        | 400000.00 |
|      4 | R7         | 400000.00 |
+--------+------------+-----------+
4 rows in set (0.00 sec)

UPDATE with ORDER BY and LIMIT:
Syntax:
UPDATE[LOW_PRIORITY] [IGNORE]
tablename
SET column1 = expression1,
    column2 = expression2,
    ....
[WHERE conditions]
[ORDER BY expression [ASC | DESC]]
[LIMIT row_count];

Example:
UPDATE car SET price=24000000 ORDER BY car_id LIMIT 3;

Multi-table UPADTE:
Syntax:
UPDATE[LOW_PRIORITY] [IGNORE]
table1,table2,....
SET column1 = expression1,
    column2 = expression2,
    ....
[WHERE conditions]

ORDER BY:
Basic Syntax: ORDER BY x;
x can be any datatype.

NULLs precede non-NULLs.
The default is ASC (lowest to highest)
Strings (VARCHAR, etc) are ordered according the COLLATION of the declaration
ENUMs are ordered by the declaration order of its strings.

ASCending / DESCending:

ORDER BY x ASC -- same as default
ORDER BY x DESC -- highest to lowest
ORDER BY lastname, firstname -- typical name sorting; using two columns
ORDER BY submit_date DESC -- latest first
ORDER BY submit_date DESC, id ASC -- latest first, but fully specifying order.

ASC = ASCENDING, DESC = DESCENDING
NULLs come first even for DESC.
In the above examples, INDEX(x), INDEX(lastname, firstname), INDEX(submit_date) may significantly
improve performance.
But... Mixing ASC and DESC, as in the last example, cannot use a composite index to benefit. Nor will
INDEX(submit_date DESC, id ASC) help -- "DESC" is recognized syntactically in the INDEX declaration, but ignored

GROUP BY:
Parameter                                           DETAILS
expression1, expression2, ...     The expressions that are not encapsulated within an aggregate function and
expression_n                      must be included in the GROUP BY clause.
aggregate_function                A function such as SUM, COUNT, MIN, MAX, or AVG functions.
tables                            the tables that you wish to retrieve records from. There must be at least one
                                  table listed in the FROM clause.
WHERE conditions                  Optional. The conditions that must be met for the records to be selected

GROUP BY using HAVING:
CREATE TABLE employees (
    employee_id INT AUTO_INCREMENT PRIMARY KEY,
    name VARCHAR(100),
    department VARCHAR(50)
);

INSERT INTO employees (name, department) VALUES
('John Smith', 'Sales'),
('Alice Brown', 'Sales'),
('Bob Johnson', 'IT'),
('Mary White', 'HR'),
('Steve Black', 'Sales'),
('Laura Green', 'IT'),
('Kevin Adams', 'IT'),
('Emma Wilson', 'HR'),
('Sophia Hill', 'IT'),
('Liam Scott', 'Sales');

SELECT * FROM employees;
+-------------+-------------+------------+
| employee_id | name        | department |
+-------------+-------------+------------+
|           1 | John Smith  | Sales      |
|           2 | Alice Brown | Sales      |
|           3 | Bob Johnson | IT         |
|           4 | Mary White  | HR         |
|           5 | Steve Black | Sales      |
|           6 | Laura Green | IT         |
|           7 | Kevin Adams | IT         |
|           8 | Emma Wilson | HR         |
|           9 | Sophia Hill | IT         |
|          10 | Liam Scott  | Sales      |
+-------------+-------------+------------+
10 rows in set (0.00 sec)

SELECT department, COUNT(*) AS Man_Power
FROM employees
GROUP BY department
HAVING COUNT(*) >= 10;

Empty set (0.00 sec)

🔵 Result:
No rows would be returned because no department has 10 or more employees in this example.

GROUP BY using GROUP CONCAT:
SELECT department, GROUP_CONCAT(name ORDER BY name SEPARATOR ', ') AS employee_names
FROM employees
GROUP BY department;

+------------+----------------------------------------------------+
| department | employee_names                                     |
+------------+----------------------------------------------------+
| HR         | Emma Wilson, Mary White                            |
| IT         | Bob Johnson, Kevin Adams, Laura Green, Sophia Hill |
| Sales      | Alice Brown, John Smith, Liam Scott, Steve Black   |
+------------+----------------------------------------------------+

GROUP BY using MIN function:
SELECT department, MIN(employee_id) AS "Early Joiner"
FROM employees
GROUP BY department;

+------------+--------------+
| department | Early Joiner |
+------------+--------------+
| Sales      |            1 |
| IT         |            3 |
| HR         |            4 |
+------------+--------------+

GROUP BY with AGGREGATE functions:

SELECT department, COUNT(*) AS total_employees
FROM employees
GROUP BY department
ORDER BY total_employees DESC;

+------------+-----------------+
| department | total_employees |
+------------+-----------------+
| Sales      |               4 |
| IT         |               4 |
| HR         |               2 |
+------------+-----------------+

SUM of employee_id by department:

SELECT department, SUM(employee_id) AS total_employee_id
FROM your_table
GROUP BY department;

AVG (Average) of employee_id by department:

SELECT department, AVG(employee_id) AS avg_employee_id
FROM your_table
GROUP BY department;

MAX (Maximum) employee_id by department:

SELECT department, MAX(employee_id) AS max_employee_id
FROM your_table
GROUP BY department;

MIN (Minimum) employee_id by department:

SELECT department, MIN(employee_id) AS min_employee_id
FROM your_table
GROUP BY department;

JOINS:
JOIN with subquery
SELECT X,...
     FROM (SELECT y,....FROM....) AS a
     JOIN (SELECT x,....FROM....) AS b.x = a.y
     WHERE....

FULL OUTER JOIN:
Mysql doesnot support FULL OUTER JOIN, but there are ways to emulate one

CREATE TABLE owners(
owner_id INT NOT NULL AUTO_INCREMENT PRIMARY KEY,
owner    VARCHAR(20) DEFAULT NULL
) ENGINE=InnoDB AUTO_INCREMENT = 10 DEFAULT CHARSET=latin1;

INSERT INTO owners VALUES ('1','Ben');
INSERT INTO owners VALUES ('2','Jim');
INSERT INTO owners VALUES ('3','Harry');
INSERT INTO owners VALUES ('6','John');
INSERT INTO owners VALUES ('9','Karry');

SELECT * FROM owners;
+----------+-------+
| owner_id | owner |
+----------+-------+
|        1 | Ben   |
|        2 | Jim   |
|        3 | Harry |
|        6 | John  |
|        9 | Karry |
+----------+-------+

CREATE TABLE tools(
tool_id INT NOT NULL AUTO_INCREMENT PRIMARY KEY,
tool VARCHAR(20) DEFAULT NULL,
owner_id INT(5) DEFAULT NULL
)ENGINE=InnoDB AUTO_INCREMENT = 11 DEFAULT CHARSET=latin1;

INSERT INTO tools VALUES ('1','Hammer','9');
INSERT INTO tools VALUES ('2','Pliers','1');
INSERT INTO tools VALUES ('3','Knife','1');
INSERT INTO tools VALUES ('4','Chisel','2');
INSERT INTO tools VALUES ('5','Hacksaw','1');
INSERT INTO tools VALUES ('6','Level',null);
INSERT INTO tools VALUES ('7','Wrench',null);
INSERT INTO tools VALUES ('8','Tape Measure','9');
INSERT INTO tools VALUES ('9','Screwdriver',null);
INSERT INTO tools VALUES ('10','Clamp',null);

+---------+--------------+----------+
| tool_id | tool         | owner_id |
+---------+--------------+----------+
|       1 | Hammer       |        9 |
|       2 | Pliers       |        1 |
|       3 | Knife        |        1 |
|       4 | Chisel       |        2 |
|       5 | Hacksaw      |        1 |
|       6 | Level        |     NULL |
|       7 | Wrench       |     NULL |
|       8 | Tape Measure |        9 |
|       9 | Screwdriver  |     NULL |
|      10 | Clamp        |     NULL |
+---------+--------------+----------+

we want to get a list,in which we can see who owns which tools and which tools might not have an owner.
Solution:
we can combine two queries by using UNION.
In first query - we are joining the tools of the owners by using a LEFT join
In second query - we are using RIGHT join to join the tools onto the owners.

SELECT owners.owner,tools.tool
FROM owners
LEFT JOIN tools ON owners.owner_id = tools.owner_id
UNION ALL
SELECT owners.owner,tools.tool
FROM owners
RIGHT JOIN tools ON owners.owner_id = tools.owner_id
WHERE owners.owner_id IS NULL;

+-------+--------------+
| owner | tool         |
+-------+--------------+
| Ben   | Hacksaw      |
| Ben   | Knife        |
| Ben   | Pliers       |
| Jim   | Chisel       |
| Harry | NULL         |
| John  | NULL         |
| Karry | Tape Measure |
| Karry | Hammer       |
| NULL  | Level        |
| NULL  | Wrench       |
| NULL  | Screwdriver  |
| NULL  | Clamp        |
+-------+--------------+

Retrieve customers with orders -- variations on a theme

creating tables Customers and Orders
CREATE TABLE Customers (
    CustomerID INT PRIMARY KEY,
    CustomerName VARCHAR(255) NOT NULL
);

CREATE TABLE Orders (
    OrderID INT PRIMARY KEY,
    CustomerID INT,
    OrderDate DATE,
    FOREIGN KEY (CustomerID) REFERENCES Customers(CustomerID)
);

Inserting data into tables
INSERT INTO Customers (CustomerID, CustomerName)
VALUES
(1, 'Alice Smith'),
(2, 'Bob Johnson'),
(3, 'Charlie Lee'),
(4, 'David Kim');

+------------+--------------+
| CustomerID | CustomerName |
+------------+--------------+
|          1 | Alice Smith  |
|          2 | Bob Johnson  |
|          3 | Charlie Lee  |
|          4 | David Kim    |
+------------+--------------+

INSERT INTO Orders (OrderID, CustomerID, OrderDate)
VALUES
(101, 1, '2025-05-01'),
(102, 1, '2025-05-02'),
(103, 2, '2025-05-03'),
(104, 3, '2025-05-04'),
(105, 4, '2025-05-05'),
(106, 4, '2025-05-06');

+---------+------------+------------+
| OrderID | CustomerID | OrderDate  |
+---------+------------+------------+
|     101 |          1 | 2025-05-01 |
|     102 |          1 | 2025-05-02 |
|     103 |          2 | 2025-05-03 |
|     104 |          3 | 2025-05-04 |
|     105 |          4 | 2025-05-05 |
|     106 |          4 | 2025-05-06 |
+---------+------------+------------+

This will get all the orders for all customers:
SELECT c.CustomerName, o.OrderID
FROM Customers AS c
INNER JOIN Orders AS o
ON c.CustomerID = o.CustomerID
ORDER BY c.CustomerName, o.OrderID;

+--------------+---------+
| CustomerName | OrderID |
+--------------+---------+
| Alice Smith  |     101 |
| Alice Smith  |     102 |
| Bob Johnson  |     103 |
| Charlie Lee  |     104 |
| David Kim    |     105 |
| David Kim    |     106 |
+--------------+---------+

This will count the number of orders for each customer:
SELECT c.CustomerName, COUNT(*) AS 'Order Count'
FROM Customers AS c
INNER JOIN Orders AS o
ON c.CustomerID = o.CustomerID
GROUP BY c.CustomerID
ORDER BY c.CustomerName;

+--------------+-------------+
| CustomerName | Order Count |
+--------------+-------------+
| Alice Smith  |           2 |
| Bob Johnson  |           1 |
| Charlie Lee  |           1 |
| David Kim    |           2 |
+--------------+-------------+

Also, counts, but probably faster with alternative query:
SELECT c.CustomerName,
( SELECT COUNT(*) FROM Orders WHERE CustomerID = c.CustomerID ) AS 'Order Count'
FROM Customers AS c
ORDER BY c.CustomerName;

+--------------+-------------+
| CustomerName | Order Count |
+--------------+-------------+
| Alice Smith  |           2 |
| Bob Johnson  |           1 |
| Charlie Lee  |           1 |
| David Kim    |           2 |
+--------------+-------------+

List only the customer with orders.
SELECT c.CustomerName
FROM Customers AS c
WHERE EXISTS ( SELECT * FROM Orders WHERE CustomerID = c.CustomerID )
ORDER BY c.CustomerName;

+--------------+
| CustomerName |
+--------------+
| Alice Smith  |
| Bob Johnson  |
| Charlie Lee  |
| David Kim    |
+--------------+

JOINS: Join 3 table with the same name of id.
Join 3 tables on a column with the same name

CREATE TABLE Table1 (
id INT UNSIGNED NOT NULL,
created_on DATE NOT NULL,
PRIMARY KEY (id)
)
CREATE TABLE Table2 (
id INT UNSIGNED NOT NULL,
personName VARCHAR(255) NOT NULL,
PRIMARY KEY (id)
)
CREATE TABLE Table3 (
id INT UNSIGNED NOT NULL,
accountName VARCHAR(255) NOT NULL,
PRIMARY KEY (id)
)
after creating the tables you could do a select query to get the id's of all three tables that are the same
SELECT
t1.id AS table1Id,
t2.id AS table2Id,
t3.id AS table3Id
FROM Table1 t1
LEFT JOIN Table2 t2 ON t2.id = t1.id
LEFT JOIN Table3 t3 ON t3.id = t1.id

UNIONS:
Combining SELECT statements with UNION:
1. Combining Results from Two Queries (with UNION)

    What it does: Combines the results of two queries into one.

    Duplicates: Removes duplicate rows by default.

    Example: Get contact info from both authors and editors tables:

    SELECT name, email, phone_number FROM authors
    UNION
    SELECT name, email, phone_number FROM editors;

2. Combining Queries with Different Columns

    What it does: If the queries return different columns, you match them by giving default values for missing columns.

    Example: Combining books (with pages) and movies (without pages):

    SELECT name, caption AS title, year, pages FROM books
    UNION
    SELECT name, title, year, 0 AS pages FROM movies;

3. Sorting Results with ORDER BY

    What it does: Sort the combined result.

    Example:

    (SELECT name, email FROM authors ORDER BY name)
    UNION
    (SELECT name, email FROM editors ORDER BY name)
    ORDER BY name;

4. Pagination with LIMIT and OFFSET

    What it does: Limits the number of rows and implements pagination.

    Example: Get the 4th page of results, 10 rows per page:

    (SELECT name FROM authors ORDER BY name LIMIT 40)
    UNION
    (SELECT name FROM editors ORDER BY name LIMIT 40)
    ORDER BY name LIMIT 30, 10;

5. Combining Data from Multiple Tables (with UNION ALL)

    What it does: Combines data from multiple tables (keeping duplicates).

    Example: Get stats from multiple server logs:

    SELECT YEAR(date_time_column), MONTH(date_time_column), MIN(DATE(date_time_column)),
    MAX(DATE(date_time_column)), COUNT(DISTINCT ip), COUNT(ip), (COUNT(ip) / COUNT(DISTINCT ip)) AS Ratio
    FROM (
        (SELECT date_time_column, ip FROM server_log_1 WHERE state = 'action' AND log_id = 150)
        UNION ALL
        (SELECT date_time_column, ip FROM server_log_2 WHERE state = 'action' AND log_id = 150)
        UNION ALL
        (SELECT date_time_column, ip FROM server_log_3 WHERE state = 'action' AND log_id = 150)
        UNION ALL
        (SELECT date_time_column, ip FROM server_log WHERE state = 'action' AND log_id = 150)
    ) AS table_all
    GROUP BY YEAR(date_time_column), MONTH(date_time_column);

6. UNION vs UNION ALL

    UNION: Removes duplicates.

    UNION ALL: Keeps duplicates.

    Example:

    -- UNION (removes duplicates)
    SELECT 1, 22, 44
    UNION
    SELECT 2, 33, 55;

    -- UNION ALL (keeps duplicates)
    SELECT 1, 22, 44
    UNION ALL
    SELECT 2, 33, 55
    UNION ALL
    SELECT 2, 33, 55;

In Short:

    Use UNION to combine results and remove duplicates.

    Use UNION ALL to combine results and keep duplicates.

    When combining data with different columns, use default values (0 or NULL).

    Use ORDER BY and LIMIT to sort and paginate the results.

Arithmetic Operations in MySQL

    Basic Arithmetic Operators

        Addition (+): Adds two numbers.

SELECT 3 + 5; -- 8

Subtraction (-): Subtracts the second number from the first.

SELECT 3 - 5; -- -2

Multiplication (*): Multiplies two numbers.

SELECT 3 * 5; -- 15

Division (/): Divides the first number by the second.

SELECT 20 / 4; -- 5
SELECT 355 / 113; -- 3.1416
SELECT 10.0 / 0; -- NULL (Division by zero returns NULL)

Integer Division (DIV): Divides two integers and returns the integer part.

SELECT 5 DIV 2; -- 2

Modulo (% or MOD): Returns the remainder after division.

    SELECT 7 % 3; -- 1
    SELECT 15 MOD 4; -- 3

Data Types

    BIGINT: Used for integer calculations, supports large numbers.

SELECT (1024 * 1024 * 1024 * 1024 * 1024 * 1024) + 1; -- 1,152,921,504,606,846,977

DOUBLE: Used for fractional arithmetic (floating-point numbers).

    SELECT (1024 * 1024 * 1024 * 1024 * 1024 * 1024 * 1024); -- Might cause overflow for large numbers

Mathematical Constants

    Pi (PI()): Returns the value of Pi.

    SELECT PI(); -- 3.141593

Trigonometric Functions

    SIN(): Sine of an angle (in radians).

SELECT SIN(PI()); -- 1.2246063538224e-16 (approx. 0)

COS(): Cosine of an angle.

SELECT COS(PI()); -- -1

TAN(): Tangent of an angle.

SELECT TAN(PI()); -- -1.2246063538224e-16 (approx. 0)

ACOS() / ASIN(): Inverse cosine/sine.

SELECT ACOS(1); -- 0
SELECT ASIN(0.2); -- 0.20135792079033

ATAN() / ATAN2(): Inverse tangent.

    SELECT ATAN(2); -- 1.1071487177941
    SELECT ATAN2(1,1); -- 0.7853981633974483

Rounding Functions

    ROUND(): Rounds to the nearest integer.

SELECT ROUND(4.51); -- 5
SELECT ROUND(4.49); -- 4

FLOOR(): Rounds down.

SELECT FLOOR(1.99); -- 1

CEIL() or CEILING(): Rounds up.

    SELECT CEIL(1.23); -- 2

Power and Square Root

    POW(): Raises a number to a power.

SELECT POW(2, 3); -- 8

SQRT(): Returns the square root of a number.

    SELECT SQRT(16); -- 4

Random Numbers

    RAND(): Generates a random floating-point number between 0 and 1.

SELECT RAND(); -- Random number between 0 and 1

Random number in a range (a <= n <= b):

    SELECT FLOOR(7 + (RAND() * 6)); -- Random number between 7 and 12

Absolute Value and Sign

    ABS(): Returns the absolute value of a number.

SELECT ABS(-46); -- 46

SIGN(): Returns the sign of a number (-1, 0, or 1).

        SELECT SIGN(-3); -- -1

String Operations in MySQL

    Basic String Functions

        LENGTH(): Returns the length of a string in bytes.

SELECT LENGTH('foobar'); -- 6
SELECT LENGTH('fööbar'); -- 8 (because of multi-byte characters)

CHAR_LENGTH(): Returns the number of characters in a string.

    SELECT CHAR_LENGTH('fööbar'); -- 6

Case Conversion

    UPPER() / UCASE(): Converts string to uppercase.

SELECT UPPER('fOoBar'); -- 'FOOBAR'

LOWER() / LCASE(): Converts string to lowercase.

    SELECT LOWER('fOoBar'); -- 'foobar'

Substring Extraction

    SUBSTRING() / SUBSTR(): Extracts a substring from a string.

    SELECT SUBSTRING('foobarbaz', 4); -- 'barbaz'
    SELECT SUBSTRING('foobarbaz', -6, 3); -- 'bar'

String Replacement

    REPLACE(): Replaces occurrences of a substring with another substring.

    SELECT REPLACE('foobarbaz', 'bar', 'BAR'); -- 'fooBARbaz'

Hexadecimal and Base64 Encoding

    HEX(): Converts a string to its hexadecimal representation.

SELECT HEX('fööbar'); -- '66F6F6626172'

TO_BASE64(): Converts a string to Base64 encoding.

    SELECT TO_BASE64('foobar'); -- 'Zm9vYmFy'

Finding and Locating Substrings

    FIND_IN_SET(): Finds the position of a value in a comma-separated list.

SELECT FIND_IN_SET('b','a,b,c'); -- 2 (position of 'b')

LOCATE(): Finds the position of the first occurrence of a substring.

    SELECT LOCATE('bar', 'foobarbaz'); -- 4

Trimming Whitespace

    TRIM(): Removes leading and trailing spaces.

SELECT TRIM('  foo  '); -- 'foo'

LTRIM(): Removes leading spaces.

SELECT LTRIM('  foo'); -- 'foo'

RTRIM(): Removes trailing spaces.

    SELECT RTRIM('foo  '); -- 'foo'

String Concatenation

    CONCAT(): Concatenates strings together.

SELECT CONCAT('foo', 'bar'); -- 'foobar'

CONCAT_WS(): Concatenates strings with a separator.

        SELECT CONCAT_WS('-', '2025', 'May', '16'); -- '2025-May-16'

Useful String Functions

    SUBSTRING_INDEX(): Returns a substring from the string before the specified number of occurrences of the delimiter.

SELECT SUBSTRING_INDEX('apple,banana,orange', ',', 2); -- 'apple,banana'


Date and Time Operations

    Date Arithmetic (Section 21.1)

        MySQL provides useful functions for date arithmetic. For example:

            NOW() + INTERVAL 1 DAY will give the date and time of "tomorrow".

            CURDATE() - INTERVAL 4 DAY gives the date four days ago, at midnight.

        The example query for filtering rows where questions were asked between 180 to 600 minutes ago (3 to 10 hours) is a good illustration of how to use TIMESTAMPDIFF() and INTERVAL to work with date differences.

    SYSDATE(), NOW(), CURDATE() (Section 21.2)

        SYSDATE() and NOW() return the current date and time, and CURDATE() returns the current date (without time).

        These functions help you get the server’s current time, which can be useful when inserting timestamps or performing calculations based on the current time.

    Testing Against Date Ranges (Section 21.3)

        Using BETWEEN for date ranges can be problematic because it is inclusive. The recommended approach is to use:

        WHERE x >= '2016-02-25'
        AND x < '2016-02-25' + INTERVAL 5 DAY

        This prevents issues related to inclusive ranges (like 23:59:59), which could cause unexpected results with DATETIME values that have microsecond precision.

    Extracting Date from DateTime (Section 21.4)

        DATE('2003-12-31 01:02:03') will return just the date part (2003-12-31), which can be useful for extracting the date from DATETIME or TIMESTAMP values.

    Using Index for Date and Time Lookup (Section 21.5)

        It’s more efficient to perform date range queries using conditions like x >= '2016-09-01' AND x < '2016-09-01' + INTERVAL 1 DAY instead of using DATE(x) = '2016-09-01'. Using functions on columns can make index usage inefficient, slowing down your queries.

    Handling Time Zones (Section 22)

        Time zone management is crucial when working with global applications. For example, SET time_zone='Asia/Kolkata'; allows you to work with local time in India, while SET time_zone='UTC'; works with UTC time.

        Converting between time zones using CONVERT_TZ() is vital when you need to display or manipulate timestamps stored in UTC or other time zones.

    Server Time Zone and Configuration (Section 22.4 & 22.5)

        You can retrieve the server's local time zone using SELECT @@time_zone. To get a list of available time zones, you can query the mysql.time_zone_name.name table.

        If you're working with time zone differences and offsets, you can calculate the difference between UTC and the server's time zone using TIMESTAMPDIFF.

Regular Expressions in MySQL
    Basic Regex Patterns

        You can use REGEXP or RLIKE to perform complex pattern matching on string columns:

            ^ to match the start of a string.

            $ to match the end of a string.

            [ABC] to match any character inside the brackets.

            | for "or" conditions in patterns.

        Example queries show how to find employees with first names starting with 'N', phone numbers ending with '4569', etc.

    Counting Matches with Regex

        You can use IF(FIRST_NAME REGEXP '^N', 'matches ^N', 'does not match ^N') to classify each row based on regex matching and then count how many match or don't match.

        A GROUP BY matching clause allows you to group and count occurrences of matching and non-matching rows.

Additional Insights

    MySQL's ability to handle dates and times effectively is very powerful, but it's important to avoid pitfalls like using functions that disable index usage on columns.

    Regular expressions provide a flexible way to search, filter, and manipulate text in MySQL, but they should be used carefully for performance reasons, especially on large datasets.

What is a View?

A view is a stored SQL query that you can reference like a regular table. It doesn't physically store data, but it dynamically retrieves data from one or more tables whenever it is queried. A view can simplify complex queries by abstracting them behind a single query reference.
Creating a View:

To create a view, you use the CREATE VIEW statement. Here's the basic syntax:

CREATE VIEW view_name AS 
SELECT * FROM table_name;

    The view name must be unique within the database, and you cannot create a view with the same name as an existing table in the same database.

    The SELECT statement defines the data that the view will return. This can be as simple or as complex as needed (joins, subqueries, etc.).

Example 1:

Create a view that selects data from a table:

CREATE VIEW v AS 
SELECT qty, price, qty * price AS value 
FROM t;

Here, the view v calculates a value for each row by multiplying qty by price.
Example 2:

Create a view from two tables using a JOIN:

CREATE VIEW myview AS
SELECT a.*, b.extra_data 
FROM main_table a
LEFT JOIN other_table b ON a.id = b.id;

This view pulls in data from two tables, main_table and other_table, and uses a LEFT JOIN to merge the data.
Privileges for Creating Views:

    To create a view, you need the CREATE VIEW privilege.

    Additionally, you need SELECT privilege for each column in the SELECT statement.

    If you use the OR REPLACE clause (to replace an existing view), you need the DROP privilege on the view being replaced.

Restrictions on Views:

    No Subqueries in the FROM Clause (before MySQL 5.7.7): A view’s SELECT statement cannot contain a subquery in the FROM clause.

    No User Variables: You can't use system or user-defined variables in a view’s SELECT statement.

    No Temporary Tables: A view cannot reference a TEMPORARY table, nor can you create a TEMPORARY view.

    No Triggers for Views: Unlike base tables, you cannot assign triggers to a view.

Updating a Table via a View:

    A view can be updated in a manner similar to a table, but there are restrictions:

        If the SELECT query used to define the view is too complex (e.g., involves JOIN, GROUP BY, UNION, etc.), then updates may not be allowed. The database might need to use a temporary table, which makes updating the view impossible.

        Simple views based on a single table and no aggregation can usually be updated directly.

Example:

If you create a view from a single table, you can update it like a regular table:

CREATE VIEW simple_view AS 
SELECT id, name FROM users;

UPDATE simple_view SET name = 'John' WHERE id = 1;

Dropping a View:

To delete a view, use the DROP VIEW command:

DROP VIEW view_name;

You can drop views in the current database or from a different database:

DROP VIEW db_name.view_name;

Example:

CREATE VIEW few_rows_from_t1 AS SELECT * FROM t1 LIMIT 10;
DROP VIEW few_rows_from_t1;

Additional Considerations:

    Materialized vs Virtual Views: In MySQL, views are not materialized, which means the query is re-executed each time the view is referenced. Some other database systems (e.g., Oracle) support materialized views that store the query result physically.

    View with Multiple Tables: A view is often used to simplify queries that involve multiple tables, like with JOIN operations, unions, or subqueries.

Practical Use Cases for Views:

    Simplifying Complex Queries: You can create a view for commonly used queries, so you don’t need to repeat the same JOIN or filtering logic every time.

    Security: Views can be used to expose only a subset of columns from a table, providing an abstraction layer between the end-users and the underlying data structure.

    Data Aggregation: If you're regularly aggregating data (e.g., summing sales data), you can encapsulate the logic in a view.

Example of a View for Reporting:

If you have a sales table with the following columns: product_id, quantity_sold, sale_date, and total_amount, you can create a view to summarize the total sales for each product:

CREATE VIEW sales_summary AS
SELECT product_id, SUM(quantity_sold) AS total_quantity, SUM(total_amount) AS total_sales
FROM sales
GROUP BY product_id;

This sales_summary view allows you to quickly fetch aggregated data for sales reports:

SELECT * FROM sales_summary;


Table Creation Concepts:

    Primary Keys:

        A PRIMARY KEY ensures that each record in a table is unique. You can define it inline or separately.

        Often, an AUTO_INCREMENT column is used as a surrogate key to generate unique values automatically.

    Foreign Keys:

        The FOREIGN KEY constraint is used to establish relationships between tables. It ensures referential integrity by ensuring that a value in the child table exists in the parent table. The data types of the referencing and referenced columns must be compatible.

        Foreign keys are supported in the InnoDB storage engine.

    Storage Engine:

        You can specify the storage engine using the ENGINE clause (e.g., ENGINE=InnoDB).

    Default Values:

        You can assign default values to fields (except for certain data types like BLOB, TEXT, and JSON). For example, if a Country field is not provided during insert, it defaults to "United States".

Altering Tables:

    Changing Storage Engine:

        Use ALTER TABLE table_name ENGINE = InnoDB; to change the storage engine, often used to optimize tables or convert between engines.

    Adding/Removing Columns:

        You can add columns, drop columns, or modify the data type of a column with the ALTER TABLE statement.

        For example, ALTER TABLE stack ADD COLUMN submit DATE; adds a new column to a table.

    Renaming Tables:

        You can rename a table using the RENAME TABLE command or by using ALTER TABLE with the RENAME TO clause.

    Indexes:

        Indexes are essential for optimizing query performance. You can add indexes using ALTER TABLE table_name ADD INDEX index_name(column_name);.

    Changing Auto-Increment Values:

        If needed, you can reset or change the auto-increment value using ALTER TABLE table_name AUTO_INCREMENT = new_value;.

Cloning Tables:

    You can create a new table from an existing one using CREATE TABLE new_table LIKE existing_table;. This will copy the table structure (including indexes).

    You can also create a new table and insert data from another table using a SELECT statement.

TimeStamps:

    The TIMESTAMP field can automatically record the time when a row is updated with DEFAULT CURRENT_TIMESTAMP ON UPDATE CURRENT_TIMESTAMP.

Show Table Structure:

    To view the structure of a table, you can use SHOW CREATE TABLE table_name; or DESCRIBE table_name;.


The DROP TABLE statement in MySQL is used to delete a table from the database permanently. Once a table is dropped, all the data and the table structure are removed, and the operation cannot be undone unless you have a backup.
Basic Syntax

DROP TABLE [IF EXISTS] table_name;

    table_name: The name of the table you want to delete.

    Optional Parameters:

        IF EXISTS: If you specify this, the command will not throw an error if the table does not exist. Without it, an error will be thrown if the table doesn't exist.

        TEMPORARY: This drops only temporary tables.

Basic Example

To delete a table named tbl:

DROP TABLE tbl;

If the table doesn’t exist and you don’t want an error, you can use the IF EXISTS clause:

DROP TABLE IF EXISTS tbl;

Important Notes About DROP TABLE

    Permanent Deletion: Dropping a table will completely delete it, including all of its data, and this action cannot be undone. Be cautious before executing DROP TABLE.

    Temporary Tables: Temporary tables can be dropped the same way, but they only exist for the duration of the session or until the connection is closed.

    Foreign Key Constraints: If a table is referenced by foreign key constraints in other tables, you may need to drop those constraints first before dropping the table.

Dropping Tables from a Specific Database

To drop a table from a different database, use the fully qualified name of the table:

DROP TABLE db_name.table_name;

Example of Creating and Dropping a Table

    Creating a Table:
    Here’s an example of creating a simple table:

CREATE TABLE tbl (
  id INT NOT NULL AUTO_INCREMENT,
  title VARCHAR(100) NOT NULL,
  author VARCHAR(40) NOT NULL,
  submission_date DATE,
  PRIMARY KEY (id)
);

Dropping the Table:
To delete this table:

    DROP TABLE tbl;

Table Locking and Transactions

In MySQL, locks are used to control access to data in the database, especially in concurrent transactions. This section touches upon row-level locking and table locking.
Row-Level Locking (InnoDB)

InnoDB automatically uses row-level locking for transactions. This means that when one transaction updates a row, other transactions can still access other rows in the table. However, if two transactions try to modify the same row simultaneously, one transaction will be forced to wait for the other to finish.

    Example of Row-Level Locking:

        Connection 1:

START TRANSACTION;
SELECT ledgerAmount FROM accDetails WHERE id = 1 FOR UPDATE;

This acquires a lock on the row with id = 1.

Connection 2:

UPDATE accDetails SET ledgerAmount = ledgerAmount + 500 WHERE id = 1;

The update in Connection 2 will wait until Connection 1 commits or rolls back the transaction.

Once Connection 1 commits the transaction:

        COMMIT;

        The lock is released, and Connection 2 can proceed with the update.

MySQL Table Locking

Table locking can be useful, especially when you're working with MyISAM tables or specific scenarios where exclusive access to a table is required. MySQL allows you to lock entire tables for reading or writing to ensure data consistency in concurrent sessions.
Lock Types

    READ LOCK: Allows other sessions to read the table but prevents any writes to it.

    WRITE LOCK: Prevents any other session from reading or writing to the table.

Locking Tables:

    READ Lock:

LOCK TABLES table_name READ;

This allows other sessions to read the table but prevents them from writing to it.

WRITE Lock:

    LOCK TABLES table_name WRITE;

    This locks the table for exclusive access. Other sessions cannot read or write to the table until the lock is released.

Unlocking Tables:

After locking a table, you must explicitly unlock it to allow other sessions to access it:

UNLOCK TABLES;

Example of Using Table Locks

Let's say you want to insert data into a table and ensure no other session can write to it during the operation:

    Acquire a WRITE Lock:

LOCK TABLES products WRITE;

Insert Data:

INSERT INTO products(id, product_name)
SELECT id, old_product_name FROM old_products;

Release the Lock:

    UNLOCK TABLES;

    After unlocking, other sessions can now perform write operations on the products table.

READ Lock Example:

If you only want to prevent writes but allow reads:

LOCK TABLES products READ;

Now, other sessions cannot modify the products table, but they can read from it.
Summary

    Dropping a table is a permanent action that deletes the table and all its data.

    Use DROP TABLE IF EXISTS to avoid errors if the table doesn't exist.

    Row-level locking allows multiple transactions to modify different rows in a table simultaneously without interfering with each other.

    Table-level locks (READ and WRITE) ensure exclusive access or prevent writes, which can be useful for certain operations that require data consistency across multiple sessions.

Error Codes Overview (29.x)
29.1: Error Code 1064: Syntax Error

    This is one of the most common errors, which usually indicates a problem with your SQL query syntax.

    Example:

SELECT LastName, FirstName, 
FROM Person;

The error occurs because there's an extra comma before FROM Person. MySQL is expecting another column after the comma. The error message will typically look like:

    Error Code: 1064. You have an error in your SQL syntax; check the manual that corresponds to your MySQL server version for the right syntax to use near 'from Person' at line 2.

    Tips to fix:

        Always check around the place where the error message points.

        Look for missing or extra commas, mismatched parentheses, or unbalanced quotes.

29.2: Error Code 1175: Safe Update

    Occurs when attempting to update or delete rows without a WHERE clause that uses the KEY column.

    How to disable Safe Update temporarily:

SET SQL_SAFE_UPDATES = 0;

Re-enable Safe Update:

    SET SQL_SAFE_UPDATES = 1;

29.3: Error Code 1215: Cannot Add Foreign Key Constraint

    This error typically happens when a foreign key constraint cannot be applied due to an issue with indexes or data type mismatches.

    Example:

CREATE TABLE someOther (
    id INT(11) NOT NULL AUTO_INCREMENT,
    someDT DATETIME NOT NULL,
    PRIMARY KEY (id),
    CONSTRAINT someOther_dt FOREIGN KEY (someDT) REFERENCES getTogethers (eventDT)
) ENGINE=InnoDB;

The error can occur if the referenced column (eventDT) is not indexed. Fix it by adding the appropriate index.

    CREATE INDEX gt_eventdt ON getTogethers (eventDT);

        Ensure that foreign key columns have the same data types and lengths as the referenced columns.

        For composite keys, ensure that the order of columns matches.

29.4: Error Codes 1067, 1292, 1366, 1411 (Bad Value Errors)

    1067: Usually related to TIMESTAMP defaults.

    1292/1366: Check for data type mismatch like inserting letters into numeric fields, or too far-off dates for DATETIME.

    1411: Might occur with STR_TO_DATE function if the date is incorrectly formatted.

29.5: Error Code 1045: Access Denied

    Common when MySQL user authentication fails. It could be due to wrong password, insufficient privileges, or database access restrictions.

    How to recover: Ensure you're using the correct username/password and check user privileges with GRANT.

29.6: Error Code 1236: "Impossible Position" in Replication

    Happens when the master server crashes before the binary log flushes, causing the slave to lose sync.

    Solution: Run CHANGE MASTER TO POS=0 to reset the replication position to the beginning of the next binary log.

29.7: Error Codes 2002, 2003: Cannot Connect

    These errors can be due to firewall issues or incorrect server settings.

        Check for firewall blocking port 3306 (MySQL’s default port).

        Ensure the MySQL server is running and accessible.

29.8: Error Codes 126, 127, 134, 144, 145 (Corruption Errors)

    Index corruption (126), table crashes (127), and related errors happen due to server crashes or improper shutdowns.

        Use CHECK TABLE <table_name> and REPAIR TABLE <table_name> to attempt a recovery.

29.9: Error Code 139

    Usually means the number and size of the fields exceed some internal limit. Consider adjusting the schema or normalizing the table structure.

29.10: Error Code 1366

    This error is often due to a mismatch in the character set between the client and server. Check that your character_set_client and character_set_server are compatible.

Stored Procedures and Functions (30.x)
30.1: Stored Procedures with IN, OUT, and INOUT Parameters

    IN: Passes a value into the procedure.

    OUT: Returns a value to the caller.

    INOUT: Both passes and receives a value.

Example:

DELIMITER $$

DROP PROCEDURE IF EXISTS sp_nested_loop$$
CREATE PROCEDURE sp_nested_loop(IN i INT, IN j INT, OUT x INT, OUT y INT, INOUT z INT)
BEGIN
    DECLARE a INTEGER DEFAULT 0;
    DECLARE b INTEGER DEFAULT 0;
    DECLARE c INTEGER DEFAULT 0;
    WHILE a < i DO
        WHILE b < j DO
            SET c = c + 1;
            SET b = b + 1;
        END WHILE;
        SET a = a + 1;
        SET b = 0;
    END WHILE;
    SET x = a, y = c;
    SET z = x + y + z;
END $$

DELIMITER ;

Invoke it with:

SET @z = 30;
CALL sp_nested_loop(10, 20, @x, @y, @z);
SELECT @x, @y, @z;

Output:

+------+------+------+
| @x   | @y   | @z   |
+------+------+------+
| 10   | 200  | 240  |
+------+------+------+

30.2: Create a Function

    Functions are similar to stored procedures but return a value.

Simple Function Example:

DELIMITER ||
CREATE FUNCTION functionname() RETURNS INT
BEGIN
    RETURN 12;
END;
||
DELIMITER ;

To execute:

SELECT functionname();

30.3: Cursors

    Cursors allow you to iterate through query results line by line.

Example:

DECLARE student CURSOR FOR SELECT name FROM students;

You can then process each result using FETCH.
30.4: Multiple Result Sets

    Stored Procedures can return multiple result sets, which can be tricky to handle in client-side code (e.g., Perl, PHP).

    This requires different methods for handling multiple sets of results.


-------------------------------------------------------------------------------------------------------------------------

Backup Using mysqldump

mysqldump is a command-line utility used for creating backups of MySQL databases. It creates a text file with SQL statements to recreate the database structure and insert data.
Common Options:

    -h (--host): Specifies the MySQL server host (IP or hostname).

    -u (--user): Specifies the MySQL username.

    -p (--password): Specifies the MySQL password. When using -p, there is no space between -p and the password. It's recommended not to specify the password directly on the command line due to security concerns.

Dump Options:

    --add-drop-database: Adds a DROP DATABASE statement before CREATE DATABASE. Useful when you want to replace an existing database.

    --add-drop-table: Adds a DROP TABLE statement before CREATE TABLE. Useful for replacing existing tables.

    --no-create-db: Omits CREATE DATABASE statements. Useful when the database already exists.

    --no-create-info (-t): Omits CREATE TABLE statements and only dumps the data.

    --no-data (-d): Only dumps CREATE TABLE statements without data. Useful for creating templates.

    --routines (-R): Includes stored procedures and functions in the dump.

    --disable-keys (-K): Disables keys for MyISAM tables temporarily to speed up inserts.

Creating a Backup:

    Entire Database:

mysqldump -u username -p db_name > backup.sql

Multiple Databases:

mysqldump -u username -p --databases db_name1 db_name2 > backup.sql

All Databases:

mysqldump -u username -p --all-databases > backup.sql

Specific Tables:

    mysqldump -u username -p db_name table1 table2 > backup.sql

Restoring a Backup:

To restore from a dump file:

mysql -u username -p db_name < backup.sql

Alternatively, you can use the source command in the MySQL client:

source backup.sql

Transfer Data Between Servers:

You can copy a database between two servers using a dump and restore process:

    Option 1: Dump on source server, copy dump file, and restore on destination server.

    Option 2: Use a pipeline to directly transfer the dump:

    mysqldump -u username -p --host=source_host db_name | mysql -u username -p --host=destination_host db_name

Compression:

To compress the data transfer:

mysqldump -u username -p --compress db_name | gzip > db_name.sql.gz

To restore from a compressed dump:

gunzip -c db_name.sql.gz | mysql -u username -p db_name

Backup Directly to Amazon S3:

You can dump a MySQL database directly to an S3 bucket using compression:

mysqldump -u root -p --all-databases | gzip -9 | s3cmd put - s3://bucket-name/db-backup.sql.gz

Data Import Using mysqlimport

mysqlimport is a utility for loading data into MySQL tables from a text file, typically in CSV or TSV format.
Basic Usage:

To import a file into a database:

mysqlimport --user=username --password=password mycompany employee.txt

Custom Field Delimiter:

For a file with a custom field delimiter (e.g., pipe |):

mysqlimport --fields-terminated-by='|' --user=username --password=password mycompany employee.txt

Custom Row Delimiter:

For files with a custom row delimiter (e.g., Windows-style \r\n line endings):

mysqlimport --lines-terminated-by='\r\n' --user=username --password=password mycompany employee.txt

Handling Duplicate Keys:

If your table has duplicate keys and you want to handle them:

    --replace: Overwrites existing rows with the same unique key.

    --ignore: Ignores rows with duplicate keys.

For example, to ignore duplicates:

mysqlimport --replace --user=username --password=password mycompany employee.txt


Using LOAD DATA INFILE to Load Large Amounts of Data into MySQL

The LOAD DATA INFILE statement is an efficient way to load large datasets into a MySQL table, particularly when you're dealing with CSV or text files. Here's a breakdown of how to handle this process, including some variations based on data formats and error handling.
1. Basic Example:

Let’s say you have a semicolon-delimited CSV file (file.txt) with data such as:

1;max;male;manager;12-7-1985
2;jack;male;executive;21-8-1990
...
1000000;marta;female;accountant;15-6-1992

You would first create a table in MySQL to hold this data:

CREATE TABLE `employee` (
  `id` INT NOT NULL,
  `name` VARCHAR(100) NOT NULL,
  `sex` VARCHAR(10) NOT NULL,
  `designation` VARCHAR(50) NOT NULL,
  `dob` VARCHAR(20) NOT NULL
);

To load this CSV file into the employee table, you use the following query:

LOAD DATA INFILE 'path/to/your/file.txt'
INTO TABLE employee
FIELDS TERMINATED BY ';'  -- Specify the delimiter separating values
LINES TERMINATED BY '\r\n' -- Define line terminator for Windows-style files
(id, name, sex, designation, dob);

This command will load the data from the file into the MySQL table with the specified field delimiter (;) and line terminator (\r\n).
2. Handling Non-Standard Date Formats:

If your date format is non-standard (for example, the month is written as a three-letter abbreviation, e.g., "17-Jan-1985"), you can use STR_TO_DATE to convert it during the load process. Here's how to handle the date format 17-Jan-1985:

LOAD DATA INFILE 'path/to/your/file.txt'
INTO TABLE employee
FIELDS TERMINATED BY ';'
LINES TERMINATED BY '\r\n'
(id, name, sex, designation, @dob)
SET dob = STR_TO_DATE(@dob, '%d-%b-%Y');

    @dob is a user-defined variable used to temporarily store the date value as it is read from the file.

    The STR_TO_DATE function converts the string date into MySQL’s DATE format (YYYY-MM-DD).

Section 52.2: Handling Duplicates During LOAD DATA INFILE

When using LOAD DATA INFILE, it's common to encounter duplicate entries, especially when the data you're importing already exists in the table. There are several strategies to handle duplicates:
1. Using LOAD DATA LOCAL:

If you need to load data from a local file (on the client machine), use LOCAL. Also, it can be useful for ignoring duplicates in the process.

LOAD DATA LOCAL INFILE 'path/to/your/file.txt'
INTO TABLE employee
FIELDS TERMINATED BY ';'
LINES TERMINATED BY '\r\n';

The LOCAL keyword can be helpful if your file is on the client rather than the server. However, you’ll need to ensure that LOAD DATA LOCAL is enabled on your MySQL server.
2. Using REPLACE:

If you want to replace existing rows with the same unique key, use the REPLACE keyword. This will overwrite existing rows that have the same primary or unique key.

LOAD DATA INFILE 'path/to/your/file.txt'
REPLACE INTO TABLE employee
FIELDS TERMINATED BY ';'
LINES TERMINATED BY '\r\n';

3. Using IGNORE:

If you want to ignore rows that would cause duplicates (i.e., keep existing rows but don’t insert the new ones), use the IGNORE keyword.

LOAD DATA INFILE 'path/to/your/file.txt'
IGNORE INTO TABLE employee
FIELDS TERMINATED BY ';'
LINES TERMINATED BY '\r\n';

This will ignore rows where there are duplicate unique key violations and leave the existing rows in place.
4. Using an Intermediary Table:

In some cases, ignoring or replacing duplicates might not be the best solution, especially if decisions need to be made based on other columns in the table. A common approach is to load the data into an intermediary table first and then process it.

CREATE TEMPORARY TABLE temp_employee LIKE employee;
LOAD DATA INFILE 'path/to/your/file.txt'
INTO TABLE temp_employee
FIELDS TERMINATED BY ';'
LINES TERMINATED BY '\r\n';

-- Insert non-duplicate rows from temp_employee into employee
INSERT INTO employee (id, name, sex, designation, dob)
SELECT id, name, sex, designation, dob FROM temp_employee
WHERE NOT EXISTS (
    SELECT 1 FROM employee WHERE employee.id = temp_employee.id
);

This approach gives you full control over how duplicates are handled before transferring data into the main table.
Section 52.3: Import a CSV File with Quoting and Escaping

When importing CSV files with quotes and escape characters, use OPTIONALLY ENCLOSED BY and ESCAPED BY to handle special characters like commas within quoted strings:

LOAD DATA INFILE '/tmp/file.csv'
INTO TABLE my_table
FIELDS TERMINATED BY ','
OPTIONALLY ENCLOSED BY '"'
ESCAPED BY '"'
LINES TERMINATED BY '\n'
IGNORE 1 LINES;  -- Skip the header row

This allows the import of CSV files where fields may contain commas or other special characters inside quotes. The IGNORE 1 LINES will skip the header row of the CSV file.
Section 53.1: Union Operator

The UNION operator is used to combine results from two or more SELECT queries while removing duplicates. Here's an example:

SELECT City FROM Customers
UNION
SELECT City FROM Suppliers
ORDER BY City;

This query will return distinct cities from both the Customers and Suppliers tables, sorted by city.
Section 53.2: Union ALL

If you want to include duplicate records in your result set, use UNION ALL. It includes all rows, even if there are duplicates:

SELECT City FROM Customers
UNION ALL
SELECT City FROM Suppliers
ORDER BY City;

Section 53.3: Union ALL with WHERE Clause

You can also filter results with a WHERE clause while using UNION ALL. Here’s an example that selects only German cities:

SELECT City, Country FROM Customers WHERE Country='Germany'
UNION ALL
SELECT City, Country FROM Suppliers WHERE Country='Germany'
ORDER BY City;

This will return all German cities from both Customers and Suppliers, including duplicates.
Section 54: MySQL Client Commands

The MySQL client allows for various parameters to control how it connects to the database and how commands are executed. Here’s a summary:

    -u --user=name: Username for MySQL login.

    -p --password=name: Password for MySQL login (without space).

    -e --execute='command': Execute SQL commands from the command line.

    --delimiter=str: Specify the statement delimiter.

    -s --silent: Use silent mode, reducing output verbosity.

    -S --socket=path: Specify the socket for local connections.

    -D --database=name: Select the database to use.

Section 55: Temporary Tables

Temporary tables are used to store data that only needs to exist during the current session. These tables are automatically dropped when the session ends or can be manually dropped.
1. Create Temporary Table:

CREATE TEMPORARY TABLE tempTable1 (
  id INT NOT NULL AUTO_INCREMENT,
  title VARCHAR(100) NOT NULL,
  PRIMARY KEY (id)
);

2. Create Temporary Table from Query:

CREATE TEMPORARY TABLE tempTable1
SELECT ColumnName1, ColumnName2 FROM table1;

3. Drop Temporary Table:

DROP TEMPORARY TABLE IF EXISTS tempTable1;

Section 56: Customize PS1 for MySQL Prompt

You can customize your MySQL prompt (PS1) for easier interaction.
1. Customize in .bashrc:

export MYSQL_PS1="\u@\h [\d]>"

This will show the current user, host, and database in the prompt.
2. Customize via MySQL Configuration File:

In mysqld.cnf, add:

[mysql]
prompt = '\u@\h [\d]> '

This will configure the prompt without needing to modify .bashrc.
Conclusion

    LOAD DATA INFILE: A powerful tool for importing large datasets into MySQL. Handle issues like duplicate records and custom date formats with various options like REPLACE, IGNORE, and STR_TO_DATE.

    UNION and UNION ALL: Combine query results from multiple SELECT statements. Use UNION for distinct values and UNION ALL for all values, including duplicates.

    Temporary Tables: Useful for intermediate data processing during a session. They are automatically dropped when the session ends.

Working with Columns Containing NULL Values

NULL values in SQL have special properties, and understanding how to handle them is crucial when querying a database. Let's break down the situation and see how NULLs behave in MySQL.
1. Basic Handling of NULL Values:

In the provided example, if we query a table where the end_date column contains NULL values, we might want to retrieve rows where the end_date is either after a certain date or NULL (indicating that the employee is still working at the company). Consider the following table:

CREATE TABLE example
(`applicant_id` INT, `company_name` VARCHAR(255), `end_date` DATE);

And data like:
applicant_id    company_name    end_date
1   Google  NULL
1   Initech 2013-01-31
2   Woodworking.com 2016-08-25
2   NY Times    2013-11-10
3   NFL.com 2014-04-13

Now, when we try the following query:

SELECT * FROM example WHERE end_date > '2016-01-01';

It will not return rows with NULL values in the end_date column because comparisons with NULL (like >, <, =) return NULL, not a boolean TRUE or FALSE.

To solve this, we can explicitly check for NULL using IS NULL:

SELECT * FROM example WHERE end_date > '2016-01-01' OR end_date IS NULL;

This would return:
applicant_id    company_name    end_date
1   Google  NULL
2   Woodworking.com 2016-08-25
2. Aggregation and NULLs:

When aggregating data, handling NULL values can get tricky. For example, if you want to find the most recent end date for each applicant_id, you might try:

SELECT applicant_id, MAX(end_date) FROM example GROUP BY applicant_id;

The result might look like this:
applicant_id    MAX(end_date)
1   2013-01-31
2   2016-08-25
3   2014-04-13

But applicant 1 should show 'present' because they are still employed (i.e., end_date is NULL). To handle this, you can use a CASE statement:

SELECT
  applicant_id,
  CASE WHEN MAX(end_date IS NULL) = 1 THEN 'present' ELSE MAX(end_date) END AS max_date
FROM example
GROUP BY applicant_id;

The result will be:
applicant_id    max_date
1   present
2   2016-08-25
3   2014-04-13
3. Join with Original Table:

If you want to find out which company each applicant is currently working at, you can join this result with the original table. Here's how you could do it:

SELECT
  data.applicant_id,
  data.company_name,
  data.max_date
FROM (
  SELECT
    *,
    CASE WHEN end_date IS NULL THEN 'present' ELSE end_date END AS max_date
  FROM example
) data
INNER JOIN (
  SELECT
    applicant_id,
    CASE WHEN MAX(end_date IS NULL) = 1 THEN 'present' ELSE MAX(end_date) END AS max_date
  FROM example
  GROUP BY applicant_id
) j
ON data.applicant_id = j.applicant_id AND data.max_date = j.max_date;

This query will give you the following result:
applicant_id    company_name    max_date
1   Google  present
2   Woodworking.com 2016-08-25
3   NFL.com 2014-04-13

This works by first marking employees as 'present' if their end_date is NULL, then performing the join to get the last company they worked at.
Key Takeaways for Working with NULLs:

    NULL values can't be compared directly using comparison operators (>, <, =). Use IS NULL for checking null values.

    Aggregations: Functions like MAX(), MIN(), and SUM() will ignore NULL values unless specifically handled (e.g., using CASE WHEN).

    Joins with NULL values: When working with NULL values, you might need to use CASE WHEN to replace NULL with a meaningful value like 'present' when doing joins or aggregations.

Section 58.1: UTF-8 Encoding in Python

When connecting to MySQL using Python, ensure that you set the correct encoding, especially if you're working with non-ASCII characters. Here’s how you can set it up:
1. Source File Encoding:

Make sure your Python source code file is UTF-8 encoded:

# -*- coding: utf-8 -*-

2. Database Connection:

When connecting to MySQL, specify the charset="utf8mb4" to ensure proper handling of UTF-8 characters:

import MySQLdb

db = MySQLdb.connect(host=DB_HOST, user=DB_USER, passwd=DB_PASS, db=DB_NAME, charset="utf8mb4", use_unicode=True)

This will ensure that both your Python script and MySQL are communicating using the correct encoding, which is crucial when dealing with characters from different languages.
Section 58.2: UTF-8 Encoding in PHP

Similarly, when working with PHP, you need to ensure that your application uses UTF-8 for proper character encoding.
1. php.ini Configuration:

Ensure that the default_charset is set to UTF-8 in your php.ini:

default_charset = UTF-8

2. Web Page Encoding:

In the HTML header of your page, ensure that the charset is set to UTF-8:

<meta charset="utf-8" />

3. Connecting to MySQL:

When using MySQL, ensure that you're using the right API. Avoid the deprecated mysql_* functions, and use either mysqli or PDO with utf8mb4:

    mysqli:

$mysqli_obj->set_charset('utf8mb4');

    PDO:

$db = new PDO('mysql:host=host;dbname=db;charset=utf8mb4', $user, $pwd);

This ensures your connection can handle all Unicode characters correctly.
4. Form Encoding:

When creating forms, ensure that the form data is submitted as UTF-8:

<form accept-charset="UTF-8">

5. JSON Encoding:

When working with JSON in PHP, ensure that it's properly encoded without escaping Unicode characters:

$t = json_encode($s, JSON_UNESCAPED_UNICODE);

This avoids encoding characters like \uxxxx and keeps the data in its original form.
Conclusion:

    Handling NULL values: Always consider NULL separately, as direct comparisons may not work. Use IS NULL for checks, and CASE WHEN for aggregations.

    UTF-8 Encoding: Ensure all parts of your application (Python, PHP, HTML, MySQL) are configured to use utf8mb4 or UTF-8 to properly handle non-ASCII characters.

Time with subsecond precision:
Get the current time with millisecond precision
mysql> SELECT NOW(3);
+-------------------------+
| NOW(3)                  |
+-------------------------+
| 2025-05-14 16:08:31.431 |
+-------------------------+

Get the current time in a form that looks like a Javascript timestamp:
Javascript timestamps are based on the venerable UNIX time_t data type, and show the number of milliseconds
since 1970-01-01 00:00:00 UTC.

This expression gets the current time as a Javascript timestamp integer. (It does so correctly regardless of the
current time_zone setting.)
ROUND(UNIX_TIMESTAMP(NOW(3)) * 1000.0, 0)

SELECT ROUND(UNIX_TIMESTAMP(NOW(3)) * 1000.0, 0);
+-------------------------------------------+
| ROUND(UNIX_TIMESTAMP(NOW(3)) * 1000.0, 0) |
+-------------------------------------------+
|                             1747219327447 |
+-------------------------------------------+

If you have TIMESTAMP values stored in a column, you can retrieve them as integer Javascript timestamps using the
UNIX_TIMESTAMP() function.
SELECT ROUND(UNIX_TIMESTAMP(column) * 1000.0, 0)

If your column contains DATETIME columns and you retrieve them as Javascript timestamps, those timestamps will
be offset by the time zone offset of the time zone they're stored in.

Create a table with columns to store sub-second time:

CREATE TABLE times(dt DATETIME(3),ts TIMESTAMP(3));
Query OK, 0 rows affected (0.03 sec)

mysql> INSERT INTO times VALUES (NOW(3),NOW(3));
Query OK, 1 row affected (0.02 sec)

mysql> SELECT * FROM times;
+-------------------------+-------------------------+
| dt                      | ts                      |
+-------------------------+-------------------------+
| 2025-05-14 16:17:41.775 | 2025-05-14 16:17:41.775 |
+-------------------------+-------------------------+

inserts a row containing NOW() values with millisecond precision into the table.

INSERT INTO times VALUES ('2015-01-01 16:34:00.123','2015-01-01 16:34:00.128');
inserts specific millisecond precision values.

Notice that you must use NOW(3) rather than NOW() if you use that function to insert high-precision time values.

Convert a millisecond-precision date / time value to text:
We can change the format of the date as per the requirement.
SELECT DATE_FORMAT(NOW(3), '%Y-%m-%d %H:%i:%s.%f')
+---------------------------------------------+
| DATE_FORMAT(NOW(3), '%Y-%m-%d %H:%i:%s.%f') |
+---------------------------------------------+
| 2025-05-14 16:29:02.178000                  |
+---------------------------------------------+

Store a Javascript timestamp into a TIMESTAMP column:
🔢 What is a "JavaScript timestamp"?

In JavaScript, the standard timestamp is:

    Milliseconds since the Unix Epoch (Jan 1, 1970 UTC)

So:

Date.now(); // → 1478960868932

This means 1,478,960,868,932 milliseconds since the epoch.
🕓 What does MySQL's FROM_UNIXTIME() expect?

In MySQL:

    FROM_UNIXTIME() expects seconds, not milliseconds.

    But it can accept fractional seconds as a decimal — e.g., .893 means 893 milliseconds.

So to convert:

JavaScript milliseconds → MySQL seconds (with fractional part)

You must divide by 1000, which is the same as multiplying by 0.001.
✅ Example:

SELECT FROM_UNIXTIME(1478960868932 * 0.001);
+--------------------------------------+
| FROM_UNIXTIME(1478960868932 * 0.001) |
+--------------------------------------+
| 2016-11-12 19:57:48.932              |
+--------------------------------------+

🔍 Why this is needed:

If you don’t divide:

SELECT FROM_UNIXTIME(1478960868932);
+------------------------------+
| FROM_UNIXTIME(1478960868932) |
+------------------------------+
| NULL                         |
+------------------------------+

-- Output: NULL or incorrect, because it's out of valid range

MySQL thinks 1478960868932 is 1.47 trillion seconds, which is over 46,000 years in the future — way outside its valid datetime range.
✅ Summary:
JavaScript Timestamp                     Unit            Example
1478960868932                          Milliseconds    JavaScript output
1478960868.932                           Seconds       What MySQL needs
1478960868932 * 0.001                   Conversion      Works correctly

So, multiplying by 0.001 converts milliseconds → seconds with fractional precision, which FROM_UNIXTIME() can parse.

ONE TO MANY(1:M):
Consider a company where every employee who is a manager, manages 1 or more employees, and every employee
has only 1 manager.

CREATE TABLE EMPLOYEES(
emp_id VARCHAR(5),
first_name VARCHAR(5),
last_name VARCHAR(10),
mgr_id VARCHAR(5)
);

INSERT INTO EMPLOYEES VALUES('E01','Jonny','Apple','M02'),('E02','Erin','Mackle','M01'),('E03','Colby','Paper','M03'),('E04','Ron','Son','M01');

 SELECT * FROM EMPLOYEES;
+--------+------------+-----------+--------+
| emp_id | first_name | last_name | mgr_id |
+--------+------------+-----------+--------+
| E01    | Jonny      | Apple     | M02    |
| E02    | Erin       | Mackle    | M01    |
| E03    | Colby      | Paper     | M03    |
| E04    | Ron        | Son       | M01    |
+--------+------------+-----------+--------+

CREATE TABLE MANAGERS(
mgr_id VARCHAR(5),
first_name VARCHAR(5),
last_name VARCHAR(10)
);

INSERT INTO MANAGERS VALUES('M01','Loud','Queen'),('M02','Bossy','Pants'),('M03','Barry','Jones');

SELECT * FROM MANAGERS;
+--------+------------+-----------+
| mgr_id | first_name | last_name |
+--------+------------+-----------+
| M01    | Loud       | Queen     |
| M02    | Bossy      | Pants     |
| M03    | Barry      | Jones     |
+--------+------------+-----------+

Selecting employees who were under same manager:
SELECT e.emp_id,e.first_name,e.last_name 
FROM EMPLOYEES e 
INNER JOIN MANAGERS m ON m.mgr_id=e.mgr_id 
WHERE m.mgr_id='M01';
+--------+------------+-----------+
| emp_id | first_name | last_name |
+--------+------------+-----------+
| E02    | Erin       | Mackle    |
| E04    | Ron        | Son       |
+--------+------------+-----------+

Getting the manager for a single employee:
SELECT m.mgr_id,m.first_name,m.last_name 
FROM MANAGERS m 
INNER JOIN EMPLOYEES e ON e.mgr_id=m.mgr_id 
WHERE e.emp_id='E03';
+--------+------------+-----------+
| mgr_id | first_name | last_name |
+--------+------------+-----------+
| M03    | Barry      | Jones     |
+--------+------------+-----------+

SERVER INFO:
Parameters    Explanation
GLOBAL        Shows the variables as they are configured for the entire server.
SESSION       Shows the variables that are configured for this session only. 

SHOW VARIABLE;
will get you all the in-built variables.

SHOW SESSION VARIABLES;
will get session variables

SHOW GLOBAL VARIABLES;
will get global variables

SHOW GLOBAL VARIABLES LIKE 'max_join_size';
+---------------+----------------------+
| Variable_name | Value                |
+---------------+----------------------+
| max_join_size | 18446744073709551615 |
+---------------+----------------------+

mysql> SHOW SESSION VARIABLES LIKE 'max_join_size';
+---------------+----------------------+
| Variable_name | Value                |
+---------------+----------------------+
| max_join_size | 18446744073709551615 |
+---------------+----------------------+

Or, using wildcards:
SHOW [GLOBAL | SESSION] VARIABLES LIKE '%size%';
You can also filter the results of the SHOW query using a WHERE parameter as follows:
SHOW [GLOBAL | SESSION] VARIABLES WHERE VALUE > 0;

SHOW STATUS;
will get the status of the database server

SHOW [GLOBAL|SESSION] STATUS;

SSL Connection Setup:
Setup for Debian-based systems
(This assumes MySQL has been installed and that sudo is being used.)
Generating a CA and SSL keys

Make sure OpenSSL and libraries are installed:
apt-get -y install openssl
apt-get -y install libssl-dev

Next make and enter a directory for the SSL files:
mkdir /home/ubuntu/mysqlcerts
cd /home/ubuntu/mysqlcerts

To generate keys, create a certificate authority (CA) to sign the keys (self-signed):
openssl genrsa 2048 > ca-key.pem
openssl req -new -x509 -nodes -days 3600 -key ca-key.pem -out ca.pem

The values entered at each prompt won't affect the configuration. Next create a key for the server, and sign using
the CA from before:
openssl req -newkey rsa:2048 -days 3600 -nodes -keyout server-key.pem -out server-req.pem
openssl rsa -in server-key.pem -out server-key.pem
openssl x509 -req -in server-req.pem -days 3600 -CA ca.pem -CAkey ca-key.pem -set_serial 01 -out
server-cert.pem

Then create a key for a client:
openssl req -newkey rsa:2048 -days 3600 -nodes -keyout client-key.pem -out client-req.pem
openssl rsa -in client-key.pem -out client-key.pem
openssl x509 -req -in client-req.pem -days 3600 -CA ca.pem -CAkey ca-key.pem -set_serial 01 -out
client-cert.pem

To make sure everything was set up correctly, verify the keys:
openssl verify -CAfile ca.pem server-cert.pem client-cert.pem

Adding the keys to MySQL
Open the MySQL configuration file. For example:
vim /etc/mysql/mysql.conf.d/mysqld.cnf
Under the [mysqld] section, add the following options:
ssl-ca = /home/ubuntu/mysqlcerts/ca.pem
ssl-cert = /home/ubuntu/mysqlcerts/server-cert.pem
ssl-key = /home/ubuntu/mysqlcerts/server-key.pem

Restart MySQL. For example:
service mysql restart

Test the SSL connection
Connect in the same way, passing in the extra options ssl-ca, ssl-cert, and ssl-key, using the generated client
key. For example, assuming cd /home/ubuntu/mysqlcerts:
mysql --ssl-ca=ca.pem --ssl-cert=client-cert.pem --ssl-key=client-key.pem -h 127.0.0.1 -u superman
-p
After logging in, verify the connection is indeed secure:
superman@127.0.0.1 [None]> SHOW VARIABLES LIKE '%ssl%';
+---------------+-----------------------------------------+
| Variable_name | Value |
+---------------+-----------------------------------------+
| have_openssl | YES |
| have_ssl | YES |
| ssl_ca | /home/ubuntu/mysqlcerts/ca.pem |
| ssl_capath | |
| ssl_cert | /home/ubuntu/mysqlcerts/server-cert.pem |
| ssl_cipher | |
| ssl_crl | |
| ssl_crlpath | |
| ssl_key | /home/ubuntu/mysqlcerts/server-key.pem |
+---------------+-----------------------------------------+
You could also check:
superman@127.0.0.1 [None]> STATUS;
...
SSL: Cipher in use is DHE-RSA-AES256-SHA
...
Enforcing SSL
This is via GRANT, using REQUIRE SSL:
GRANT ALL PRIVILEGES ON *.* TO 'superman'@'127.0.0.1' IDENTIFIED BY 'pass' REQUIRE SSL;
FLUSH PRIVILEGES;
Now, superman must connect via SSL.
If you don't want to manage client keys, use the client key from earlier and automatically use that for all clients.
Open MySQL configuration file, for example:
vim /etc/mysql/mysql.conf.d/mysqld.cnf
Under the [client] section, add the following options:
ssl-ca = /home/ubuntu/mysqlcerts/ca.pem
ssl-cert = /home/ubuntu/mysqlcerts/client-cert.pem
ssl-key = /home/ubuntu/mysqlcerts/client-key.pem
Now superman only has to type the following to login via SSL:
GoalKicker.com – MySQL® Notes for Professionals 168
mysql -h 127.0.0.1 -u superman -p
Connecting from another program, for example in Python, typically only requires an additional parameter to the
connect function. A Python example:
import MySQLdb
ssl = {'cert': '/home/ubuntu/mysqlcerts/client-cert.pem', 'key': '/home/ubuntu/mysqlcerts/client-
key.pem'}
conn = MySQLdb.connect(host='127.0.0.1', user='superman', passwd='imsoawesome', ssl=ssl)

Create New User:
Create a MySQL User
For creating new user, We need to follow simple steps as below :
Step 1: Login to MySQL as root
$ mysql -u root -p

Step 2 : We will see mysql command prompt
mysql> CREATE USER 'my_new_user'@'localhost' IDENTIFIED BY 'test_password';

Here, We have successfully created new user, But this user won't have any permissions, So to assign permissions
to user use following command :
mysql> GRANT ALL PRIVILEGES ON my_db.* TO 'my_new_user'@'localhost' identified by 'my_password';

Specify the password:
The basic usage is:
mysql> CREATE USER 'my_new_user'@'localhost' IDENTIFIED BY 'test_password';

However for situations where is not advisable to hard-code the password in cleartext it is also possible to specify
directly, using the directive PASSWORD, the hashed value as returned by the PASSWORD() function:

mysql> select PASSWORD('test_password'); -- returns *4414E26EDED6D661B5386813EBBA95065DBC4728
mysql> CREATE USER 'my_new_user'@'localhost' IDENTIFIED BY PASSWORD
'*4414E26EDED6D661B5386813EBBA95065DBC4728';

Create new user and grant all priviliges to schema:
grant all privileges on schema_name.* to 'new_user_name'@'%' identified by 'newpassword';
Attention: This can be used to create new root user

Renaming user:
rename user 'user'@'%' to 'new_name`@'%';
If you create a user by mistake, you can change his name

Security via GRANTs
Best Practice
Limit root (and any other SUPER-privileged user) to

GRANT ... TO root@localhost ...

That prevents access from other servers. You should hand out SUPER to very few people, and they should be aware
of their responsibility. The application should not have SUPER.

Limit application logins to the one database it uses:
GRANT ... ON dbname.* ...

That way, someone who hacks into the application code can't get past dbname. This can be further refined via either of these:

GRANT SELECT ON dname.* ... -- "read only"
GRANT ... ON dname.tblname ... -- "just one table"

The readonly may also need 'safe' things like
GRANT SELECT, CREATE TEMPORARY TABLE ON dname.* ... -- "read only"

As you say, there is no absolute security. My point here is there you can do a few things to slow hackers down.
(Same goes for honest people goofing.)
In rare cases, you may need the application to do something available only to root. this can be done via a "Stored Procedure" that has SECURITY DEFINER (and root defines it). That will expose only what the SP does, which might,for example, be one particular action on one particular table.

Host (of user@host)
The "host" can be either a host name or an IP address. Also, it can involve wild cards.

GRANT SELECT ON db.* TO sam@'my.domain.com' IDENTIFIED BY 'foo';

Examples: Note: these usually need to be quoted
localhost -- the same machine as mysqld
'my.domain.com' -- a specific domain; this involves a lookup
'11.22.33.44' -- a specific IP address
'192.168.1.%' -- wild card for trailing part of IP address. (192.168.% and 10.% and 11.% are "internal" ip addresses.)

Using localhost relies on the security of the server. For best practice root should only be allowed in through localhost. In some cases, these mean the same thing: 0.0.0.1 and ::1.

Change Password
Change MySQL root password in Linux
To change MySQL's root user password:

Step 1: Stop the MySQL server.

in Ubuntu or Debian:
sudo /etc/init.d/mysql stop

in CentOS, Fedora or Red Hat Enterprise Linux:
sudo /etc/init.d/mysqld stop

Step 2: Start the MySQL server without the privilege system.

sudo mysqld_safe --skip-grant-tables &
or, if mysqld_safe is unavailable,
sudo mysqld --skip-grant-tables &

Step 3: Connect to the MySQL server.

mysql -u root

Step 4: Set a new password for root user.

Version > 5.7
FLUSH PRIVILEGES;
ALTER USER 'root'@'localhost' IDENTIFIED BY 'new_password';
FLUSH PRIVILEGES;
exit;

Version ≤ 5.7
FLUSH PRIVILEGES;
SET PASSWORD FOR 'root'@'localhost' = PASSWORD('new_password');
FLUSH PRIVILEGES;
exit;

Note: The ALTER USER syntax was introduced in MySQL 5.7.6.

Step 5: Restart the MySQL server.

in Ubuntu or Debian:
sudo /etc/init.d/mysql stop
sudo /etc/init.d/mysql start
in CentOS, Fedora or Red Hat Enterprise Linux:
sudo /etc/init.d/mysqld stop
sudo /etc/init.d/mysqld start

Change MySQL root password in Windows

When we want to change root password in windows, We need to follow following steps :
Step 1 : Start your Command Prompt by using any of below method :
Press Crtl+R or Goto Start Menu > Run and then type cmd and hit enter

Step 2 : Change your directory to where MYSQL is installed, In my case it's
C:\> cd C:\mysql\bin

Step 3 : Now we need to start mysql command prompt
C:\mysql\bin> mysql -u root mysql

Step 4 : Fire query to change root password
mysql> SET PASSWORD FOR root@localhost=PASSWORD('my_new_password');

Process
1.Stop the MySQL (mysqld) server/daemon process.
2.Start the MySQL server process the --skip-grant-tables option so that it will not prompt for a password:
mysqld_safe --skip-grant-tables &
3.Connect to the MySQL server as the root user: mysql -u root.
4.Change password:.
(5.7.6 and newer): ALTER USER 'root'@'localhost' IDENTIFIED BY 'new-password';
(5.7.5 and older, or MariaDB): SET PASSWORD FOR 'root'@'localhost' = PASSWORD('new-password); flush
privileges; quit;
5.Restart the MySQL server.

Note: this will work only if you are physically on the same server.

Recover and reset the default root password for MySQL 5.7+:

After MySQL 5.7, when we install MySQL sometimes we don't need to create a root account or give a root password.By default when we start the server, the default password is stored in the mysqld.log file. We need to login in to the system using that password and we need to change it.

What happens when the initial start up of the server
Given that the data directory of the server is empty:
-->The server is initialized.
-->SSL certificate and key files are generated in the data directory.
-->The validate_password plugin is installed and enabled.
-->The superuser account 'root'@'localhost' is created. The password for the superuser is set and stored in the error log file.

How to change the root password by using the default password:

To reveal the default "root" password:

shell> sudo grep 'temporary password' /var/log/mysqld.log

Change the root password as soon as possible by logging in with the generated temporary password and set a custom password for the superuser account:

shell> mysql -uroot -p

mysql> ALTER USER 'root'@'localhost' IDENTIFIED BY 'MyNewPass5!';

Note: MySQL's validate_password plugin is installed by default. This will require that passwords contain at least one upper case letter, one lower case letter, one digit, and one special character, and that the total password length is at least 8 characters.

reset root password when " /var/run/mysqld' for UNIX socket file don't exists":

if I forget the password then I'll get error.

$ mysql -u root -p

Enter password:

ERROR 1045 (28000): Access denied for user 'root'@'localhost' (using password: YES)

I tried to solve the issue by first knowing the status:
$ systemctl status mysql.service

mysql.service - MySQL Community Server Loaded: loaded (/lib/systemd/system/mysql.service; enabled; vendor preset: en Active: active (running) since Thu 2017-06-08 14:31:33 IST; 38s ago

Then I used the code mysqld_safe --skip-grant-tables & but I get the error:

mysqld_safe Directory '/var/run/mysqld' for UNIX socket file don't exists.

$ systemctl stop mysql.service
$ ps -eaf|grep mysql
$ mysqld_safe --skip-grant-tables &

I solved:

$ mkdir -p /var/run/mysqld
$ chown mysql:mysql /var/run/mysqld

Now I use the same code mysqld_safe --skip-grant-tables & and get

mysqld_safe Starting mysqld daemon with databases from /var/lib/mysql

If I use $ mysql -u root I'll get :

Server version: 5.7.18-0ubuntu0.16.04.1 (Ubuntu)
Copyright (c) 2000, 2017, Oracle and/or its affiliates. All rights reserved.
Oracle is a registered trademark of Oracle Corporation and/or its affiliates. Other names may be trademarks of
their respective owners.
Type 'help;' or '\h' for help. Type '\c' to clear the current input statement.
mysql>

Now time to change password:

mysql> use mysql
mysql> describe user;

Reading table information for completion of table and column names You can turn off this feature to get a quicker startup with -A

Database changed

mysql> FLUSH PRIVILEGES;
mysql> SET PASSWORD FOR root@'localhost' = PASSWORD('newpwd');

or If you have a mysql root account that can connect from everywhere, you should also do:

UPDATE mysql.user SET Password=PASSWORD('newpwd') WHERE User='root';

Alternate Method:

USE mysql
UPDATE user SET Password = PASSWORD('newpwd')
WHERE Host = 'localhost' AND User = 'root';

And if you have a root account that can access from everywhere:

USE mysql
UPDATE user SET Password = PASSWORD('newpwd')
WHERE Host = '%' AND User = 'root';`enter code here

now need to quit from mysql and stop/start

FLUSH PRIVILEGES;
sudo /etc/init.d/mysql stop
sudo /etc/init.d/mysql start

now again ` mysql -u root -p' and use the new password to get

mysql>

Recover from lost root password:
Set root password, enable root user for socket and http access

Solves problem of: access denied for user root using password YES Stop mySQL:

sudo systemctl stop mysql

Restart mySQL, skipping grant tables:

sudo mysqld_safe --skip-grant-tables

Login:
mysql -u root

In SQL shell, look if users exist:

select User, password,plugin FROM mysql.user ;

Update the users (plugin null enables for all plugins):

update mysql.user set password=PASSWORD('mypassword'), plugin = NULL WHERE User = 'root';
exit;

In Unix shell stop mySQL without grant tables, then restart with grant tables:

sudo service mysql stop
sudo service mysql start


Performance Tips:
Building a Composite Index:
When creating a composite index (an index on multiple columns), it can improve performance over using individual indexes on each column. To create the best composite index, you should prioritize the order of the columns in the following way:

Columns in the WHERE Clause:

If you have a query like WHERE a=12 AND b='xyz', the composite index should start with column a and then include column b. So, it would look like INDEX(a, b).

IN Clauses:

If your query uses IN (e.g., WHERE a IN (1, 2, 3)), the optimizer can efficiently use the index to jump directly to the matching rows.

Range Conditions (e.g., BETWEEN, LIKE):

If you have a range condition in the query (like x BETWEEN 3 AND 9 or name LIKE 'J%'), this column should come before other columns in the index. However, only one range condition can be part of the composite index. If you have multiple range conditions, MySQL will only use the first one in the index.

GROUP BY and ORDER BY Columns:

If your query includes GROUP BY or ORDER BY, try to include these columns in the same order in the index. The index should match the columns in the GROUP BY or ORDER BY clause for optimal performance.

General Tips for Composite Indexes:

1.Avoid Duplicating Columns: Don't add columns to the index that are already covered by others.
2.Don’t Overcomplicate: If you don't need certain columns in the query (like those in GROUP BY or ORDER BY), don’t include them in the index.
3.Avoid Using Functions on Indexed Columns: For example, DATE(x) = ... cannot leverage an index on column x because you're modifying it with a function.
4.Prefix Indexing (indexing only part of a string column, like VARCHAR(99)): This is often not very helpful and could even slow things down.

Optimizing Storage Layout for InnoDB Tables:

InnoDB storage can be optimized in several ways to make your database more efficient, particularly with large tables:

Avoid Long Primary Keys:

Long primary keys (e.g., a composite key made up of several large columns) can cause problems because the primary key is duplicated in all secondary indexes. If your primary key is long, consider using an AUTO_INCREMENT column as the primary key to avoid this issue.

Use VARCHAR Instead of CHAR:

The CHAR data type always reserves space for the full length of the column, even if it’s not fully used (e.g., a CHAR(50) column will still take up 50 bytes, even if the string is shorter). Instead, use VARCHAR for variable-length strings or columns with many NULL values to save space and reduce disk I/O.

Consider Using COMPRESSED Row Format:

If you have a large table or repetitive data (like long strings or numbers), consider using the COMPRESSED row format, which reduces the amount of disk I/O and saves space. However, the compression may have some overhead, so it’s important to benchmark to see if it’s worthwhile.

Use OPTIMIZE TABLE for Cleanup:

Over time, as data grows, InnoDB tables can accumulate wasted space. Running the OPTIMIZE TABLE command can help reorganize the table and improve performance by reducing fragmentation and packing the data more efficiently.

Warning: OPTIMIZE TABLE is a costly operation (it rebuilds indexes and the table), and should only be done when necessary, such as after large data insertions. It’s usually not needed very frequently since InnoDB does a decent job of managing space internally.

Performance Tuning:
Don't hide in function:

A common mistake is to hide an indexed column inside a function call.

WHERE DATE(dt) = '2000-01-01'

Instead, given INDEX(dt) then these may use the index:
WHERE dt = '2000-01-01' -- if `dt` is datatype `DATE`

This works for DATE, DATETIME, TIMESTAMP, and even DATETIME(6) (microseconds):
WHERE dt >= '2000-01-01'
AND dt < '2000-01-01' + INTERVAL 1 DAY

OR:
In general OR kills optimization.
WHERE a = 12 OR b = 78

cannot use INDEX(a,b), and may or may not use INDEX(a), INDEX(b) via "index merge". Index merge is better
than nothing, but only barely.

WHERE x = 3 OR x = 5  is turned into  WHERE x IN (3, 5) which may use an index with x in it.

Add the correct index:

This is a huge topic, but it is also the most important "performance" issue.
The main lesson for a novice is to learn of "composite" indexes.

INDEX(last_name, first_name)

is excellent for these:
WHERE last_name = '...'
WHERE first_name = '...' AND last_name = '...' --> (order in WHERE does not matter)

but not for
WHERE first_name = '...' --> order in INDEX _does_ matter
WHERE last_name = '...' OR first_name = '...' --> "OR" is a killer

Indexes:
Simple Indexing:
For improving queries with WHERE clauses:

WHERE a = 12: INDEX(a) is efficient.
WHERE a > 12: INDEX(a) still works well.
WHERE a = 12 AND b > 78: INDEX(a,b) is more useful than INDEX(b,a) because a comes first.
WHERE a > 12 AND b > 78: No single index can handle both conditions efficiently.
ORDER BY x: INDEX(x) is good.
ORDER BY x, y: INDEX(x, y) is effective when the columns are in the same order.
ORDER BY x DESC, y ASC: No index will help, because the combination of ascending and descending makes the index less effective.

Subqueries:
Correlated vs Uncorrelated Subqueries:
Correlated Subqueries: These depend on values from the outer query. Often useful for handling one value at a time.

Example: SELECT a, b, (SELECT ... FROM t WHERE t.x = u.x) AS c

Uncorrelated Subqueries: These don't depend on outer values, which makes them easier to optimize but may still have efficiency issues when returning many rows.

Example: SELECT ... FROM (SELECT ...) AS a JOIN b ON ...

Best Practice: If a subquery returns 1 row, it's efficient. Subqueries returning many rows, especially with joins, can degrade performance.

Optimizing Pre-5.6: Without indexes on temp tables, it could lead to a CROSS JOIN, which can be inefficient. In MySQL 5.6+, there is more potential to optimize subqueries through temporary indexes, but this might still come at a cost.

JOIN + GROUP BY:
When using JOIN with GROUP BY, MySQL first expands the result set through the join and then reduces it using GROUP BY, which can be inefficient.

Optimization Tip: Instead of doing a JOIN + GROUP BY, consider turning the JOIN into a correlated subquery within the SELECT clause. This might remove the need for a GROUP BY altogether.

Database Configuration

InnoDB Buffer Pool Size:
Should be set to around 70% of available RAM for best performance.

Query Cache:
query_cache_size should generally not exceed 100MB, as increasing it beyond that can hurt performance.

MySQL Performance Myths:

MyISAM vs InnoDB: InnoDB has matured and is now almost always better than MyISAM.
Partitioning: It's rarely beneficial and can actually hurt performance in many cases.
Optimize Table: Running OPTIMIZE TABLE is often not helpful and locks the table, which can degrade performance.
Prefix Indexes: For example, INDEX(foo(20)) (indexing only the first 20 characters) is usually not effective.

Negative Impact on Performance:
1.Increasing MySQL Configurations Too Much: Over-tuning things like buffer sizes can lead to system swapping, which severely degrades performance.
2.Prefix Indexes: Indexing just a part of a column (e.g., the first 20 characters of a VARCHAR) is typically not a good performance strategy unless the column has specific characteristics (e.g., long text fields with a clear,