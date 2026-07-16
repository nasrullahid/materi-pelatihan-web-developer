# MODUL AJAR — HARI 10
## CRUD & Validasi

*Bagian dari Pelatihan Web Programmer Dasar — Berbasis Laravel (15 Hari)*

---

## INFORMASI SESI

| Item | Keterangan |
|---|---|
| **Hari** | 10 dari 15 |
| **Fase** | Fase 3 — Laravel & Proyek |
| **Topik** | Membangun modul CRUD lengkap dengan validasi |
| **Durasi** | 8 jam |
| **Prasyarat** | Hari 7–9 (Laravel, Blade, Controller, Eloquent) |
| **Output** | Modul CRUD produk lengkap & berfungsi (tambah, tampil, edit, hapus) dengan validasi |

### Tujuan Pembelajaran
Setelah menyelesaikan hari ini, peserta mampu:
1. Menjelaskan alur CRUD dan pemetaannya ke 7 method resource controller.
2. Menampilkan daftar (index) dan detail (show) data.
3. Membuat form tambah dan menyimpan data (create, store).
4. Mengedit dan memperbarui data (edit, update).
5. Menghapus data dengan konfirmasi (destroy).
6. Memvalidasi input dan memberi umpan balik (flash message & redirect).

### Alat & Bahan
- Proyek Laravel dari Hari 9 (Model `Produk` & tabel `produks` sudah ada)
- Laragon/XAMPP, VS Code, browser

---

## PETA WAKTU HARI INI

| Waktu | Sesi | Fokus |
|---|---|---|
| 08.00–10.00 | Sesi 1 — Konsep | Alur CRUD & menampilkan data (Read) |
| 10.00–10.15 | Istirahat | |
| 10.15–12.00 | Sesi 2 — Lab | Menambah data (Create) |
| 12.00–13.00 | ISHOMA | |
| 13.00–15.00 | Sesi 3 — Lab | Mengubah & menghapus (Update, Delete) |
| 15.00–15.15 | Istirahat | |
| 15.15–16.30 | Sesi 4 — Mini-project | Validasi, flash message, CRUD penuh |
| 16.30–17.00 | Sesi 5 — Review | Evaluasi & jembatan Hari 11 |

---

# SESI 1 — ALUR CRUD & READ (08.00–10.00)

> **Metode:** ceramah singkat + lab. Ini hari puncak — semua materi Laravel bersatu. Tekankan CRUD adalah pola inti hampir semua aplikasi.

### 1.1 Apa itu CRUD?
**CRUD** = empat operasi dasar terhadap data:
| Operasi | Arti | Method resource |
|---|---|---|
| **Create** | menambah data | `create` (form), `store` (simpan) |
| **Read** | membaca data | `index` (daftar), `show` (detail) |
| **Update** | mengubah data | `edit` (form), `update` (simpan) |
| **Delete** | menghapus data | `destroy` |

### 1.2 Satu baris route untuk semua
```php
// routes/web.php
use App\Http\Controllers\ProdukController;

Route::resource('produk', ProdukController::class);
```
Baris ini otomatis membuat **7 route** yang terhubung ke 7 method di controller. Lihat dengan `php artisan route:list`.

Buat resource controller sekaligus:
```bash
php artisan make:controller ProdukController --resource --model=Produk
```

### 1.3 Read — menampilkan daftar (index)
```php
public function index()
{
    $produk = Produk::all();
    return view('produk.index', compact('produk'));
}
```
```blade
{{-- produk/index.blade.php --}}
<a href="{{ route('produk.create') }}">+ Tambah Produk</a>
<table>
@foreach($produk as $p)
    <tr>
        <td>{{ $p->nama }}</td>
        <td>Rp{{ $p->harga }}</td>
        <td>{{ $p->stok }}</td>
        <td>
            <a href="{{ route('produk.edit', $p->id) }}">Edit</a>
        </td>
    </tr>
@endforeach
</table>
```

### 1.4 Read — menampilkan detail (show)
```php
public function show($id)
{
    $produk = Produk::findOrFail($id);
    return view('produk.show', compact('produk'));
}
```
> `findOrFail($id)` mengambil satu data; bila tidak ada, otomatis menampilkan halaman **404**.

### 🔨 Latihan 1 (25 menit)
1. Buat resource controller `ProdukController`.
2. Daftarkan `Route::resource('produk', ...)`.
3. Isi method `index()` dan buat view tabel yang menampilkan semua produk.

### ✅ Cek pemahaman Sesi 1
1. Sebutkan 4 operasi CRUD dan method-nya.
2. Apa keuntungan `Route::resource`?
3. Apa beda `index` dan `show`?

---

# SESI 2 — CREATE (10.15–12.00)

> **Metode:** demo + lab.

### 2.1 Form tambah (create)
```php
public function create()
{
    return view('produk.create');
}
```
```blade
{{-- produk/create.blade.php --}}
<form action="{{ route('produk.store') }}" method="POST">
    @csrf
    <label>Nama:</label>
    <input type="text" name="nama"><br>

    <label>Harga:</label>
    <input type="number" name="harga"><br>

    <label>Stok:</label>
    <input type="number" name="stok"><br>

    <button type="submit">Simpan</button>
</form>
```
> **`@csrf` WAJIB** di setiap form Laravel. Ini token keamanan yang mencegah pemalsuan pengiriman form (CSRF). Lupa `@csrf` → error **419**.

### 2.2 Menyimpan (store)
```php
public function store(Request $request)
{
    Produk::create($request->all());

    return redirect()->route('produk.index')
        ->with('sukses', 'Produk berhasil ditambahkan');
}
```
Alurnya: ambil input form (`$request`) → simpan lewat Eloquent → **redirect** kembali ke daftar dengan **pesan sukses**.
> Ingat: kolom yang disimpan harus terdaftar di `$fillable` model (Hari 9).

### 🔨 Latihan 2 (35 menit)
1. Buat method `create()` dan view form-nya (jangan lupa `@csrf`).
2. Buat method `store()` yang menyimpan data dan redirect ke index.
3. Uji: tambah produk baru lewat form, pastikan muncul di daftar.

**Kunci (untuk instruktur):** lihat solusi lengkap di Sesi 4.

---

# SESI 3 — UPDATE & DELETE (13.00–15.00)

> **Metode:** demo + lab.

### 3.1 Form edit
```php
public function edit($id)
{
    $produk = Produk::findOrFail($id);
    return view('produk.edit', compact('produk'));
}
```
```blade
{{-- produk/edit.blade.php: data lama sudah terisi --}}
<form action="{{ route('produk.update', $produk->id) }}" method="POST">
    @csrf
    @method('PUT')
    <input type="text" name="nama" value="{{ $produk->nama }}"><br>
    <input type="number" name="harga" value="{{ $produk->harga }}"><br>
    <input type="number" name="stok" value="{{ $produk->stok }}"><br>
    <button type="submit">Update</button>
</form>
```
> **`@method('PUT')`** memberi tahu Laravel ini permintaan *update*. Form HTML hanya mendukung GET & POST, jadi Laravel memakai trik ini untuk PUT/DELETE.

### 3.2 Memperbarui (update)
```php
public function update(Request $request, $id)
{
    $produk = Produk::findOrFail($id);
    $produk->update($request->all());

    return redirect()->route('produk.index')
        ->with('sukses', 'Produk berhasil diperbarui');
}
```

### 3.3 Menghapus (destroy) + konfirmasi
```blade
<form action="{{ route('produk.destroy', $p->id) }}" method="POST"
      onsubmit="return confirm('Yakin hapus produk ini?')">
    @csrf
    @method('DELETE')
    <button type="submit">Hapus</button>
</form>
```
```php
public function destroy($id)
{
    Produk::findOrFail($id)->delete();
    return redirect()->route('produk.index')
        ->with('sukses', 'Produk berhasil dihapus');
}
```
> `confirm()` memunculkan dialog "Yakin?" — mencegah penghapusan tak sengaja.

### 🔨 Latihan 3 (40 menit)
1. Buat method `edit()` dan `update()` beserta view form edit (isi `@method('PUT')`).
2. Buat tombol hapus dengan konfirmasi dan method `destroy()`.
3. Uji: edit sebuah produk, lalu hapus produk lain.

---

# SESI 4 — VALIDASI, FLASH & MINI-PROJECT (15.15–16.30)

> **Metode:** demo singkat lalu kerja mandiri menyatukan semuanya. Menghasilkan **output resmi Hari 10**.

### 4.1 Validasi input
Jangan percaya input pengguna begitu saja. Validasi di controller (`store` & `update`):
```php
$request->validate([
    'nama'  => 'required',
    'harga' => 'required|numeric',
    'stok'  => 'required|integer|min:0',
]);
```
| Aturan | Arti |
|---|---|
| `required` | wajib diisi |
| `numeric` | harus angka |
| `integer` | harus bilangan bulat |
| `min:0` | nilai minimal 0 |
| `max:255` | panjang/nilai maksimal |
| `email` | format email valid |

Jika validasi gagal, Laravel otomatis kembali ke form dengan pesan error.

### 4.2 Menampilkan error di view
```blade
@if($errors->any())
    <ul style="color:red">
    @foreach($errors->all() as $error)
        <li>{{ $error }}</li>
    @endforeach
    </ul>
@endif
```

### 4.3 Flash message
Pesan singkat yang tampil sekali setelah aksi berhasil:
```php
// di controller
->with('sukses', 'Data tersimpan');
```
```blade
{{-- di layout / view --}}
@if(session('sukses'))
    <div class="alert">{{ session('sukses') }}</div>
@endif
```

### 📦 Brief Mini-project: CRUD Produk Lengkap
Bangun modul manajemen produk penuh — pencapaian besar yang menyatukan semua materi.

**Wajib ada:**
1. Daftar produk (index) dalam tabel + tombol Tambah/Edit/Hapus.
2. Form tambah + simpan (create, store).
3. Form edit + update.
4. Hapus dengan konfirmasi.
5. Validasi input di store & update.
6. Flash message setelah setiap aksi berhasil.

**Kriteria lulus:**
- Keempat operasi CRUD berfungsi dari halaman web.
- Input tidak valid ditolak dengan pesan error.
- Setiap aksi berhasil menampilkan flash message.
- Data tersimpan permanen di database.

### Kunci — Contoh Solusi Lengkap (untuk instruktur)

**`routes/web.php`**
```php
use App\Http\Controllers\ProdukController;
Route::resource('produk', ProdukController::class);
```

**`app/Http/Controllers/ProdukController.php`**
```php
<?php
namespace App\Http\Controllers;

use App\Models\Produk;
use Illuminate\Http\Request;

class ProdukController extends Controller
{
    public function index()
    {
        $produk = Produk::all();
        return view('produk.index', compact('produk'));
    }

    public function create()
    {
        return view('produk.create');
    }

    public function store(Request $request)
    {
        $request->validate([
            'nama'  => 'required',
            'harga' => 'required|numeric',
            'stok'  => 'required|integer|min:0',
        ]);
        Produk::create($request->all());
        return redirect()->route('produk.index')
            ->with('sukses', 'Produk ditambahkan');
    }

    public function edit($id)
    {
        $produk = Produk::findOrFail($id);
        return view('produk.edit', compact('produk'));
    }

    public function update(Request $request, $id)
    {
        $request->validate([
            'nama'  => 'required',
            'harga' => 'required|numeric',
            'stok'  => 'required|integer|min:0',
        ]);
        Produk::findOrFail($id)->update($request->all());
        return redirect()->route('produk.index')
            ->with('sukses', 'Produk diperbarui');
    }

    public function destroy($id)
    {
        Produk::findOrFail($id)->delete();
        return redirect()->route('produk.index')
            ->with('sukses', 'Produk dihapus');
    }
}
```

**`resources/views/produk/index.blade.php`**
```blade
@extends('layouts.app')
@section('konten')
    @if(session('sukses'))
        <div class="alert">{{ session('sukses') }}</div>
    @endif

    <a href="{{ route('produk.create') }}">+ Tambah Produk</a>
    <table border="1">
        <tr><th>Nama</th><th>Harga</th><th>Stok</th><th>Aksi</th></tr>
        @foreach($produk as $p)
        <tr>
            <td>{{ $p->nama }}</td>
            <td>{{ $p->harga }}</td>
            <td>{{ $p->stok }}</td>
            <td>
                <a href="{{ route('produk.edit', $p->id) }}">Edit</a>
                <form action="{{ route('produk.destroy', $p->id) }}"
                      method="POST"
                      onsubmit="return confirm('Yakin hapus?')"
                      style="display:inline">
                    @csrf
                    @method('DELETE')
                    <button>Hapus</button>
                </form>
            </td>
        </tr>
        @endforeach
    </table>
@endsection
```

**`resources/views/produk/create.blade.php`**
```blade
@extends('layouts.app')
@section('konten')
    @if($errors->any())
        <ul style="color:red">
        @foreach($errors->all() as $e) <li>{{ $e }}</li> @endforeach
        </ul>
    @endif

    <form action="{{ route('produk.store') }}" method="POST">
        @csrf
        <input type="text" name="nama" placeholder="Nama"><br>
        <input type="number" name="harga" placeholder="Harga"><br>
        <input type="number" name="stok" placeholder="Stok"><br>
        <button>Simpan</button>
    </form>
@endsection
```
(`edit.blade.php` sama seperti `create` + `@method('PUT')` dan `value="{{ $produk->... }}"`.)

---

# SESI 5 — REVIEW & PENUTUP (16.30–17.00)

### Checklist Output Hari 10
- [ ] `Route::resource` terpasang & `route:list` menampilkan 7 route
- [ ] Daftar produk tampil (index)
- [ ] Tambah produk berfungsi (create/store)
- [ ] Edit produk berfungsi (edit/update)
- [ ] Hapus produk berfungsi + konfirmasi
- [ ] Validasi menolak input kosong/salah
- [ ] Flash message muncul setelah aksi berhasil

### Titik Rawan Pemula (perhatian instruktur)
- **Lupa `@csrf`** di form → error **419 Page Expired**.
- **Lupa `@method('PUT')` / `@method('DELETE')`** pada edit/hapus → aksi tak berjalan.
- **Nama `name` input tak cocok** kolom / `$fillable` → data tak tersimpan.
- **Lupa menampilkan `$errors`** → user tak tahu kenapa gagal.
- **Salah nama route** di `route('...')` → error. Cek dengan `route:list`.
- **`create` vs `store`, `edit` vs `update`** tertukar — ingat: yang tanpa "form" (store/update) memproses data.

### Tugas / Persiapan Hari 11
1. Selesaikan CRUD produk hingga lolos checklist.
2. Tambah CRUD untuk tabel `kategori` sebagai latihan mandiri.
3. Renungkan: siapa saja kini bisa menambah & menghapus produk — tanpa login. Bagaimana membatasi agar hanya pengguna terdaftar yang boleh? → itulah **Autentikasi**, materi besok.

### Jembatan ke Hari 11
"Selamat — kalian baru saja membangun **aplikasi CRUD penuh**, inti dari hampir semua sistem informasi. Tapi ada satu masalah: halaman kelola produk kita terbuka untuk siapa saja. Besok kita tambahkan **autentikasi** — sistem login/logout dan halaman terproteksi — agar hanya pengguna yang berhak bisa mengubah data."

---

*Modul ini bisa dibagikan ke peserta sebagai bahan bacaan, atau dipegang instruktur sebagai panduan mengajar. Kunci jawaban sebaiknya tidak dibagikan sebelum sesi latihan selesai.*
