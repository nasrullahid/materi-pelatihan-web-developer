# MODUL AJAR — HARI 8
## Blade Template & Controller

*Bagian dari Pelatihan Web Programmer Dasar — Berbasis Laravel (15 Hari)*

---

## INFORMASI SESI

| Item | Keterangan |
|---|---|
| **Hari** | 8 dari 15 |
| **Fase** | Fase 3 — Laravel & Proyek |
| **Topik** | Membuat tampilan dinamis dengan Blade & menata logika dengan Controller |
| **Durasi** | 8 jam |
| **Prasyarat** | Hari 7 (Laravel & routing) |
| **Output** | Aplikasi multi-halaman dengan layout master konsisten & data dinamis |

### Tujuan Pembelajaran
Setelah menyelesaikan hari ini, peserta mampu:
1. Menulis view dengan Blade (`{{ }}`) dan directive (`@if`, `@foreach`).
2. Membuat layout master dan mewarisinya dengan `@extends`, `@yield`, `@section`.
3. Memakai ulang potongan tampilan dengan `@include`.
4. Membuat Controller dan menghubungkannya dari route.
5. Mengirim data dari Controller ke view.
6. Memuat aset statis (`asset()`) dan mengenal Blade component.

### Alat & Bahan
- Proyek Laravel dari Hari 7 (atau proyek baru), Laragon/XAMPP, VS Code, browser

---

## PETA WAKTU HARI INI

| Waktu | Sesi | Fokus |
|---|---|---|
| 08.00–10.00 | Sesi 1 — Konsep | Mengenal Blade & directive |
| 10.00–10.15 | Istirahat | |
| 10.15–12.00 | Sesi 2 — Lab | Layout & inheritance |
| 12.00–13.00 | ISHOMA | |
| 13.00–15.00 | Sesi 3 — Lab | Controller & passing data |
| 15.00–15.15 | Istirahat | |
| 15.15–16.30 | Sesi 4 — Mini-project | Assets, component, aplikasi berlayout |
| 16.30–17.00 | Sesi 5 — Review | Evaluasi & jembatan Hari 9 |

---

# SESI 1 — MENGENAL BLADE (08.00–10.00)

> **Metode:** demo + lab. Tunjukkan betapa berantakannya menaruh HTML di dalam route (Hari 7), lalu perkenalkan Blade sebagai solusinya.

### 1.1 Apa itu Blade?
**Blade** adalah templating engine bawaan Laravel untuk membuat tampilan. File Blade berakhiran `.blade.php` dan disimpan di `resources/views/`.

Kelebihan dibanding PHP biasa: sintaks lebih bersih, aman, dan punya fitur layout & komponen.
```php
<!-- PHP biasa (Hari 4) -->
<?php echo $nama; ?>

<!-- Blade -->
{{ $nama }}
```
> `{{ $nama }}` menampilkan isi variabel dan **otomatis aman** dari kode berbahaya (XSS).

### 1.2 Membuat & menampilkan view
1. Buat file `resources/views/beranda.blade.php`.
2. Panggil dari route:
```php
Route::get('/', function () {
    return view('beranda');
});
```
Nama view memakai **titik** untuk folder: `view('produk.index')` → `resources/views/produk/index.blade.php`.

### 1.3 Directive — logika di dalam Blade
Directive diawali tanda `@`, versi Blade dari struktur kontrol PHP.
```blade
@if($umur >= 18)
    <p>Dewasa</p>
@else
    <p>Belum dewasa</p>
@endif

<ul>
@foreach($produk as $item)
    <li>{{ $item }}</li>
@endforeach
</ul>
```
| Directive | Fungsi |
|---|---|
| `@if / @else / @endif` | percabangan |
| `@foreach / @endforeach` | perulangan |
| `@include('...')` | menyisipkan file lain |
| `{{ $var }}` | menampilkan variabel |

### 🔨 Latihan 1 (25 menit)
Buat view `profil.blade.php` dan route yang memanggilnya, lalu:
1. Tampilkan nama dan kota (sementara boleh nilai statis via `with`).
2. Gunakan `@if` untuk menampilkan "Member" jika sebuah variabel `true`.
3. Gunakan `@foreach` menampilkan daftar 3 hobi.

**Kunci (untuk instruktur):**
Route:
```php
Route::get('/profil', function () {
    return view('profil', [
        'nama' => 'Budi',
        'member' => true,
        'hobi' => ['Membaca', 'Futsal', 'Ngoding'],
    ]);
});
```
`profil.blade.php`:
```blade
<h1>{{ $nama }}</h1>
@if($member)
    <p>Status: Member</p>
@endif
<ul>
@foreach($hobi as $h)
    <li>{{ $h }}</li>
@endforeach
</ul>
```

---

# SESI 2 — LAYOUT & INHERITANCE (10.15–12.00)

> **Metode:** demo + lab. Konsep paling berdampak hari ini — hilangkan pengulangan header/footer.

### 2.1 Masalah: HTML berulang
Tanpa layout, setiap halaman menulis ulang `<html>`, `<head>`, navbar, footer. Boros dan sulit dirawat. Solusinya: **satu layout master** yang diwarisi semua halaman.

### 2.2 Membuat layout master
`resources/views/layouts/app.blade.php`:
```blade
<!DOCTYPE html>
<html lang="id">
<head>
    <meta charset="UTF-8">
    <title>@yield('judul')</title>
</head>
<body>
    @include('partials.navbar')

    <main>
        @yield('konten')
    </main>

    @include('partials.footer')
</body>
</html>
```
`@yield('nama')` = "lubang" yang akan diisi tiap halaman.

### 2.3 Halaman anak mewarisi layout
`resources/views/beranda.blade.php`:
```blade
@extends('layouts.app')

@section('judul', 'Beranda')

@section('konten')
    <h1>Selamat datang di Toko</h1>
    <p>Ini halaman utama.</p>
@endsection
```
- `@extends` = memakai layout master.
- `@section('konten') ... @endsection` = mengisi lubang `@yield('konten')`.

### 2.4 @include — potongan berulang
Simpan navbar di `resources/views/partials/navbar.blade.php`, lalu sisipkan:
```blade
@include('partials.navbar')
```
> **`@extends` vs `@include`:** `@extends` mewarisi **seluruh kerangka**; `@include` menyisipkan **sepotong bagian**.

### 🔨 Latihan 2 (35 menit)
1. Buat `layouts/app.blade.php` dengan `@yield('judul')` dan `@yield('konten')`.
2. Buat `partials/navbar.blade.php` berisi menu, `@include` di layout.
3. Buat 2 halaman (`beranda`, `tentang`) yang `@extends` layout tersebut.

**Kunci (untuk instruktur):** (lihat contoh solusi lengkap di Sesi 4)

---

# SESI 3 — CONTROLLER & PASSING DATA (13.00–15.00)

> **Metode:** demo + lab. Memindahkan logika dari route ke Controller — menerapkan MVC.

### 3.1 Kenapa Controller?
Menaruh semua logika di `web.php` membuatnya cepat berantakan. **Controller** adalah class tempat logika ditata rapi (huruf "C" dalam MVC).

### 3.2 Membuat Controller
```bash
php artisan make:controller ProdukController
```
Menghasilkan `app/Http/Controllers/ProdukController.php`:
```php
<?php
namespace App\Http\Controllers;

class ProdukController extends Controller
{
    public function index()
    {
        return view('produk.index');
    }
}
```
> Perhatikan: ini **class yang `extends`** — persis OOP Hari 5. Semua yang dipelajari di sana terpakai di sini.

### 3.3 Menghubungkan route ke Controller
`routes/web.php`:
```php
use App\Http\Controllers\ProdukController;

Route::get('/produk', [ProdukController::class, 'index']);
```

### 3.4 Mengirim data ke view
```php
public function index()
{
    $produk = ['Buku', 'Pulpen', 'Tas'];
    return view('produk.index', ['produk' => $produk]);
    // singkatnya: return view('produk.index', compact('produk'));
}
```
Di `produk/index.blade.php`:
```blade
<ul>
@foreach($produk as $item)
    <li>{{ $item }}</li>
@endforeach
</ul>
```
> Controller **menyiapkan** data → view **menampilkan**. Inilah "C" dan "V" bekerja sama.

### 3.5 Resource Controller (pengenalan)
```bash
php artisan make:controller ProdukController --resource
```
```php
Route::resource('produk', ProdukController::class);
```
Satu baris ini membuat **7 route CRUD** sekaligus: `index` (daftar), `create` (form tambah), `store` (simpan), `show` (detail), `edit` (form edit), `update` (perbarui), `destroy` (hapus). Pola ini dipakai penuh di **Hari 10**.

### 🔨 Latihan 3 (40 menit)
1. Buat `ProdukController` dengan method `index()`.
2. Di dalamnya, siapkan array 4 produk dan kirim ke view `produk.index`.
3. Hubungkan route `/produk` ke controller tersebut.
4. Tampilkan daftar produk di view dengan `@foreach`.

**Kunci (untuk instruktur):**
```php
// ProdukController.php
public function index()
{
    $produk = ['Buku', 'Pulpen', 'Tas', 'Topi'];
    return view('produk.index', compact('produk'));
}
```
```php
// web.php
use App\Http\Controllers\ProdukController;
Route::get('/produk', [ProdukController::class, 'index']);
```
```blade
{{-- produk/index.blade.php --}}
@extends('layouts.app')
@section('judul', 'Daftar Produk')
@section('konten')
    <h1>Produk</h1>
    <ul>
    @foreach($produk as $item)
        <li>{{ $item }}</li>
    @endforeach
    </ul>
@endsection
```

---

# SESI 4 — ASSETS, COMPONENT & MINI-PROJECT (15.15–16.30)

> **Metode:** demo singkat lalu kerja mandiri. Menghasilkan **output resmi Hari 8**.

### 4.1 Aset statis (CSS, gambar)
Simpan file di folder `public/` (mis. `public/css/style.css`), lalu panggil dengan `asset()`:
```blade
<link rel="stylesheet" href="{{ asset('css/style.css') }}">
<img src="{{ asset('img/logo.png') }}">
```
`asset()` menghasilkan URL yang benar ke folder `public/`.

### 4.2 Blade Component (pengenalan)
Component adalah potongan UI yang dipakai ulang seperti tag HTML.
```bash
php artisan make:component Alert
```
```blade
<x-alert>Data berhasil disimpan!</x-alert>
```
> Untuk pemula, `@include` sudah cukup. Component diperkenalkan sebagai langkah lanjut.

### 📦 Brief Mini-project: Aplikasi Multi-halaman Berlayout
Buat aplikasi Laravel dengan layout konsisten dan data dinamis.

**Wajib ada:**
1. Layout master `layouts/app.blade.php` (`@yield('judul')`, `@yield('konten')`).
2. Navbar sebagai partial (`@include('partials.navbar')`).
3. Tiga halaman: **beranda**, **tentang**, **produk** — semua `@extends` layout master.
4. Halaman **produk** menampilkan data dari **ProdukController** (`@foreach`).
5. Sisipkan satu file CSS via `asset()` agar tampilan rapi.

**Kriteria lulus:**
- Ketiga halaman memakai layout master yang sama (navbar konsisten).
- Navigasi antar halaman berfungsi.
- Halaman produk menampilkan daftar dari controller.
- Tampilan tertata dengan CSS.

### Kunci — Contoh Solusi Lengkap (untuk instruktur)

`resources/views/layouts/app.blade.php`
```blade
<!DOCTYPE html>
<html lang="id">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>@yield('judul') - Toko</title>
    <link rel="stylesheet" href="{{ asset('css/style.css') }}">
</head>
<body>
    @include('partials.navbar')
    <main>
        @yield('konten')
    </main>
    <footer>&copy; 2026 Toko</footer>
</body>
</html>
```

`resources/views/partials/navbar.blade.php`
```blade
<nav>
    <a href="/">Beranda</a>
    <a href="/tentang">Tentang</a>
    <a href="/produk">Produk</a>
</nav>
```

`resources/views/beranda.blade.php`
```blade
@extends('layouts.app')
@section('judul', 'Beranda')
@section('konten')
    <h1>Selamat Datang di Toko</h1>
    <p>Aplikasi Laravel pertama dengan layout rapi.</p>
@endsection
```

`app/Http/Controllers/ProdukController.php`
```php
<?php
namespace App\Http\Controllers;

class ProdukController extends Controller
{
    public function index()
    {
        $produk = ['Buku', 'Pulpen', 'Tas', 'Topi'];
        return view('produk.index', compact('produk'));
    }
}
```

`resources/views/produk/index.blade.php`
```blade
@extends('layouts.app')
@section('judul', 'Produk')
@section('konten')
    <h1>Daftar Produk</h1>
    <ul>
    @foreach($produk as $item)
        <li>{{ $item }}</li>
    @endforeach
    </ul>
@endsection
```

`routes/web.php`
```php
use App\Http\Controllers\ProdukController;

Route::get('/', function () { return view('beranda'); });
Route::get('/tentang', function () { return view('tentang'); });
Route::get('/produk', [ProdukController::class, 'index']);
```

---

# SESI 5 — REVIEW & PENUTUP (16.30–17.00)

### Checklist Output Hari 8
- [ ] Layout master `layouts/app.blade.php` dibuat
- [ ] Navbar partial di-`@include`
- [ ] Minimal 3 halaman `@extends` layout master
- [ ] ProdukController mengirim data ke view
- [ ] View menampilkan data dengan `@foreach`
- [ ] CSS dimuat via `asset()`
- [ ] Navigasi antar halaman berfungsi

### Titik Rawan Pemula (perhatian instruktur)
- **Salah titik nama view** — `layouts.app` (folder pakai titik, bukan garis miring).
- **Lupa `@endif` / `@endforeach` / `@endsection`**.
- **Variabel tidak dikirim controller** tapi dipakai di view → error "undefined variable".
- **Nama `@section` tak sama dengan `@yield`** → bagian tak muncul.
- **Aset ditaruh di luar `public/`** → `asset()` tak menemukannya.
- **Lupa `use App\Http\Controllers\...`** di web.php saat memanggil controller.

### Tugas / Persiapan Hari 9
1. Sempurnakan aplikasi berlayout hingga lolos checklist.
2. Tambah halaman keempat yang juga mewarisi layout.
3. Renungkan: data produk masih **ditulis manual** di controller (array). Bagaimana kalau data diambil dari **database** yang bisa ditambah/diubah? → itulah **Eloquent & migration**, materi besok.

### Jembatan ke Hari 9
"Sekarang aplikasi kita sudah punya tampilan rapi berlayout dan bisa menampilkan data dari controller. Tapi datanya masih ditulis manual sebagai array. Besok kita hubungkan Laravel ke **database** lewat **migration** (membuat tabel dari kode) dan **Eloquent** (mengelola data tanpa menulis SQL) — data pun jadi nyata dan permanen."

---

*Modul ini bisa dibagikan ke peserta sebagai bahan bacaan, atau dipegang instruktur sebagai panduan mengajar. Kunci jawaban sebaiknya tidak dibagikan sebelum sesi latihan selesai.*
