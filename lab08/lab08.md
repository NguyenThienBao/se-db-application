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


