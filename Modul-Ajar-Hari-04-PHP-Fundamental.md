# MODUL AJAR — HARI 4
## PHP Fundamental

*Bagian dari Pelatihan Web Programmer Dasar — Berbasis Laravel (15 Hari)*

---

## INFORMASI SESI

| Item | Keterangan |
|---|---|
| **Hari** | 4 dari 15 |
| **Fase** | Fase 2 — Jembatan Backend |
| **Topik** | Dasar pemrograman sisi server dengan PHP |
| **Durasi** | 8 jam |
| **Prasyarat** | Hari 1–3 (HTML, CSS, JavaScript) |
| **Output** | Form pendaftaran + halaman hasil yang diproses server (`form.php` + `proses.php`) |

### Tujuan Pembelajaran
Setelah menyelesaikan hari ini, peserta mampu:
1. Menjelaskan cara PHP bekerja di server (berbeda dari JavaScript di browser).
2. Menyiapkan server lokal (Laragon/XAMPP) dan menjalankan file `.php`.
3. Menulis sintaks dasar PHP: `echo`, variabel, tipe data.
4. Memakai operator, percabangan, dan perulangan.
5. Membuat fungsi (bawaan & buatan sendiri) dan mengelola array (indexed & associative).
6. Memproses data form dengan `$_POST` / `$_GET` dan memecah file dengan `include` / `require`.

### Alat & Bahan
- **Laragon** (disarankan) atau XAMPP — sudah terpasang di komputer peserta
- VS Code, browser
- Folder proyek diletakkan di folder `www` (Laragon) atau `htdocs` (XAMPP)

---

## PETA WAKTU HARI INI

| Waktu | Sesi | Fokus |
|---|---|---|
| 08.00–10.00 | Sesi 1 — Konsep | Mengenal PHP & setup server |
| 10.00–10.15 | Istirahat | |
| 10.15–12.00 | Sesi 2 — Lab | Operator, kondisi & perulangan |
| 12.00–13.00 | ISHOMA | |
| 13.00–15.00 | Sesi 3 — Lab | Fungsi & array |
| 15.00–15.15 | Istirahat | |
| 15.15–16.30 | Sesi 4 — Mini-project | Form, proses server, include |
| 16.30–17.00 | Sesi 5 — Review | Evaluasi & jembatan Hari 5 |

---

# SESI 1 — MENGENAL PHP & SETUP (08.00–10.00)

> **Metode:** ceramah + guided. Tekankan pergeseran besar: tiga hari kemarin di **browser** (front-end), sekarang pindah ke **server** (back-end).

### 1.1 Apa itu PHP?
**PHP** adalah bahasa pemrograman yang berjalan di **server**. PHP menghasilkan HTML yang lalu dikirim ke browser.

Recap analogi warung (Hari 1):
- Front-end (HTML/CSS/JS) = **ruang makan** — yang dilihat pelanggan.
- Back-end (PHP) = **dapur** — tempat pesanan diproses.

### 1.2 PHP dikerjakan di server, bukan di browser
```
[ Browser ] --- request ---> [ Server menjalankan PHP ] --- HTML jadi ---> [ Browser ]
```
Poin penting: **browser tidak pernah melihat kode PHP**. Server menjalankan PHP lalu hanya mengirim **HTML hasilnya**. (Bandingkan dengan JavaScript Hari 3 yang berjalan di browser dan bisa dilihat.)

Konsekuensinya: untuk menjalankan PHP, kita **butuh server** — tidak cukup klik dua kali file seperti HTML.

### 1.3 Menyiapkan server lokal
Untuk menjalankan PHP di komputer sendiri, kita pakai paket server lokal berisi tiga komponen:
| Komponen | Fungsi |
|---|---|
| **Apache** | web server yang melayani halaman |
| **PHP** | menjalankan kode PHP |
| **MySQL** | database (baru dipakai mulai Hari 6) |

**Laragon** (disarankan) atau **XAMPP** menyatukan ketiganya.
1. Buka Laragon → **Start All**.
2. Taruh folder proyek di dalam folder `www` (Laragon) atau `htdocs` (XAMPP).
3. Buka lewat browser: `http://localhost/nama-folder/`.
> **Penting:** file harus berakhiran `.php`, dan diakses lewat `http://localhost`, **bukan** dengan klik dua kali file (yang hanya menampilkan kode mentah).

### 1.4 Sintaks dasar & echo
```php
<?php
    echo "Halo Dunia!";
?>
```
- `<?php ... ?>` = penanda blok kode PHP.
- `echo` = menampilkan teks ke halaman.

### 1.5 Variabel & tipe data
```php
<?php
    $nama = "Budi";     // string — variabel diawali tanda $
    $umur = 25;         // number (integer)
    $tinggi = 1.75;     // number (float)
    $aktif = true;      // boolean

    echo "Nama: " . $nama;   // . menggabung teks
?>
```
> **Beda penting dari JavaScript:**
> - Variabel PHP **selalu diawali `$`**.
> - Menggabung teks pakai **titik `.`**, bukan `+`.
> - Setiap pernyataan diakhiri titik koma `;`.

### 🔨 Latihan 1 (20 menit)
Buat file `latihan.php` di folder `www`:
1. Simpan nama, umur, dan kota ke variabel.
2. Tampilkan kalimat "Saya Budi, umur 25, dari Makassar."
3. Buka lewat `http://localhost/...` dan pastikan tampil (bukan kode mentah).

**Kunci (untuk instruktur):**
```php
<?php
    $nama = "Budi";
    $umur = 25;
    $kota = "Makassar";
    echo "Saya " . $nama . ", umur " . $umur . ", dari " . $kota . ".";
?>
```

### ✅ Cek pemahaman Sesi 1
1. Di mana PHP berjalan — browser atau server?
2. Kenapa file PHP harus dibuka lewat `localhost`?
3. Apa dua perbedaan penulisan PHP vs JavaScript?

---

# SESI 2 — OPERATOR, KONDISI & PERULANGAN (10.15–12.00)

> **Metode:** demo + lab. Banyak kemiripan dengan JS Hari 3 — manfaatkan untuk mempercepat.

### 2.1 Operator
```php
$total = 10 + 5;          // 15
$sisa = 10 % 3;           // 1 (sisa bagi)
$sapaan = "Halo " . $nama;  // gabung teks pakai titik

var_dump($umur >= 18);    // bool(true)
```
| Kelompok | Operator |
|---|---|
| Hitung | `+  -  *  /  %` |
| Perbandingan | `==  !=  >  <  >=  <=` |
| Gabung teks | `.` (titik) |

### 2.2 Percabangan: if / else
```php
$nilai = 80;

if ($nilai >= 85) {
    echo "A";
} elseif ($nilai >= 70) {
    echo "B";
} else {
    echo "C";
}
```

### 2.3 switch
```php
switch ($hari) {
    case "Sabtu":
    case "Minggu":
        echo "Akhir pekan";
        break;
    default:
        echo "Hari kerja";
}
```

### 2.4 Perulangan: for
```php
for ($i = 1; $i <= 5; $i++) {
    echo $i . " ";
}
```

### 2.5 Perulangan: while & foreach
```php
// while
$n = 1;
while ($n <= 5) {
    echo $n;
    $n++;
}

// foreach — menelusuri array (paling sering dipakai)
foreach ($buah as $item) {
    echo $item;
}
```

### 🔨 Latihan 2 (35 menit)
1. Buat perulangan yang mencetak angka 1–10.
2. Untuk tiap angka, cetak "Genap" atau "Ganjil" (petunjuk: `$i % 2`).

**Kunci (untuk instruktur):**
```php
<?php
    for ($i = 1; $i <= 10; $i++) {
        if ($i % 2 == 0) {
            echo $i . ": Genap<br>";
        } else {
            echo $i . ": Ganjil<br>";
        }
    }
?>
```
> Catatan: `<br>` dipakai agar tiap baris turun di halaman HTML.

---

# SESI 3 — FUNGSI & ARRAY (13.00–15.00)

> **Metode:** demo + lab. Array associative adalah bekal penting untuk data form nanti.

### 3.1 Fungsi buatan sendiri
```php
function sapa($nama) {
    return "Halo, " . $nama;
}

echo sapa("Budi");    // Halo, Budi
echo sapa("Andi");    // Halo, Andi
```
- **parameter** (`$nama`) = input fungsi.
- **return** = nilai yang dikembalikan.

### 3.2 Fungsi bawaan PHP
PHP punya ribuan fungsi siap pakai:
```php
echo strtoupper("budi");   // BUDI
echo strlen("halo");       // 4
echo count($buah);         // jumlah item array
echo date("d-m-Y");        // tanggal hari ini
```

### 3.3 Array indexed
```php
$buah = ["apel", "jeruk", "mangga"];
echo $buah[0];        // apel (index mulai dari 0)
$buah[] = "pisang";   // menambah item
echo count($buah);    // 4
```

### 3.4 Array associative (kunci berupa nama)
```php
$siswa = [
    "nama" => "Budi",
    "umur" => 20,
    "kota" => "Makassar"
];

echo $siswa["nama"];   // Budi
$siswa["umur"] = 21;   // mengubah nilai
```
> Array associative sangat penting — data dari database dan form nanti berbentuk seperti ini.

### 3.5 Menelusuri associative array
```php
foreach ($siswa as $kunci => $nilai) {
    echo $kunci . ": " . $nilai . "<br>";
}
// nama: Budi
// umur: 21
// kota: Makassar
```

### 🔨 Latihan 3 (40 menit)
1. Buat array associative `mahasiswa` (nama, jurusan, semester).
2. Tampilkan semua isinya dalam bentuk daftar dengan `foreach`.
3. Buat fungsi `luasPersegi($sisi)` yang mengembalikan luas, lalu cetak `luasPersegi(5)`.

**Kunci (untuk instruktur):**
```php
<?php
    $mahasiswa = [
        "nama" => "Budi",
        "jurusan" => "Teknik Informatika",
        "semester" => 3
    ];
    foreach ($mahasiswa as $k => $v) {
        echo $k . ": " . $v . "<br>";
    }

    function luasPersegi($sisi) {
        return $sisi * $sisi;
    }
    echo luasPersegi(5);   // 25
?>
```

---

# SESI 4 — FORM, PROSES SERVER & MINI-PROJECT (15.15–16.30)

> **Metode:** demo singkat lalu kerja mandiri. Menghasilkan **output resmi Hari 4**.

### 4.1 Alur form → server
1. Pengguna mengisi form di halaman HTML.
2. Form dikirim (`submit`) ke sebuah file PHP.
3. PHP membaca data, memprosesnya, lalu menampilkan hasil.

```html
<!-- form.php -->
<form action="proses.php" method="POST">
    <input type="text" name="nama">
    <input type="email" name="email">
    <button type="submit">Kirim</button>
</form>
```
- `action` = file tujuan pemrosesan.
- `method="POST"` = cara mengirim data (tersembunyi, cocok untuk data).
- `name` pada tiap input = kunci untuk membaca datanya nanti.

### 4.2 Membaca data dengan superglobals
```php
<!-- proses.php -->
<?php
    $nama = $_POST["nama"];
    $email = $_POST["email"];
    echo "Halo, " . $nama . " (" . $email . ")";
?>
```
| Superglobal | Untuk |
|---|---|
| `$_POST` | data form (tidak tampil di URL) |
| `$_GET` | data lewat URL (`?nama=budi`) |

### 4.3 Memecah file: include & require
```php
<?php
    include "header.php";    // menyisipkan isi file lain
    require "koneksi.php";   // sama, tapi WAJIB ada
?>
```
| | Jika file hilang |
|---|---|
| `include` | muncul peringatan, program **lanjut** |
| `require` | muncul error, program **berhenti** |
> Berguna untuk memakai ulang bagian yang sama (header, menu, koneksi database) di banyak halaman.

### 📦 Brief Mini-project: Form Pendaftaran
Buat form pendaftaran yang datanya diproses dan ditampilkan kembali oleh server.

**Wajib ada:**
1. `form.php` — form isian: nama, email, jurusan.
2. Data dikirim ke `proses.php` dengan `method="POST"`.
3. `proses.php` membaca `$_POST` dan menampilkan kembali data yang dikirim.
4. Gunakan `include "header.php"` untuk bagian atas halaman.
5. Validasi sederhana: jika nama kosong, tampilkan pesan.

**Kriteria lulus:**
- Form terkirim dan data tampil di halaman hasil.
- `include` bekerja (header muncul di kedua halaman).
- Berjalan lewat `http://localhost` tanpa error.

### Kunci — Contoh Solusi Lengkap (untuk instruktur)

**`header.php`**
```php
<header>
    <h1>Pendaftaran Peserta</h1>
    <hr>
</header>
```

**`form.php`**
```php
<?php include "header.php"; ?>

<form action="proses.php" method="POST">
    <label>Nama:</label>
    <input type="text" name="nama"><br>

    <label>Email:</label>
    <input type="email" name="email"><br>

    <label>Jurusan:</label>
    <input type="text" name="jurusan"><br>

    <button type="submit">Daftar</button>
</form>
```

**`proses.php`**
```php
<?php include "header.php"; ?>

<?php
    $nama = $_POST["nama"];
    $email = $_POST["email"];
    $jurusan = $_POST["jurusan"];

    if ($nama == "") {
        echo "Nama wajib diisi. Silakan kembali.";
    } else {
        echo "<h2>Pendaftaran Berhasil</h2>";
        echo "Nama: " . $nama . "<br>";
        echo "Email: " . $email . "<br>";
        echo "Jurusan: " . $jurusan;
    }
?>
```

---

# SESI 5 — REVIEW & PENUTUP (16.30–17.00)

### Checklist Output Hari 4
- [ ] Server lokal berjalan; file dibuka lewat `localhost`
- [ ] `form.php` menampilkan form isian
- [ ] Data terkirim ke `proses.php` dengan POST
- [ ] `proses.php` membaca `$_POST` dan menampilkan datanya
- [ ] `include "header.php"` bekerja di kedua halaman
- [ ] Ada validasi sederhana (nama kosong)
- [ ] Tidak ada error saat dijalankan

### Titik Rawan Pemula (perhatian instruktur)
- **Lupa tanda `$`** di depan variabel → error.
- **Pakai `+` untuk menggabung teks** → di PHP harus titik `.`.
- **Lupa titik koma `;`** di akhir baris.
- **File berakhiran `.html`** tidak menjalankan PHP — harus `.php`.
- **Klik dua kali file** alih-alih membuka lewat `localhost` → kode mentah tampil.
- **Salah nama `name`** input vs kunci `$_POST` → data kosong.
- **Lupa `method="POST"`** atau `action` salah → data tidak terkirim.

### Tugas / Persiapan Hari 5
1. Sempurnakan form pendaftaran hingga lolos checklist.
2. Tantangan: percantik form dengan CSS Hari 2 (via `include` file css).
3. Renungkan: kode kita mulai panjang dan berulang. Bagaimana kalau kita "membungkus" data + perilaku dalam satu unit rapi? → itu **OOP**, materi besok.

### Jembatan ke Hari 5
"Hari ini kita menulis PHP dengan gaya **prosedural** — perintah demi perintah. Besok kita pelajari **PHP OOP (Object-Oriented Programming)**: cara menyusun kode dalam bentuk 'objek' yang rapi dan bisa dipakai ulang. Ini **fondasi wajib** — karena Laravel (mulai Hari 7) sepenuhnya dibangun di atas OOP."

---

*Modul ini bisa dibagikan ke peserta sebagai bahan bacaan, atau dipegang instruktur sebagai panduan mengajar. Kunci jawaban sebaiknya tidak dibagikan sebelum sesi latihan selesai.*
