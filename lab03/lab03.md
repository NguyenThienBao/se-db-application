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

List all user 
```sql
SELECT USER();
```

or
```sql
SELECT CURRENT_USER();
```