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
-------------------------------------------------------------------
SELECT * FROM HangSanXuat_Lamaze;
```

* Edit VIEW to get short information of products

```sql
CREATE OR REPLACE VIEW HangSanXuat_Lamaze AS
SELECT s.MaSanPham, s.TenSanPham, s.GiaSanPham, h.TenHangSanXuat, l.TenLoaiSanPham
FROM SanPham s 
INNER JOIN HangSanXuat h ON s.MaHangSanXuat = h.MaHangSanXuat
INNER JOIN LoaiSanPham l ON s.MaLoaiSanPham = l.MaLoaiSanPham
WHERE h.TenHangSanXuat = "Lamaze";
-------------------------------------------------------------------
SELECT * FROM HangSanXuat_Lamaze;
```
* Drop a View

```sql
DROP VIEW IF EXISTS HangSanXuat_Lamaze;
```