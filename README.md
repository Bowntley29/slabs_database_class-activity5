# Author:Bontle Mogapi

# Data Modeling Theory 
# 1. ER Components
a) Entity: is a distinct real-world object (living or non-living) that can be easily identified and stored in a database.
- Example: A book or a customer.

b) Relationship: is the connection or association that links different entities together.
- Example: A customer places an order, or an author writes a book.

c) Attribute: are the specific properties or characteristics that describe an entity.  
- Example: For the book entity the attributes would be things like book_id, title, and author_id or even price and genre.

# 2. Data Model Levels
- Conceptual Data Model focuses on what the system contains at a high level by organizing and scoping out the main business concepts and rules. The people who create it are business stakeholders and data architects. 
- Physical Data Model focuses on how the system will actually be built and implemented inside a specific Database Management System (DBMS), such as PostgreSQL, including actual tables, data types, and keys. The people who create it are database administrators (DBAs) and developers.

# Section 3: Practical ER-to-Relational Conversion
1. ER Mapping:   
Conceptual Rule: A customer places many orders.

Entity 1: Customer (Attributes: customer_id, full_name, email)   
Entity 2: Order (Attributes: order_id, order_date, total_amount, customer_id)   

Relationship: customer_id serves as the Primary Key in the Customer entity and is placed as a Foreign Key in the Order entity to link each order back to the customer who placed it.

#### 2. PostgreSQL Implementation

**SQL Commands & Terminal Output:**

```text
$ psql -U postgres
Password for user postgres:

psql (17.11, server 18.6)
WARNING: psql major version 17, server major version 18.
         Some psql features might not work.
WARNING: Console code page (437) differs from Windows code page (1252)
         8-bit characters might not work correctly. See psql reference
         page "Notes for Windows users" for details.
Type "help" for help.

postgres=# CREATE DATABASE store_modeling_db;
CREATE DATABASE
postgres=# \c store_modeling_db
psql (17.11, server 18.6)
WARNING: psql major version 17, server major version 18.
         Some psql features might not work.
You are now connected to database "store_modeling_db" as user "postgres".

store_modeling_db=# CREATE TABLE customers (
store_modeling_db(#     customer_id SERIAL PRIMARY KEY,
store_modeling_db(#     full_name VARCHAR(100) NOT NULL,
store_modeling_db(#     email VARCHAR(100) UNIQUE NOT NULL
store_modeling_db(# );
CREATE TABLE

store_modeling_db=# CREATE TABLE orders (
store_modeling_db(#     order_id SERIAL PRIMARY KEY,
store_modeling_db(#     order_date DATE NOT NULL DEFAULT CURRENT_DATE,
store_modeling_db(#     total_amount NUMERIC(10, 2) NOT NULL,
store_modeling_db(#     customer_id INTEGER REFERENCES customers(customer_id)
store_modeling_db(# );
CREATE TABLE

store_modeling_db=# \dt
           List of relations
 Schema |   Name    | Type  |  Owner
--------+-----------+-------+----------
 public | customers | table | postgres
 public | orders    | table | postgres
(2 rows)

store_modeling_db=# SELECT * FROM customers;
 customer_id | full_name | email
-------------+-----------+-------
(0 rows)

store_modeling_db=# SELECT * FROM orders;
 order_id | order_date | total_amount | customer_id
----------+------------+--------------+-------------
(0 rows)
```
