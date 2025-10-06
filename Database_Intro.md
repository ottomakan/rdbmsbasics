# Database Intro

# Links
Raw Cosmetics data: https://docs.google.com/spreadsheets/d/1ALjnWm6bUMGW7aY05qSrB9z7sn4RoW7tozmqheSY8J8/edit?gid=1495894486#gid=1495894486

SQL Developer Data Modeler: https://www.oracle.com/database/sqldeveloper/technologies/sql-data-modeler/download/

SQL Developer: https://www.oracle.com/database/sqldeveloper/technologies/download/

# Basics

There are several database technologies out there. Of all of these, RDBMS remains one of the oldest and most popular even today. Others include — columnar databases, JSON/Document databases, Key value stores etc.

# What is RDBMS?

Relational Database Management System

## What is a Relational Database?

It is a scheme of organizing data as “relations” 

### Is RDBMS then a database?

No\! RDBMS is a database software that is used to create and interact with the database. The database is nothing but a set of files on your filesystem that is in proprietary format. The RDBMS software is used to interact with the database. However, colloquially, we refer to the database as a running instance of the RDBMS software.

RDBMS software allows multiple concurrent users to access and manipulate data. As an analogy, MS Word software is akin to RDBMS software and the actual word doc you create, is akin to a database. You cannot create or interact with the database (i.e. the word doc), without using MS Word; although, these days there are tools that can understand the .doc format file and read them – but that is besides the point.

The difference is, a RDBMS software is a server class software that runs on servers as opposed to a user’s desktop. The reason being, it is a multi user software and allows hundreds of users to concurrently connect and work on their own piece of data.

To connect to the RDBMS server software, a client software is installed and run on the user’s desktop (Windows, Mac, etc.). These client tools/software use a database driver to initiate a connection to the server running your RDBMS. The database driver is a separate set of files installed or downloaded on the client computer and is used by the client software that the user will work on to interact with the RDBMS software on the server.

There are many RDBMS technologies to choose from. Many are paid licenses and some are open source or free licenses. Paid ones include Oracle, SQL Server, DB2 etc. The popular free ones include PostgresSQL, MySQL, MariaDB and more. Remember, these are server side RDBMS software we are talking about.

The client software on the other hand, is more general purpose. For instance you can find one client software that can connect to Oracle, DB2, Postgres and more. All you do is download the correct driver for the database you are interested in.

Regardless of which RDBMS variant you use, the key concepts about relational databases are going to be the same. They are like OO concepts that apply the same way between various OO languages.

# Data Organization in a Relational Database

The whole purpose for having a relational database is to have rules around organizing data. As the implementor of the database you are free to organize the data the way you see fit, as long as you follow the rules laid out by relational theory. 

The purpose of the relational rules is to make sure that the data conforms to a set of protocols that machines can effectively work with. The interface to put data and pull out data from a relational database is the SQL syntax.

#### Some key rules are:

- Data is organized into relations. Relations are also called Tables. You can think of a table as a google sheet. So, one database can have countless google sheets or tables. You use SQL to create new tables, add data to existing tables, update or modify existing data in tables or delete data from existing tables. This is true regardless of whichever programming language (Java, Python etc.) you use to write your application that interacts with a relational database to persist data.  
- Tables have columns. Just like a google sheet does. Each column has a datatype.   
- A row of data is like a row in your google sheet. So thinking about a table as a google sheet is perfect for a mental visual representation of your data.  
- Now, think about how you can have a set of these tables or sheets related to one another. This is the crux of database organization\!

Remember, data in client software products like google sheets, MS Word, Excel etc. is designed for interactive use. RDBMS based databases are designed for programmatic use. The clients are usually applications and not individuals (like in the case of MS Excel for example).

So this follows that the database can be (and frequently is) “designed” before there is even a shred of application/user data in it\!

You can define the tables, the columns, datatypes, etc. well before you have any actual data in it. This act of database designing is called data modeling.

If you are going to create a data model, you have to know something or enough about the data you are going to store in the database. This is called “domain knowledge”. So, if you are going to have a database that deals with cosmetic sales, you would need to know something about the business of cosmetics and for that you would typically work with a subject matter expert or a domain expert (usually your client who you are creating the database for).

A database is ultimately a collection of related tables.

### Rules of data design – Normalization

1. Separation of concerns: Identify related fields in your data and separate them into their own “ENTITIES”. These are often repeating groups of information \- meaning the same related set repeats for multiple rows in the transaction table.   
     
   Transaction table is an entity that contains a row of data for each occurrence of the “transaction”. For example, the ORDER table contains orders for cosmetics. Each order row represents a single order from a customer.  
     
   Here we are starting with a google sheet that contains order transactions. For purposes of this data modeling exercise, we are separating or organizing repeating groups of related data into their own entities, so they do not unnecessarily repeat in the transaction table.

2. Find how they relate to the main concept (e.g. order). For instance, do they have a 1:1 relationship? Or is it 1:M or M:M?  
3. Leave the PK of the group of columns you are pulling out into its own entity, in the transaction table. This new entity is the parent and the transaction table is the child. This PK you leave in the transaction table is called a FK. So a FK in the transaction table is the PK of the parent. It allows you to take any order and use the FK to look up the row in the parent table that contains the rest of the values that used to be in the transaction table (child) for the said row.

Order database example:

#### Entities:

- ORDER (central concept. Also the transaction table)  
- STORE  
- CUSTOMER  
- PRODUCT  
- PROMOTION

## NOTES for modeling:

1. Create the central concept first. E.g. ORDER  
2. Create the dimensions next. E.g. CUSTOMER, STORE  
3. Since the dimension is parent and the transaction table is child, it is a good idea to define the columns for the parent first.  
   1. Every table should have an ID field. The ID field will contain a value that is unique across all rows. E.g. STORE\_ID, CUSTOMER\_ID etc. You only need one column to be the id column in a table (this can be a composite ID also, but more on that later).
