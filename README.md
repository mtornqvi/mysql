# MySQL general

1. [Useful programs](#1-useful-programs) 
2. [Linux command line ](#2-linux-command-line) 
3. [Controlling user privledges](#3-controlling-user-priviledges) 
4. [Creating database](#4-creating-database) 
5. [Manipulating tables](#5-manipulating-tables) 
6. [Importing data](#6-importing-data) 
7. [Storing data](#7-storing-data)   
7.1. [Data types](#71-data-types)
8. [Retrieving data](#8-retrieving-data)

## 1. Useful programs

<a href="https://www.phpmyadmin.net/">  phpMyAdmin </a>  
<a href="https://dbeaver.io/">  DBeaver </a>
<a href="https://www.libreoffice.org/">  LibreOffice </a>

Linux command-line tools:
mysql


## 2. Linux command line 

Login as root
```sh
sudo mysql -u root -p
```

Login as ordinary user
```sh
mysql -u usernmame -p
```


All MYSQL commands should be terminated with semi-colon (;)

Rename user:
```sh
RENAME USER old_user TO new_user;
```

Rename database (little bit tricky)
```sh
mysqladmin -u username -p create newdatabase
mysqldump -u username -v olddatabase -p | mysql -u username -p -D newdatabase
mysql -username -p DROP database olddatabase
```

## 3. Controlling user priviledges

```sh
SHOW GRANTS FOR 'username';
SHOW GRANTS FOR 'username'@'somelocation.com';
```

```sh
GRANT ALL PRIVILEGES ON *.* TO 'username'@'%';
GRANT ALL PRIVILEGES ON `databasename`.* TO 'username'@'%';
```

Revoking prviledges, note the word FROM
```sh
REVOKE ALL ON *.* FROM 'username'@'%';
```


## 4. Creating database 

Login to database using suitable program

```sh
CREATE DATABASE name;
```

Allow user to use database from all addresses
```sh
GRANT ALL PRIVILEGES ON user.* to 'user'@'%';
```


Database tables are organized like other tables that you're used to — in rows and columns. Each row represents an entity in the database, such as a customer, a book, or a project. Each column contains an item of information about the entity, such as a customer name, a book name, or a project start date.

Selecting database
```sh
USE name;

```
## 5. Manipulating tables

Rename table:
```sh
RENAME TABLE old_table TO new_table;
```
or
```
ALTER TABLE old_table RENAME new_table;
```

RENAME TABLE, unlike ALTER TABLE, can rename multiple tables within a single statement: 
```
RENAME TABLE old_table1 TO new_table1,
             old_table2 TO new_table2,
             old_table3 TO new_table3;
```          

Add a column
```
ALTER TABLE `databasename`.tablename ADD column_name TIME NULL;
```

Change column orders
```
ALTER TABLE `databasename`.tablename CHANGE column_1 column_1 TIME NULL AFTER column_2;
```


## 6. Importing data

Excel:
Export data to csv, deliminated with commas.
Best tool for this is Libreoffice Calc, where you can choose coding and deliminators.

```
LOAD DATA LOCAL INFILE "/location/name.csv" INTO TABLE databasename.tablename
FIELDS TERMINATED BY ','
LINES TERMINATED BY '\n'
(field)
```

On DBeaver, select table with right mouse button => import data.

Imported data must have header row.
This can be matched in DBeaver with field (column) names : Tables mapping => Columns.

## 7. Storing data

### 7.1. Data types

TIME(fsp) 	A time. Format: hh:mm:ss. The supported range is from '-838:59:59' to '838:59:59'

### 7.2 Updating existing row

```
UPDATE `database_name`.table_name
SET column_1 = value_1
WHERE column_2=value_2;
```

```
UPDATE `database_name`.table_name
SET column_1 = value_1, column_2 = value_2
WHERE column_3=value_3;
```

## 8. Retrieving data

```
SELECT column_1
FROM table_name
WHERE column_2=value;
```

