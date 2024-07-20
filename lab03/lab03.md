# Lab03 - Create and Access database on MySQL Docker Container

## Step 01:
Install Client GUI tool to access Database

* MySQL Workbench: link
* Azure Data Studio: link

Install extension:

* MySQL
* SQL Database Project

## Step 02:
Connect to Database with Terminal 

### Step 2.1:

Start MySQL Docker Container

``` shell
docker container start db-mysql
```

Check status of MySQL Docker Container

``` shell
docker ps
```

### Step 2.2:

Access to MySQL Docker Conatiner

``` shell
docker exec -it db-mysql bash
```

### Step 2.3:

Connect to Database on MySQL Docker Container

``` shell
mysql -u db_user -p
```

## Step 3:
Create Database with command

```sql
CREATE {DATABASE | SCHEMA} [IF NOT EXISTS] db_name
    [create_option] ...

create_option: [DEFAULT] {
    CHARACTER SET [=] charset_name
  | COLLATE [=] collation_name
  | ENCRYPTION [=] {'Y' | 'N'}
}
```

andd now, we create database **db-product**

```sql
CREATE DATABASE IF NOT EXISTS db_product
CHARACTER SET 'utf16'
COLLATE 'utf16_unicode_ci';
```

```sql
SELECT DEFAULT_CHARACTER_SET_NAME, DEFAULT_COLLATION_NAME FROM INFORMATION_SCHEMA SCHEMATA WHERE SCHEMA_NAME = 'db_product';
```

????

Use database
```sql
use db_product;
```

Show current database:
```sql
SELECT DATABASE();
```

Drop database:
```sql
DROP DATABASE db_product;
```

Show all database:
```sql
SHOW DATABASES;
```

## Step 04:
Create new table with foreign key

* choose default storage engine for current section.

```sql
SET default_storage_engine = InnoDB;
```

* choose database to create categories table


```sql

```