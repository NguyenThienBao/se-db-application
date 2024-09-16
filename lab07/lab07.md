# View in MySQL 

* In SQL, a View is a virtual table based on the ressult-set of an SQL statement. A View contains rows and columns just like a real table. The fields in a view are fields from one or more real tables in the database.

* Create View Syntax

```sql
CREATE VIEW view_name AS
SELECT column1, column2, ...
FROM table_name
WHERE condition;
```

* Using View to show the full information of products with Lamaze brand.

```sql
CREATE VIEW HangSanXuat_Lamaze AS
SELECT s.*, h.TenHangSanXuat
FROM SanPham s LEFT JOIN HangSanXuat h ON s.MaHangSanXuat = h.MaHangSanXuat
WHERE h.TenHangSanXuat = "Lamaze";

SELECT * FROM HangSanXuat_Lamaze;
```

* Using View to show the 