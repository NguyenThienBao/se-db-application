# Lab04 - Basic MySQL Commands

Ref: https://dev.mysql.com/doc/search/?d=201&p=1&q=data+mani

## 1 - Set Working Database

```sql
USER db_product;
```

## 2 - Insert data to table

* Insert data to tb_categories

```sql
INSERT INTO tb_categories(id, name) VALUES
(1, 'mobile'),
(2, 'tablet'),
(3, 'laptop'),
(4, 'smart watch');
```

* Insert data to tb_products

```sql
INSERT INTO tb_products(id, name, price, cat_id) VALUES
(1, 'Iphone X', 200, 1),
(2, 'Iphone Xs', 300, 1),
(3, 'Iphone XI', 400, 1),
(4, 'Iphone XIII', 600, 1),
(5, 'Iphone XIV', 700, 1),
(6, 'Ipad gen 10', 400, 2),
(7, 'IPad air 4', 500, 2),
(8, 'IPad Pro 4', 700, 2),
(9, 'Galaxy S24', 1200, 1),
(10, 'Galaxy fold Z 6', 2500, 1),
(11, 'Galaxy Flip 6', 2500, 1),
(12, 'Galaxy Tab S9', 2000, 2),
(13, 'MacBook Pro M2 16 inch', 2500, 3),
(14, 'MacBook Pro M3 14 inch', 2200, 3),
(15, 'MacBook Pro M3 16 inch', 3000, 3),
(16, 'Apple Watch 9', 500, 4),
(17, 'Apple Watch Ultra 2', 800, 4),
(18, 'Galaxy Watch Ultra', 800, 4);
```

## 3 - Query Data 

* Using WHERE to map data from between tb_cat and tb_pro by column 'cat_id'

```sql
SELECT p.id, p.name, p.price, c.name
FROM  tb_products p, tb_categories c
WHERE p.cat_id = c.id;
```

* Using JOIN Command with foreign key relationship 

```sql
SELECT p.id, p.name, p.price, c.name
FROM tb_products p
LEFT JOIN tb_categories c ON p.cat_id = c.id;
```

* Limit number of rows in the result (Skip first 5 rows and get the next 10 rows)

```sql
SELECT p.id, p.name, p.price, c.name
FROM tb_products p
LEFT JOIN tb_categories c ON p.cat_id = c.id
LIMIT 5, 10;
```

* Get first 5 rows

```sql
SELECT p.id, p.name, p.price, c.name
FROM tb_products p
LEFT JOIN tb_categories c ON p.cat_id = c.id
LIMIT 5;
```

* Using COUNT and GROUP BY commands to group data 

```sql
SELECT c.name, COUNT(p.id) AS num_of_products
FROM tb_products p
LEFT JOIN tb_categories c ON p.cat_id = c.id
GROUP BY p.cat_id;
```

* Using HAVING to set condition filter of the result data

```sql
SELECT c.name, COUNT(p.id) AS num_of_products
FROM tb_products p
LEFT JOIN tb_categories c ON p.cat_id = c.id
GROUP BY p.cat_id
HAVING num_of_products > 5;
```

## 4 - Delete Data 

* Remove All of Products from category Smart Watches 

```sql
DELETE FROM tb_products p
WHERE p.cat_id = ( SELECT id 
                    FROM tb_categories 
                    WHERE name = "smart watch"
);
```

## 5 - Update data

* Rename of product which is from "Galaxy S24" to "Galaxy Ultra S24"

```sql
UPDATE tb_products
SET name = "Galaxy S24"
WHERE name like '%GALAXY S2';
```