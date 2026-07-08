# MODUL PELATIHAN WEB PROGRAMMER DASAR
## Berbasis Framework Laravel

---

## A. INFORMASI UMUM

| Item | Keterangan |
|---|---|
| **Judul Program** | Web Programmer Dasar — Membangun Aplikasi Web dengan Laravel |
| **Durasi** | 15 hari × 8 jam = **120 jam** |
| **Target Peserta** | Pemula (belum/baru mengenal pemrograman web) |
| **Prasyarat** | Bisa mengoperasikan komputer, logika dasar, tidak wajib punya latar belakang coding |
| **Metode** | 30% teori — 70% praktik (project-based & hands-on) |
| **Rasio ideal** | 1 instruktur : maks. 15–20 peserta (disarankan ada 1 asisten) |

### Tujuan Akhir (Learning Outcome)
Setelah menyelesaikan pelatihan, peserta **mampu membangun sebuah aplikasi web fungsional berbasis Laravel** yang memiliki fitur CRUD, autentikasi, relasi database, dan dapat di-deploy ke server.

### Kompetensi yang Dikuasai
1. Memahami cara kerja web (client-server, HTTP, request-response)
2. Membuat tampilan web dengan HTML, CSS, dan JavaScript dasar
3. Memahami pemrograman PHP prosedural & OOP
4. Merancang dan mengelola database MySQL
5. Membangun aplikasi Laravel dengan pola MVC
6. Mengimplementasikan CRUD, validasi, autentikasi, dan relasi data
7. Membuat REST API sederhana
8. Melakukan deployment aplikasi ke server

---

## B. PETA KURIKULUM (ROADMAP)

Pelatihan dibagi menjadi **3 fase**:

| Fase | Hari | Fokus |
|---|---|---|
| **Fase 1 — Fondasi Web** | 1–3 | HTML, CSS, JavaScript (tampilan & interaksi) |
| **Fase 2 — Jembatan Backend** | 4–6 | PHP prosedural, PHP OOP, Database & SQL |
| **Fase 3 — Laravel & Proyek** | 7–15 | Framework Laravel + Proyek Akhir |

**Kenapa urutan ini?**
Laravel adalah framework PHP yang menerapkan konsep OOP dan database. Peserta pemula tidak bisa langsung melompat ke Laravel tanpa memahami HTML (untuk tampilan), PHP (bahasa dasarnya), dan SQL (data). Tiga hari pertama membangun "kanvas", tiga hari berikutnya membangun "mesin", sisanya menyatukan semuanya dalam Laravel.

---

## C. STRUKTUR JADWAL HARIAN (Template 8 Jam)

| Waktu | Segmen | Sifat |
|---|---|---|
| 08.00 – 10.00 | Sesi konsep & demo instruktur | Teori + demonstrasi |
| 10.00 – 10.15 | Istirahat | — |
| 10.15 – 12.00 | Praktik terbimbing (guided) | Praktik bersama |
| 12.00 – 13.00 | ISHOMA | — |
| 13.00 – 15.00 | Lab mandiri / studi kasus | Praktik individu |
| 15.00 – 15.15 | Istirahat | — |
| 15.15 – 16.30 | Latihan / mini-project harian | Praktik |
| 16.30 – 17.00 | Review, tanya jawab, output harian | Evaluasi |

> Setiap hari **wajib menghasilkan output nyata** (deliverable) yang bisa dinilai.

---

## D. RINCIAN MATERI PER HARI

### FASE 1 — FONDASI WEB

---

#### HARI 1 — Pengenalan Web & HTML
**Tujuan:** Peserta memahami cara kerja web dan mampu membangun struktur halaman dengan HTML.

**Materi:**
- Cara kerja web: browser, server, HTTP request-response, URL & domain
- Perbedaan front-end vs back-end
- Setup environment: VS Code + ekstensi, browser, struktur folder proyek
- Pengenalan HTML: struktur dokumen, tag, atribut
- Elemen dasar: heading, paragraf, list, link, gambar
- HTML semantik: `header`, `nav`, `main`, `section`, `footer`
- Tabel dan form (input, label, button, select)

**Praktik:** Membuat halaman profil diri statis (CV online).
**Output Hari 1:** Halaman `profil.html` berisi biodata, foto, tabel keahlian, dan form kontak.

---

#### HARI 2 — CSS & Layout Responsif
**Tujuan:** Peserta mampu mempercantik dan menata tampilan halaman agar rapi & responsif.

**Materi:**
- Cara menyisipkan CSS (inline, internal, external)
- Selector, properti dasar: warna, font, spacing, border
- Box model (margin, padding, border, content)
- Layout modern: **Flexbox** dan **Grid**
- Responsive design: unit relatif, `media query`
- Pengenalan singkat framework CSS (Tailwind/Bootstrap) — konsep utility class

**Praktik:** Menata ulang halaman profil Hari 1 menjadi tampilan modern & responsif.
**Output Hari 2:** Halaman profil dengan styling profesional, responsif di HP & desktop.

---

#### HARI 3 — JavaScript Dasar
**Tujuan:** Peserta memahami logika pemrograman dan mampu membuat interaksi di halaman.

**Materi:**
- Variabel, tipe data, operator
- Struktur kontrol: `if/else`, `switch`
- Perulangan: `for`, `while`
- Fungsi dan parameter
- Array dan object
- Manipulasi DOM (mengubah elemen HTML)
- Event handling (`click`, `input`, `submit`)

**Praktik:** Membuat kalkulator sederhana / to-do list interaktif / validasi form sisi client.
**Output Hari 3:** Aplikasi interaktif kecil (mis. to-do list yang bisa tambah & hapus item).

---

### FASE 2 — JEMBATAN BACKEND

---

#### HARI 4 — PHP Fundamental
**Tujuan:** Peserta memahami dasar pemrograman server-side dengan PHP.

**Materi:**
- Apa itu PHP & bagaimana server memproses PHP
- Setup: XAMPP/Laragon (Apache, PHP, MySQL)
- Sintaks dasar: variabel, tipe data, echo/print
- Operator, struktur kontrol, perulangan
- Fungsi bawaan & fungsi buatan sendiri
- Array (indexed & associative)
- Menangani form: `$_GET`, `$_POST`, superglobals
- Include & require (memecah file)

**Praktik:** Membuat form yang datanya diproses & ditampilkan kembali oleh server.
**Output Hari 4:** Form pendaftaran sederhana + halaman hasil proses server-side.

---

#### HARI 5 — PHP OOP & Composer
**Tujuan:** Peserta memahami konsep OOP sebagai fondasi wajib sebelum masuk Laravel.

**Materi:**
- Mengapa OOP penting untuk Laravel
- Class dan object, property & method
- Constructor
- Inheritance (pewarisan), encapsulation
- Access modifier: `public`, `private`, `protected`
- Interface & abstract class (pengenalan)
- Namespace & autoloading
- **Composer**: manajemen dependency (fondasi instalasi Laravel)

**Praktik:** Membuat mini-program OOP (mis. class `Produk` dengan operasi kelola stok).
**Output Hari 5:** Program berorientasi objek sederhana yang berjalan di terminal/browser.

---

#### HARI 6 — Database & SQL (MySQL)
**Tujuan:** Peserta mampu merancang database dan menjalankan operasi data dengan SQL.

**Materi:**
- Konsep RDBMS: database, tabel, kolom, baris, primary key, foreign key
- Tool: phpMyAdmin / DBeaver
- DDL: `CREATE`, `ALTER`, `DROP`
- DML: `INSERT`, `SELECT`, `UPDATE`, `DELETE`
- Filter & pengurutan: `WHERE`, `ORDER BY`, `LIMIT`
- Agregasi: `COUNT`, `SUM`, `GROUP BY`
- Relasi antar tabel & `JOIN`
- Perancangan ERD sederhana

**Praktik:** Merancang skema database aplikasi (mis. produk & kategori) dan menjalankan query CRUD.
**Output Hari 6:** Skema database + kumpulan query CRUD yang berfungsi.

---

### FASE 3 — LARAVEL & PROYEK AKHIR

---

#### HARI 7 — Pengenalan Laravel & MVC
**Tujuan:** Peserta memahami struktur Laravel dan pola MVC.

**Materi:**
- Apa itu framework & keunggulan Laravel
- Instalasi via Composer, struktur folder Laravel
- Konsep **MVC** (Model–View–Controller)
- Request lifecycle (alur request di Laravel)
- Routing dasar (`web.php`, parameter route)
- Laravel Artisan CLI
- **Git dasar**: `init`, `add`, `commit` (kebiasaan version control sejak awal)

**Praktik:** Instalasi proyek Laravel pertama, membuat beberapa route & halaman.
**Output Hari 7:** Aplikasi Laravel berjalan di `localhost` dengan routing dasar + repo Git.

---

#### HARI 8 — Blade Template & Controller
**Tujuan:** Peserta mampu membuat tampilan dinamis terstruktur.

**Materi:**
- Blade templating engine
- Layout & inheritance (`@extends`, `@section`, `@yield`)
- Blade directive (`@if`, `@foreach`, `@include`)
- Blade component
- Controller & resource controller
- Mengirim data dari controller ke view
- Mengelola aset statis (CSS/JS/gambar)

**Praktik:** Membuat layout master + beberapa halaman dinamis yang mewarisinya.
**Output Hari 8:** Aplikasi multi-halaman dengan layout konsisten & data dinamis.

---

#### HARI 9 — Eloquent, Migration & Model
**Tujuan:** Peserta mampu menghubungkan Laravel dengan database.

**Materi:**
- Konfigurasi `.env` & koneksi database
- **Migration**: membuat & mengubah struktur tabel lewat kode
- **Model** & Eloquent ORM
- Seeder & Factory (mengisi data dummy)
- Query dasar Eloquent: `all`, `find`, `where`, `create`, `save`
- Tinker (uji query interaktif)

**Praktik:** Membuat migration, model, dan seeder untuk tabel utama aplikasi.
**Output Hari 9:** Tabel dibuat via migration + terisi data via seeder + bisa ditampilkan.

---

#### HARI 10 — CRUD & Validasi
**Tujuan:** Peserta mampu membangun fitur CRUD lengkap — inti dari aplikasi web.

**Materi:**
- Alur CRUD: Create, Read, Update, Delete
- Form input & menyimpan data
- Menampilkan daftar & detail data
- Edit & update data
- Hapus data + konfirmasi
- Validasi input (Form Request)
- Flash message & redirect

**Praktik:** Membangun modul CRUD penuh (mis. manajemen produk).
**Output Hari 10:** Modul CRUD lengkap & berfungsi dengan validasi.

---

#### HARI 11 — Autentikasi & Otorisasi
**Tujuan:** Peserta mampu membuat sistem login & area terproteksi.

**Materi:**
- Konsep autentikasi vs otorisasi
- Instalasi starter kit (Laravel Breeze)
- Register, login, logout
- Middleware & proteksi route
- Session & user yang sedang login
- Role/hak akses sederhana (mis. admin vs user)

**Praktik:** Menambahkan sistem login ke aplikasi & memproteksi halaman admin.
**Output Hari 11:** Aplikasi dengan login/logout & area yang hanya bisa diakses user terautentikasi.

---

#### HARI 12 — Relasi Eloquent & Fitur Lanjutan
**Tujuan:** Peserta mampu mengelola data yang saling berhubungan.

**Materi:**
- Relasi: One-to-One, One-to-Many, Many-to-Many
- Eager loading (`with`) & menghindari N+1 query
- Upload & pengelolaan file/gambar
- Pagination
- Fitur pencarian (search) & filter
- Sorting data

**Praktik:** Menghubungkan tabel (mis. kategori–produk), tambah upload gambar & search.
**Output Hari 12:** Aplikasi dengan data relasional, upload gambar, pencarian & pagination.

---

#### HARI 13 — REST API & Integrasi
**Tujuan:** Peserta memahami konsep API dan mampu membuat endpoint sederhana.

**Materi:**
- Konsep REST API & format JSON
- Perbedaan route `web` vs `api`
- API Controller & API Resource
- Method HTTP: GET, POST, PUT, DELETE
- Menguji API dengan Postman / Thunder Client
- Pengenalan token/API key (opsional: Sanctum)

**Praktik:** Membuat endpoint API CRUD & mengujinya di Postman.
**Output Hari 13:** REST API fungsional untuk salah satu modul aplikasi.

---

#### HARI 14 — Proyek Akhir (Pengembangan)
**Tujuan:** Peserta menerapkan seluruh materi dalam satu aplikasi utuh.

**Kegiatan:**
- Penentuan tema & fitur proyek akhir
- Perancangan database (ERD) & wireframe sederhana
- Implementasi: migration → model → controller → view
- Bimbingan intensif (mentoring per peserta/kelompok)

**Output Hari 14:** Aplikasi proyek akhir mencapai 70–80% (fitur inti sudah jalan).

---

#### HARI 15 — Finalisasi, Deployment & Presentasi
**Tujuan:** Peserta menyelesaikan, mendeploy, dan mempresentasikan aplikasi.

**Materi & Kegiatan:**
- Debugging & penyempurnaan fitur
- Persiapan produksi: konfigurasi `.env`, `php artisan migrate`
- **Deployment**: upload ke shared hosting / VPS, setting database & domain
- Alur deploy dengan Git
- Presentasi proyek akhir per peserta/kelompok
- Evaluasi akhir & sertifikasi

**Output Hari 15:** Aplikasi Laravel **online (deployed)** + presentasi + evaluasi.

---

## E. PROYEK AKHIR

Peserta memilih **satu** tema aplikasi (harus mencakup CRUD + autentikasi + relasi):

| Opsi | Deskripsi |
|---|---|
| **Manajemen Inventori/Stok Barang** | Kelola produk, kategori, stok masuk-keluar |
| **Sistem Informasi Data Peserta** | Kelola data peserta pelatihan + laporan |
| **Aplikasi Kasir Sederhana (POS mini)** | Transaksi, produk, struk |
| **Blog / CMS Sederhana** | Post, kategori, komentar, admin panel |
| **To-Do / Task Manager** | Tugas, kategori, status, multi-user |

**Syarat minimal proyek:**
- Minimal 2 tabel yang berelasi
- Fitur CRUD lengkap
- Sistem login/autentikasi
- Validasi input
- Tampilan responsif
- Ter-deploy & bisa diakses online

---

## F. PENILAIAN (ASSESSMENT)

### Komponen Penilaian
| Komponen | Bobot |
|---|---|
| Output harian (formatif, Hari 1–13) | 30% |
| Keaktifan & partisipasi | 10% |
| Proyek akhir | 45% |
| Presentasi proyek | 15% |

### Rubrik Proyek Akhir
| Kriteria | Belum Kompeten | Kompeten | Sangat Kompeten |
|---|---|---|---|
| Fungsionalitas CRUD | Tidak lengkap | Berjalan penuh | Penuh + fitur tambahan |
| Autentikasi | Tidak ada | Login berfungsi | Login + role/hak akses |
| Relasi database | Tidak ada | 1 relasi benar | Beberapa relasi tepat |
| Validasi & error handling | Minim | Ada validasi dasar | Validasi menyeluruh |
| Tampilan (UI) | Berantakan | Rapi & responsif | Rapi, responsif, konsisten |
| Deployment | Gagal deploy | Ter-deploy | Ter-deploy + rapi |

### Checklist Kompetensi Akhir (Ya/Belum)
- [ ] Mampu menjelaskan cara kerja web & MVC
- [ ] Mampu membuat tampilan HTML/CSS responsif
- [ ] Mampu menulis logika dengan PHP OOP
- [ ] Mampu merancang & mengoperasikan database
- [ ] Mampu membuat CRUD di Laravel
- [ ] Mampu menerapkan autentikasi
- [ ] Mampu mengelola relasi data
- [ ] Mampu membuat REST API sederhana
- [ ] Mampu men-deploy aplikasi

---

## G. TOOLS & PRASYARAT TEKNIS

**Perangkat lunak (per komputer peserta):**
- Code editor: **VS Code**
- Web server lokal: **Laragon** (rekomendasi) atau XAMPP
- PHP 8.2+ & **Composer**
- Database: **MySQL** + phpMyAdmin/DBeaver
- Browser modern (Chrome/Firefox)
- **Git** + akun GitHub
- **Postman** / Thunder Client (untuk uji API)
- Node.js & NPM (untuk aset Laravel/Vite)

**Spesifikasi komputer minimal:**
- RAM 8 GB (disarankan), prosesor setara Core i3 ke atas, koneksi internet stabil

**Untuk deployment (opsional, disediakan penyelenggara):**
- Akun shared hosting atau VPS untuk latihan deploy

---

## H. CATATAN UNTUK INSTRUKTUR

1. **Jaga rasio praktik 70%** — pemula belajar coding dengan mengetik, bukan mendengar.
2. **Setiap hari harus ada output** yang bisa dinilai; ini menjaga motivasi & mudah dievaluasi.
3. **Sediakan asisten/co-trainer** untuk membantu peserta yang tertinggal saat lab.
4. **Konsistenkan satu studi kasus** (mis. "aplikasi produk") dari Hari 4–13 agar peserta melihat benang merah dari PHP → SQL → Laravel.
5. **Siapkan repo starter & materi cadangan** bila ada perbedaan kecepatan belajar.
6. Fase 1–2 adalah titik rawan drop-off; beri perhatian ekstra pada peserta yang benar-benar nol.
