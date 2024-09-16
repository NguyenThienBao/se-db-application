# View in MySQL 

## 1 - Basic Syntax

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

## 2 - Advance VIEW implementation

* Cannot create View with parameters because view is stored static data after execute query

* Example: create a view to count the numbers of product

```sql
CREATE VIEW v_DemTongDonDatHang AS
SELECT COUNT(MaDonDatHang) AS Total
FROM DonDatHang;

SELECT * FROM v_DemTongDonDatHang;
```

* Select first-time is 8 orders

```sql
SELECT * FROM v_DemTongDonDatHang;
```

* After that, we create new order 

```sql
INSERT INTO DonDatHang(MaDonDatHang, NgayLap, TongThanhTien, MaTaiKhoan, MaTinhTrang) 
VALUES ('131216001', NOW(), 999, 1, 1);
```

* Then select the second time result is 9 orders. So the view is auto update when there are new changes within the table.

```sql
SELECT * FROM v_DemTongDonDatHang;
```

* Now we use View for caching common data such as:

    * Show top 5 lastest products with view "v_product_lastest"
    * Show top 5 best seller products with view "v_product_best_seller"
    * Show top 5 hottest products with view "v_product_hottest"

```sql
CREATE OR REPLACE VIEW v_product_lastest AS
SELECT s.*
FROM SanPham s
ORDER BY s.NgayNhap DESC
LIMIT 5;
----------------------------------------------
CREATE OR REPLACE VIEW v_product_best_seller AS
SELECT s.*
FROM SanPham s
ORDER BY s.SoLuongBan DESC
LIMIT 5;
----------------------------------------------
CREATE OR REPLACE VIEW v_product_hottest AS
SELECT s.*
FROM SanPham s
ORDER BY s.SoLuocXem DESC
LIMIT 5;
```