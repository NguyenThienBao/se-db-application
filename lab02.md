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

``` shell
mysql -u root -p 
```

Enter root-password (admin123) after enter the command above.

* Create MySQL Database User

``` shell
CREATE USER 'db_user'@'localhost' IDENTIFIED BY 'user_password'
```

* Set permission for db_user to access to database.

``` shell
GRANT ALL PRIVILEGES On *.* TO "db_user'@'localhost'
```
* __db_user__: is the database user which is used for aaccess to database.
* __user_password__: is password of database user.

* Show all users on mySQL

``` shell
SELECT user, host FROM mysql.user;
```

* Log out MySQL Database (with root user)

``` shell
\q
```

* Log in into new user database (db_user)

``` shell
mysql -u db-user -p
```

Enter db_user password (user_password)

* Show current user information login to mySQL

``` shell
SELECT CURRENT_USER();
```

