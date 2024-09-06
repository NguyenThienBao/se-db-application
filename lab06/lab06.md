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
    WHERE s.BiXoa = 0
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
    WHERE s.BiXoa = 0
    ORDER BY s.SoLuocXem DESC
    LIMIT 5;
END;

call sp_Lay5SanPhamQuanTam;
```

* Get Products by ID

```sql
CREATE PROCEDURE sp_LaySanPhamTheoID(
    IN MaSanPham INT
)
BEGIN
    SELECT *
    FROM SanPham s 
    LEFT JOIN LoaiSanPham l ON s.MaLoaiSanPham = l.MaLoaiSanPham
    LEFT JOIN HangSanXuat h ON s.MaHangSanXuat = h.MaHangSanXuat
    WHERE s.MaSanPham = MaSanPham
        AND s.BiXoa = 0;
END;

call sp_LaySanPhamTheoID(5);
```

* Get products by Category

```sql
CREATE PROCEDURE sp_LayDanhSachSanPhamTheoLoai(
    IN MaLoaiSanPham INT
)
BEGIN
    SELECT s.*, l.MaLoaiSanPham, h.MaHangSanXuat
    FROM SanPham s 
    LEFT JOIN LoaiSanPham l ON s.MaLoaiSanPham = l.MaLoaiSanPham
    LEFT JOIN HangSanXuat h ON s.MaHangSanXuat = h.MaHangSanXuat
    WHERE l.MaLoaiSanPham = MaLoaiSanPham
        AND s.BiXoa = 0 ;
END;

call sp_LayDanhSachSanPhamTheoLoai(1);
```

* Get products by Brand

```sql
CREATE PROCEDURE sp_LayDanhSachSanPhamTheoHangSanXuat(
    IN MaHangSanXuat INT
)
BEGIN
    SELECT s.*, l.MaLoaiSanPham, h.MaHangSanXuat
    FROM SanPham s 
    LEFT JOIN LoaiSanPham l ON s.MaLoaiSanPham = l.MaLoaiSanPham
    LEFT JOIN HangSanXuat h ON s.MaHangSanXuat = h.MaHangSanXuat
    WHERE h.MaHangSanXuat = MaHangSanXuat
        AND s.BiXoa = 0 ;
END;

call sp_LayDanhSachSanPhamTheoHangSanXuat(1);
```

* Get Products which dont have transaction

```sql
CREATE PROCEDURE sp_LayDanhSachCacTaiKhoanChuaThucHienGiaoDich()
BEGIN
    SET @ds_taikhoan_cogiaodich := (SELECT t.MaTaiKhoan FROM TaiKhoan t INNER JOIN DonDatHang d ON t.MaTaiKhoan = d.MaTaiKhoan WHERE t.BiXoa = 0 GROUP BY t.MaTaiKhoan);
    SELECT * FROM TaiKhoan WHERE MaTaiKhoan NOT IN (@ds_taikhoan_cogiaodich);
END;

call sp_LayDanhSachCacTaiKhoanChuaThucHienGiaoDich;
```

* Add Column "Have" or "Not Have" to Products which (dont) have transaction

```sql
SELECT * FROM DonDatHang;

DROP PROCEDURE IF EXISTS ds_KiemTraGiaoDichTaiKhoan;

CREATE PROCEDURE ds_KiemTraGiaoDichTaiKhoan()
BEGIN
    DECLARE mtk INT;
    DECLARE done INT DEFAULT FALSE;
    --SET @ds_taikhoan_cogiaodich := (SELECT t.MaTaiKhoan FROM TaiKhoan t INNER JOIN DonDatHang d ON t.MaTaiKhoan = d.MaTaiKhoan WHERE t.BiXoa = 0 GROUP BY t.MaTaiKhoan);
    DECLARE curs CURSOR FOR
    SELECT sp.MaSanPham FROM SanPham sp WHERE t.BiXoa = 0;
    DECLARE CONTINUE HANDLER FOR NOT FOUND SET done = TRUE;

    OPEN curs;

        myLoop : LOOP

            FETCH curs INTO mtk;
            SELECT mtk;

            IF done THEN 
                LEAVE myLoop;
            END IF;
    
        END LOOP myLoop;

    CLOSE curs;

END;

call ds_KiemTraGiaoDichTaiKhoan;


```