# DATABASE NOTE ON POSTGRESQL BY OLUMUYIWA KOLAYEMI

## What's up with PostgreSQL?

**PostgreSQL** is a powerful, open source object-relational database system that uses and extends the SQL language combined with many features that safely store and scale the most complicated data workloads. It comes with many features aimed to help developers build applications, administrators to protect data integrity and build fault-tolerant environments, and help you manage your data no matter how big or small the dataset. In addition to being free and open source, **PostgreSQL** is highly extensible. For example, you can define your own data types, build out custom functions, even write code **FROM** different programming languages without recompiling your database!
**PostgreSQL** tries to conform with the SQL standard **WHERE** such conformance does not contradict traditional features or could lead to poor architectural decisions. Many of the features required by the SQL standard are supported, though sometimes with slightly differing syntax or function.


## SQL COMMAND CATEGORIES: DDL || DML || DCL || TCL

### 1) Data Definition Lang (DDL): <<< CREATE, DROP, **ALTER**, TRUNCATE >>>
This consists of the commands that can be used to define the **DATABASE SCHEMA**.
A **database schema** is the skeleton structure that represents the logical view of the entire *database*. It defines how the *data* is organized and how the relations among them are associated.
A **database instance** is a state of *operational database* with *data* at any given time. Examples are showed below;

**CREATE**: This is majorly use to create *database*., schema and table e.g CREAT TABLE table_name
**DROP**: this is majorly use to remove *database*. and table
**TRUNCATE** TABLE will delete every data content in the table without deleting the table itself.
****ALTER**** TABLE table_name **RENAME** TO new_table_name
****ALTER**** TABLE table_name **ADD**  column_name *datatype*

### 2) Data Manipulation Lang (DML): <<< **SELECT**, **INSERT**, UPDATE, DELETE >>>

These are the *sql* commands that deals with the *manipulation of data* present in *database*.

****SELECT****: This command are used to select records **FROM** *database*. They are used with the following commands;
- **ODER BY**:
- **DISTINCT**:To give unique output
We can also carry out comparison operation with ****SELECT****
****SELECT**** 1 > 2; will return true.


### OFFSET || LIMIT || FETCH:

**SELECT** * ****FROM**** random_people LIMIT 10; will return only 10 records.
**SELECT** * **FROM** random_people OFFSET 10 LIMIT 10; will return only 10 records starting **FROM** the 11th records i.e 11 - 21.
**SELECT** * **FROM** random_people OFFSET 5 FETCH FIRST 5 ROW ONLY; will return only 5 records starting **FROM** the 6th records.


****INSERT****:

**INSERT** **INTO** table name ( 
 first_name,
 last_name,
 gender)
**VALUES** ('Zin', 'Jin', 'MALE');

### UPDATE Command:

**UPDATE** random_people SET first_name = 'Zin', last_name = 'Jin' **WHERE** id = 20;

## DELETE Command:

**DELETE** **FROM** random_people **WHERE** gender = " Hello";

 
## 3) Data Control Lang (DCL): <<< GRANT, INVOKE >>>

These includes commands which mainly deals with the rights, permissions and other controls of the database system.

## 4) Transaction Control Lang (TCL): <<< COMMIT, ROLLBACK, SAVEPOINT >>>

These includes the commands which mainly deals with the transaction of database.



## Keys in Database:

- **Primary key**: A primary is a column or set of columns in a table that uniquely identifies tuples (rows) in that table.  Primary key is selected **FROM** a set of candidate keys
- **Super key**: A super key is a set of one of more columns (attributes) to uniquely identify rows in a table.
- **Candidate key**:A super key with no redundant attribute. Candidate keys are selected **FROM** the set of super keys, the only thing we take care while selecting candidate key is: It should not have any redundant attribute
- **Alternate key**: Out of all candidate keys, only one gets selected as primary key, remaining keys are known as alternate or secondary keys.
- **Composite Key** – A key that consists of more than one attribute to uniquely identify rows (also known as records & tuples) in a table is called composite key.
- **Foreign Key** – Foreign keys are the columns of a table that points to the primary key of another table. They act as a cross-reference between tables.

## Constraints in Database

**NOT NULL**: ensures that a null value cannot be stored in a column 
**UNIQUE**: this constraint makes sure that all the values in a column are different
**CHECK**: This constraint ensures that all the values in a column staify a specific condition
**DEFAULT**: This constraint consists of a set of default values for a column when no value is specified 
**INDEX**: This constraint is used to create and retrieve data **FROM** the database very quickly.

## KEYWORDS:

### IN: It takes an array of values and return the query matching those values e.g;

**SELECT**
 first_name, last _name, country_of_birth
**FROM**
 random_people
****WHERE****
 counrty_of_birth
**IN**
 ('China', 'Nigeria', 'Ghana')
**ORDER BY**
 country_of_birth DESC; ===> This will return names and country of random people **FROM** China, Nigeria & Ghana and ordered them by their countries in descending order.

### BETWEEN:

**SELECT** first_name, last_name 
**FROM** random_people 
**WHERE** date_of_birth 
**BETWEEN DATE** '2020-01-01' AND '2020-06-30'
**ORDER BY** date_of_birth DESC; ===> This will return names of people with date of birth between 01/01/2020 & 06/30/2020

## OPERATORS:

### LIKE:

**SELECT** * **FROM** random_people
**WHERE** email **LIKE** '%@google.com' ===> This will return all records that look like @google.com

**SELECT** * **FROM** random_people **WHERE** country_of_birth LIKE 'P%'; ===> This will return people **FROM** country that start with P.

## Purpose of wildcards in SQL
• % permits substituting one or more characters in a field 
• _ permits substituting a single character in a syntax expression

*Wildcard* are used with the **WHERE** clause and LIKE operator. They can also be used in combinations.

The substring_index function allows you to select an index; specifically, the -1 index or the last item.


### GROUP BY:
**SELECT** country_of_birth, COUNT(*) **FROM** random_people GROUP BY country_of_birth ORDER BY country_of_birth;
This will count the number of people **FROM** each country and order them **FROM** Alfghanistan - Zimbabwe 

### GROUP BY HAVING: Add extra filter to GROUP BY
 
**SELECT** country_of_birth, COUNT(*) **FROM** random_people GROUP BY country_of_birth HAVING COUNT(*) > 5 ORDER BY country_of_birth;

### AGGREGATE FUNCTIONS:

MIN || MAX || SUM


### Alias and maths operation e.g

**SELECT** id, make, model, price AS orig_price, ROUND(price * .10, 2) AS discount, (price - (price * .10)) AS promo_price **FROM** cars_series

### COALESCE:

**SELECT** **COALESCE**(


### EXTRACT FIELD

**SELECT EXTRACT**(YEAR **FROM** NOW());


### AGE():

**SELECT** last_name, gender, **AGE(NOW()**, date_of_birth) **AS** age **FROM** random_people;


### To Add constraint
****ALTER**** TABLE random_people ADD UNIQUE (email);
//**ALTER** TABLE random_people ADD CONSTRAINT unique_email_address UNIQUE (email);//

### To drop constraint:
**ALTER** TABLE random_people DROP CONSTRAINT unique_email_address;

### To check constraint:
**ALTER** TABLE random_people ADD CONSTRAINT gender_constraint CHECK(gender = 'Female' or gender = 'Male');


### TO RUN A FILE ON TERMINAL:

- Go to www.mockaroo.com to generate 1000 random data
- make sure to change file type to sql and click include create a table
- open VSCode, go to file and open the file from downloads into VSCode env
- Edit the query to include pry key, not null and adjust the length of datatype.
- open a new terminal, cd to Download and pwd to display the file path and copy the path
- Go back to the formal terminal 
- type \i copy the path here e.g *\i /home/muyi/Downloads/random_file.sql* and run the code

[ Check out this Postgresql Cheat Sheet for more commands](https://s3.us-west-2.amazonaws.com/secure.notion-static.com/642a6f63-aee8-4ff0-a245-304229e3e4ab/PostgreSQL-Cheat-Sheet.pdf?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Credential=AKIAT73L2G45O3KS52Y5%2F20201116%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20201116T130502Z&X-Amz-Expires=86400&X-Amz-Signature=8fcd8f300c45475180ec720d8c1c9269153593c61793ba2121965f38fc7fc4f0&X-Amz-SignedHeaders=host&response-content-disposition=filename%20%3D%22PostgreSQL-Cheat-Sheet.pdf%22)