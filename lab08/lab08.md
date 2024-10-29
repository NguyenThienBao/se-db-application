# Event schedule in MySQL

Using Database "db_product" for this lab

## 1 - Basic Event Syntax

```sql
CREATE
    [DEFINER = user]
    EVENT
    [IF NOT EXISTS]
    event_name
    ON SCHEDULE schedule
    [ON COMPLETION [NOT] PRESERVE]
    [ENABLE | DISABLE | DISABLE ON {REPLICA | SLAVE}]
    [COMMENT 'string']
    DO event_body;

schedule: {
    AT timestamp [+ INTERVAL interval] ...
  | EVERY interval
    [STARTS timestamp [+ INTERVAL interval] ...]
    [ENDS timestamp [+ INTERVAL interval] ...]
}

interval:
    quantity {YEAR | QUARTER | MONTH | DAY | HOUR | MINUTE |
              WEEK | SECOND | YEAR_MONTH | DAY_HOUR | DAY_MINUTE |
              DAY_SECOND | HOUR_MINUTE | HOUR_SECOND | MINUTE_SECOND}
```

* Create table "tb_report" to summarize total product in database for every minutes

```sql
CREATE TABLE tb_report (
    id INT PRIMARY KEY NOT NULL AUTO_INCREMENT,
    total INT NOT NULL,
    created_at TIMESTAMP
);
```

* Create event for every minute update "tb_report" which store total of products 

```sql
CREATE EVENT event_total_product_report_minute
    ON SCHEDULE EVERY 5 SECOND
    DO
    	BEGIN
    		DECLARE total INT;
			SELECT COUNT(id) INTO total FROM tb_products;
    		INSERT INTO tb_report(total, created_at) VALUE (total, NOW());
    	END;

DROP EVENT IF EXISTS event_total_product_report_minute;
```

* After that, select "tb_report" to show log with total of 20 products

```sql
SELECT * FROM tb_report;
```

* And then, add 1 product to table "tb_product" 

```sql
INSERT INTO tb_products(id, name, price, cat_id) VALUES (21, 'iPhone 16 PRO MAX', 2000, 4);
```

* And Now, select "tb_report" , the log is updated with new value 21 products.

```sql
SELECT * FROM tb_report;
```
* Stop Event

```sql
DROP EVENT IF EXISTS event_total_product_report_minute;
```

## 2 - Advanced functions/methods for Event/Schedule

* Show current times of the system

```sql
SELECT NOW();
```

* Show ALL events/schedules in mysql

```sql
SHOW EVENTS;
```

* List of objects showing commands of mysql

```sql
SHOW PROCEDURE STATUS;
SHOW FUNCTION STATUS;

SHOW TRIGGERS;

SHOW INDEXES;

SHOW CREATE TABLE table_name;

SHOW CREATE EVENT event_name;

SHOW CREATE PROCEDURE procedure_name;

SHOW CREATE FUNCTION function_name;

SHOW CREATE TRIGGER trigger_name;

SHOW CREATE VIEW view_name;

SHOW CREATE USER user_name;

SHOW GRANTS FOR user_name;

SHOW CREATE DATABASE database_name;

SHOW CREATE SCHEMA schema_name;

SHOW CREATE TABLESPACE tablespace_name;

SHOW CREATE USER user_name;

SHOW CREATE VIEW view_name;
```

* Show tables object and structure in mysql

```sql
SHOW DATABASES;

SHOW COLUMNS FROM table_name;

SHOW INDEX FROM table_name;

SHOW TABLE STATUS;

SHOW CREATE TABLE table_name;

SHOW GRANTS FOR 'user'@'host';

SHOW TRIGGERS;

SHOW EVENTS;

SHOW PROCESSLIST;

SHOW VARIABLES;

SHOW STATUS;

SHOW WARNINGS;

SHOW ERRORS;

SHOW ENGINE INNODB STATUS;

SHOW CREATE DATABASE db_name;

SHOW FULL PROCESSLIST;

SHOW MASTER STATUS;

SHOW SLAVE STATUS;

SHOW BINARY LOGS;

SHOW BINLOG EVENTS;

SHOW CHARACTER SET;

SHOW COLLATION;

SHOW CREATE EVENT event_name;

SHOW CREATE FUNCTION function_name;

SHOW CREATE PROCEDURE procedure_name;

SHOW CREATE TRIGGER trigger_name;

SHOW CREATE VIEW view_name;

SHOW ENGINE engine_name STATUS;

SHOW FUNCTION STATUS;

SHOW GRANTS;

SHOW PRIVILEGES;

SHOW PROCEDURE STATUS;

SHOW PROFILE;

SHOW PROFILES;

SHOW RELAYLOG EVENTS;

SHOW SLAVE HOSTS;

SHOW STORAGE ENGINES;

SHOW TABLE STATUS LIKE 'pattern';

SHOW TRIGGERS LIKE 'pattern';

SHOW VARIABLES LIKE 'pattern';

SHOW GLOBAL VARIABLES LIKE 'pattern';

SHOW SESSION VARIABLES LIKE 'pattern';

SHOW WARNINGS LIMIT row_count;

SHOW ERRORS LIMIT row_count;

SHOW COUNT(*) FROM table_name;

SHOW COUNT(*) FROM table_name WHERE condition;

SHOW COUNT(*) FROM table_name GROUP BY column_name;

SHOW COUNT(*) FROM table_name ORDER BY column_name;

SHOW COUNT(*) FROM table_name LIMIT row_count;

SHOW COUNT(*) FROM table_name WHERE condition GROUP BY column_name ORDER BY column_name LIMIT row_count;

SHOW COUNT(*) FROM table_name WHERE condition GROUP BY column_name ORDER BY column_name LIMIT row_count FOR UPDATE;

SHOW COUNT(*) FROM table_name WHERE condition GROUP BY column_name ORDER BY column_name LIMIT row_count LOCK IN SHARE MODE;

SHOW COUNT(*) FROM table_name WHERE condition GROUP BY column_name ORDER BY column_name LIMIT row_count FOR UPDATE;

SHOW COUNT(*) FROM table_name WHERE condition GROUP BY column_name ORDER BY column_name LIMIT row_count LOCK IN SHARE MODE;

SHOW COUNT(*) FROM table_name WHERE condition GROUP BY column_name ORDER BY column_name LIMIT row_count FOR UPDATE;

SHOW COUNT(*) FROM table_name WHERE condition GROUP BY column_name ORDER BY column_name LIMIT row_count LOCK IN SHARE MODE;

SHOW COUNT(*) FROM table_name WHERE condition GROUP BY column_name ORDER BY column_name LIMIT row_count FOR UPDATE;

SHOW COUNT(*) FROM table_name WHERE condition GROUP BY column_name ORDER BY column_name LIMIT row_count LOCK IN SHARE MODE;

SHOW COUNT(*) FROM table
```