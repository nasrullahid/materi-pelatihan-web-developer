# MODUL AJAR — HARI 6
## Database & SQL (MySQL)

*Bagian dari Pelatihan Web Programmer Dasar — Berbasis Laravel (15 Hari)*

---

## INFORMASI SESI

| Item | Keterangan |
|---|---|
| **Hari** | 6 dari 15 |
| **Fase** | Fase 2 — Jembatan Backend (penutup) |
| **Topik** | Menyimpan & mengelola data dengan database relasional |
| **Durasi** | 8 jam |
| **Prasyarat** | Hari 4–5 (PHP & OOP) |
| **Output** | Skema database (produk & kategori) + kumpulan query CRUD yang berfungsi |

### Tujuan Pembelajaran
Setelah menyelesaikan hari ini, peserta mampu:
1. Menjelaskan konsep RDBMS (tabel, kolom, baris, primary key, foreign key).
2. Membuat database dan tabel dengan `CREATE TABLE`.
3. Menjalankan operasi CRUD SQL: `INSERT`, `SELECT`, `UPDATE`, `DELETE`.
4. Menyaring, mengurutkan, dan membatasi data (`WHERE`, `ORDER BY`, `LIMIT`).
5. Meringkas data dengan agregasi (`COUNT`, `SUM`, `GROUP BY`).
6. Menghubungkan tabel dengan foreign key dan menggabungkannya dengan `JOIN`.

### Alat & Bahan
- Laragon/XAMPP dengan **MySQL** aktif
- **phpMyAdmin** (buka `http://localhost/phpmyadmin`) atau DBeaver
- VS Code untuk menyimpan skrip SQL

---

## PETA WAKTU HARI INI

| Waktu | Sesi | Fokus |
|---|---|---|
| 08.00–10.00 | Sesi 1 — Konsep | Konsep database & membuat tabel |
| 10.00–10.15 | Istirahat | |
| 10.15–12.00 | Sesi 2 — Lab | CRUD dengan SQL |
| 12.00–13.00 | ISHOMA | |
| 13.00–15.00 | Sesi 3 — Lab | Query lanjutan & agregasi |
| 15.00–15.15 | Istirahat | |
| 15.15–16.30 | Sesi 4 — Mini-project | Relasi, JOIN, skema aplikasi |
| 16.30–17.00 | Sesi 5 — Review | Evaluasi & jembatan Hari 7 |

---

# SESI 1 — KONSEP DATABASE (08.00–10.00)

> **Metode:** ceramah + guided di phpMyAdmin. Kaitkan dengan keluhan hari-hari sebelumnya: data To-Do (Hari 3) dan produk (Hari 5) hilang saat program ditutup.

### 1.1 Kenapa perlu database?
Sampai kemarin, semua data kita **hilang** begitu program selesai — karena hanya tersimpan di memori. **Database** menyimpan data secara **permanen**, terstruktur, dan bisa diakses berulang.

### 1.2 Konsep RDBMS
**RDBMS** (Relational Database Management System) seperti MySQL menyimpan data dalam **tabel** — mirip spreadsheet, tapi jauh lebih kuat.
| Istilah | Arti |
|---|---|
| **database** | wadah besar berisi banyak tabel |
| **tabel** | kumpulan data sejenis (mis. tabel `produk`) |
| **kolom (field)** | jenis data (mis. `nama`, `harga`) |
| **baris (record)** | satu data utuh (mis. satu produk) |
| **primary key** | penanda unik tiap baris (biasanya `id`) |
| **foreign key** | kolom yang menghubungkan ke tabel lain |

Contoh tabel `produk`:
| id (PK) | nama | harga | stok |
|---|---|---|---|
| 1 | Buku | 50000 | 10 |
| 2 | Pulpen | 5000 | 100 |

### 1.3 Membuat database & tabel (phpMyAdmin)
1. Buka `http://localhost/phpmyadmin`.
2. Buat database baru, mis. `toko`.
3. Jalankan SQL di tab **SQL**:
```sql
CREATE TABLE produk (
    id INT AUTO_INCREMENT PRIMARY KEY,
    nama VARCHAR(100),
    harga INT,
    stok INT
);
```
| Bagian | Arti |
|---|---|
| `INT` | tipe angka bulat |
| `VARCHAR(100)` | teks maksimal 100 karakter |
| `AUTO_INCREMENT` | `id` bertambah otomatis tiap baris baru |
| `PRIMARY KEY` | menandai kolom `id` sebagai penanda unik |

### 🔨 Latihan 1 (25 menit)
1. Buat database `toko`.
2. Buat tabel `pelanggan` (id, nama, email, kota).
3. Perhatikan struktur tabel di phpMyAdmin (tab **Structure**).

**Kunci (untuk instruktur):**
```sql
CREATE TABLE pelanggan (
    id INT AUTO_INCREMENT PRIMARY KEY,
    nama VARCHAR(100),
    email VARCHAR(100),
    kota VARCHAR(50)
);
```

### ✅ Cek pemahaman Sesi 1
1. Apa beda kolom dan baris?
2. Apa fungsi primary key?
3. Kenapa data di database tidak hilang saat program ditutup?

---

# SESI 2 — CRUD DENGAN SQL (10.15–12.00)

> **Metode:** demo + lab. CRUD = Create, Read, Update, Delete — inti semua aplikasi.

### 2.1 INSERT — menambah data (Create)
```sql
INSERT INTO produk (nama, harga, stok)
VALUES ('Buku', 50000, 10);

INSERT INTO produk (nama, harga, stok)
VALUES ('Pulpen', 5000, 100);
```
> Teks selalu diapit **tanda kutip tunggal** `'...'`. Angka tidak perlu.

### 2.2 SELECT — membaca data (Read)
```sql
SELECT * FROM produk;                 -- semua kolom, semua baris
SELECT nama, harga FROM produk;       -- kolom tertentu saja
```
`*` berarti "semua kolom".

### 2.3 UPDATE — mengubah data
```sql
UPDATE produk
SET harga = 55000
WHERE id = 1;
```

### 2.4 DELETE — menghapus data
```sql
DELETE FROM produk WHERE id = 2;
```

> ⚠️ **Peringatan penting:** `UPDATE` atau `DELETE` **tanpa `WHERE`** akan mengubah/menghapus **SELURUH** baris. Selalu pastikan `WHERE`-nya benar sebelum menjalankan.

### 🔨 Latihan 2 (30 menit)
Pada tabel `produk`:
1. Tambahkan 3 produk dengan `INSERT`.
2. Tampilkan semua produk.
3. Ubah harga salah satu produk.
4. Hapus satu produk berdasarkan id.

**Kunci (untuk instruktur):**
```sql
INSERT INTO produk (nama, harga, stok) VALUES ('Tas', 150000, 4);
INSERT INTO produk (nama, harga, stok) VALUES ('Topi', 35000, 20);
INSERT INTO produk (nama, harga, stok) VALUES ('Sepatu', 250000, 8);

SELECT * FROM produk;

UPDATE produk SET harga = 40000 WHERE nama = 'Topi';

DELETE FROM produk WHERE id = 1;
```

---

# SESI 3 — QUERY LANJUTAN & AGREGASI (13.00–15.00)

### 3.1 WHERE — menyaring
```sql
SELECT * FROM produk WHERE harga > 10000;
SELECT * FROM produk WHERE stok < 5;
SELECT * FROM produk WHERE nama = 'Buku';
```

### 3.2 ORDER BY — mengurutkan
```sql
SELECT * FROM produk ORDER BY harga ASC;    -- kecil ke besar
SELECT * FROM produk ORDER BY harga DESC;   -- besar ke kecil
```

### 3.3 LIMIT — membatasi
```sql
SELECT * FROM produk ORDER BY harga DESC LIMIT 3;   -- 3 termahal
```

### 3.4 Agregasi — meringkas data
```sql
SELECT COUNT(*) FROM produk;        -- jumlah baris
SELECT SUM(stok) FROM produk;       -- total stok
SELECT AVG(harga) FROM produk;      -- rata-rata harga
SELECT MAX(harga) FROM produk;      -- harga tertinggi
```

### 3.5 GROUP BY — mengelompokkan
```sql
SELECT kategori_id, COUNT(*) AS jumlah
FROM produk
GROUP BY kategori_id;
```
`GROUP BY` mengelompokkan baris yang punya nilai sama, lalu agregasi dihitung per kelompok. `AS` memberi nama kolom hasil.

### 🔨 Latihan 3 (40 menit)
1. Tampilkan produk dengan stok di bawah 10.
2. Tampilkan 3 produk termahal.
3. Hitung total nilai stok seluruh produk (petunjuk: belum bisa langsung — hitung `SUM(stok)` dan `COUNT(*)` dulu).

**Kunci (untuk instruktur):**
```sql
SELECT * FROM produk WHERE stok < 10;

SELECT * FROM produk ORDER BY harga DESC LIMIT 3;

SELECT COUNT(*) AS jumlah_produk, SUM(stok) AS total_stok
FROM produk;
```

---

# SESI 4 — RELASI, JOIN & MINI-PROJECT (15.15–16.30)

> **Metode:** konsep relasi, lalu kerja mandiri merancang skema. Menghasilkan **output resmi Hari 6**.

### 4.1 Kenapa relasi?
Menyimpan nama kategori berulang di tiap produk itu boros dan rawan salah. Lebih baik: pisahkan kategori ke tabelnya sendiri, lalu **hubungkan** dengan foreign key.

### 4.2 Foreign key
```sql
CREATE TABLE kategori (
    id INT AUTO_INCREMENT PRIMARY KEY,
    nama VARCHAR(100)
);

CREATE TABLE produk (
    id INT AUTO_INCREMENT PRIMARY KEY,
    nama VARCHAR(100),
    harga INT,
    stok INT,
    kategori_id INT,
    FOREIGN KEY (kategori_id) REFERENCES kategori(id)
);
```
- `kategori_id` di tabel `produk` menunjuk ke `id` di tabel `kategori`.
- Relasi ini **one-to-many**: satu kategori bisa punya banyak produk.

### 4.3 ERD sederhana
```
[ kategori ]                 [ produk ]
  id (PK)  ───────< banyak    id (PK)
  nama                        nama
                              kategori_id (FK)
```

### 4.4 JOIN — menggabung data
```sql
SELECT produk.nama, kategori.nama AS kategori
FROM produk
JOIN kategori ON produk.kategori_id = kategori.id;
```
`JOIN` mengambil data dari dua tabel sekaligus, dicocokkan lewat foreign key — menghasilkan nama produk beserta nama kategorinya.

### 📦 Brief Mini-project: Skema Database Aplikasi Toko
Rancang dan isi database dua tabel yang berelasi.

**Wajib ada:**
1. Tabel `kategori` (id, nama).
2. Tabel `produk` dengan kolom `kategori_id` sebagai foreign key.
3. Isi minimal 3 kategori dan 6 produk dengan `INSERT`.
4. Kumpulan query CRUD lengkap (insert, select, update, delete).
5. Minimal satu query `JOIN` yang menampilkan produk beserta nama kategorinya.

**Kriteria lulus:**
- Dua tabel dibuat dengan relasi foreign key yang benar.
- Data terisi.
- Query CRUD berjalan.
- Query JOIN menampilkan gabungan produk + kategori.

### Kunci — Contoh Solusi Lengkap (untuk instruktur)
```sql
-- 1. Struktur
CREATE TABLE kategori (
    id INT AUTO_INCREMENT PRIMARY KEY,
    nama VARCHAR(100)
);

CREATE TABLE produk (
    id INT AUTO_INCREMENT PRIMARY KEY,
    nama VARCHAR(100),
    harga INT,
    stok INT,
    kategori_id INT,
    FOREIGN KEY (kategori_id) REFERENCES kategori(id)
);

-- 2. Isi data
INSERT INTO kategori (nama) VALUES ('Alat Tulis'), ('Tas & Aksesoris'), ('Buku');

INSERT INTO produk (nama, harga, stok, kategori_id) VALUES
('Pulpen', 5000, 100, 1),
('Pensil', 3000, 150, 1),
('Tas Ransel', 150000, 10, 2),
('Dompet', 80000, 15, 2),
('Novel', 65000, 20, 3),
('Kamus', 90000, 8, 3);

-- 3. CRUD
SELECT * FROM produk;
UPDATE produk SET harga = 6000 WHERE nama = 'Pulpen';
DELETE FROM produk WHERE id = 6;

-- 4. JOIN
SELECT produk.nama AS produk, kategori.nama AS kategori, produk.harga
FROM produk
JOIN kategori ON produk.kategori_id = kategori.id;

-- 5. Agregasi per kategori
SELECT kategori.nama, COUNT(*) AS jumlah_produk
FROM produk
JOIN kategori ON produk.kategori_id = kategori.id
GROUP BY kategori.nama;
```

---

# SESI 5 — REVIEW & PENUTUP (16.30–17.00)

### Checklist Output Hari 6
- [ ] Database `toko` dibuat
- [ ] Tabel `kategori` & `produk` dengan foreign key
- [ ] Data terisi (INSERT)
- [ ] Query CRUD berjalan (select, update, delete)
- [ ] WHERE, ORDER BY, LIMIT dipakai benar
- [ ] Query JOIN menampilkan produk + kategori
- [ ] Query agregasi (COUNT/SUM/GROUP BY) berjalan

### Titik Rawan Pemula (perhatian instruktur)
- **`UPDATE`/`DELETE` tanpa `WHERE`** → semua baris terkena. Tekankan berulang.
- **Teks tanpa tanda kutip tunggal** `'...'` → error sintaks.
- **Lupa titik koma `;`** di akhir perintah.
- **Foreign key tak cocok** dengan `id` di tabel acuan → error / data yatim.
- **Salah nama kolom/tabel** (huruf besar-kecil, ejaan).
- **Membuat tabel `produk` sebelum `kategori`** padahal `produk` merujuk ke `kategori` → buat tabel acuan lebih dulu.

### Tugas / Persiapan Hari 7
1. Sempurnakan skema database toko hingga lolos checklist.
2. Simpan seluruh query dalam satu file `toko.sql`.
3. Renungkan: menulis SQL manual untuk tiap operasi itu melelahkan. Bagaimana kalau ada alat yang menangani CRUD & relasi secara otomatis dari kode PHP? → itulah **Eloquent** di Laravel (Hari 9).

### Jembatan ke Hari 7 — Fase 2 selesai!
"Kita telah menyelesaikan **Fase 2**: PHP (Hari 4), OOP (Hari 5), dan Database (Hari 6). Sekarang kita punya semua bahan — cara memproses (PHP), cara menata kode (OOP), dan cara menyimpan data (database). Besok kita satukan semuanya dalam **Laravel** — framework yang membuat semua ini jauh lebih cepat dan rapi. **Fase 3 dimulai.**"

---

*Modul ini bisa dibagikan ke peserta sebagai bahan bacaan, atau dipegang instruktur sebagai panduan mengajar. Kunci jawaban sebaiknya tidak dibagikan sebelum sesi latihan selesai.*
