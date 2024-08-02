# Lab01 - Access MySQL withh command

## Step 01

* Start ***db-mysql*** Docker Container

``` shell
docker container start db-mysql 
```

Or use alias docker command

``` shell
docker start db-mysql 
```

## Step 02

* Access to MySQL Docker Container.

``` shell
docker exec -it db-mysql bash
```


## Step 03

* Login to MySQL Database.

``` sql
mysql -u root -p 
```

Enter root-password (admin123) after enter the command above.

* Create MySQL Database User

``` sql
CREATE USER 'db_user'@'localhost' IDENTIFIED BY 'user_password'
```

* Set permission for db_user to access to database.

``` sql
GRANT ALL PRIVILEGES On *.* TO "db_user'@'localhost'
```
* __db_user__: is the database user which is used for aaccess to database.
* __user_password__: is password of database user.

* Show all users on mySQL

``` sql
SELECT user, host FROM mysql.user;
```

* Log out MySQL Database (with root user)

``` sql
\q
```

* Log in into new user database (db_user)

``` sql
mysql -u db-user -p
```

Enter db_user password (user_password)

* Show current user information login to mySQL

``` shell
SELECT CURRENT_USER();
```

list all user
``` sql
SELECT host, user FROM mysql.user;
```

## To change user password, using root user and run command
* Connect Database with **root**

```shell
mysql -u root -p
```

enter root paswword (admin123)

* change db-user password to 'new-password'

```sql
ALTER USER 'username'@'localhost' IDENTIFIED BY 'new-password';
```

* Reload Grant Table
```sql
FLUSH PRIVILEDGES
```

* when we want to run MySQL Docker Container

``` Shell
docker container start db-mysql
```

with __db-mysql__ is docker container or container ID

