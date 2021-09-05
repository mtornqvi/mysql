# MySQL general

1. [Useful programs](#Useful_programs) 
2. [Linux command line ](#Linux_command_line) 
3. [Controlling user privledges](#Controlling_user_priviledges) 
4. [Creating database](#Creating_database) 
4. [Manipulating tables](#Manipulating_tables) 
6. [Importing data](#Importing_data) 

## 1. Useful programs

<a href="https://www.phpmyadmin.net/">  phpMyAdmin </a>  
<a href="https://dbeaver.io/">  DBeaver </a>

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


## 6. Importing data

Excel:
Export data to csv, deliminated with commas.


USE AIKA; # change database
LOAD DATA LOCAL INFILE "/usr/local/notes/asiakkaat.csv" INTO TABLE aika.asiakkaat
FIELDS TERMINATED BY ','
LINES TERMINATED BY '\n'
(nimi)


