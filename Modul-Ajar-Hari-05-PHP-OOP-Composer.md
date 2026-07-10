# MODUL AJAR — HARI 5
## PHP OOP & Composer

*Bagian dari Pelatihan Web Programmer Dasar — Berbasis Laravel (15 Hari)*

---

## INFORMASI SESI

| Item | Keterangan |
|---|---|
| **Hari** | 5 dari 15 |
| **Fase** | Fase 2 — Jembatan Backend |
| **Topik** | Pemrograman berorientasi objek & manajemen paket |
| **Durasi** | 8 jam |
| **Prasyarat** | Hari 4 (PHP Fundamental) |
| **Output** | Mini program **Manajemen Produk** berbasis OOP (in-memory) |

### Tujuan Pembelajaran
Setelah menyelesaikan hari ini, peserta mampu:
1. Menjelaskan alasan dan manfaat OOP dibanding gaya prosedural.
2. Membuat class & object beserta property dan method.
3. Menggunakan constructor dan menerapkan encapsulation (public/private/protected).
4. Menerapkan inheritance (`extends`) dan interface.
5. Memahami namespace, autoloading, dan peran Composer.
6. Menjelaskan mengapa OOP menjadi fondasi wajib untuk Laravel.

### Alat & Bahan
- Laragon/XAMPP, VS Code, browser
- **Composer** terpasang (cek dengan `composer --version` di terminal)

---

## PETA WAKTU HARI INI

| Waktu | Sesi | Fokus |
|---|---|---|
| 08.00–10.00 | Sesi 1 — Konsep | Konsep OOP: class & object |
| 10.00–10.15 | Istirahat | |
| 10.15–12.00 | Sesi 2 — Lab | Constructor & encapsulation |
| 12.00–13.00 | ISHOMA | |
| 13.00–15.00 | Sesi 3 — Lab | Inheritance & interface |
| 15.00–15.15 | Istirahat | |
| 15.15–16.30 | Sesi 4 — Mini-project | Namespace, Composer, proyek |
| 16.30–17.00 | Sesi 5 — Review | OOP untuk Laravel & jembatan Hari 6 |

---

# SESI 1 — KONSEP OOP (08.00–10.00)

> **Metode:** ceramah + lab. Tegaskan sejak awal: **hari ini adalah kunci untuk memahami Laravel nanti.**

### 1.1 Kenapa OOP?
Di Hari 4 kita menulis PHP **prosedural** — perintah demi perintah. Saat program membesar, gaya ini punya kelemahan:
- Data dan fungsi yang mengolahnya **terpisah**.
- Kode gampang **berulang**.
- **Susah dirawat** ketika fitur bertambah.

**OOP (Object-Oriented Programming)** menyelesaikan ini dengan **membungkus data + perilaku** menjadi satu unit rapi yang bisa dipakai berulang.

Analogi: **class = cetakan kue**, **object = kue yang dicetak**. Satu cetakan bisa mencetak banyak kue yang seragam.

### 1.2 Class & Object
```php
<?php
class Produk {
    public $nama;      // property (data)
    public $harga;

    public function tampil() {   // method (perilaku)
        return $this->nama . " - Rp" . $this->harga;
    }
}

$p = new Produk();      // membuat OBJECT dari class
$p->nama = "Buku";
$p->harga = 50000;
echo $p->tampil();      // Buku - Rp50000
```
| Istilah | Arti |
|---|---|
| **class** | cetakan / blueprint |
| **object** | hasil cetak dari class (`new`) |
| **property** | data milik object |
| **method** | fungsi milik object |
| `$this` | menunjuk object yang sedang aktif |
| `->` | mengakses property/method object |

### 🔨 Latihan 1 (25 menit)
1. Buat class `Mahasiswa` dengan property `nama` dan `jurusan`.
2. Tambahkan method `perkenalan()` yang mengembalikan "Saya [nama], jurusan [jurusan]".
3. Buat 2 object dan panggil method-nya.

**Kunci (untuk instruktur):**
```php
<?php
class Mahasiswa {
    public $nama;
    public $jurusan;

    public function perkenalan() {
        return "Saya " . $this->nama . ", jurusan " . $this->jurusan;
    }
}

$m1 = new Mahasiswa();
$m1->nama = "Budi";
$m1->jurusan = "Informatika";
echo $m1->perkenalan();
```

### ✅ Cek pemahaman Sesi 1
1. Apa beda class dan object?
2. Apa fungsi `$this`?
3. Kenapa OOP lebih rapi dibanding prosedural saat program membesar?

---

# SESI 2 — CONSTRUCTOR & ENCAPSULATION (10.15–12.00)

### 2.1 Constructor
Constructor adalah method khusus yang **otomatis berjalan** saat object dibuat — cocok untuk mengisi nilai awal.
```php
<?php
class Produk {
    public $nama;
    public $harga;

    public function __construct($nama, $harga) {
        $this->nama = $nama;
        $this->harga = $harga;
    }
}

$p = new Produk("Buku", 50000);   // langsung terisi
echo $p->nama;                    // Buku
```
> Nama method-nya wajib `__construct` (dua garis bawah di depan).

### 2.2 Encapsulation — melindungi data
Encapsulation membatasi akses ke data agar tidak diubah sembarangan dari luar.
```php
<?php
class Akun {
    private $saldo = 0;    // tidak bisa diakses langsung dari luar

    public function setor($jumlah) {
        $this->saldo += $jumlah;
    }
    public function cekSaldo() {
        return $this->saldo;
    }
}

$a = new Akun();
$a->setor(100000);
echo $a->cekSaldo();   // 100000
// $a->saldo = -999;   // ERROR: private, tidak bisa diakses
```

### 2.3 Access modifier
| Modifier | Bisa diakses dari |
|---|---|
| `public` | mana saja |
| `private` | hanya dari dalam class itu sendiri |
| `protected` | dari class itu & class turunannya |
> Prinsipnya: buat property `private`, sediakan method `public` untuk mengubah/membacanya secara terkontrol.

### 🔨 Latihan 2 (30 menit)
1. Buat class `Produk` dengan constructor (nama, harga, stok).
2. Buat property `stok` sebagai `private`.
3. Tambah method `jual($jumlah)` yang mengurangi stok, dan `cekStok()`.

**Kunci (untuk instruktur):**
```php
<?php
class Produk {
    public $nama;
    public $harga;
    private $stok;

    public function __construct($nama, $harga, $stok) {
        $this->nama = $nama;
        $this->harga = $harga;
        $this->stok = $stok;
    }
    public function jual($jumlah) {
        $this->stok -= $jumlah;
    }
    public function cekStok() {
        return $this->stok;
    }
}

$p = new Produk("Buku", 50000, 10);
$p->jual(3);
echo $p->cekStok();   // 7
```

---

# SESI 3 — INHERITANCE & INTERFACE (13.00–15.00)

### 3.1 Inheritance (pewarisan)
Class **anak** dapat mewarisi property & method class **induk** dengan `extends`.
```php
<?php
class Hewan {
    public function bernapas() {
        return "bernapas";
    }
}

class Kucing extends Hewan {
    public function suara() {
        return "Meong";
    }
}

$k = new Kucing();
echo $k->bernapas();   // warisan dari Hewan
echo $k->suara();      // Meong
```
> Manfaat: menghindari penulisan ulang kode yang sama untuk banyak class serupa.

### 3.2 Override
Class anak boleh **menimpa** (override) method induk:
```php
<?php
class Ayam extends Hewan {
    public function bernapas() {
        return "bernapas lewat paru-paru unggas";
    }
}
```

### 3.3 Interface — kontrak method
Interface adalah **daftar method yang wajib** dipunyai class pemakainya. Menjaga konsistensi antar class.
```php
<?php
interface Bentuk {
    public function luas();
}

class Persegi implements Bentuk {
    public $sisi;
    public function __construct($sisi) {
        $this->sisi = $sisi;
    }
    public function luas() {
        return $this->sisi * $this->sisi;
    }
}

$b = new Persegi(5);
echo $b->luas();   // 25
```
> Class yang `implements` sebuah interface **harus** menuliskan semua method yang didaftarkan interface itu.

### 🔨 Latihan 3 (40 menit)
1. Buat class induk `Kendaraan` dengan method `info()`.
2. Buat class `Mobil` dan `Motor` yang `extends Kendaraan`, masing-masing menambah method `jumlahRoda()`.
3. Buat object dari keduanya dan panggil `info()` serta `jumlahRoda()`.

**Kunci (untuk instruktur):**
```php
<?php
class Kendaraan {
    public $merk;
    public function __construct($merk) {
        $this->merk = $merk;
    }
    public function info() {
        return "Kendaraan merk " . $this->merk;
    }
}
class Mobil extends Kendaraan {
    public function jumlahRoda() { return 4; }
}
class Motor extends Kendaraan {
    public function jumlahRoda() { return 2; }
}

$mobil = new Mobil("Toyota");
echo $mobil->info() . " - " . $mobil->jumlahRoda() . " roda";
```

---

# SESI 4 — NAMESPACE, COMPOSER & MINI-PROJECT (15.15–16.30)

### 4.1 Namespace
Saat file bertambah banyak, nama class bisa **bentrok**. Namespace memberi "alamat" agar tidak tabrakan.
```php
<?php
// file: app/Produk.php
namespace App;

class Produk {
    // ...
}
```
```php
<?php
// file lain — memanggil class dari namespace
use App\Produk;

$p = new Produk();
```

### 4.2 Autoloading
Tanpa autoload, kita harus `include` tiap file class satu per satu. **Autoloading** memuat class secara otomatis saat dipakai. Composer menyediakan autoload standar (PSR-4).

### 4.3 Composer — manajer paket PHP
Composer memasang dan mengelola **paket (library)** buatan orang lain.
```bash
# di terminal
composer init                          # membuat proyek baru
composer require guzzlehttp/guzzle     # memasang sebuah paket
composer install                       # memasang semua dari composer.json
```
```php
<?php
require "vendor/autoload.php";   // memuat semua paket + autoload class kita
```
> **Penting untuk nanti:** Laravel sendiri dipasang lewat Composer. Folder `vendor/` berisi ribuan file paket — inilah alasan hosting Laravel butuh **batas inode yang besar** (yang kita bahas saat memilih hosting).

### 📦 Brief Mini-project: Manajemen Produk (OOP)
Buat program pengelolaan produk sederhana menggunakan OOP (data cukup di memori/array, belum database).

**Wajib ada:**
1. Class `Produk` dengan property `nama`, `harga`, `stok` dan constructor.
2. Method `tampil()` (menampilkan info) dan `totalNilai()` (harga × stok).
3. Buat beberapa object produk.
4. Simpan object-object itu dalam sebuah **array**.
5. Tampilkan semuanya dengan `foreach`, plus total nilai seluruh produk.

**Kriteria lulus:**
- Class terstruktur rapi dengan constructor & method.
- Banyak object dibuat dan disimpan di array.
- Output menampilkan tiap produk dan total keseluruhan.

### Kunci — Contoh Solusi Lengkap (untuk instruktur)
```php
<?php
class Produk {
    public $nama;
    public $harga;
    public $stok;

    public function __construct($nama, $harga, $stok) {
        $this->nama = $nama;
        $this->harga = $harga;
        $this->stok = $stok;
    }

    public function totalNilai() {
        return $this->harga * $this->stok;
    }

    public function tampil() {
        return $this->nama . " | Rp" . $this->harga .
               " | stok " . $this->stok .
               " | nilai Rp" . $this->totalNilai();
    }
}

// membuat banyak object dan menyimpannya di array
$daftar = [
    new Produk("Buku", 50000, 10),
    new Produk("Pulpen", 5000, 100),
    new Produk("Tas", 150000, 4),
];

$totalSemua = 0;
foreach ($daftar as $produk) {
    echo $produk->tampil() . "<br>";
    $totalSemua += $produk->totalNilai();
}
echo "<hr>Total nilai seluruh produk: Rp" . $totalSemua;
```

---

# SESI 5 — OOP UNTUK LARAVEL & PENUTUP (16.30–17.00)

### 5.1 Kenapa semua ini penting untuk Laravel?
Laravel **sepenuhnya** dibangun dengan OOP. Contoh nyata yang akan kita temui mulai Hari 7:
```php
<?php
// Controller di Laravel = sebuah class yang extends Controller
class ProdukController extends Controller {
    public function index() {
        return view("produk.index");
    }
}

// Model di Laravel = sebuah class yang extends Model
class Produk extends Model {
    // ...
}
```
Semua yang dipelajari hari ini langsung terpakai:
- **class & object** → setiap komponen Laravel adalah object.
- **extends** → Controller, Model, Middleware mewarisi class dasar Laravel.
- **method & constructor** → tempat logika ditulis.
- **namespace & Composer** → cara Laravel menata dan memuat ribuan class-nya.

> Pesan kunci: **tanpa OOP, kode Laravel terasa asing. Dengan OOP, semuanya masuk akal.**

### Checklist Output Hari 5
- [ ] Class `Produk` dengan constructor & method
- [ ] Property dengan access modifier yang sesuai
- [ ] Beberapa object dibuat dengan `new`
- [ ] Object disimpan dalam array
- [ ] `foreach` menampilkan semua produk + total nilai
- [ ] Program berjalan tanpa error

### Titik Rawan Pemula (perhatian instruktur)
- **Lupa `$this->`** saat mengakses property di dalam class.
- **Tertukar `->` (object) dengan `=>` (array)**.
- **Lupa `new`** saat membuat object.
- **Nama `__construct` salah tulis** (harus dua underscore).
- **Nama file/namespace tidak sesuai** → autoload gagal.
- **Mengakses property `private` dari luar** → error (memang disengaja).

### Tugas / Persiapan Hari 6
1. Sempurnakan program Manajemen Produk hingga lolos checklist.
2. Tantangan: tambah class `Kategori` dan hubungkan tiap produk ke satu kategori.
3. Renungkan: object produk kita **hilang saat program selesai** — masih di memori. Bagaimana menyimpannya permanen? → itu peran **database**, materi besok.

### Jembatan ke Hari 6
"Selama dua hari (Hari 4–5) kita belajar PHP: prosedural lalu OOP. Tapi semua data kita masih **hilang begitu program selesai**. Besok kita masuk **Database & SQL** — tempat data disimpan secara permanen. Setelah itu (Hari 7) barulah kita satukan semuanya di **Laravel**."

---

*Modul ini bisa dibagikan ke peserta sebagai bahan bacaan, atau dipegang instruktur sebagai panduan mengajar. Kunci jawaban sebaiknya tidak dibagikan sebelum sesi latihan selesai.*
