# Lab 05 - Export and Import Data

## 1 - Using Terminal

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