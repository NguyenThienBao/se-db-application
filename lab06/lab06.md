# Advanced Stored Procedure

## 1 - Configure database for Website Babyshop

* Import SQL Script file ***db_babyshop*** to create the database.

## 2 - Advanced Stored Procedure

* Get all products.

```sql
CREATE PROCEDURE sp_LayTatCaSanPham()
BEGIN
    SELECT *
    FROM SanPham s 
    LEFT JOIN LoaiSanPham l ON s.MaLoaiSanPham = l.MaLoaiSanPham
    LEFT JOIN HangSanXuat h ON s.MaHangSanXuat = h.MaHangSanXuat
    ORDER BY s.MaSanPham;
END;

call sp_LayTatCaSanPham;
```

* Get 5 Newest Products.

```sql
CREATE PROCEDURE sp_Lay5SanPhamMoiNhat()
BEGIN
    SELECT *
    FROM SanPham s 
    LEFT JOIN LoaiSanPham l ON s.MaLoaiSanPham = l.MaLoaiSanPham
    LEFT JOIN HangSanXuat h ON s.MaHangSanXuat = h.MaHangSanXuat
    ORDER BY s.NgayNhap DESC
    LIMIT 5;
END;

call sp_Lay5SanPhamMoiNhat;
```

* Get 5 Hottest products.

```sql
CREATE PROCEDURE sp_Lay5SanPhamQuanTam()
BEGIN
    SELECT *
    FROM SanPham s 
    LEFT JOIN LoaiSanPham l ON s.MaLoaiSanPham = l.MaLoaiSanPham
    LEFT JOIN HangSanXuat h ON s.MaHangSanXuat = h.MaHangSanXuat
    ORDER BY s.SoLuocXem DESC
    LIMIT 5;
END;

call sp_Lay5SanPhamQuanTam;
```