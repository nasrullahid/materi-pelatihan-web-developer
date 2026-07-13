# MODUL AJAR — HARI 7
## Pengenalan Laravel & MVC

*Bagian dari Pelatihan Web Programmer Dasar — Berbasis Laravel (15 Hari)*

---

## INFORMASI SESI

| Item | Keterangan |
|---|---|
| **Hari** | 7 dari 15 |
| **Fase** | Fase 3 — Laravel & Proyek (**dimulai**) |
| **Topik** | Framework Laravel, pola MVC, routing, Artisan, dan Git |
| **Durasi** | 8 jam |
| **Prasyarat** | Hari 4–6 (PHP, OOP, Database) |
| **Output** | Aplikasi Laravel berjalan di `localhost` dengan routing dasar + repo Git |

### Tujuan Pembelajaran
Setelah menyelesaikan hari ini, peserta mampu:
1. Menjelaskan apa itu framework dan keunggulan Laravel.
2. Menginstal proyek Laravel via Composer dan menjalankannya dengan Artisan.
3. Mengenali struktur folder Laravel dan fungsi tiap bagian.
4. Menjelaskan pola MVC dan alur (lifecycle) sebuah request.
5. Membuat route dasar dan route berparameter di `routes/web.php`.
6. Menggunakan perintah Artisan dan dasar Git (`init`, `add`, `commit`).

### Alat & Bahan
- Laragon/XAMPP (PHP **8.2+**), **Composer**, **Git** — semua terpasang
- VS Code, browser, koneksi internet (untuk mengunduh Laravel)

---

## PETA WAKTU HARI INI

| Waktu | Sesi | Fokus |
|---|---|---|
| 08.00–10.00 | Sesi 1 — Konsep | Mengenal Laravel & instalasi |
| 10.00–10.15 | Istirahat | |
| 10.15–12.00 | Sesi 2 — Konsep | MVC & request lifecycle |
| 12.00–13.00 | ISHOMA | |
| 13.00–15.00 | Sesi 3 — Lab | Routing & Artisan |
| 15.00–15.15 | Istirahat | |
| 15.15–16.30 | Sesi 4 — Mini-project | Git & Laravel pertama |
| 16.30–17.00 | Sesi 5 — Review | Evaluasi & jembatan Hari 8 |

---

# SESI 1 — MENGENAL LARAVEL (08.00–10.00)

> **Metode:** ceramah + guided instalasi. Ini momen besar — rayakan bahwa peserta kini masuk ke framework nyata yang dipakai industri.

### 1.1 Apa itu framework?
Selama Hari 4–6 kita menulis semuanya **dari nol** dengan PHP murni: mengatur routing, koneksi database, keamanan, semuanya manual. Ini lambat dan rawan salah.

**Framework** menyediakan fondasi siap pakai. **Laravel** adalah framework PHP paling populer.

Analogi: PHP murni = **merakit mobil dari komponen satu per satu**. Framework = **rangka mobil yang sudah jadi** — kita tinggal menyesuaikan.

### 1.2 Keunggulan Laravel
- **Routing** rapi (menentukan URL dengan mudah).
- **Eloquent ORM** — mengelola database tanpa menulis SQL manual (Hari 9).
- **Blade** — templating tampilan yang bersih (Hari 8).
- **Artisan** — asisten baris perintah.
- **Keamanan bawaan** (proteksi form, autentikasi).
- **Ekosistem & dokumentasi** yang sangat besar.
> Semua yang kita pelajari sebelumnya terpakai: PHP (bahasa), OOP (struktur), database (data). Laravel **menyatukan** ketiganya.

### 1.3 Menginstal Laravel
Pastikan berada di folder kerja (mis. `www`), lalu di terminal:
```bash
composer create-project laravel/laravel toko
cd toko
php artisan serve
```
Buka `http://localhost:8000` — halaman sambutan Laravel akan muncul.
> `composer create-project` mengunduh Laravel beserta seluruh paketnya ke folder `vendor/`. Inilah yang membuat proyek Laravel berisi ribuan file (ingat: alasan hosting butuh inode besar).

### 1.4 Struktur folder Laravel
```
toko/
├── app/          → kode utama: Model, Controller
├── routes/       → web.php (definisi URL/route)
├── resources/    → views/ (tampilan Blade), css, js
├── database/     → migration & seeder
├── public/       → pintu masuk aplikasi (index.php)
├── vendor/       → paket dari Composer (jangan diedit)
└── .env          → konfigurasi & pengaturan database
```
| Folder | Isi |
|---|---|
| `routes/web.php` | tempat mendefinisikan URL |
| `app/` | Model & Controller (logika aplikasi) |
| `resources/views/` | file tampilan Blade |
| `.env` | pengaturan aplikasi & password database |

### 🔨 Latihan 1 (25 menit)
1. Instal proyek Laravel baru bernama `latihan-laravel`.
2. Jalankan dengan `php artisan serve` dan buka di browser.
3. Telusuri folder proyek di VS Code; temukan `routes/web.php`.

### ✅ Cek pemahaman Sesi 1
1. Apa keuntungan pakai framework dibanding PHP murni?
2. Perintah apa untuk membuat & menjalankan proyek Laravel?
3. Di folder mana route didefinisikan?

---

# SESI 2 — KONSEP MVC (10.15–12.00)

> **Metode:** ceramah interaktif dengan diagram. Ini mental model inti Laravel.

### 2.1 Apa itu MVC?
**MVC** memisahkan aplikasi menjadi tiga bagian dengan tugas berbeda, agar rapi dan mudah dirawat:
| Bagian | Tugas | Contoh |
|---|---|---|
| **Model** | mengurus data & database | `Produk` |
| **View** | tampilan yang dilihat pengguna | `produk.blade.php` |
| **Controller** | logika & pengatur alur | `ProdukController` |

Analogi restoran:
- **Controller** = pelayan (menerima pesanan, mengoordinasi).
- **Model** = dapur/gudang (menyiapkan bahan/data).
- **View** = piring saji (menyajikan ke pelanggan).

### 2.2 Alur sebuah request (lifecycle)
```
1. Browser  → pengguna membuka sebuah URL
2. Route    → Laravel mencocokkan URL dengan route di web.php
3. Controller → menjalankan logika yang sesuai
4. Model / DB → mengambil / menyimpan data (bila perlu)
5. View     → membungkus data menjadi HTML
6. Browser  → HTML dikirim & ditampilkan
```
> Hari ini kita fokus pada langkah 1–2 (routing). Controller (Hari 8), Model & database (Hari 9) menyusul — sedikit demi sedikit alur ini akan lengkap.

### ✅ Cek pemahaman Sesi 2
1. Sebutkan tugas Model, View, dan Controller.
2. Setelah URL dibuka, apa yang dicek Laravel pertama kali?
3. Kenapa memisahkan tugas (MVC) itu berguna?

---

# SESI 3 — ROUTING & ARTISAN (13.00–15.00)

> **Metode:** demo + lab. Peserta mulai menulis kode Laravel pertamanya.

### 3.1 Routing dasar
Route didefinisikan di `routes/web.php`:
```php
use Illuminate\Support\Facades\Route;

Route::get('/', function () {
    return 'Halo Laravel!';
});

Route::get('/tentang', function () {
    return 'Ini halaman tentang.';
});
```
- `Route::get` = menangani permintaan tipe GET (membuka halaman).
- Argumen pertama = URL. Argumen kedua = kode yang dijalankan.

### 3.2 Menampilkan view
```php
Route::get('/tentang', function () {
    return view('tentang');   // memuat resources/views/tentang.blade.php
});
```
Buat file `resources/views/tentang.blade.php` berisi HTML biasa. (Blade dibahas tuntas Hari 8.)

### 3.3 Route dengan parameter
```php
Route::get('/produk/{id}', function ($id) {
    return 'Menampilkan produk ke-' . $id;
});
```
- `{id}` = bagian URL yang berubah-ubah.
- `/produk/5` → "Menampilkan produk ke-5".
> Ini dasar dari halaman **detail** — satu route melayani banyak halaman berbeda.

### 3.4 Artisan CLI
Artisan adalah asisten baris perintah Laravel:
```bash
php artisan serve            # jalankan server lokal
php artisan route:list       # daftar semua route
php artisan make:controller ProdukController
php artisan make:model Produk
php artisan make:migration buat_tabel_produk
```
> `make:*` membuat file kerangka secara otomatis — menghemat banyak waktu.

### 🔨 Latihan 3 (45 menit)
Di `routes/web.php`:
1. Buat route `/` yang menampilkan "Selamat datang".
2. Buat route `/tentang` yang memuat view `tentang`.
3. Buat route `/salam/{nama}` yang menampilkan "Halo, [nama]!".
4. Jalankan `php artisan route:list` dan amati hasilnya.

**Kunci (untuk instruktur):**
```php
Route::get('/', function () {
    return 'Selamat datang';
});

Route::get('/tentang', function () {
    return view('tentang');
});

Route::get('/salam/{nama}', function ($nama) {
    return 'Halo, ' . $nama . '!';
});
```
`resources/views/tentang.blade.php`:
```html
<h1>Tentang Kami</h1>
<p>Halaman ini dibuat dengan Laravel.</p>
```

---

# SESI 4 — GIT & MINI-PROJECT (15.15–16.30)

> **Metode:** guided Git lalu kerja mandiri. Menghasilkan **output resmi Hari 7**.

### 4.1 Kenapa Git?
**Git** merekam riwayat perubahan kode. Manfaatnya: bisa kembali ke versi sebelumnya, bekerja tim, dan menjadi dasar deployment (Hari 15). Biasakan sejak proyek pertama.

### 4.2 Perintah dasar Git
```bash
git init                          # mulai melacak folder proyek
git add .                         # siapkan semua perubahan
git commit -m "Laravel pertama"   # simpan snapshot dengan pesan
```
| Perintah | Fungsi |
|---|---|
| `git init` | mulai melacak proyek |
| `git add .` | memilih perubahan yang akan disimpan |
| `git commit -m "..."` | merekam snapshot beserta pesan |
> Laravel sudah menyediakan file `.gitignore` yang otomatis mengecualikan `vendor/` dan `.env` — jadi folder berat & data rahasia tidak ikut tercatat.

### 📦 Brief Mini-project: Laravel Pertamamu
**Wajib ada:**
1. Proyek Laravel baru, berjalan dengan `php artisan serve`.
2. Route `/` yang menampilkan sapaan.
3. Route `/profil/{nama}` yang menampilkan nama dari parameter.
4. Satu view sederhana yang dipanggil dari sebuah route.
5. Inisialisasi Git dan buat **commit pertama**.

**Kriteria lulus:**
- Laravel berjalan di `http://localhost:8000`.
- Kedua route berfungsi (termasuk parameter).
- View tampil dari route.
- Repo Git punya minimal satu commit.

### Panduan Ringkas (untuk instruktur)
```bash
composer create-project laravel/laravel toko
cd toko
```
`routes/web.php`:
```php
Route::get('/', function () {
    return view('beranda');
});

Route::get('/profil/{nama}', function ($nama) {
    return 'Profil milik ' . $nama;
});
```
`resources/views/beranda.blade.php`:
```html
<h1>Selamat Datang di Aplikasi Toko</h1>
<p>Dibuat dengan Laravel.</p>
```
```bash
php artisan serve
# di terminal lain:
git init
git add .
git commit -m "Setup awal Laravel + routing dasar"
```

---

# SESI 5 — REVIEW & PENUTUP (16.30–17.00)

### Checklist Output Hari 7
- [ ] Laravel terinstal & berjalan di `localhost:8000`
- [ ] Route `/` berfungsi
- [ ] Route berparameter (`/profil/{nama}`) berfungsi
- [ ] Minimal satu view ditampilkan dari route
- [ ] `php artisan route:list` menampilkan route
- [ ] Git diinisialisasi & ada commit pertama

### Titik Rawan Pemula (perhatian instruktur)
- **Menjalankan `artisan` dari luar folder proyek** → error. Harus `cd` ke folder Laravel dulu.
- **Nama view di `view('...')` tak cocok** dengan nama file `.blade.php`.
- **PHP/Composer versi lama** → instalasi gagal (Laravel butuh PHP 8.2+).
- **Lupa `use Illuminate\Support\Facades\Route;`** bila menulis route manual (biasanya sudah ada).
- **Port 8000 dipakai** → jalankan `php artisan serve --port=8001`.
- Panik melihat banyak folder → tekankan cukup fokus ke `routes/`, `resources/views/`, dan `app/` dulu.

### Tugas / Persiapan Hari 8
1. Sempurnakan proyek Laravel pertama hingga lolos checklist.
2. Buat 2 route tambahan yang masing-masing menampilkan view berbeda.
3. Renungkan: menaruh seluruh HTML di dalam route/string itu berantakan. Bagaimana membuat tampilan yang rapi, punya layout bersama, dan bisa menampilkan data? → itulah **Blade & Controller**, materi besok.

### Jembatan ke Hari 8
"Hari ini kita sudah punya Laravel yang berjalan dan bisa merespons URL lewat routing. Tapi tampilan kita masih sekadar teks. Besok kita pakai **Controller** untuk menata logika, dan **Blade** untuk membuat tampilan dinamis yang rapi dengan layout bersama — langkah nyata pertama membangun antarmuka aplikasi."

---

*Modul ini bisa dibagikan ke peserta sebagai bahan bacaan, atau dipegang instruktur sebagai panduan mengajar. Kunci jawaban sebaiknya tidak dibagikan sebelum sesi latihan selesai.*
