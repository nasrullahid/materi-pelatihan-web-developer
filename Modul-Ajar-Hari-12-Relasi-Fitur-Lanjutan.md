# MODUL AJAR — HARI 12
## Relasi Eloquent & Fitur Lanjutan

*Bagian dari Pelatihan Web Programmer Dasar — Berbasis Laravel (15 Hari)*

---

## INFORMASI SESI

| Item | Keterangan |
|---|---|
| **Hari** | 12 dari 15 |
| **Fase** | Fase 3 — Laravel & Proyek |
| **Topik** | Menghubungkan data antar tabel & fitur aplikasi lanjutan |
| **Durasi** | 8 jam |
| **Prasyarat** | Hari 9–11 (Eloquent, CRUD, Auth) |
| **Output** | Aplikasi dengan data relasional, upload gambar, pencarian & pagination |

### Tujuan Pembelajaran
Setelah menyelesaikan hari ini, peserta mampu:
1. Membuat relasi one-to-many (`hasMany`, `belongsTo`) antara kategori & produk.
2. Menggunakan eager loading (`with()`) dan menghindari masalah N+1.
3. Mengenali relasi one-to-one dan many-to-many.
4. Mengunggah, menyimpan, dan menampilkan gambar.
5. Menerapkan pagination pada daftar data.
6. Menambahkan pencarian (search) dan pengurutan (sorting).

### Alat & Bahan
- Proyek Laravel dari Hari 11 (CRUD produk + auth)
- MySQL aktif, VS Code, browser

---

## PETA WAKTU HARI INI

| Waktu | Sesi | Fokus |
|---|---|---|
| 08.00–10.00 | Sesi 1 — Konsep | Relasi one-to-many (kategori–produk) |
| 10.00–10.15 | Istirahat | |
| 10.15–12.00 | Sesi 2 — Konsep | Relasi one-to-one & many-to-many |
| 12.00–13.00 | ISHOMA | |
| 13.00–15.00 | Sesi 3 — Lab | Upload & pengelolaan gambar |
| 15.00–15.15 | Istirahat | |
| 15.15–16.30 | Sesi 4 — Mini-project | Pagination, search, aplikasi kaya fitur |
| 16.30–17.00 | Sesi 5 — Review | Evaluasi & jembatan Hari 13 |

---

# SESI 1 — RELASI ONE-TO-MANY (08.00–10.00)

> **Metode:** ceramah + lab. Sambungkan dengan Hari 6 (foreign key manual) — kini Eloquent yang mengaturnya.

### 1.1 Konsep relasi
Data nyata saling berhubungan. Contoh: **satu kategori** punya **banyak produk**, dan **satu produk** milik **satu kategori**. Ini disebut relasi **one-to-many**.

Recap Hari 6: dihubungkan lewat **foreign key** `kategori_id` di tabel `produk`. Migration:
```php
Schema::table('produks', function (Blueprint $table) {
    $table->foreignId('kategori_id')->constrained();
});
```
(atau langsung saat membuat tabel produk).

### 1.2 Mendefinisikan relasi di Model
```php
// app/Models/Kategori.php
class Kategori extends Model
{
    public function produk()
    {
        return $this->hasMany(Produk::class);   // satu kategori → banyak produk
    }
}

// app/Models/Produk.php
class Produk extends Model
{
    public function kategori()
    {
        return $this->belongsTo(Kategori::class); // satu produk → satu kategori
    }
}
```

### 1.3 Mengakses relasi
```php
// nama kategori dari sebuah produk
$produk->kategori->nama;

// semua produk dalam sebuah kategori
foreach ($kategori->produk as $p) {
    echo $p->nama;
}
```
Di Blade:
```blade
<td>{{ $produk->kategori->nama }}</td>
```
> Perhatikan: `->kategori` (tunggal, belongsTo) vs `->produk` (jamak, hasMany). Diakses seperti property, tanpa tanda kurung.

### 1.4 Eager loading & masalah N+1
```php
// LAMBAT — masalah N+1: 1 query + 1 query per produk
$produk = Produk::all();
foreach ($produk as $p) {
    echo $p->kategori->nama;   // query database tiap perulangan!
}

// CEPAT — eager loading: cukup 2 query
$produk = Produk::with('kategori')->get();
```
> `with('kategori')` memuat relasi sekaligus di awal. Untuk data banyak, ini perbaikan performa yang signifikan. Biasakan sejak sekarang.

### 🔨 Latihan 1 (35 menit)
1. Buat tabel & model `Kategori` (jika belum ada dari Hari 6/9).
2. Tambahkan foreign key `kategori_id` ke tabel `produk` (migration).
3. Definisikan relasi `hasMany` & `belongsTo`.
4. Di halaman daftar produk, tampilkan nama kategori tiap produk (pakai `with('kategori')`).

**Kunci (untuk instruktur):**
```php
// ProdukController@index
$produk = Produk::with('kategori')->get();
return view('produk.index', compact('produk'));
```
```blade
@foreach($produk as $p)
    <tr>
        <td>{{ $p->nama }}</td>
        <td>{{ $p->kategori->nama }}</td>
    </tr>
@endforeach
```

---

# SESI 2 — RELASI LAINNYA (10.15–12.00)

> **Metode:** ceramah + demo ringan. Cukup pengenalan; one-to-many tetap yang utama.

### 2.1 One-to-One
Satu entitas berpasangan tepat dengan satu entitas lain. Contoh: satu `User` punya satu `Profil`.
```php
// Model User
public function profil()
{
    return $this->hasOne(Profil::class);
}
// Model Profil
public function user()
{
    return $this->belongsTo(User::class);
}
```
Akses: `$user->profil->bio;`

### 2.2 Many-to-Many
Kedua sisi bisa punya banyak. Contoh: satu `Produk` punya banyak `Tag`, dan satu `Tag` dipakai banyak produk. Butuh **tabel pivot** (`produk_tag`).
```php
// Model Produk
public function tags()
{
    return $this->belongsToMany(Tag::class);
}
```
Akses: `$produk->tags;` (collection).

### 2.3 Ringkasan
| Method | Jenis relasi |
|---|---|
| `hasOne` / `belongsTo` | one-to-one |
| `hasMany` / `belongsTo` | one-to-many |
| `belongsToMany` | many-to-many (via pivot) |

### 🔨 Latihan 2 (25 menit)
Diskusi & rancang: untuk aplikasi toko, relasi apa yang cocok antara:
1. Produk dan Kategori? (jawab: one-to-many)
2. Produk dan Tag/Label? (jawab: many-to-many)
3. User dan Profil? (jawab: one-to-one)
Tuliskan method relasi yang sesuai untuk masing-masing.

---

# SESI 3 — UPLOAD GAMBAR (13.00–15.00)

> **Metode:** demo + lab.

### 3.1 Persiapan penyimpanan
Jalankan sekali agar file di `storage/app/public` bisa diakses dari web:
```bash
php artisan storage:link
```
Ini membuat pranala `public/storage` → `storage/app/public`.

### 3.2 Form upload
```blade
<form action="{{ route('produk.store') }}" method="POST"
      enctype="multipart/form-data">
    @csrf
    <input type="text" name="nama">
    <input type="file" name="gambar">
    <button>Simpan</button>
</form>
```
> **`enctype="multipart/form-data"` WAJIB** untuk form berisi file. Lupa ini → file tidak terkirim.

### 3.3 Menyimpan file di controller
```php
public function store(Request $request)
{
    $data = $request->validate([
        'nama'  => 'required',
        'harga' => 'required|numeric',
        'gambar' => 'nullable|image|max:2048',   // maks 2MB
    ]);

    if ($request->hasFile('gambar')) {
        $data['gambar'] = $request->file('gambar')->store('produk', 'public');
    }

    Produk::create($data);
    return redirect()->route('produk.index')->with('sukses', 'Produk ditambahkan');
}
```
`store('produk', 'public')` menyimpan file ke `storage/app/public/produk/` dan mengembalikan path-nya (mis. `produk/abc123.jpg`), yang disimpan di kolom `gambar`.

### 3.4 Menampilkan gambar
```blade
@if($produk->gambar)
    <img src="{{ asset('storage/' . $produk->gambar) }}" width="120">
@endif
```
> Path gambar disimpan di **database**; file fisiknya di **storage**. `asset('storage/...')` membentuk URL yang benar.

### 🔨 Latihan 3 (40 menit)
1. Tambahkan kolom `gambar` ke tabel produk (migration) dan `$fillable`.
2. Tambah input file di form (jangan lupa `enctype`).
3. Simpan file di `store()`, lalu tampilkan gambar di daftar produk.

---

# SESI 4 — PAGINATION, SEARCH & MINI-PROJECT (15.15–16.30)

> **Metode:** demo singkat lalu kerja mandiri. Menghasilkan **output resmi Hari 12**.

### 4.1 Pagination
```php
// controller
$produk = Produk::with('kategori')->paginate(10);   // 10 per halaman
```
```blade
{{-- view --}}
@foreach($produk as $p) ... @endforeach

{{ $produk->links() }}   {{-- navigasi 1-2-3 otomatis --}}
```
> `paginate()` membagi data per halaman; `links()` membuat tombol navigasi.

### 4.2 Pencarian (search)
```php
public function index(Request $request)
{
    $cari = $request->input('cari');

    $produk = Produk::with('kategori')
        ->when($cari, function ($query) use ($cari) {
            $query->where('nama', 'like', "%$cari%");
        })
        ->orderBy('harga', 'asc')
        ->paginate(10);

    return view('produk.index', compact('produk'));
}
```
```blade
<form method="GET">
    <input type="text" name="cari" value="{{ request('cari') }}" placeholder="Cari produk...">
    <button>Cari</button>
</form>
```
> `when($cari, ...)` hanya menerapkan filter bila kotak pencarian diisi. `value="{{ request('cari') }}"` menjaga kata kunci tetap tampil setelah mencari.

### 4.3 Sorting
```php
Produk::orderBy('harga', 'asc')->get();   // termurah dulu
Produk::orderBy('harga', 'desc')->get();  // termahal dulu
Produk::orderBy('nama', 'asc')->get();    // A–Z
```

### 📦 Brief Mini-project: Aplikasi Produk Kaya Fitur
Kembangkan aplikasi produk menjadi mendekati produk nyata.

**Wajib ada:**
1. Relasi kategori–produk (`hasMany` / `belongsTo`); tampilkan nama kategori tiap produk (pakai `with()`).
2. Upload & tampilkan gambar produk.
3. Pencarian produk berdasarkan nama.
4. Pagination pada daftar produk.
5. Pengurutan berdasarkan harga.

**Kriteria lulus:**
- Nama kategori muncul di daftar produk (tanpa error N+1).
- Gambar tampil setelah diupload.
- Pencarian menyaring hasil sesuai kata kunci.
- Daftar terbagi per halaman dengan navigasi.

### Panduan Ringkas (untuk instruktur)
```php
// ProdukController@index (menggabungkan semua)
public function index(Request $request)
{
    $cari = $request->input('cari');
    $produk = Produk::with('kategori')
        ->when($cari, fn($q) => $q->where('nama', 'like', "%$cari%"))
        ->orderBy('harga', 'asc')
        ->paginate(10);
    return view('produk.index', compact('produk'));
}
```
Form tambah butuh `enctype="multipart/form-data"`, controller `store()` menangani file (lihat Sesi 3), dan view menampilkan `<img>` + `{{ $produk->links() }}`.

---

# SESI 5 — REVIEW & PENUTUP (16.30–17.00)

### Checklist Output Hari 12
- [ ] Relasi kategori–produk berfungsi (`hasMany` / `belongsTo`)
- [ ] Nama kategori tampil di daftar produk
- [ ] `with()` dipakai untuk menghindari N+1
- [ ] Upload gambar tersimpan & tampil
- [ ] Pencarian produk berjalan
- [ ] Pagination + pengurutan berfungsi

### Titik Rawan Pemula (perhatian instruktur)
- **Lupa `enctype="multipart/form-data"`** → file tidak terkirim.
- **Lupa `php artisan storage:link`** → gambar tidak tampil.
- **Nama method relasi salah** atau foreign key (`kategori_id`) tak sesuai konvensi.
- **Masalah N+1** — lupa `with()` saat menampilkan relasi pada data banyak.
- **Tanda kurung pada relasi** — `$produk->kategori` (property), bukan `$produk->kategori()`.
- **`gambar` tak ada di `$fillable`** → path tidak tersimpan.

### Tugas / Persiapan Hari 13
1. Selesaikan aplikasi produk kaya fitur hingga lolos checklist.
2. Tambahkan filter berdasarkan kategori (dropdown).
3. Renungkan: sejauh ini data hanya bisa diakses lewat halaman web (HTML). Bagaimana jika aplikasi lain (mobile, dll) ingin mengambil data kita? → itulah **REST API**, materi besok.

### Jembatan ke Hari 13
"Aplikasi kita kini kaya fitur: data terhubung, bergambar, bisa dicari, dan tertata per halaman — sudah menyerupai produk nyata. Besok kita buka data ini agar bisa diakses aplikasi lain lewat **REST API**: menyajikan data dalam format JSON yang bisa dikonsumsi aplikasi mobile atau front-end terpisah. Ini bekal penting menuju proyek akhir."

---

*Modul ini bisa dibagikan ke peserta sebagai bahan bacaan, atau dipegang instruktur sebagai panduan mengajar. Kunci jawaban sebaiknya tidak dibagikan sebelum sesi latihan selesai.*
