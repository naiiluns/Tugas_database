# Pemanfaatan AI untuk Normalisasi Database: Panduan Praktis Step by Step

## Daftar Isi

- [Pengenalan](#pengenalan)
- [Apa itu Normalisasi Database?](#apa-itu-normalisasi-database)
- [Langkah-Langkah Praktis Menggunakan AI](#langkah-langkah-praktis-menggunakan-ai)
  - [Langkah 1: Persiapan Data Awal](#langkah-1-persiapan-data-awal)
  - [Langkah 2: Gunakan AI untuk Analisis Struktur Data](#langkah-2-gunakan-ai-untuk-analisis-struktur-data)
  - [Langkah 3: Normalisasi ke Bentuk Normal Pertama (1NF)](#langkah-3-normalisasi-ke-bentuk-normal-pertama-1nf)
  - [Langkah 4: Normalisasi ke Bentuk Normal Kedua (2NF)](#langkah-4-normalisasi-ke-bentuk-normal-kedua-2nf)
  - [Langkah 5: Normalisasi ke Bentuk Normal Ketiga (3NF)](#langkah-5-normalisasi-ke-bentuk-normal-ketiga-3nf)
  - [Langkah 6: Validasi dengan AI](#langkah-6-validasi-dengan-ai)
  - [Langkah 7: Generate SQL Script dengan AI](#langkah-7-generate-sql-script-dengan-ai)
  - [Langkah 8: Migrasi Data](#langkah-8-migrasi-data)
- [Tool AI yang Dapat Digunakan](#tool-ai-yang-dapat-digunakan)
- [Tips Praktis](#tips-praktis)
- [Kesimpulan](#kesimpulan)

---

## Pengenalan

Normalisasi database adalah proses penting dalam desain database untuk mengurangi redundansi data dan meningkatkan integritas data. Dengan kemajuan teknologi AI, proses normalisasi yang sebelumnya memakan waktu kini dapat dilakukan lebih efisien. 

Artikel ini akan memandu Anda langkah demi langkah memanfaatkan AI untuk normalisasi database hingga bentuk normal ketiga (3NF).

---

## Apa itu Normalisasi Database?

Normalisasi adalah teknik desain database yang mengorganisir tabel untuk meminimalkan redundansi dan dependensi data. Terdapat beberapa tingkat normalisasi:

- **1NF (First Normal Form)**: Menghilangkan kelompok berulang dan memastikan setiap kolom berisi nilai atomik
- **2NF (Second Normal Form)**: Memenuhi 1NF dan menghilangkan ketergantungan parsial pada primary key
- **3NF (Third Normal Form)**: Memenuhi 2NF dan menghilangkan ketergantungan transitif

> **Catatan**: Artikel ini fokus pada normalisasi hingga 3NF karena merupakan standar yang paling umum digunakan dalam praktik industri.

---

## Langkah-Langkah Praktis Menggunakan AI

### Langkah 1: Persiapan Data Awal

Mulailah dengan mengidentifikasi tabel yang perlu dinormalisasi. Contoh tabel yang belum dinormalisasi:

**Tabel Penjualan (Tidak Dinormalisasi)**

| ID_Penjualan | Tanggal    | Nama_Pelanggan | Alamat_Pelanggan | Produk        | Harga            | Jumlah |
|--------------|------------|----------------|------------------|---------------|------------------|--------|
| 1            | 2024-01-15 | Ahmad          | Jl. Merdeka 10   | Laptop, Mouse | 15000000, 50000  | 1, 2   |

**Masalah yang terlihat:**
- Kolom Produk, Harga, dan Jumlah berisi multiple values (pelanggaran 1NF)
- Data pelanggan berulang untuk setiap transaksi (redundansi)
- Data produk berulang untuk setiap penjualan (redundansi)

---

### Langkah 2: Gunakan AI untuk Analisis Struktur Data

Manfaatkan AI seperti ChatGPT, Claude, atau tool khusus database untuk menganalisis struktur tabel Anda. 

**Contoh Prompt:**

```text
Analisis tabel berikut dan identifikasi masalah normalisasi:

Tabel Penjualan:
- ID_Penjualan (PK)
- Tanggal
- Nama_Pelanggan
- Alamat_Pelanggan
- Produk (multiple values)
- Harga (multiple values)
- Jumlah (multiple values)

Tolong jelaskan pelanggaran bentuk normal yang terjadi dan berikan rekomendasi perbaikan.
```

**Response AI akan mengidentifikasi:**
- ❌ Nilai multi-nilai dalam satu kolom (pelanggaran 1NF)
- ❌ Ketergantungan parsial (Nama_Pelanggan dan Alamat_Pelanggan bergantung pada pelanggan, bukan transaksi)
- ❌ Ketergantungan transitif (Harga bergantung pada Produk)
- ❌ Redundansi data yang tinggi

---

### Langkah 3: Normalisasi ke Bentuk Normal Pertama (1NF)

**Tujuan**: Pastikan setiap kolom hanya berisi nilai atomik (tidak dapat dibagi lagi).

**Prompt untuk AI:**

```text
Bantu saya mengubah tabel ini ke bentuk normal pertama (1NF). 
Pisahkan nilai-nilai yang berganda dalam kolom Produk, Harga, dan Jumlah.
Berikan struktur tabel baru yang memenuhi 1NF.
```

**Hasil yang diharapkan:**

**Tabel Penjualan (1NF)**

| ID_Penjualan | Tanggal    | Nama_Pelanggan | Alamat_Pelanggan | Produk | Harga    | Jumlah |
|--------------|------------|----------------|------------------|--------|----------|--------|
| 1            | 2024-01-15 | Ahmad          | Jl. Merdeka 10   | Laptop | 15000000 | 1      |
| 1            | 2024-01-15 | Ahmad          | Jl. Merdeka 10   | Mouse  | 50000    | 2      |

**✅ Validasi 1NF:**
- Setiap kolom sekarang hanya berisi satu nilai tunggal
- Tidak ada repeating groups
- Setiap baris dapat diidentifikasi secara unik

**⚠️ Masalah yang masih ada:**
- Data pelanggan masih redundan
- Belum ada primary key yang jelas untuk composite key

---

### Langkah 4: Normalisasi ke Bentuk Normal Kedua (2NF)

**Tujuan**: Hilangkan ketergantungan parsial dengan memisahkan data yang tidak sepenuhnya bergantung pada primary key.

**Prompt untuk AI:**

```text
Identifikasi ketergantungan parsial dalam tabel 1NF saya. 
Bantu pisahkan menjadi beberapa tabel untuk mencapai 2NF.
Sertakan diagram hubungan antar tabel dan foreign key yang diperlukan.
```

**Hasil yang diharapkan:**

#### **Tabel 1: Pelanggan**

| ID_Pelanggan | Nama_Pelanggan | Alamat_Pelanggan |
|--------------|----------------|------------------|
| P001         | Ahmad          | Jl. Merdeka 10   |

#### **Tabel 2: Produk**

| ID_Produk | Nama_Produk | Harga    |
|-----------|-------------|----------|
| 101       | Laptop      | 15000000 |
| 102       | Mouse       | 50000    |

#### **Tabel 3: Transaksi**

| ID_Penjualan | Tanggal    | ID_Pelanggan |
|--------------|------------|--------------|
| 1            | 2024-01-15 | P001         |

#### **Tabel 4: Detail_Penjualan**

| ID_Detail | ID_Penjualan | ID_Produk | Jumlah |
|-----------|--------------|-----------|--------|
| 1         | 1            | 101       | 1      |
| 2         | 1            | 102       | 2      |

**✅ Validasi 2NF:**
- Memenuhi semua persyaratan 1NF
- Tidak ada ketergantungan parsial
- Setiap atribut non-key bergantung sepenuhnya pada primary key

**Diagram Relasi:**

```
Pelanggan (1) ----< Transaksi (M)
Transaksi (1) ----< Detail_Penjualan (M)
Produk (1) ----< Detail_Penjualan (M)
```

---

### Langkah 5: Normalisasi ke Bentuk Normal Ketiga (3NF)

**Tujuan**: Hilangkan ketergantungan transitif (ketika kolom non-key bergantung pada kolom non-key lainnya).

**Prompt untuk AI:**

```text
Periksa apakah ada ketergantungan transitif dalam tabel 2NF saya. 
Jika ada, bantu saya mencapai 3NF dengan memisahkan tabel yang diperlukan.
```

Dalam contoh di atas, struktur sudah memenuhi 3NF karena tidak ada ketergantungan transitif. 

**Contoh Kasus dengan Ketergantungan Transitif:**

**Tabel Karyawan (Sebelum 3NF):**

| ID_Karyawan | Nama  | ID_Departemen | Nama_Departemen | Lokasi_Departemen |
|-------------|-------|---------------|-----------------|-------------------|
| K001        | Budi  | D01           | IT              | Jakarta           |
| K002        | Siti  | D02           | HR              | Bandung           |

**❌ Masalah:**
- Nama_Departemen bergantung pada ID_Departemen (bukan pada ID_Karyawan)
- Lokasi_Departemen bergantung pada ID_Departemen (bukan pada ID_Karyawan)
- Ini adalah ketergantungan transitif: ID_Karyawan → ID_Departemen → Nama_Departemen

**Solusi 3NF:**

#### **Tabel Karyawan (3NF)**

| ID_Karyawan | Nama | ID_Departemen |
|-------------|------|---------------|
| K001        | Budi | D01           |
| K002        | Siti | D02           |

#### **Tabel Departemen (3NF)**

| ID_Departemen | Nama_Departemen | Lokasi_Departemen |
|---------------|-----------------|-------------------|
| D01           | IT              | Jakarta           |
| D02           | HR              | Bandung           |

**✅ Validasi 3NF:**
- Memenuhi semua persyaratan 2NF
- Tidak ada ketergantungan transitif
- Setiap atribut non-key bergantung langsung pada primary key

---

### Langkah 6: Validasi dengan AI

Setelah proses normalisasi selesai, gunakan AI untuk memvalidasi hasil:

**Prompt untuk AI:**

```text
Periksa apakah struktur database berikut sudah memenuhi 3NF:

Tabel Pelanggan:
- ID_Pelanggan (PK)
- Nama_Pelanggan
- Alamat_Pelanggan

Tabel Produk:
- ID_Produk (PK)
- Nama_Produk
- Harga

Tabel Transaksi:
- ID_Penjualan (PK)
- Tanggal
- ID_Pelanggan (FK)

Tabel Detail_Penjualan:
- ID_Detail (PK)
- ID_Penjualan (FK)
- ID_Produk (FK)
- Jumlah

Identifikasi jika masih ada masalah dan berikan saran perbaikan.
```

**Checklist Validasi:**
- ✅ Semua tabel dalam 1NF (nilai atomik)
- ✅ Tidak ada ketergantungan parsial (2NF)
- ✅ Tidak ada ketergantungan transitif (3NF)
- ✅ Foreign key relationships sudah benar
- ✅ Tidak ada redundansi data yang tidak perlu

---

### Langkah 7: Generate SQL Script dengan AI

Minta AI untuk membuat SQL script untuk implementasi:

**Prompt untuk AI:**

```text
Buatkan SQL script lengkap untuk membuat tabel-tabel hasil normalisasi, 
termasuk:
1. CREATE TABLE statements
2. Primary key constraints
3. Foreign key constraints
4. Index yang diperlukan
5. Data type yang sesuai

Gunakan MySQL sebagai DBMS.
```

**Contoh Output:**

```sql
-- =============================================
-- Script Normalisasi Database Penjualan
-- Database: MySQL
-- Versi: 8.0+
-- =============================================

-- Hapus tabel jika sudah ada (hati-hati di production!)
DROP TABLE IF EXISTS Detail_Penjualan;
DROP TABLE IF EXISTS Transaksi;
DROP TABLE IF EXISTS Pelanggan;
DROP TABLE IF EXISTS Produk;

-- =============================================
-- Tabel Master: Pelanggan
-- =============================================
CREATE TABLE Pelanggan (
    ID_Pelanggan VARCHAR(10) PRIMARY KEY,
    Nama_Pelanggan VARCHAR(100) NOT NULL,
    Alamat_Pelanggan TEXT,
    Telepon VARCHAR(15),
    Email VARCHAR(100),
    Tanggal_Daftar TIMESTAMP DEFAULT CURRENT_TIMESTAMP,
    INDEX idx_nama_pelanggan (Nama_Pelanggan)
) ENGINE=InnoDB DEFAULT CHARSET=utf8mb4 COLLATE=utf8mb4_unicode_ci;

-- =============================================
-- Tabel Master: Produk
-- =============================================
CREATE TABLE Produk (
    ID_Produk INT PRIMARY KEY AUTO_INCREMENT,
    Nama_Produk VARCHAR(100) NOT NULL,
    Harga DECIMAL(15,2) NOT NULL CHECK (Harga >= 0),
    Stok INT DEFAULT 0 CHECK (Stok >= 0),
    Kategori VARCHAR(50),
    Deskripsi TEXT,
    INDEX idx_nama_produk (Nama_Produk),
    INDEX idx_kategori (Kategori)
) ENGINE=InnoDB DEFAULT CHARSET=utf8mb4 COLLATE=utf8mb4_unicode_ci;

-- =============================================
-- Tabel Transaksi (Header)
-- =============================================
CREATE TABLE Transaksi (
    ID_Penjualan INT PRIMARY KEY AUTO_INCREMENT,
    Tanggal DATE NOT NULL,
    ID_Pelanggan VARCHAR(10) NOT NULL,
    Total_Harga DECIMAL(15,2) DEFAULT 0,
    Status_Pembayaran ENUM('Pending', 'Lunas', 'Batal') DEFAULT 'Pending',
    Catatan TEXT,
    Created_At TIMESTAMP DEFAULT CURRENT_TIMESTAMP,
    Updated_At TIMESTAMP DEFAULT CURRENT_TIMESTAMP ON UPDATE CURRENT_TIMESTAMP,
    FOREIGN KEY (ID_Pelanggan) REFERENCES Pelanggan(ID_Pelanggan)
        ON DELETE RESTRICT
        ON UPDATE CASCADE,
    INDEX idx_tanggal (Tanggal),
    INDEX idx_pelanggan (ID_Pelanggan),
    INDEX idx_status (Status_Pembayaran)
) ENGINE=InnoDB DEFAULT CHARSET=utf8mb4 COLLATE=utf8mb4_unicode_ci;

-- =============================================
-- Tabel Detail Penjualan (Detail)
-- =============================================
CREATE TABLE Detail_Penjualan (
    ID_Detail INT PRIMARY KEY AUTO_INCREMENT,
    ID_Penjualan INT NOT NULL,
    ID_Produk INT NOT NULL,
    Jumlah INT NOT NULL CHECK (Jumlah > 0),
    Harga_Satuan DECIMAL(15,2) NOT NULL,
    Subtotal DECIMAL(15,2) GENERATED ALWAYS AS (Jumlah * Harga_Satuan) STORED,
    Diskon DECIMAL(5,2) DEFAULT 0 CHECK (Diskon >= 0 AND Diskon <= 100),
    FOREIGN KEY (ID_Penjualan) REFERENCES Transaksi(ID_Penjualan)
        ON DELETE CASCADE
        ON UPDATE CASCADE,
    FOREIGN KEY (ID_Produk) REFERENCES Produk(ID_Produk)
        ON DELETE RESTRICT
        ON UPDATE CASCADE,
    INDEX idx_penjualan (ID_Penjualan),
    INDEX idx_produk (ID_Produk),
    UNIQUE KEY unique_penjualan_produk (ID_Penjualan, ID_Produk)
) ENGINE=InnoDB DEFAULT CHARSET=utf8mb4 COLLATE=utf8mb4_unicode_ci;

-- =============================================
-- Trigger untuk update total harga
-- =============================================
DELIMITER $$

CREATE TRIGGER trg_update_total_after_insert
AFTER INSERT ON Detail_Penjualan
FOR EACH ROW
BEGIN
    UPDATE Transaksi
    SET Total_Harga = (
        SELECT SUM(Subtotal * (1 - Diskon/100))
        FROM Detail_Penjualan
        WHERE ID_Penjualan = NEW.ID_Penjualan
    )
    WHERE ID_Penjualan = NEW.ID_Penjualan;
END$$

CREATE TRIGGER trg_update_total_after_update
AFTER UPDATE ON Detail_Penjualan
FOR EACH ROW
BEGIN
    UPDATE Transaksi
    SET Total_Harga = (
        SELECT SUM(Subtotal * (1 - Diskon/100))
        FROM Detail_Penjualan
        WHERE ID_Penjualan = NEW.ID_Penjualan
    )
    WHERE ID_Penjualan = NEW.ID_Penjualan;
END$$

CREATE TRIGGER trg_update_total_after_delete
AFTER DELETE ON Detail_Penjualan
FOR EACH ROW
BEGIN
    UPDATE Transaksi
    SET Total_Harga = (
        SELECT COALESCE(SUM(Subtotal * (1 - Diskon/100)), 0)
        FROM Detail_Penjualan
        WHERE ID_Penjualan = OLD.ID_Penjualan
    )
    WHERE ID_Penjualan = OLD.ID_Penjualan;
END$$

DELIMITER ;

-- =============================================
-- Insert Sample Data
-- =============================================

-- Data Pelanggan
INSERT INTO Pelanggan (ID_Pelanggan, Nama_Pelanggan, Alamat_Pelanggan, Telepon, Email) VALUES
('P001', 'Ahmad Budiman', 'Jl. Merdeka No. 10, Jakarta', '081234567890', 'ahmad@email.com'),
('P002', 'Siti Nurhaliza', 'Jl. Sudirman No. 25, Bandung', '081234567891', 'siti@email.com'),
('P003', 'Budi Santoso', 'Jl. Gatot Subroto No. 15, Surabaya', '081234567892', 'budi@email.com');

-- Data Produk
INSERT INTO Produk (Nama_Produk, Harga, Stok, Kategori, Deskripsi) VALUES
('Laptop ASUS ROG', 15000000, 10, 'Elektronik', 'Laptop gaming dengan spesifikasi tinggi'),
('Mouse Logitech', 50000, 100, 'Aksesoris', 'Mouse wireless dengan sensor presisi'),
('Keyboard Mechanical', 500000, 50, 'Aksesoris', 'Keyboard mechanical RGB'),
('Monitor LG 27 inch', 3000000, 25, 'Elektronik', 'Monitor IPS Full HD'),
('Webcam HD', 250000, 75, 'Aksesoris', 'Webcam 1080p untuk meeting online');

-- Data Transaksi
INSERT INTO Transaksi (Tanggal, ID_Pelanggan, Status_Pembayaran) VALUES
('2024-01-15', 'P001', 'Lunas'),
('2024-01-16', 'P002', 'Pending'),
('2024-01-17', 'P003', 'Lunas');

-- Data Detail Penjualan
INSERT INTO Detail_Penjualan (ID_Penjualan, ID_Produk, Jumlah, Harga_Satuan, Diskon) VALUES
(1, 1, 1, 15000000, 0),
(1, 2, 2, 50000, 0),
(2, 3, 1, 500000, 10),
(2, 5, 2, 250000, 5),
(3, 4, 1, 3000000, 0),
(3, 2, 3, 50000, 0);

-- =============================================
-- View untuk Reporting
-- =============================================

-- View: Laporan Penjualan Lengkap
CREATE OR REPLACE VIEW v_laporan_penjualan AS
SELECT 
    t.ID_Penjualan,
    t.Tanggal,
    p.Nama_Pelanggan,
    p.Alamat_Pelanggan,
    pr.Nama_Produk,
    d.Jumlah,
    d.Harga_Satuan,
    d.Diskon,
    d.Subtotal,
    (d.Subtotal * (1 - d.Diskon/100)) AS Total_Setelah_Diskon,
    t.Total_Harga AS Total_Transaksi,
    t.Status_Pembayaran
FROM Transaksi t
JOIN Pelanggan p ON t.ID_Pelanggan = p.ID_Pelanggan
JOIN Detail_Penjualan d ON t.ID_Penjualan = d.ID_Penjualan
JOIN Produk pr ON d.ID_Produk = pr.ID_Produk
ORDER BY t.Tanggal DESC, t.ID_Penjualan;

-- View: Summary Penjualan per Pelanggan
CREATE OR REPLACE VIEW v_summary_pelanggan AS
SELECT 
    p.ID_Pelanggan,
    p.Nama_Pelanggan,
    COUNT(DISTINCT t.ID_Penjualan) AS Total_Transaksi,
    SUM(t.Total_Harga) AS Total_Pembelian,
    AVG(t.Total_Harga) AS Rata_rata_Transaksi,
    MAX(t.Tanggal) AS Transaksi_Terakhir
FROM Pelanggan p
LEFT JOIN Transaksi t ON p.ID_Pelanggan = t.ID_Pelanggan
GROUP BY p.ID_Pelanggan, p.Nama_Pelanggan
ORDER BY Total_Pembelian DESC;

-- View: Produk Terlaris
CREATE OR REPLACE VIEW v_produk_terlaris AS
SELECT 
    pr.ID_Produk,
    pr.Nama_Produk,
    pr.Kategori,
    pr.Harga,
    COUNT(d.ID_Detail) AS Jumlah_Transaksi,
    SUM(d.Jumlah) AS Total_Terjual,
    SUM(d.Subtotal) AS Total_Pendapatan
FROM Produk pr
LEFT JOIN Detail_Penjualan d ON pr.ID_Produk = d.ID_Produk
GROUP BY pr.ID_Produk, pr.Nama_Produk, pr.Kategori, pr.Harga
ORDER BY Total_Terjual DESC;

-- =============================================
-- Query Validasi
-- =============================================

-- Cek integritas referential
SELECT 'Pelanggan' AS Tabel, COUNT(*) AS Jumlah FROM Pelanggan
UNION ALL
SELECT 'Produk', COUNT(*) FROM Produk
UNION ALL
SELECT 'Transaksi', COUNT(*) FROM Transaksi
UNION ALL
SELECT 'Detail_Penjualan', COUNT(*) FROM Detail_Penjualan;

-- Cek foreign key yang valid
SELECT 
    'Transaksi -> Pelanggan' AS Relasi,
    COUNT(*) AS Valid
FROM Transaksi t
JOIN Pelanggan p ON t.ID_Pelanggan = p.ID_Pelanggan
UNION ALL
SELECT 
    'Detail -> Transaksi',
    COUNT(*)
FROM Detail_Penjualan d
JOIN Transaksi t ON d.ID_Penjualan = t.ID_Penjualan
UNION ALL
SELECT 
    'Detail -> Produk',
    COUNT(*)
FROM Detail_Penjualan d
JOIN Produk p ON d.ID_Produk = p.ID_Produk;
```

---

### Langkah 8: Migrasi Data

Gunakan AI untuk membuat script migrasi data dari tabel lama ke tabel baru:

**Prompt untuk AI:**

```text
Buatkan script SQL untuk memigrasikan data dari tabel lama yang tidak dinormalisasi 
ke tabel-tabel baru yang sudah dinormalisasi. 
Sertakan:
1. Script untuk backup data lama
2. Script transformasi data
3. Script validasi setelah migrasi
4. Rollback plan jika terjadi error
```

**Contoh Script Migrasi:**

```sql
-- =============================================
-- Script Migrasi Data
-- Dari tabel tidak dinormalisasi ke tabel dinormalisasi
-- =============================================

-- STEP 1: Backup tabel lama
CREATE TABLE Penjualan_Backup AS SELECT * FROM Penjualan_Lama;

-- STEP 2: Buat temporary table untuk parsing data
CREATE TEMPORARY TABLE temp_penjualan AS
SELECT 
    ID_Penjualan,
    Tanggal,
    Nama_Pelanggan,
    Alamat_Pelanggan,
    SUBSTRING_INDEX(SUBSTRING_INDEX(Produk, ',', numbers.n), ',', -1) AS Produk_Item,
    CAST(SUBSTRING_INDEX(SUBSTRING_INDEX(Harga, ',', numbers.n), ',', -1) AS DECIMAL(15,2)) AS Harga_Item,
    CAST(SUBSTRING_INDEX(SUBSTRING_INDEX(Jumlah, ',', numbers.n), ',', -1) AS INT) AS Jumlah_Item,
    numbers.n AS Item_Number
FROM Penjualan_Lama
JOIN (
    SELECT 1 AS n UNION ALL SELECT 2 UNION ALL 
    SELECT 3 UNION ALL SELECT 4 UNION ALL SELECT 5
) numbers
ON CHAR_LENGTH(Penjualan_Lama.Produk) 
   - CHAR_LENGTH(REPLACE(Penjualan_Lama.Produk, ',', '')) >= numbers.n - 1
ORDER BY ID_Penjualan, numbers.n;

-- STEP 3: Migrasi ke tabel Pelanggan
INSERT INTO Pelanggan (ID_Pelanggan, Nama_Pelanggan, Alamat_Pelanggan)
SELECT DISTINCT
    CONCAT('P', LPAD(ROW_NUMBER() OVER (ORDER BY Nama_Pelanggan), 3, '0')) AS ID_Pelanggan,
    Nama_Pelanggan,
    Alamat_Pelanggan
FROM temp_penjualan
WHERE NOT EXISTS (
    SELECT 1 FROM Pelanggan p 
    WHERE p.Nama_Pelanggan = temp_penjualan.Nama_Pelanggan
);

-- STEP 4: Migrasi ke tabel Produk
INSERT INTO Produk (Nama_Produk, Harga)
SELECT DISTINCT
    TRIM(Produk_Item) AS Nama_Produk,
    Harga_Item
FROM temp_penjualan
WHERE NOT EXISTS (
    SELECT 1 FROM Produk pr 
    WHERE pr.Nama_Produk = TRIM(temp_penjualan.Produk_Item)
);

-- STEP 5: Migrasi ke tabel Transaksi
INSERT INTO Transaksi (ID_Penjualan, Tanggal, ID_Pelanggan)
SELECT DISTINCT
    tp.ID_Penjualan,
    tp.Tanggal,
    p.ID_Pelanggan
FROM temp_penjualan tp
JOIN Pelanggan p ON p.Nama_Pelanggan = tp.Nama_Pelanggan;

-- STEP 6: Migrasi ke tabel Detail_Penjualan
INSERT INTO Detail_Penjualan (ID_Penjualan, ID_Produk, Jumlah, Harga_Satuan)
SELECT DISTINCT
    tp.ID_Penjualan,
    pr.ID_Produk,
    tp.Jumlah_Item,
    tp.Harga_Item
FROM temp_penjualan tp
JOIN Produk pr ON pr.Nama_Produk = TRIM(tp.Produk_Item);

-- STEP 7: Validasi hasil migrasi
SELECT 
    'Data Comparison' AS Check_Type,
    (SELECT COUNT(*) FROM Penjualan_Lama) AS Old_Table_Rows,
    (SELECT COUNT(*) FROM Transaksi) AS New_Transaksi_Rows,
    (SELECT COUNT(*) FROM Detail_Penjualan) AS New_Detail_Rows;

-- STEP 8: Validasi total harga
SELECT 
    'Price Validation' AS Check_Type,
    (SELECT SUM(Harga * Jumlah) FROM temp_penjualan) AS Old_Total,
    (SELECT SUM(Total_Harga) FROM Transaksi) AS New_Total,
    (SELECT SUM(Subtotal) FROM Detail_Penjualan) AS Detail_Total;

-- STEP 9: Cleanup temporary table
DROP TEMPORARY TABLE IF EXISTS temp_penjualan;

-- =============================================
-- Rollback Plan (jika diperlukan)
-- =============================================
/*
-- Untuk rollback, jalankan script berikut:

TRUNCATE TABLE Detail_Penjualan;
TRUNCATE TABLE Transaksi;
TRUNCATE TABLE Pelanggan;
TRUNCATE TABLE Produk;

-- Restore dari backup
INSERT INTO Penjualan_Lama SELECT * FROM Penjualan_Backup;

-- Hapus backup setelah yakin migrasi sukses
DROP TABLE Penjualan_Backup;
*/
```

**Script Validasi Post-Migration:**

```sql
-- =============================================
-- Validasi Komprehensif Setelah Migrasi
-- =============================================

-- 1. Validasi jumlah record
SELECT 'Record Count Validation' AS Test;
SELECT 
    'Pelanggan' AS Tabel, 
    COUNT(*) AS Jumlah,
    'OK' AS Status
FROM Pelanggan
UNION ALL
SELECT 'Produk', COUNT(*), 
    CASE WHEN COUNT(*) > 0 THEN 'OK' ELSE 'ERROR' END
FROM Produk
UNION ALL
SELECT 'Transaksi', COUNT(*), 
    CASE WHEN COUNT(*) > 0 THEN 'OK' ELSE 'ERROR' END
FROM Transaksi
UNION ALL
SELECT 'Detail_Penjualan', COUNT(*), 
    CASE WHEN COUNT(*) > 0 THEN 'OK' ELSE 'ERROR' END
FROM Detail_Penjualan;

-- 2. Validasi referential integrity
SELECT 'Referential Integrity Check' AS Test;
SELECT 
    t.ID_Penjualan,
    t.ID_Pelanggan,
    CASE 
        WHEN p.ID_Pelanggan IS NULL THEN 'ERROR: Pelanggan tidak ditemukan'
        ELSE 'OK'
    END AS Status
FROM Transaksi t
LEFT JOIN Pelanggan p ON t.ID_Pelanggan = p.ID_Pelanggan
WHERE p.ID_Pelanggan IS NULL;

-- 3. Validasi data integrity (tidak ada null di kolom wajib)
SELECT 'Data Integrity Check' AS Test;
SELECT 
    'Pelanggan' AS Tabel,
    COUNT(*) AS Null_Count,
    'Nama_Pelanggan' AS Kolom
FROM Pelanggan
WHERE Nama_Pelanggan IS NULL OR Nama_Pelanggan = ''
UNION ALL
SELECT 'Produk', COUNT(*), 'Nama_Produk'
FROM Produk
WHERE Nama_Produk IS NULL OR Nama_Produk = ''
UNION ALL
SELECT 'Produk', COUNT(*), 'Harga'
FROM Produk
WHERE Harga IS NULL OR Harga < 0;

-- 4. Validasi perhitungan total
SELECT 'Total Calculation Check' AS Test;
SELECT 
    t.ID_Penjualan,
    t.Total_Harga AS Total_di_Header,
    SUM(d.Subtotal * (1 - d.Diskon/100)) AS Total_dari_Detail,
    CASE 
        WHEN ABS(t.Total_Harga - SUM(d.Subtotal * (1 - d.Diskon/100))) < 0.01 
        THEN 'OK' 
        ELSE 'ERROR: Selisih perhitungan'
    END AS Status
FROM Transaksi t
JOIN Detail_Penjualan d ON t.ID_Penjualan = d.ID_Penjualan
GROUP BY t.ID_Penjualan, t.Total_Harga;

-- 5. Validasi duplikasi data
SELECT 'Duplicate Check' AS Test;
SELECT 
    'Pelanggan' AS Tabel,
    Nama_Pelanggan,
    COUNT(*) AS Jumlah_Duplikat
FROM Pelanggan
GROUP BY Nama_Pelanggan, Alamat_Pelanggan
HAVING COUNT(*) > 1
UNION ALL
SELECT 
    'Produk',
    Nama_Produk,
    COUNT(*)
FROM Produk
GROUP BY Nama_Produk
HAVING COUNT(*) > 1;
```

---

## Tool AI yang Dapat Digunakan

### 1. **Large Language Models (LLM)**

#### **ChatGPT / Claude / Gemini**
- **Kegunaan**: Analisis struktur database, konsultasi desain, generate SQL script
- **Kelebihan**: 
  - Pemahaman konteks yang baik
  - Dapat menjelaskan konsep dengan detail
  - Generate code dengan berbagai variasi
- **Cara Penggunaan**:
  ```text
  Tanya jawab langsung tentang desain database
  Request generate script SQL
  Minta review dan saran perbaikan
  ```

### 2. **Database-Specific AI Tools**

#### **DataGrip AI Assistant**
- **Kegunaan**: Code completion, query optimization, schema suggestion
- **Kelebihan**: Terintegrasi langsung dengan IDE
- **Website**: https://www.jetbrains.com/datagrip/

#### **SQL AI Tools**
- **AI2SQL**: Konversi natural language ke SQL
- **Text2SQL**: Generate query dari deskripsi
- **QueryPie**: Kolaborasi dan AI-powered query builder

### 3. **Database Modeling Tools dengan AI**

#### **dbdiagram.io**
- **Kegunaan**: Visualisasi ERD dengan text-to-diagram
- **Kelebihan**: Syntax sederhana, real-time preview
- **Website**: https://dbdiagram.io/

#### **ERDPlus**
- **Kegunaan**: Membuat ER Diagram dengan AI suggestions
- **Website**: https://erdplus.com/

#### **Lucidchart**
- **Kegunaan**: Diagramming dengan AI-powered suggestions
- **Website**: https://www.lucidchart.com/

### 4. **Code Generation & Analysis**

#### **GitHub Copilot**
- **Kegunaan**: Auto-complete SQL queries, generate table structure
- **Kelebihan**: Context-aware suggestions
- **Website**: https://github.com/features/copilot

#### **Tabnine**
- **Kegunaan**: AI code completion untuk SQL dan berbagai bahasa
- **Website**: https://www.tabnine.com/

### 5. **Database Documentation & Analysis**

#### **Dataedo**
- **Kegunaan**: Automatic database documentation, data lineage
- **Kelebihan**: AI-powered column description generation
- **Website**: https://dataedo.com/

#### **SchemaSpy**
- **Kegunaan**: Automatic database schema documentation
- **Website**: https://schemaspy.org/

### 6. **Specialized Normalization Tools**

#### **Vertabelo**
- **Kegunaan**: Database modeling dengan normalization checker
- **Website**: https://vertabelo.com/

#### **SQL Server Data Tools (SSDT)**
- **Kegunaan**: Built-in analysis untuk Microsoft SQL Server
- **Kelebihan**: Integrated dengan Visual Studio

### 7. **Online Normalization Validators**

#### **Normalization Checker Tools**
- **FD Analyzer**: Analyze functional dependencies
- **Normal Form Checker**: Validate normalization level
- **3NF Converter**: Online tool untuk konversi ke 3NF

---

## Tips Praktis

### 1. **Persiapan Sebelum Normalisasi**

#### ✅ **Do's:**
- Dokumentasikan struktur tabel existing dengan lengkap
- Backup seluruh database sebelum melakukan perubahan
- Identifikasi semua functional dependencies
- Buat ERD (Entity Relationship Diagram) dari struktur saat ini
- Catat semua business rules yang berlaku

#### ❌ **Don'ts:**
- Jangan langsung melakukan perubahan di production database
- Jangan skip tahap analisis untuk langsung ke implementasi
- Jangan abaikan konsultasi dengan stakeholder

### 2. **Saat Menggunakan AI**

#### ✅ **Best Practices:**
- **Berikan konteks lengkap**: Jelaskan business case dan requirement
- **Iterasi bertahap**: Normalisasi step by step (1NF → 2NF → 3NF)
- **Validasi setiap output**: Jangan blind trust pada hasil AI
- **Simpan conversation history**: Untuk reference dan audit trail
- **Test dengan sample data**: Validasi script dengan data dummy terlebih dahulu

#### ❌ **Common Mistakes:**
- Over-reliance pada AI tanpa pemahaman konsep dasar
- Tidak memvalidasi hasil generate code
- Menggunakan prompt yang terlalu general atau ambigu
- Skip testing dan langsung deploy ke production

### 3. **Manajemen Perubahan**

#### **Change Management Checklist:**
```markdown
[ ] Analisis impact terhadap aplikasi existing
[ ] Update dokumentasi database
[ ] Modify aplikasi code yang terpengaruh
[ ] Update stored procedures dan views
[ ] Testing menyeluruh di development environment
[ ] User Acceptance Testing (UAT)
[ ] Persiapan rollback plan
[ ] Schedule maintenance window
[ ] Backup database sebelum deployment
[ ] Execute migration script
[ ] Validasi post-deployment
[ ] Monitoring performa setelah deployment
```

### 4. **Performance Testing**

#### **Query Performance Comparison:**
```sql
-- Test query speed sebelum dan sesudah normalisasi

-- Enable query profiling
SET profiling = 1;

-- Jalankan query test
SELECT * FROM v_laporan_penjualan WHERE Tanggal BETWEEN '2024-01-01' AND '2024-12-31';

-- Lihat hasil profiling
SHOW PROFILES;

-- Detail breakdown
SHOW PROFILE FOR QUERY 1;
```

#### **Index Optimization:**
```sql
-- Analyze query execution plan
EXPLAIN SELECT 
    p.Nama_Pelanggan,
    SUM(t.Total_Harga) AS Total
FROM Pelanggan p
JOIN Transaksi t ON p.ID_Pelanggan = t.ID_Pelanggan
GROUP BY p.ID_Pelanggan;

-- Create index jika diperlukan
CREATE INDEX idx_pelanggan_transaksi ON Transaksi(ID_Pelanggan, Total_Harga);
```

### 5. **Dokumentasi**

#### **Template Dokumentasi Normalisasi:**

```markdown
# Dokumentasi Normalisasi Database

## Informasi Proyek
- **Nama Database**: [nama_database]
- **Tanggal Normalisasi**: [tanggal]
- **PIC**: [nama_pic]
- **Tools yang Digunakan**: [list tools]

## Struktur Sebelum Normalisasi
[Deskripsi dan diagram]

## Analisis Masalah
1. Pelanggaran 1NF: [detail]
2. Pelanggaran 2NF: [detail]
3. Pelanggaran 3NF: [detail]

## Struktur Setelah Normalisasi
[Deskripsi dan diagram]

## Perubahan yang Dilakukan
- Tabel yang ditambahkan: [list]
- Tabel yang dimodifikasi: [list]
- Tabel yang dihapus: [list]

## Script SQL
[Link ke file SQL]

## Testing & Validasi
- [x] Unit testing
- [x] Integration testing
- [x] Performance testing
- [x] UAT

## Rollback Plan
[Prosedur rollback]

## Lessons Learned
[Catatan dan pembelajaran]
```

### 6. **Security Considerations**

```sql
-- Buat user dengan privilege terbatas untuk aplikasi
CREATE USER 'app_user'@'localhost' IDENTIFIED BY 'secure_password';

-- Grant hanya permission yang diperlukan
GRANT SELECT, INSERT, UPDATE ON database_name.* TO 'app_user'@'localhost';

-- Untuk reporting, buat user read-only
CREATE USER 'report_user'@'localhost' IDENTIFIED BY 'secure_password';
GRANT SELECT ON database_name.* TO 'report_user'@'localhost';

-- Enable audit logging
SET GLOBAL general_log = 'ON';
SET GLOBAL log_output = 'TABLE';
```

### 7. **Monitoring & Maintenance**

#### **Setup Monitoring:**
```sql
-- Monitor table size
SELECT 
    table_name AS 'Table',
    ROUND(((data_length + index_length) / 1024 / 1024), 2) AS 'Size (MB)'
FROM information_schema.TABLES
WHERE table_schema = 'database_name'
ORDER BY (data_length + index_length) DESC;

-- Monitor slow queries
SET GLOBAL slow_query_log = 'ON';
SET GLOBAL long_query_time = 2; -- queries lebih dari 2 detik
SET GLOBAL slow_query_log_file = '/var/log/mysql/slow-query.log';

-- Check index usage
SELECT 
    table_schema,
    table_name,
    index_name,
    seq_in_index,
    column_name
FROM information_schema.statistics
WHERE table_schema = 'database_name'
ORDER BY table_name, index_name, seq_in_index;
```

### 8. **Troubleshooting Common Issues**

#### **Issue 1: Foreign Key Constraint Error**
```sql
-- Disable foreign key checks sementara (hati-hati!)
SET FOREIGN_KEY_CHECKS = 0;

-- Lakukan operasi yang diperlukan
-- ...

-- Enable kembali
SET FOREIGN_KEY_CHECKS = 1;
```

#### **Issue 2: Data Migration Error**
```sql
-- Check orphaned records
SELECT t.ID_Penjualan, t.ID_Pelanggan
FROM Transaksi t
LEFT JOIN Pelanggan p ON t.ID_Pelanggan = p.ID_Pelanggan
WHERE p.ID_Pelanggan IS NULL;

-- Fix orphaned records
DELETE FROM Transaksi
WHERE ID_Pelanggan NOT IN (SELECT ID_Pelanggan FROM Pelanggan);
```

#### **Issue 3: Performance Degradation**
```sql
-- Analyze and optimize tables
ANALYZE TABLE Pelanggan, Produk, Transaksi, Detail_Penjualan;
OPTIMIZE TABLE Pelanggan, Produk, Transaksi, Detail_Penjualan;

-- Update table statistics
ANALYZE TABLE table_name UPDATE HISTOGRAM ON column_name;
```

---

## Kesimpulan

Pemanfaatan AI dalam proses normalisasi database membawa banyak keuntungan:

### **Keuntungan Menggunakan AI:**

1. ⚡ **Efisiensi Waktu**
   - Proses analisis yang biasanya memakan waktu berjam-jam dapat diselesaikan dalam hitungan menit
   - Auto-generation SQL script menghemat waktu coding

2. 🎯 **Akurasi Tinggi**
   - AI dapat mendeteksi anomali dan pelanggaran normalisasi yang mungkin terlewat
   - Konsistensi dalam penerapan best practices

3. 📚 **Pembelajaran**
   - AI dapat menjelaskan konsep dengan berbagai cara
   - Memberikan contoh dan alternatif solusi

4. 🔄 **Iterasi Cepat**
   - Mudah untuk mencoba berbagai pendekatan
   - Cepat dalam melakukan revisi dan perbaikan

### **Catatan Penting:**

⚠️ **AI adalah ALAT BANTU, bukan pengganti:**
- Tetap perlukan pemahaman fundamental tentang normalisasi database
- Validasi manual tetap diperlukan untuk memastikan akurasi
- Business logic dan requirement hanya bisa dipahami oleh manusia
- Keputusan akhir tentang desain database harus melibatkan expertise manusia

### **Best Practices Summary:**

```plaintext
1. Pahami konsep dasar normalisasi (1NF, 2NF, 3NF)
2. Gunakan AI untuk analisis dan generate code
3. SELALU validasi hasil output AI
4. Test menyeluruh sebelum production deployment
5. Dokumentasikan setiap perubahan
6. Prepare rollback plan
7. Monitor performance post-deployment
8. Iterate dan improve based on feedback
```

### **Next Steps:**

Setelah menguasai normalisasi hingga 3NF, Anda dapat mempelajari:
- **BCNF (Boyce-Codd Normal Form)**: Untuk kasus-kasus khusus
- **4NF & 5NF**: Untuk database yang lebih kompleks
- **Denormalization**: Kapan dan bagaimana melakukan denormalisasi untuk optimasi
- **Database Indexing Strategies**: Optimasi performa query
- **Database Sharding**: Untuk scalability di level enterprise

### **Resources untuk Belajar Lebih Lanjut:**

📖 **Buku Rekomendasi:**
- "Database Design and Normalization" - Dennis Shasha & Philippe Bonnet
- "Database Systems: The Complete Book" - Hector Garcia-Molina

🎓 **Online Courses:**
- Coursera: Database Management Essentials
- Udemy: The Complete Database Design & Modeling Beginners Tutorial
- edX: Databases: Modeling and Theory

🔗 **Dokumentasi & Tutorial:**
- MySQL Official Documentation: https://dev.mysql.com/doc/
- PostgreSQL Documentation: https://www.postgresql.org/docs/
- W3Schools SQL Tutorial: https://www.w3schools.com/sql/

💬 **Community & Forum:**
- Stack Overflow: Tag [database-normalization]
- Reddit: r/Database
- DBA Stack Exchange: https://dba.stackexchange.com/

---

## Lampiran

### A. Glossary

**Terminologi Database:**

- **Atomik**: Nilai yang tidak dapat dibagi lagi menjadi bagian yang lebih kecil
- **Candidate Key**: Minimal set of attributes yang dapat uniquely identify setiap tuple
- **Composite Key**: Primary key yang terdiri dari 2 atau lebih kolom
- **Dependency (Ketergantungan)**: Relasi antara attributes dalam sebuah tabel
- **Denormalization**: Proses menggabungkan tabel untuk optimasi performa
- **Entity**: Objek atau konsep yang dapat diidentifikasi secara unik
- **Foreign Key**: Kolom yang mereferensikan primary key di tabel lain
- **Functional Dependency**: X → Y, dimana nilai X menentukan nilai Y
- **Primary Key**: Unique identifier untuk setiap record dalam tabel
- **Redundancy**: Data yang tersimpan berulang-ulang
- **Referential Integrity**: Aturan yang memastikan foreign key valid
- **Transitive Dependency**: A → B dan B → C, maka A → C

### B. Cheat Sheet: Normalization Rules

```plaintext
╔════════════════════════════════════════════════════════════╗
║                    NORMALIZATION RULES                      ║
╠════════════════════════════════════════════════════════════╣
║ 1NF (First Normal Form)                                    ║
║ ├─ Each column contains atomic values                      ║
║ ├─ Each column contains values of single type             ║
║ ├─ Each column has unique name                            ║
║ └─ No repeating groups or arrays                          ║
║                                                            ║
║ 2NF (Second Normal Form)                                   ║
║ ├─ Must be in 1NF                                         ║
║ └─ All non-key attributes fully dependent on PK           ║
║    (No partial dependencies)                              ║
║                                                            ║
║ 3NF (Third Normal Form)                                    ║
║ ├─ Must be in 2NF                                         ║
║ └─ No transitive dependencies                             ║
║    (Non-key attributes depend only on PK)                 ║
║                                                            ║
║ BCNF (Boyce-Codd Normal Form)                             ║
║ ├─ Must be in 3NF                                         ║
║ └─ Every determinant must be a candidate key              ║
╚════════════════════════════════════════════════════════════╝
```

### C. Common Prompt Templates

**Template 1: Analisis Tabel**
```text
Analisis tabel database berikut:

Nama Tabel: [nama_tabel]
Kolom:
- [kolom1]: [tipe_data] [constraint]
- [kolom2]: [tipe_data] [constraint]
...

Primary Key: [pk]
Sample Data: [paste sample data]

Tolong identifikasi:
1. Bentuk normal saat ini (1NF/2NF/3NF)
2. Pelanggaran normalisasi yang terjadi
3. Functional dependencies
4. Rekomendasi perbaikan untuk mencapai 3NF
```

**Template 2: Generate SQL Script**
```text
Buatkan SQL script lengkap untuk struktur database dinormalisasi berikut:

Tabel-tabel:
1. [nama_tabel1]
   - Kolom: [list kolom dengan tipe data]
   - Primary Key: [pk]
   - Foreign Key: [fk jika ada]

2. [nama_tabel2]
   ...

Requirements:
- Gunakan [MySQL/PostgreSQL/SQL Server]
- Include constraints (NOT NULL, UNIQUE, CHECK)
- Include indexes untuk optimization
- Include sample data INSERT statements
- Include basic views untuk reporting
```

**Template 3: Migrasi Data**
```text
Buatkan script migrasi data dari struktur lama ke struktur baru:

Struktur Lama:
[paste struktur tabel lama]

Struktur Baru:
[paste struktur tabel baru]

Include:
1. Backup script
2. Data transformation logic
3. Validation queries
4. Rollback plan
```

---

## Penutup

Normalisasi database adalah fundamental skill yang harus dikuasai setiap database designer dan developer. Dengan memanfaatkan AI sebagai assistant, proses yang kompleks ini menjadi lebih mudah dan efisien.

## Bukti Absensi 
![bukti absensi workshop](/Session%203/Image/absensi%20workshop.png) 