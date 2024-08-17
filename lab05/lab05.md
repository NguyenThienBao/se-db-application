# Lab 05 - Export and Import Data

## 1 - Using Terminal

### 1.1 - Export Database

* Connect to MySQL Docker Container

```shell
docker exec -it db-mysql bash
```

* Navigate to Docker's directory "/var/lib/mysql" because docker volume is previously mapped here.

```shell
cd /var/lib/mysql
```

* Dump database to Script SQL File with name db_product_script.sql

```shell
mysqldump -u root -p db_product > db_product_script.sql
```

* Copy exported Script file "db_product_script.sql" from Docker's volume or Docker's container "db-mysql-new-data" to host (PC) 

```shell
docker cp db-mysql:/var/lib/mysql/db_product_script.sql ./scripts/db_product_script_01.sql
```

### 1.2 - Import Database

* Duplicate the exported script file db_product_script.sql to db_product_new.sql
* Create new database in MYSQL

```sql
CREATE DATABASE IF NOT EXISTS db_product
CHARACTER SET 'utf16'
COLLATE 'utf16_unicode_ci';
```

* Copy file "db_product_new.sql" to Docker's Volume (Docker Container) ["/var/lib/mysql"]

```shell
docker cp ./scripts/db_product_new.sql db-mysql:/var/lib/mysql/
```

* In MySQL Docker Container, Execute "db_product_new.sql" with import data to database "db_product_new"

```shell
mysql -u root -p db_product_new < ./var/lib/mysql/db_product_new.sql
```

* Connect to database to chheck data after import

```shell
mysql -u root -p
```

Input root pass (admin123)

* Show all databases

```sql
SHOW DATABASES;
```

* Set working curret database "db_product_new"

```sql
USE db_product_new;
```

* Show all tables in "db_product_new"

```sql
SHOW TABLES;
```

* Execute query to check data 

```sql
SELECT p.id, p.name, p.price, c.name
FROM tb_products p LEFT JOIN tb_categories c ON p.cat_id = c.id;
```