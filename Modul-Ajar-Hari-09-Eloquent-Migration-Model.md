# MODUL AJAR — HARI 9
## Eloquent, Migration & Model

*Bagian dari Pelatihan Web Programmer Dasar — Berbasis Laravel (15 Hari)*

---

## INFORMASI SESI

| Item | Keterangan |
|---|---|
| **Hari** | 9 dari 15 |
| **Fase** | Fase 3 — Laravel & Proyek |
| **Topik** | Menghubungkan Laravel ke database dengan migration, model, dan Eloquent |
| **Durasi** | 8 jam |
| **Prasyarat** | Hari 6 (SQL), Hari 7–8 (Laravel, MVC, Controller) |
| **Output** | Tabel dibuat via migration + terisi via seeder + data tampil di halaman |

### Tujuan Pembelajaran
Setelah menyelesaikan hari ini, peserta mampu:
1. Mengatur koneksi database melalui file `.env`.
2. Membuat dan menjalankan migration untuk membentuk tabel dari kode.
3. Membuat Model dan memahami Eloquent ORM.
4. Menjalankan query dasar Eloquent (`all`, `find`, `where`, `count`).
5. Menyimpan, mengubah, dan menghapus data dengan Eloquent.
6. Mengisi database dengan seeder & factory, dan menguji lewat Tinker.

### Alat & Bahan
- Proyek Laravel dari Hari 7–8, MySQL aktif (Laragon/XAMPP)
- phpMyAdmin, VS Code, terminal

---

## PETA WAKTU HARI INI

| Waktu | Sesi | Fokus |
|---|---|---|
| 08.00–10.00 | Sesi 1 — Konsep | Koneksi database & migration |
| 10.00–10.15 | Istirahat | |
| 10.15–12.00 | Sesi 2 — Lab | Model & Eloquent ORM |
| 12.00–13.00 | ISHOMA | |
| 13.00–15.00 | Sesi 3 — Lab | Menyimpan data & Tinker |
| 15.00–15.15 | Istirahat | |
| 15.15–16.30 | Sesi 4 — Mini-project | Seeder, factory, tabel utama |
| 16.30–17.00 | Sesi 5 — Review | Evaluasi & jembatan Hari 10 |

---

# SESI 1 — KONEKSI & MIGRATION (08.00–10.00)

> **Metode:** guided. Sambungkan dengan Hari 6 (kita sudah bisa SQL manual) dan Hari 8 (data produk masih array). Hari ini data jadi nyata.

### 1.1 Mengatur koneksi database (.env)
File `.env` di akar proyek menyimpan pengaturan. Untuk database:
```
DB_CONNECTION=mysql
DB_HOST=127.0.0.1
DB_PORT=3306
DB_DATABASE=toko
DB_USERNAME=root
DB_PASSWORD=
```
Langkah:
1. Buat database kosong bernama `toko` di phpMyAdmin.
2. Cocokkan `DB_DATABASE=toko` di `.env`.
3. Untuk Laragon/XAMPP standar, username `root` tanpa password.
> Setelah mengubah `.env`, kadang perlu `php artisan config:clear`.

### 1.2 Apa itu Migration?
**Migration** adalah cara membuat & mengubah struktur tabel **lewat kode**, bukan klik manual di phpMyAdmin. Keuntungannya: struktur tercatat, mudah dibagikan ke tim, dan bisa diulang di server lain.

### 1.3 Membuat migration
```bash
php artisan make:migration create_produks_table
```
File dibuat di `database/migrations/`. Isi method `up()`:
```php
public function up(): void
{
    Schema::create('produks', function (Blueprint $table) {
        $table->id();                 // primary key auto increment
        $table->string('nama');       // VARCHAR
        $table->integer('harga');     // INT
        $table->integer('stok');
        $table->timestamps();         // created_at & updated_at
    });
}
```
| Perintah | Menghasilkan |
|---|---|
| `$table->id()` | kolom `id` (primary key) |
| `$table->string('nama')` | kolom teks |
| `$table->integer('harga')` | kolom angka |
| `$table->timestamps()` | `created_at` & `updated_at` otomatis |

### 1.4 Menjalankan migration
```bash
php artisan migrate            # buat semua tabel dari migration
php artisan migrate:rollback   # batalkan migration terakhir
php artisan migrate:fresh      # hapus semua tabel & buat ulang
```
Setelah `migrate`, cek phpMyAdmin — tabel `produks` sudah terbentuk.

### 🔨 Latihan 1 (25 menit)
1. Atur `.env` agar terhubung ke database `toko`.
2. Buat migration `create_kategoris_table` (kolom: nama).
3. Jalankan `php artisan migrate` dan periksa tabelnya di phpMyAdmin.

**Kunci (untuk instruktur):**
```php
Schema::create('kategoris', function (Blueprint $table) {
    $table->id();
    $table->string('nama');
    $table->timestamps();
});
```

### ✅ Cek pemahaman Sesi 1
1. File apa yang mengatur koneksi database?
2. Apa keuntungan migration dibanding membuat tabel manual?
3. Perintah apa untuk menjalankan migration?

---

# SESI 2 — MODEL & ELOQUENT (10.15–12.00)

> **Metode:** demo + lab. Tekankan: ini menggantikan SQL manual Hari 6 dengan gaya OOP Hari 5.

### 2.1 Eloquent menggantikan SQL manual
**Eloquent** adalah ORM (Object-Relational Mapping) Laravel: setiap tabel diwakili sebuah **Model** (class), dan operasi database dilakukan lewat method — tanpa menulis SQL.
```sql
-- SQL manual (Hari 6)
SELECT * FROM produks;
SELECT * FROM produks WHERE stok < 10;
```
```php
// Eloquent (hari ini)
Produk::all();
Produk::where('stok', '<', 10)->get();
```
Hasil sama, tapi Eloquent lebih singkat, aman, dan konsisten dengan OOP.

### 2.2 Membuat Model
```bash
php artisan make:model Produk
```
Menghasilkan `app/Models/Produk.php`:
```php
<?php
namespace App\Models;

use Illuminate\Database\Eloquent\Model;

class Produk extends Model
{
    protected $fillable = ['nama', 'harga', 'stok'];
}
```
> **Konvensi nama:** Model `Produk` (tunggal) otomatis terhubung ke tabel `produks` (jamak). Laravel menjamak-kan nama model. `$fillable` = daftar kolom yang boleh diisi massal (keamanan).
>
> Tip: buat model + migration sekaligus dengan `php artisan make:model Produk -m`.

### 2.3 Query dasar Eloquent
```php
Produk::all();                          // semua data
Produk::find(1);                        // cari berdasarkan id
Produk::where('stok', '<', 10)->get();  // dengan syarat
Produk::orderBy('harga', 'desc')->get();// urutkan
Produk::count();                        // jumlah data
```

### 🔨 Latihan 2 (35 menit)
1. Buat Model `Produk` dengan `$fillable`.
2. Buat route/controller yang menjalankan `Produk::all()` dan menampilkannya di view.
3. (Jika data belum ada, isi dulu lewat phpMyAdmin atau tunggu seeder di Sesi 4.)

**Kunci (untuk instruktur):**
```php
// ProdukController.php
use App\Models\Produk;

public function index()
{
    $produk = Produk::all();
    return view('produk.index', compact('produk'));
}
```
```blade
{{-- produk/index.blade.php --}}
@foreach($produk as $item)
    <li>{{ $item->nama }} - Rp{{ $item->harga }}</li>
@endforeach
```
> Perhatikan: `$item->nama` — tiap baris adalah **object**, propertinya diakses dengan `->` (OOP Hari 5).

---

# SESI 3 — MENYIMPAN DATA & TINKER (13.00–15.00)

### 3.1 Menambah data (Create)
```php
// cara 1: create() — perlu $fillable
Produk::create([
    'nama' => 'Buku',
    'harga' => 50000,
    'stok' => 10,
]);

// cara 2: new + save()
$p = new Produk();
$p->nama = 'Pulpen';
$p->harga = 5000;
$p->stok = 100;
$p->save();
```

### 3.2 Mengubah data (Update)
```php
$p = Produk::find(1);
$p->harga = 55000;
$p->save();
```

### 3.3 Menghapus data (Delete)
```php
Produk::find(1)->delete();
```
> Semua operasi database kini lewat method Eloquent — **tanpa satu baris SQL pun**.

### 3.4 Tinker — menguji query interaktif
```bash
php artisan tinker
```
```
>>> Produk::all();
>>> Produk::create(['nama'=>'Tas','harga'=>150000,'stok'=>4]);
>>> Produk::count();
>>> Produk::find(1)->nama;
```
Tinker adalah konsol interaktif untuk mencoba kode Laravel **tanpa** membuat route/halaman — sangat berguna untuk uji cepat. Keluar dengan `exit`.

### 🔨 Latihan 3 (40 menit)
Lewat Tinker:
1. Tambah 3 produk dengan `Produk::create()`.
2. Tampilkan semua produk.
3. Ubah harga produk id 1.
4. Hapus produk id 2, lalu hitung sisa produk.

**Kunci (untuk instruktur):**
```
>>> Produk::create(['nama'=>'Buku','harga'=>50000,'stok'=>10]);
>>> Produk::create(['nama'=>'Pulpen','harga'=>5000,'stok'=>100]);
>>> Produk::create(['nama'=>'Tas','harga'=>150000,'stok'=>4]);
>>> Produk::all();
>>> $p = Produk::find(1); $p->harga = 60000; $p->save();
>>> Produk::find(2)->delete();
>>> Produk::count();
```

---

# SESI 4 — SEEDER, FACTORY & MINI-PROJECT (15.15–16.30)

> **Metode:** demo singkat lalu kerja mandiri. Menghasilkan **output resmi Hari 9**.

### 4.1 Seeder — mengisi data awal
Seeder mengisi database dengan data tertentu secara otomatis (mis. data awal saat aplikasi disiapkan).
```bash
php artisan make:seeder ProdukSeeder
```
`database/seeders/ProdukSeeder.php`:
```php
use App\Models\Produk;

public function run(): void
{
    Produk::create(['nama' => 'Buku', 'harga' => 50000, 'stok' => 10]);
    Produk::create(['nama' => 'Pulpen', 'harga' => 5000, 'stok' => 100]);
    Produk::create(['nama' => 'Tas', 'harga' => 150000, 'stok' => 4]);
}
```
Jalankan:
```bash
php artisan db:seed --class=ProdukSeeder
```

### 4.2 Factory — data dummy dalam jumlah banyak
Factory membuat banyak data acak untuk pengujian:
```php
Produk::factory()->count(10)->create();
```
(Untuk pemula, seeder manual sudah cukup; factory diperkenalkan sebagai langkah lanjut.)

### 📦 Brief Mini-project: Tabel Produk Lengkap
Bangun tabel utama aplikasi dari nol hingga tampil di halaman.

**Wajib ada:**
1. Koneksi `.env` ke database `toko`.
2. Migration tabel `produks` (nama, harga, stok, timestamps).
3. Model `Produk` dengan `$fillable`.
4. Seeder yang mengisi minimal 5 produk.
5. Halaman web yang menampilkan seluruh produk dengan `Produk::all()`.

**Kriteria lulus:**
- `php artisan migrate` membentuk tabel di database.
- `php artisan db:seed` mengisi data.
- Halaman `/produk` menampilkan data dari database (bukan array manual).
- Data tetap ada setelah server dimatikan (permanen).

### Panduan Ringkas (untuk instruktur)
```bash
php artisan make:model Produk -m          # model + migration sekaligus
# isi migration (kolom), lalu:
php artisan migrate
php artisan make:seeder ProdukSeeder
# isi seeder, lalu:
php artisan db:seed --class=ProdukSeeder
```
```php
// ProdukController.php
use App\Models\Produk;
public function index() {
    $produk = Produk::all();
    return view('produk.index', compact('produk'));
}
```
```php
// web.php
use App\Http\Controllers\ProdukController;
Route::get('/produk', [ProdukController::class, 'index']);
```

---

# SESI 5 — REVIEW & PENUTUP (16.30–17.00)

### Checklist Output Hari 9
- [ ] `.env` terhubung ke database `toko`
- [ ] Migration tabel `produks` dibuat & dijalankan
- [ ] Model `Produk` dengan `$fillable`
- [ ] Seeder mengisi minimal 5 produk
- [ ] Halaman menampilkan data via `Produk::all()`
- [ ] Data permanen (masih ada setelah server dimatikan)

### Titik Rawan Pemula (perhatian instruktur)
- **Nama tabel** — Laravel menjamak-kan model: `Produk` → `produks`. Bila tabel bernama lain, set `protected $table = 'nama_tabel';`.
- **Lupa `$fillable`** → `create()` gagal ("Add [...] to fillable").
- **Nama `DB_DATABASE` di `.env` tak cocok** dengan database yang dibuat.
- **Lupa `php artisan migrate`** setelah membuat migration.
- **Mengubah `.env` tapi tak ter-refresh** → jalankan `php artisan config:clear`.
- **Akses property salah** — `$item->nama` (object), bukan `$item['nama']`.

### Tugas / Persiapan Hari 10
1. Sempurnakan tabel produk (migration + seeder + tampil) hingga lolos checklist.
2. Tambah kolom baru lewat migration baru (mis. `deskripsi`) dan `migrate` lagi.
3. Renungkan: kita sudah bisa **menampilkan** data dari database. Tapi menambah/mengedit/menghapus masih lewat Tinker. Bagaimana kalau semua itu bisa dilakukan **dari halaman web** oleh pengguna? → itulah **CRUD lengkap**, materi besok.

### Jembatan ke Hari 10 — MVC lengkap!
"Kini ketiga bagian MVC sudah bekerja: **Model** (Eloquent, hari ini), **View** (Blade, Hari 8), **Controller** (Hari 8). Besok kita satukan semuanya menjadi **CRUD lengkap** — pengguna bisa menambah, menampilkan, mengedit, dan menghapus data langsung dari halaman web, lengkap dengan validasi. Inilah inti dari hampir semua aplikasi."

---

*Modul ini bisa dibagikan ke peserta sebagai bahan bacaan, atau dipegang instruktur sebagai panduan mengajar. Kunci jawaban sebaiknya tidak dibagikan sebelum sesi latihan selesai.*
