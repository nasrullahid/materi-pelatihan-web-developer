# MODUL AJAR — HARI 11
## Autentikasi & Otorisasi

*Bagian dari Pelatihan Web Programmer Dasar — Berbasis Laravel (15 Hari)*

---

## INFORMASI SESI

| Item | Keterangan |
|---|---|
| **Hari** | 11 dari 15 |
| **Fase** | Fase 3 — Laravel & Proyek |
| **Topik** | Sistem login, proteksi halaman, dan hak akses |
| **Durasi** | 8 jam |
| **Prasyarat** | Hari 10 (CRUD) — aplikasi produk sudah berjalan |
| **Output** | Aplikasi dengan login/logout & area kelola produk yang hanya bisa diakses user terautentikasi |

### Tujuan Pembelajaran
Setelah menyelesaikan hari ini, peserta mampu:
1. Membedakan autentikasi (siapa) dan otorisasi (boleh apa).
2. Memasang Laravel Breeze untuk register, login, dan logout.
3. Memproteksi route/halaman dengan middleware `auth`.
4. Mengakses data user yang sedang login lewat `auth()`.
5. Menampilkan konten berbeda dengan `@auth` dan `@guest`.
6. Membuat role sederhana (admin vs user) dan membatasi akses.

### Alat & Bahan
- Proyek Laravel dari Hari 10 (CRUD produk)
- **Node.js & NPM** (untuk aset Breeze), Composer, MySQL aktif

---

## PETA WAKTU HARI INI

| Waktu | Sesi | Fokus |
|---|---|---|
| 08.00–10.00 | Sesi 1 — Konsep | Konsep auth & instalasi Breeze |
| 10.00–10.15 | Istirahat | |
| 10.15–12.00 | Sesi 2 — Lab | Middleware & proteksi route |
| 12.00–13.00 | ISHOMA | |
| 13.00–15.00 | Sesi 3 — Lab | Session & user yang login |
| 15.00–15.15 | Istirahat | |
| 15.15–16.30 | Sesi 4 — Mini-project | Role, otorisasi, amankan CRUD |
| 16.30–17.00 | Sesi 5 — Review | Evaluasi & jembatan Hari 12 |

---

# SESI 1 — KONSEP & BREEZE (08.00–10.00)

> **Metode:** ceramah + guided instalasi. Mulai dari masalah Hari 10: CRUD produk terbuka untuk siapa saja.

### 1.1 Autentikasi vs Otorisasi
Dua konsep berbeda yang sering tertukar:
| | Autentikasi | Otorisasi |
|---|---|---|
| Pertanyaan | **Siapa kamu?** | **Apa yang boleh kamu lakukan?** |
| Cara | login (email + password) | role / hak akses |
| Contoh | "Kamu adalah Budi" | "Budi boleh menghapus produk" |
> Urutannya: autentikasi dulu (login), baru otorisasi (cek hak).

### 1.2 Laravel Breeze
Membuat sistem login dari nol itu rumit dan rawan salah (enkripsi password, keamanan session, dll). **Laravel Breeze** menyediakan semuanya siap pakai: halaman register, login, logout, dan reset password.
```bash
composer require laravel/breeze --dev
php artisan breeze:install
npm install && npm run dev
php artisan migrate
```
> `breeze:install` akan menanyakan stack tampilan — pilih **Blade** untuk pelatihan ini. Setelah `migrate`, tabel `users` terbentuk.

### 1.3 Register, Login, Logout
Breeze langsung memberi:
- **Register** — mendaftar akun baru. Password otomatis **dienkripsi (hash)** — tak pernah disimpan sebagai teks asli.
- **Login** — masuk dengan email & password.
- **Logout** — keluar & mengakhiri sesi.

Coba: buka `/register`, buat akun, lalu `/login`.

### 🔨 Latihan 1 (30 menit)
1. Pasang Breeze pada proyek CRUD produk.
2. Jalankan `npm run dev` dan `php artisan migrate`.
3. Daftar satu akun, login, lalu logout. Amati halaman `/dashboard`.

### ✅ Cek pemahaman Sesi 1
1. Apa beda autentikasi dan otorisasi?
2. Kenapa memakai Breeze dibanding membuat login sendiri?
3. Kenapa password tidak disimpan sebagai teks biasa?

---

# SESI 2 — MIDDLEWARE & PROTEKSI (10.15–12.00)

> **Metode:** demo + lab. Terapkan langsung ke halaman produk.

### 2.1 Apa itu middleware?
**Middleware** adalah "penjaga pintu" yang memeriksa setiap request sebelum masuk ke controller. Middleware `auth` memastikan pengguna sudah login; jika belum, otomatis dialihkan ke halaman login.

### 2.2 Memproteksi route
```php
// satu route
Route::get('/dashboard', function () {
    return view('dashboard');
})->middleware('auth');

// banyak route sekaligus (group)
Route::middleware('auth')->group(function () {
    Route::resource('produk', ProdukController::class);
});
```

### 2.3 Proteksi dari dalam Controller
Alternatif: taruh di constructor controller agar **semua** method-nya terlindungi.
```php
class ProdukController extends Controller
{
    public function __construct()
    {
        $this->middleware('auth');
    }
    // semua method (index, store, dst) kini butuh login
}
```
> Bisa juga selektif: `$this->middleware('auth')->only(['create', 'store', 'edit', 'update', 'destroy']);` — agar daftar produk boleh dilihat publik, tapi mengubahnya butuh login.

### 🔨 Latihan 2 (30 menit)
1. Bungkus `Route::resource('produk', ...)` dengan middleware `auth`.
2. Coba akses `/produk` tanpa login → harus dialihkan ke `/login`.
3. Login, lalu akses lagi → harus bisa masuk.

---

# SESI 3 — SESSION & USER LOGIN (13.00–15.00)

> **Metode:** demo + lab.

### 3.1 Mengakses user yang login
Laravel menyimpan status login di **session**. Helper `auth()` memberi akses mudah:
```php
auth()->user();          // object user yang login
auth()->user()->name;    // namanya
auth()->user()->email;   // emailnya
auth()->id();            // id user
auth()->check();         // true bila sudah login
```

### 3.2 Menampilkan nama user
Di controller atau view:
```blade
<p>Selamat datang, {{ auth()->user()->name }}!</p>
```

### 3.3 @auth & @guest di Blade
Menampilkan konten berbeda tergantung status login:
```blade
@auth
    <p>Halo, {{ auth()->user()->name }}</p>
    <form action="{{ route('logout') }}" method="POST">
        @csrf
        <button>Logout</button>
    </form>
@endauth

@guest
    <a href="{{ route('login') }}">Login</a>
    <a href="{{ route('register') }}">Daftar</a>
@endguest
```
> Menu navigasi akan menyesuaikan otomatis: tombol Login untuk tamu, tombol Logout untuk yang sudah masuk.

### 🔨 Latihan 3 (40 menit)
1. Di navbar (partial Hari 8), tampilkan nama user dengan `@auth`.
2. Tambahkan tombol Logout untuk user yang login, tombol Login untuk tamu.
3. Uji dengan login & logout — pastikan menu berubah.

---

# SESI 4 — ROLE, OTORISASI & MINI-PROJECT (15.15–16.30)

> **Metode:** demo singkat lalu kerja mandiri. Menghasilkan **output resmi Hari 11**.

### 4.1 Role sederhana (admin vs user)
Cara paling sederhana membedakan hak akses: simpan kolom `role` di tabel `users`.
```php
// migration baru: menambah kolom role
$table->string('role')->default('user');
```
```bash
php artisan make:migration add_role_to_users_table
php artisan migrate
```
Tambahkan `role` ke `$fillable` model `User`.

### 4.2 Membatasi akses berdasarkan role
Di Blade:
```blade
@if(auth()->user()->role == 'admin')
    <a href="{{ route('produk.create') }}">+ Tambah Produk</a>
@endif
```
Di controller (lebih aman):
```php
public function destroy($id)
{
    if (auth()->user()->role !== 'admin') {
        abort(403);   // Terlarang
    }
    Produk::findOrFail($id)->delete();
    return back()->with('sukses', 'Produk dihapus');
}
```
> Pemeriksaan di controller lebih aman daripada hanya menyembunyikan tombol di view — jangan hanya mengandalkan tampilan.

### 📦 Brief Mini-project: Amankan Aplikasi Produk
Tambahkan sistem login & hak akses ke aplikasi CRUD produk (Hari 10).

**Wajib ada:**
1. Breeze terpasang (register, login, logout berfungsi).
2. Seluruh kelola produk (CRUD) diproteksi middleware `auth`.
3. Nama user yang login tampil di halaman.
4. Menu login/logout adaptif (`@auth` / `@guest`).
5. Tombol tambah/hapus hanya muncul & berjalan untuk **admin**.

**Kriteria lulus:**
- Mengakses `/produk` tanpa login → dialihkan ke `/login`.
- Setelah login → bisa mengelola produk.
- Nama user tampil; logout mengakhiri sesi.
- User biasa tidak melihat/menjalankan aksi khusus admin.

### Panduan Ringkas (untuk instruktur)
```php
// web.php
Route::middleware('auth')->group(function () {
    Route::resource('produk', ProdukController::class);
});
```
```php
// menandai user sebagai admin (lewat Tinker)
// php artisan tinker
$u = App\Models\User::find(1);
$u->role = 'admin';
$u->save();
```
```blade
{{-- navbar --}}
@auth
    <span>{{ auth()->user()->name }}</span>
    @if(auth()->user()->role == 'admin')
        <a href="{{ route('produk.create') }}">Tambah</a>
    @endif
    <form action="{{ route('logout') }}" method="POST">@csrf<button>Logout</button></form>
@endauth
@guest
    <a href="{{ route('login') }}">Login</a>
@endguest
```

---

# SESI 5 — REVIEW & PENUTUP (16.30–17.00)

### Checklist Output Hari 11
- [ ] Breeze terpasang; register/login/logout berfungsi
- [ ] CRUD produk diproteksi middleware `auth`
- [ ] Tanpa login diarahkan ke `/login`
- [ ] Nama user login tampil di halaman
- [ ] Menu adaptif dengan `@auth` / `@guest`
- [ ] Role admin membatasi aksi tambah/hapus

### Titik Rawan Pemula (perhatian instruktur)
- **Lupa `npm install && npm run dev`** setelah `breeze:install` → tampilan berantakan.
- **Lupa `php artisan migrate`** → tabel `users` belum ada, login error.
- **Route penting tak diberi middleware `auth`** → tetap bisa diakses tanpa login.
- **`role` tak ditambahkan ke `$fillable`** model User → gagal disimpan.
- **Hanya menyembunyikan tombol admin di view** tanpa cek di controller → tidak aman.
- **Logout memakai form POST** (butuh `@csrf`), bukan link biasa.

### Tugas / Persiapan Hari 12
1. Selesaikan proteksi aplikasi produk hingga lolos checklist.
2. Buat satu halaman yang hanya bisa dilihat admin.
3. Renungkan: setiap produk sekarang berdiri sendiri. Bagaimana menghubungkan produk ke **kategori**, atau mencatat **siapa** yang membuatnya? → itulah **relasi Eloquent**, materi besok.

### Jembatan ke Hari 12
"Aplikasi kita kini aman — hanya pengguna berhak yang bisa mengelola data. Besok kita perkaya datanya dengan **relasi Eloquent**: menghubungkan produk ke kategori (one-to-many), lalu fitur lanjutan seperti upload gambar, pencarian, dan pagination. Aplikasi mulai terasa seperti produk nyata."

---

*Modul ini bisa dibagikan ke peserta sebagai bahan bacaan, atau dipegang instruktur sebagai panduan mengajar. Kunci jawaban sebaiknya tidak dibagikan sebelum sesi latihan selesai.*
