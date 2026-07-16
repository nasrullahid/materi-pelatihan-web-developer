# MODUL AJAR — HARI 14
## Proyek Akhir — Development

*Bagian dari Pelatihan Web Programmer Dasar — Berbasis Laravel (15 Hari)*

---

## INFORMASI SESI

| Item | Keterangan |
|---|---|
| **Hari** | 14 dari 15 |
| **Fase** | Fase 3 — Laravel & Proyek |
| **Topik** | Membangun aplikasi lengkap dari nol (hari pengembangan) |
| **Durasi** | 8 jam |
| **Prasyarat** | Hari 1–13 (seluruh materi) |
| **Sifat** | **Workshop** — bukan materi baru, tapi menerapkan semuanya |
| **Output** | Aplikasi proyek akhir mencapai 70–80% (fitur inti berjalan) |

### Tujuan Hari Ini
Di akhir hari, setiap peserta memiliki:
1. Rencana proyek yang jelas (daftar fitur + skema database/ERD).
2. Proyek Laravel yang sudah ter-setup, ber-Git, dan berautentikasi.
3. Database berelasi (migration + model + relasi) yang berjalan.
4. Modul CRUD utama yang berfungsi.
5. Halaman kelola data yang terproteksi login.
6. Minimal satu fitur lanjutan (pencarian / upload / pagination).

### Alat & Bahan
- Semua alat pelatihan (Laravel, MySQL, VS Code, Git, Postman)
- **Instruktur + asisten** berperan sebagai mentor, berkeliling membantu

> **Catatan untuk instruktur:** Hari ini rasio praktik hampir 100%. Sesi konsep di pagi hari singkat saja (perencanaan). Selebihnya peserta membangun, instruktur & asisten mentoring intensif per peserta/kelompok. Jaga agar tiap peserta menyelesaikan minimal fitur inti hari ini agar Hari 15 cukup untuk finalisasi & deploy.

---

## PETA WAKTU HARI INI

| Waktu | Fase | Fokus |
|---|---|---|
| 08.00–10.00 | Fase 1 | Perencanaan & setup proyek |
| 10.00–10.15 | Istirahat | |
| 10.15–12.00 | Fase 2 | Fondasi: database, model, auth |
| 12.00–13.00 | ISHOMA | |
| 13.00–15.00 | Fase 3 | Membangun CRUD utama |
| 15.00–15.15 | Istirahat | |
| 15.15–16.30 | Fase 4 | Fitur lanjutan & mentoring |
| 16.30–17.00 | Fase 5 | Checkpoint & rencana finalisasi |

---

# FASE 1 — PERENCANAAN & SETUP (08.00–10.00)

### 1.1 Bekalmu: 13 hari, satu kotak peralatan lengkap
Sebelum mulai, sadari betapa banyak yang sudah dikuasai:
| Kelompok | Kemampuan | Hari |
|---|---|---|
| **Front-end** | HTML, CSS, JavaScript | 1–3 |
| **Backend** | PHP, OOP, Database SQL | 4–6 |
| **Laravel Inti** | MVC, Blade, Controller, Eloquent | 7–9 |
| **Fitur Aplikasi** | CRUD, Auth, Relasi, API | 10–13 |

Hari ini semuanya digabung menjadi satu aplikasi utuh.

### 1.2 Pilih ide proyek
Pilih **satu** (atau ide sendiri):
| Ide | Data utama |
|---|---|
| Manajemen Inventaris / Stok | produk, kategori, transaksi stok |
| Perpustakaan | buku, anggota, peminjaman |
| Katalog Produk / Toko sederhana | produk, kategori |
| Manajemen Data Siswa / Sekolah | siswa, kelas, nilai |
| Aplikasi Keuangan | transaksi, kategori (pemasukan/pengeluaran) |
| Manajemen Tugas / Proyek tim | tugas, kategori, status |

**Syarat minimal proyek** (dari kurikulum):
- Minimal **2 tabel yang berelasi**
- Fitur **CRUD lengkap**
- Sistem **login/autentikasi**
- **Validasi** input
- Tampilan **responsif**
- (Hari 15) **ter-deploy** & bisa diakses online

### 1.3 Rancang sebelum koding
Jangan langsung mengetik kode. Rancang dulu:

**A. Daftar fitur**
- Siapa penggunanya? (admin saja, atau admin + user?)
- Data apa yang dikelola?
- Aksi CRUD apa saja untuk tiap data?
- Fitur lanjutan yang diinginkan?

**B. Skema database (ERD sederhana)** — gambar di kertas dulu:
- Tabel apa saja & kolomnya
- Primary key tiap tabel
- Relasi antar tabel (foreign key)

Contoh (Perpustakaan):
```
[ kategori ]        [ buku ]              [ peminjaman ]
  id (PK)   ──<      id (PK)      >──       id (PK)
  nama              judul                   buku_id (FK)
                    kategori_id (FK)        anggota_id (FK)
                    stok                    tanggal_pinjam
```

### 🎯 Target Fase 1
Setiap peserta punya: (1) tema proyek, (2) daftar fitur tertulis, (3) sketsa ERD.

---

# FASE 2 — FONDASI PROYEK (10.15–12.00)

### 2.1 Urutan membangun (roadmap)
Membangun dengan **urutan yang benar** menghemat banyak waktu:
1. Setup proyek Laravel + `git init` + commit awal
2. Pasang autentikasi (Breeze)
3. Buat migration: semua tabel + relasi (foreign key)
4. Buat Model tiap tabel + definisikan relasi + seeder
5. Bangun CRUD utama (resource controller + Blade)
6. Tambah relasi di tampilan + validasi
7. Fitur lanjutan: search / upload / pagination

### 2.2 Checklist Fondasi (Fase 2)
- [ ] `composer create-project` → `git init` → commit awal
- [ ] `php artisan breeze:install` → register/login berjalan
- [ ] Rancang & buat migration semua tabel (dengan foreign key)
- [ ] `php artisan migrate` — cek tabel di phpMyAdmin
- [ ] Buat Model tiap tabel + definisikan relasi (`hasMany`/`belongsTo`)
- [ ] Buat seeder untuk data awal (disarankan)

Perintah kunci (rujukan cepat):
```bash
composer create-project laravel/laravel proyek-akhir
cd proyek-akhir
git init && git add . && git commit -m "Setup awal"

composer require laravel/breeze --dev
php artisan breeze:install     # pilih Blade
npm install && npm run dev
php artisan migrate

php artisan make:model Buku -m         # model + migration
php artisan make:seeder BukuSeeder
```

### 🎯 Target Fase 2
Proyek jalan, login berfungsi, tabel-tabel berelasi sudah ada di database.

---

# FASE 3 — MEMBANGUN CRUD UTAMA (13.00–15.00)

### 3.1 Bangun modul CRUD inti
Fokus pada **satu tabel utama** dulu (mis. `buku`), buat CRUD-nya lengkap sebelum pindah ke tabel lain. Rujuk Hari 8 (Blade/Controller) & Hari 10 (CRUD).

### 3.2 Checklist CRUD (Fase 3)
- [ ] `Route::resource` + resource controller
- [ ] Layout master + navbar (`@extends`, `@include`)
- [ ] `index`: menampilkan daftar data dalam tabel
- [ ] `create`/`store`: form tambah + `@csrf` + simpan (dengan validasi)
- [ ] `edit`/`update`: form edit + `@method('PUT')`
- [ ] `destroy`: hapus + konfirmasi + flash message

Perintah kunci:
```bash
php artisan make:controller BukuController --resource --model=Buku
```
```php
// web.php
Route::resource('buku', BukuController::class);
```

### 💡 Strategi
Selesaikan CRUD satu tabel penuh (bisa tambah/tampil/edit/hapus) **sebelum** pindah ke tabel berikutnya. Lebih baik satu fitur utuh daripada banyak fitur setengah jadi.

### 🎯 Target Fase 3
Minimal satu modul CRUD berfungsi penuh dari halaman web.

---

# FASE 4 — FITUR LANJUTAN & MENTORING (15.15–16.30)

### 4.1 Checklist Fitur Lanjutan (Fase 4)
- [ ] Proteksi kelola data dengan middleware `auth`
- [ ] Tampilkan data relasi (nama kategori, dll) pakai `with()`
- [ ] Validasi input di semua form
- [ ] Pilih **minimal 1**: pencarian / upload gambar / pagination
- [ ] Rapikan tampilan dengan CSS (layout konsisten)
- [ ] Commit berkala ke Git

### 4.2 Cara mengatasi kebuntuan (baca ini saat stuck!)
- **Baca pesan error** — Laravel menampilkan baris & sebab error dengan jelas. Baca dari atas, jangan panik.
- **Uji sepotong-sepotong** — jangan menulis banyak kode lalu menjalankan sekaligus. Uji tiap fitur kecil segera.
- **Commit saat berhasil** — setiap fitur jalan, `git commit`. Mudah kembali bila sesuatu rusak.
- **Tanya dengan konteks** — sampaikan ke mentor: (1) mau melakukan apa, (2) kode yang ditulis, (3) pesan error-nya. Jangan hanya bilang "error".

### 4.3 Rubrik Proyek (target untuk presentasi Hari 15)
| Kriteria | Bobot |
|---|---|
| Aplikasi berjalan tanpa error | 20% |
| CRUD lengkap & berfungsi | 25% |
| Autentikasi & proteksi halaman | 15% |
| Min. 2 tabel berelasi + validasi | 15% |
| Min. 1 fitur lanjutan | 10% |
| Tampilan rapi & konsisten | 10% |
| Git + presentasi jelas | 5% |

### 🎯 Target Fase 4
Aplikasi terproteksi, punya data relasional, dan minimal satu fitur lanjutan.

---

# FASE 5 — CHECKPOINT & RENCANA FINALISASI (16.30–17.00)

### Checkpoint Hari 14 — pastikan tercapai
- [ ] Proyek berjalan di `localhost` tanpa error fatal
- [ ] CRUD utama sudah berfungsi
- [ ] Sudah di-commit ke Git
- [ ] Catat fitur yang **belum selesai** untuk dikerjakan besok

### Refleksi singkat (per peserta/kelompok)
- Apa yang sudah berjalan?
- Fitur apa yang belum & jadi prioritas besok?
- Kendala teknis apa yang masih mengganjal?

### Persiapan Hari 15
1. Pastikan kode ter-commit (aman bila terjadi apa-apa).
2. Siapkan daftar tugas sisa (finishing) untuk pagi Hari 15.
3. Mulai pikirkan poin presentasi: masalah apa yang dipecahkan aplikasimu, fitur unggulannya apa.

### Jembatan ke Hari 15
"Hari ini kalian membangun inti aplikasi — fondasi, CRUD, proteksi, dan fitur. Besok adalah hari terakhir: kita **finalisasi** sisa fitur, **deploy ke internet** agar bisa diakses siapa saja, lalu **presentasi** karya kalian. Simpan kodenya dengan commit, dan datang besok dengan semangat menyelesaikan!"

---

*Modul ini adalah panduan hari pengembangan proyek. Instruktur berperan sebagai mentor, bukan pengajar materi baru. Fokus: memastikan tiap peserta menyelesaikan fitur inti dan siap untuk finalisasi & deploy di Hari 15.*
