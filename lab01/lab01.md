# Lab 01 ~ Setup mySQL with Docker ~ 

Ref: https://www.datacamp.com/tutorial/set-up-and-configure-mysql-in-docker

# Step by Step

## Step 01
* Dowload mySQL Docker
```shell
$ docker pull mysql:lastest
```

* List docker images on PC
```shell
$ docker images
```

## Step 02 - Running and managing mySQL Container
```shell
$ docker run -d --name db-mysql -p 3307:3306 -e MYSQL_ROOT_PASSWORD=admin123 mysql
```

Command Description

* __run__: create a new container or staarts an existing one.
* __--name <CONTAINER_NAME>__: setup container name.
* __-p <HOST_PORT:DOCKER_PORT>__: define the port mmapping from Host(PC) Port to Docker Port. In this case is from 3307 host port (real port of PC) to docker port 3306 (default port of mysql).
* __-e [ENV_VARIABLE=value]__: the -e tag creates an environment variable. In this case is MYSQL_ROOT_PASSWORD, which is the root password of MySQL DB.
* __-d__: thhis tag make the countainer run in the background.
* __<IMAGE_NAME>__: is the name of image. In this case is ***mysql***

## Step 03 - Access to mySQL container
```shell
$ docker exec -it db-mysql bash
```

* __exec__: is a command to access to the container
* __-it__:
    * __-i__: Keep STDIN open even if not attached.
    * __-t__: Allocation a pseduo -TTY.
* __CONTAINER_NAME__: is the name the container which you want to access. In this case is ***db-mysql***

## Step 04 - Using bash command to connect mysql-command

* Connect to client as ROOT user of MySQL
```shell
$ mysql -u root -p
```
* Enter password after the prompt.

Now, we can used MySQL command (query) to access to the database.

## Step 05 - Configuring the MySQL Container

* We can edit configure of MYSQL by access to thhe directories in MySQL docker container:
> /etc/mysql/

> /etc/mysql/conf.d

> /etc/mysql/mysql.conf.d

After that, remove current mysql docker container and create new withh command.

* remove current mysql docker container
```shell
$ docker container rm db-mysql -f
```

* Create host directory conffigure for MySQL configure.
```shell
$ mkdir ./mysql-conf
$ touch ./mysql-conf/my.cnf
```

* Enter the config to apply for MySQL.

```shell
$ vim ./mysql-conf/my.cnf
[mysqld]
max_connections=200
```

* Create new mySQK Docker container with configure directory mounted

```shell
$ docker run \ 
    --name db-mysql \
    -e MYSQL_ROOT_PASSWORD=admin123 \ 
    -p 3307:3306
    -v ./mysql-conf:/etc/mysql/conf.d \
    -d mysql 
```


## Step 06 - Advance command docker to preserve thhe database storage in MySQL Storage.

* Create a volume
```shell
$ docker volume create db-mysql-data
```

* Create new MySQL container with the volume mounted.
```shell
$ docker run \
    --name db-mysql \
    -e MYSQL_ROOT_PASSWORD=admin123 \
    -p 3307:3306 \
    -v db-mysql-data:/var/lib/mysql \
    -d mysql
``` 

## Finally

```shell
$ docker run \
    --name db-mysql \
    -e MYSQL_ROOT_PASSWORD=admin123 \
    -v ./mysql-conf:/etc/mysql/conf.d \
    -v db-mysql-new-data:/var/lib/mysql \
    -d mysql
```

* This command woll create new volume db-mysql-new-dat and map to MYSQL Docker Container