# MODUL AJAR — HARI 13
## REST API & Integrasi

*Bagian dari Pelatihan Web Programmer Dasar — Berbasis Laravel (15 Hari)*

---

## INFORMASI SESI

| Item | Keterangan |
|---|---|
| **Hari** | 13 dari 15 |
| **Fase** | Fase 3 — Laravel & Proyek |
| **Topik** | Menyajikan data sebagai REST API dalam format JSON |
| **Durasi** | 8 jam |
| **Prasyarat** | Hari 10–12 (CRUD, Auth, Relasi) |
| **Output** | API CRUD produk berfungsi & teruji lewat Postman |

### Tujuan Pembelajaran
Setelah menyelesaikan hari ini, peserta mampu:
1. Menjelaskan konsep REST API dan format JSON.
2. Memakai HTTP method (GET, POST, PUT, DELETE) dan status code.
3. Membuat route API di `routes/api.php`.
4. Membuat controller API yang mengembalikan JSON.
5. Merapikan output dengan API Resource.
6. Menguji API menggunakan Postman.

### Alat & Bahan
- Proyek Laravel dari Hari 12
- **Postman** (atau alternatif seperti Insomnia / Thunder Client di VS Code)

---

## PETA WAKTU HARI INI

| Waktu | Sesi | Fokus |
|---|---|---|
| 08.00–10.00 | Sesi 1 — Konsep | Konsep REST API & JSON |
| 10.00–10.15 | Istirahat | |
| 10.15–12.00 | Sesi 2 — Lab | API routes & controller |
| 12.00–13.00 | ISHOMA | |
| 13.00–15.00 | Sesi 3 — Lab | CRUD API & API Resource |
| 15.00–15.15 | Istirahat | |
| 15.15–16.30 | Sesi 4 — Mini-project | Testing Postman & API CRUD |
| 16.30–17.00 | Sesi 5 — Review | Evaluasi & jembatan Hari 14 |

---

# SESI 1 — KONSEP REST & JSON (08.00–10.00)

> **Metode:** ceramah + demo. Mulai dari pertanyaan: bagaimana aplikasi mobile bisa mengambil data dari aplikasi web kita?

### 1.1 Web biasa vs API
| | Web biasa | API |
|---|---|---|
| Mengembalikan | **HTML** | **JSON** (data mentah) |
| Untuk | dilihat manusia di browser | dikonsumsi aplikasi lain (mobile, dll) |
| Kode | `return view(...)` | `return response()->json(...)` |

**Backend (dapur) sama**; yang berbeda cara menyajikan — HTML untuk mata manusia, JSON untuk mesin. **REST API** adalah gaya standar membangun API menggunakan HTTP.

### 1.2 JSON — format pertukaran data
```json
{
    "id": 1,
    "nama": "Buku",
    "harga": 50000,
    "stok": 10
}
```
- Berupa pasangan `"kunci": nilai`.
- Ringan, mudah dibaca, dan **standar universal** — dipahami hampir semua bahasa.
- Mirip associative array PHP (Hari 4).

### 1.3 HTTP method & status code
Method menyatakan operasi (sama seperti CRUD):
| Method | Operasi |
|---|---|
| `GET` | ambil data (Read) |
| `POST` | buat data (Create) |
| `PUT` / `PATCH` | ubah data (Update) |
| `DELETE` | hapus data (Delete) |

Status code menyatakan hasil:
| Code | Arti |
|---|---|
| `200` | OK — berhasil |
| `201` | Created — berhasil dibuat |
| `404` | Not Found — data tak ditemukan |
| `422` | Unprocessable — validasi gagal |
| `500` | Server Error — kesalahan server |

### 🔨 Latihan 1 (20 menit — diskusi)
Untuk setiap aksi, tentukan method + status code yang tepat:
1. Menampilkan daftar produk. (GET, 200)
2. Menambah produk baru. (POST, 201)
3. Mengubah harga produk. (PUT, 200)
4. Meminta produk yang tidak ada. (GET, 404)

### ✅ Cek pemahaman Sesi 1
1. Apa beda output web biasa dan API?
2. Method HTTP apa untuk menambah data?
3. Apa arti status code 201 dan 404?

---

# SESI 2 — API ROUTES & CONTROLLER (10.15–12.00)

> **Metode:** demo + lab.

### 2.1 Mengaktifkan API (Laravel 11+)
Sejak Laravel 11, `routes/api.php` tidak ada secara default. Aktifkan sekali:
```bash
php artisan install:api
```
Ini membuat `routes/api.php` dan menyiapkan Laravel Sanctum (untuk keamanan API).
> Pada Laravel 10 ke bawah, `routes/api.php` sudah tersedia — langkah ini dilewati.

### 2.2 Route API
```php
// routes/api.php
use App\Http\Controllers\Api\ProdukController;

Route::apiResource('produk', ProdukController::class);
```
- Semua route di `api.php` otomatis berawalan **`/api`** → jadi `/api/produk`.
- `apiResource` membuat **5 endpoint**: `index`, `store`, `show`, `update`, `destroy` (tanpa `create`/`edit` karena API tidak punya form).

Cek dengan `php artisan route:list`.

### 2.3 Controller API
```bash
php artisan make:controller Api/ProdukController --api
```
```php
<?php
namespace App\Http\Controllers\Api;

use App\Http\Controllers\Controller;
use App\Models\Produk;
use Illuminate\Http\Request;

class ProdukController extends Controller
{
    public function index()
    {
        return response()->json(Produk::all());
    }
}
```
> `response()->json()` mengubah data menjadi JSON. Bahkan `return Produk::all();` saja sudah otomatis diubah Laravel menjadi JSON.

### 🔨 Latihan 2 (30 menit)
1. Jalankan `php artisan install:api` (jika Laravel 11+).
2. Buat `Api/ProdukController` dengan `--api`.
3. Isi `index()` untuk mengembalikan semua produk sebagai JSON.
4. Daftarkan `apiResource` dan buka `/api/produk` di browser — harus muncul JSON.

---

# SESI 3 — CRUD API & RESOURCE (13.00–15.00)

> **Metode:** demo + lab.

### 3.1 CRUD API lengkap
```php
// Read satu
public function show($id)
{
    return response()->json(Produk::findOrFail($id));
}

// Create
public function store(Request $request)
{
    $request->validate([
        'nama'  => 'required',
        'harga' => 'required|numeric',
    ]);
    $produk = Produk::create($request->all());
    return response()->json($produk, 201);   // 201 = Created
}

// Update
public function update(Request $request, $id)
{
    $produk = Produk::findOrFail($id);
    $produk->update($request->all());
    return response()->json($produk);
}

// Delete
public function destroy($id)
{
    Produk::findOrFail($id)->delete();
    return response()->json(['message' => 'Produk dihapus']);
}
```
> Bila validasi gagal, Laravel otomatis mengembalikan JSON error dengan status **422** (asalkan request mengirim header `Accept: application/json`).

### 3.2 API Resource — merapikan output
Kadang kita ingin memilih kolom mana yang tampil atau memformatnya.
```bash
php artisan make:resource ProdukResource
```
```php
// app/Http/Resources/ProdukResource.php
public function toArray($request)
{
    return [
        'id'    => $this->id,
        'nama'  => $this->nama,
        'harga' => 'Rp' . number_format($this->harga),
    ];
}
```
Pakai di controller:
```php
use App\Http\Resources\ProdukResource;

public function index()
{
    return ProdukResource::collection(Produk::all());
}

public function show($id)
{
    return new ProdukResource(Produk::findOrFail($id));
}
```
> API Resource memisahkan **bentuk data yang dikirim** dari struktur tabel — output jadi rapi & konsisten.

### 🔨 Latihan 3 (40 menit)
1. Lengkapi controller API: `show`, `store`, `update`, `destroy`.
2. Tambahkan validasi di `store`.
3. (Lanjut) Buat `ProdukResource` dan pakai di `index` & `show`.

---

# SESI 4 — TESTING POSTMAN & MINI-PROJECT (15.15–16.30)

> **Metode:** demo Postman lalu kerja mandiri. Menghasilkan **output resmi Hari 13**.

### 4.1 Menguji dengan Postman
Postman adalah alat untuk mengirim request HTTP dan melihat responsnya.
Langkah menguji sebuah endpoint:
1. **Pilih method** (GET/POST/PUT/DELETE) dari dropdown.
2. **Isi URL**, mis. `http://localhost:8000/api/produk`.
3. **Set header**: `Accept: application/json` (penting agar error pun berupa JSON).
4. Untuk **POST/PUT**: buka tab **Body → raw → JSON**, isi datanya:
   ```json
   {
       "nama": "Meja",
       "harga": 300000,
       "stok": 5
   }
   ```
5. Klik **Send**, amati **respons** (JSON) dan **status code**.

### 4.2 Contoh pengujian tiap endpoint
| Method | URL | Hasil diharapkan |
|---|---|---|
| GET | `/api/produk` | daftar produk, 200 |
| GET | `/api/produk/1` | satu produk, 200 |
| POST | `/api/produk` | produk baru, 201 |
| PUT | `/api/produk/1` | produk terupdate, 200 |
| DELETE | `/api/produk/1` | pesan sukses, 200 |

### 📦 Brief Mini-project: API CRUD Produk
Bangun dan uji API lengkap untuk data produk.

**Wajib ada:**
1. `apiResource('produk', ...)` di `routes/api.php`.
2. GET semua & GET satu produk (JSON).
3. POST menambah produk (status **201**) dengan validasi.
4. PUT mengubah & DELETE menghapus produk.
5. Semua diuji lewat Postman (screenshot/bukti hasil).

**Kriteria lulus:**
- Kelima endpoint berfungsi dan mengembalikan JSON.
- Status code sesuai (201 saat create, 404 saat data tak ada).
- Validasi menolak input tidak lengkap (422).
- Pengujian Postman terdokumentasi.

### Panduan Ringkas (untuk instruktur)
```bash
php artisan install:api
php artisan make:controller Api/ProdukController --api
```
```php
// routes/api.php
Route::apiResource('produk', ProdukController::class);
```
Isi kelima method (lihat Sesi 3), lalu uji tiap endpoint di Postman sesuai tabel di atas.

---

# SESI 5 — REVIEW & PENUTUP (16.30–17.00)

### Checklist Output Hari 13
- [ ] `routes/api.php` aktif (install:api bila Laravel 11+)
- [ ] `apiResource` terpasang; `/api/produk` menghasilkan JSON
- [ ] GET (index & show) berfungsi
- [ ] POST menambah dengan status 201
- [ ] PUT & DELETE berfungsi
- [ ] Validasi mengembalikan 422 saat gagal
- [ ] Semua diuji di Postman

### Titik Rawan Pemula (perhatian instruktur)
- **Lupa `php artisan install:api`** (Laravel 11+) → route `/api` tidak ada.
- **Lupa header `Accept: application/json`** di Postman → error tampil HTML, bukan JSON.
- **Body POST bukan format JSON** (pilih raw → JSON) → data tak terbaca.
- **Salah URL** — API memakai awalan `/api/...`, bukan URL web biasa.
- **Field tak di `$fillable`** → data tak tersimpan (sama seperti CRUD web).
- **Mengharap form** — API tidak punya halaman `create`/`edit`.

### Tugas / Persiapan Hari 14
1. Selesaikan & uji API CRUD produk hingga lolos checklist.
2. Tambahkan endpoint API untuk kategori (dengan relasi).
3. **Persiapan Proyek Akhir:** pikirkan ide aplikasi yang ingin dibangun besok (mis. manajemen inventaris, perpustakaan, to-do, katalog). Siapkan gambaran fitur CRUD utamanya.

### Jembatan ke Hari 14
"Kalian kini menguasai fondasi lengkap Laravel: routing, MVC, database, relasi, autentikasi, CRUD, dan API. Dua hari terakhir adalah puncaknya — **Proyek Akhir**. Besok (Hari 14) kita bangun sebuah aplikasi lengkap dari nol, menerapkan semua yang dipelajari. Lusa (Hari 15) kita finalisasi, **deploy ke internet**, dan presentasi. Mulai pikirkan aplikasi apa yang ingin kalian buat!"

---

*Modul ini bisa dibagikan ke peserta sebagai bahan bacaan, atau dipegang instruktur sebagai panduan mengajar. Kunci jawaban sebaiknya tidak dibagikan sebelum sesi latihan selesai.*
