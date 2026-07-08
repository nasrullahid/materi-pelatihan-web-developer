# MODUL AJAR — HARI 1
## Pengenalan Web & HTML

*Bagian dari Pelatihan Web Programmer Dasar — Berbasis Laravel (15 Hari)*

---

## INFORMASI SESI

| Item | Keterangan |
|---|---|
| **Hari** | 1 dari 15 |
| **Fase** | Fase 1 — Fondasi Web |
| **Topik** | Cara kerja web & dasar HTML |
| **Durasi** | 8 jam |
| **Prasyarat** | Tidak ada (materi pembuka) |
| **Output** | Halaman `profil.html` (CV online statis) |

### Tujuan Pembelajaran
Setelah menyelesaikan hari ini, peserta mampu:
1. Menjelaskan cara kerja web (client–server, request–response) dengan bahasa sendiri.
2. Membedakan peran front-end dan back-end.
3. Menyiapkan lingkungan kerja (VS Code + Live Server) dan struktur folder proyek.
4. Menulis dokumen HTML yang benar dari nol.
5. Menggunakan elemen HTML dasar: heading, paragraf, list, link, gambar, tabel, dan form.
6. Menyusun halaman dengan tag semantik (`header`, `nav`, `main`, `section`, `footer`).

### Alat & Bahan
- Laptop tiap peserta, koneksi internet
- **VS Code** + ekstensi: **Live Server**, **Prettier**, **Auto Rename Tag**
- Browser (Chrome/Firefox)
- 1 file foto (bisa foto peserta atau gambar contoh) untuk latihan
- Proyektor untuk instruktur

---

## PETA WAKTU HARI INI

| Waktu | Sesi | Fokus |
|---|---|---|
| 08.00–10.00 | Sesi 1 — Konsep | Bagaimana web bekerja |
| 10.00–10.15 | Istirahat | |
| 10.15–12.00 | Sesi 2 — Guided | Setup + dokumen HTML pertama |
| 12.00–13.00 | ISHOMA | |
| 13.00–15.00 | Sesi 3 — Lab | Elemen HTML & tag semantik |
| 15.00–15.15 | Istirahat | |
| 15.15–16.30 | Sesi 4 — Mini-project | Halaman profil (tabel + form) |
| 16.30–17.00 | Sesi 5 — Review | Output, evaluasi, PR |

---

# SESI 1 — BAGAIMANA WEB BEKERJA (08.00–10.00)

> **Metode:** ceramah interaktif + tanya jawab. Belum ada praktik ngoding. Tujuannya membangun "peta besar" supaya peserta paham *kenapa* mereka belajar HTML, PHP, dan Laravel nanti.

### 1.1 Apa itu website?
Website adalah kumpulan halaman yang bisa dibuka lewat browser. Setiap halaman pada dasarnya adalah **file teks** yang dikirim dari sebuah komputer (server) ke komputer kita (client), lalu ditampilkan oleh browser.

**Analogi warung makan:**
- Kamu (browser/client) datang dan **memesan** menu → ini disebut **request**.
- Dapur (server) **menyiapkan** pesanan → memproses request.
- Pelayan **mengantar** makanan ke meja → ini disebut **response**.
- Kamu **menikmati** makanan → browser menampilkan halaman.

### 1.2 Client & Server
- **Client**: perangkat yang meminta halaman (biasanya browser di HP/laptop).
- **Server**: komputer yang menyimpan file website dan menyajikannya saat diminta.

Keduanya berkomunikasi lewat aturan bernama **HTTP** (HyperText Transfer Protocol).

```
[ Browser ]  ---- request (GET /profil.html) ---->  [ Server ]
[ Browser ]  <---- response (kode HTML) ----------  [ Server ]
```

### 1.3 URL, Domain, DNS
- **URL** contoh: `https://situssaya.com/tentang`
  - `https` = protokol (cara berkomunikasi, versi aman dari http)
  - `situssaya.com` = **domain** (alamat yang mudah diingat)
  - `/tentang` = path (halaman spesifik)
- **DNS** = "buku telepon internet". Mengubah nama domain menjadi alamat IP server (mis. `situssaya.com` → `103.xx.xx.xx`).
- **Hosting** = tempat file website disimpan agar online 24 jam. (Ini yang nanti kita pakai di Hari 15 untuk deploy.)

### 1.4 Front-end vs Back-end
| | Front-end | Back-end |
|---|---|---|
| Apa | Yang **dilihat & disentuh** pengguna | Yang bekerja **di balik layar** |
| Berjalan di | Browser (client) | Server |
| Bahasa | HTML, CSS, JavaScript | PHP, database, Laravel |
| Analogi warung | Meja, menu, tampilan | Dapur, gudang bahan |

**Di mana HTML?** HTML adalah fondasi front-end — **kerangka** halaman. Hari 1–3 kita bangun front-end; mulai Hari 4 masuk ke back-end (PHP), lalu Hari 7 menyatukan semua dengan Laravel.

### 1.5 Tiga bahasa front-end (gambaran singkat)
Analogi rumah:
- **HTML** = struktur/kerangka bangunan (tembok, pintu, jendela) → **Hari 1**
- **CSS** = cat, dekorasi, tata letak (indah dan rapi) → **Hari 2**
- **JavaScript** = fungsi & interaksi (lampu menyala, pintu otomatis) → **Hari 3**

> **Diskusi kelas (10 menit):** minta peserta menyebut 3 website yang sering dibuka, lalu tebak bersama: bagian mana front-end, bagian mana yang butuh back-end (mis. login, keranjang belanja).

### ✅ Cek pemahaman Sesi 1
Peserta bisa menjawab lisan:
1. Apa beda request dan response?
2. Sebutkan satu contoh pekerjaan front-end dan satu back-end.
3. HTML termasuk front-end atau back-end?

---

# SESI 2 — SETUP & DOKUMEN HTML PERTAMA (10.15–12.00)

> **Metode:** guided/ikuti-bersama. Instruktur mengetik di proyektor, peserta mengikuti langkah demi langkah.

### 2.1 Menyiapkan VS Code
1. Pastikan **VS Code** terpasang.
2. Buka tab **Extensions** (ikon kotak di kiri), pasang:
   - **Live Server** — menjalankan halaman & auto-refresh saat file disimpan.
   - **Prettier** — merapikan kode otomatis.
   - **Auto Rename Tag** — mengubah tag pembuka & penutup sekaligus.

### 2.2 Struktur folder proyek
Buat folder kerja yang rapi sejak awal. Ini kebiasaan penting.

```
latihan-web/
├── index.html
├── profil.html
└── img/
    └── foto.jpg
```

Langkah: buat folder `latihan-web` → buka lewat menu **File > Open Folder** di VS Code → buat file baru `index.html`.

### 2.3 Anatomi dokumen HTML
Ketik kode berikut di `index.html`. Di VS Code, ketik `!` lalu tekan **Tab** untuk membuat kerangka otomatis (Emmet), tapi hari ini kita ketik manual dulu agar paham tiap bagian.

```html
<!DOCTYPE html>
<html lang="id">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Halaman Pertamaku</title>
</head>
<body>
    <h1>Halo Dunia!</h1>
    <p>Ini halaman web pertama saya.</p>
</body>
</html>
```

Penjelasan tiap bagian:
- `<!DOCTYPE html>` — memberi tahu browser ini dokumen HTML modern.
- `<html lang="id">` — pembungkus seluruh halaman; `lang="id"` = bahasa Indonesia.
- `<head>` — **info di balik layar** (judul tab, encoding, pengaturan), tidak tampil di halaman.
- `<meta charset="UTF-8">` — agar huruf & simbol (termasuk é, ©, emoji) tampil benar.
- `<meta name="viewport" ...>` — agar tampilan pas di layar HP (penting untuk Hari 2).
- `<title>` — teks yang muncul di tab browser.
- `<body>` — **isi yang tampil** di halaman.

### 2.4 Menjalankan dengan Live Server
Klik kanan di file `index.html` → **Open with Live Server**. Browser terbuka otomatis. Ubah teks, tekan **Ctrl+S**, lihat browser refresh sendiri.

### 2.5 Konsep: Tag, Elemen, Atribut
- **Tag**: penanda, ditulis dalam kurung siku. Umumnya berpasangan: pembuka `<p>` dan penutup `</p>`.
- **Elemen**: tag pembuka + isi + tag penutup. Contoh: `<p>Halo</p>`.
- **Atribut**: informasi tambahan di dalam tag pembuka, format `nama="nilai"`. Contoh: `<html lang="id">` — `lang` adalah atribut.

```
<a href="https://google.com">Klik di sini</a>
 │   │       │                    │        │
tag  atribut nilai              isi     tag penutup
```

### 🔨 Latihan 2 (15 menit)
Buat file `latihan-2.html` yang menampilkan:
1. Judul tab bertuliskan nama peserta.
2. Satu `<h1>` berisi "Perkenalan".
3. Dua `<p>`: satu tentang asal kota, satu tentang hobi.

Jalankan dengan Live Server dan pastikan tampil di browser.

**Kunci (untuk instruktur):**
```html
<!DOCTYPE html>
<html lang="id">
<head>
    <meta charset="UTF-8">
    <title>Budi Santoso</title>
</head>
<body>
    <h1>Perkenalan</h1>
    <p>Saya berasal dari Makassar.</p>
    <p>Hobi saya membaca dan bermain futsal.</p>
</body>
</html>
```

---

# SESI 3 — ELEMEN HTML & TAG SEMANTIK (13.00–15.00)

> **Metode:** demo singkat tiap elemen, langsung diikuti latihan lab.

### 3.1 Heading & Paragraf
```html
<h1>Judul Terbesar</h1>
<h2>Sub-judul</h2>
<h3>Sub-sub-judul</h3>
<!-- sampai h6 -->

<p>Ini paragraf biasa.</p>
<hr>                 <!-- garis pemisah horizontal -->
<p>Paragraf setelah garis.<br>Baris baru dalam paragraf.</p>
```
> **Aturan penting:** gunakan **satu `<h1>` per halaman** (judul utama). `h2`–`h6` untuk hierarki di bawahnya.

### 3.2 Format teks
```html
<p><strong>Tebal</strong> untuk penting, <em>miring</em> untuk penekanan.</p>
```

### 3.3 List (daftar)
```html
<!-- Unordered list: bullet -->
<ul>
    <li>HTML</li>
    <li>CSS</li>
    <li>JavaScript</li>
</ul>

<!-- Ordered list: bernomor -->
<ol>
    <li>Buka VS Code</li>
    <li>Ketik kode</li>
    <li>Jalankan Live Server</li>
</ol>
```

### 3.4 Link
```html
<a href="https://laravel.com">Situs Laravel</a>          <!-- ke situs lain -->
<a href="profil.html">Halaman Profil</a>                <!-- ke file lain di folder -->
<a href="https://laravel.com" target="_blank">Buka tab baru</a>
```

### 3.5 Gambar
```html
<img src="img/foto.jpg" alt="Foto profil Budi" width="200">
```
- `src` = lokasi file gambar.
- `alt` = teks pengganti bila gambar gagal tampil (**wajib**, juga penting untuk aksesibilitas & SEO).
- Perhatikan huruf besar/kecil pada nama file: `Foto.JPG` ≠ `foto.jpg` di server.

### 3.6 Tag Semantik (kerangka halaman)
Tag semantik memberi **makna** pada bagian halaman — memudahkan dibaca manusia, browser, dan mesin pencari.

```html
<body>
    <header>
        <h1>Nama Situs</h1>
    </header>

    <nav>
        <a href="#">Beranda</a>
        <a href="#">Tentang</a>
    </nav>

    <main>
        <section>
            <h2>Bagian Isi</h2>
            <p>Konten utama di sini.</p>
        </section>
    </main>

    <footer>
        <p>&copy; 2026 Nama Saya</p>
    </footer>
</body>
```
| Tag | Fungsi |
|---|---|
| `<header>` | Bagian atas / kepala halaman |
| `<nav>` | Menu navigasi |
| `<main>` | Konten utama (satu per halaman) |
| `<section>` | Kelompok konten yang berkaitan |
| `<footer>` | Bagian bawah / kaki halaman |

> **Catatan:** hari ini halaman masih tampak "polos" karena belum ada CSS. Itu normal — kerapian visual dikerjakan di **Hari 2**. Hari ini fokus ke **struktur yang benar**.

### 🔨 Latihan 3 (lab, 45 menit)
Buat file `latihan-3.html` berisi halaman "Tentang Kota Saya" dengan ketentuan:
1. Gunakan kerangka semantik lengkap (`header`, `nav`, `main`, `section`, `footer`).
2. `<header>` berisi `<h1>` nama kota.
3. `<nav>` berisi minimal 2 link.
4. `<main>` berisi 2 `<section>`: satu "Tempat Wisata" (pakai `<ul>`), satu "Kuliner Khas" (pakai `<ol>`).
5. Ada minimal 1 gambar dengan `alt` yang benar.
6. `<footer>` berisi simbol copyright `&copy;` dan tahun.

**Kunci ringkas (untuk instruktur):**
```html
<!DOCTYPE html>
<html lang="id">
<head>
    <meta charset="UTF-8">
    <title>Tentang Makassar</title>
</head>
<body>
    <header><h1>Makassar</h1></header>
    <nav>
        <a href="#wisata">Wisata</a>
        <a href="#kuliner">Kuliner</a>
    </nav>
    <main>
        <section id="wisata">
            <h2>Tempat Wisata</h2>
            <ul>
                <li>Pantai Losari</li>
                <li>Benteng Rotterdam</li>
            </ul>
        </section>
        <section id="kuliner">
            <h2>Kuliner Khas</h2>
            <ol>
                <li>Coto Makassar</li>
                <li>Pallubasa</li>
            </ol>
        </section>
        <img src="img/losari.jpg" alt="Pantai Losari saat senja">
    </main>
    <footer><p>&copy; 2026 Budi Santoso</p></footer>
</body>
</html>
```

---

# SESI 4 — MINI-PROJECT: HALAMAN PROFIL (15.15–16.30)

> **Metode:** kerja mandiri. Ini **output resmi Hari 1**. Instruktur berkeliling membantu.

Sebelum menyusun profil, peserta perlu dua elemen baru: **tabel** dan **form**.

### 4.1 Tabel
```html
<table border="1">
    <thead>
        <tr>
            <th>Keahlian</th>
            <th>Level</th>
        </tr>
    </thead>
    <tbody>
        <tr>
            <td>HTML</td>
            <td>Dasar</td>
        </tr>
        <tr>
            <td>Microsoft Word</td>
            <td>Mahir</td>
        </tr>
    </tbody>
</table>
```
- `<tr>` = baris (table row), `<th>` = sel judul (header), `<td>` = sel data.
- `border="1"` sementara dipakai agar garis tabel terlihat (nanti diganti CSS di Hari 2).

### 4.2 Form
```html
<form>
    <label for="nama">Nama:</label>
    <input type="text" id="nama" name="nama">

    <label for="email">Email:</label>
    <input type="email" id="email" name="email">

    <label for="pesan">Pesan:</label>
    <textarea id="pesan" name="pesan"></textarea>

    <label for="topik">Topik:</label>
    <select id="topik" name="topik">
        <option value="umum">Umum</option>
        <option value="kerjasama">Kerja sama</option>
    </select>

    <button type="submit">Kirim</button>
</form>
```
- `<label>` + `for` yang cocok dengan `id` input → klik label memfokuskan input (aksesibilitas).
- `type` menentukan jenis input: `text`, `email`, `password`, dll.
- `<textarea>` untuk teks panjang, `<select>`/`<option>` untuk pilihan, `<button>` untuk tombol.
> Form belum benar-benar mengirim data hari ini — itu urusan back-end (Hari 4). Sekarang cukup **tampilannya benar**.

### 📦 Brief Proyek: `profil.html` (CV Online)
Buat file `profil.html` berisi profil diri dengan **struktur semantik** dan komponen berikut:

**Wajib ada:**
1. `<header>`: `<h1>` nama lengkap + `<img>` foto (dengan `alt`).
2. `<nav>`: minimal 2 link.
3. `<main>` berisi minimal 3 `<section>`:
   - **Biodata** — paragraf singkat tentang diri (nama, kota, cita-cita).
   - **Keahlian** — dalam bentuk **tabel** (keahlian + level), minimal 3 baris.
   - **Kontak** — dalam bentuk **form** (nama, email, pesan, tombol kirim).
4. `<footer>`: copyright `&copy;` + tahun + nama.

**Kriteria lulus:**
- Semua tag pembuka punya penutup.
- Struktur semantik dipakai dengan benar.
- Halaman tampil tanpa error di browser (Live Server).
- Ada tabel dan form yang berfungsi secara tampilan.

### Kunci — Contoh Solusi Lengkap (untuk instruktur)
```html
<!DOCTYPE html>
<html lang="id">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Profil - Budi Santoso</title>
</head>
<body>
    <header>
        <h1>Budi Santoso</h1>
        <img src="img/foto.jpg" alt="Foto Budi Santoso" width="150">
    </header>

    <nav>
        <a href="#biodata">Biodata</a>
        <a href="#keahlian">Keahlian</a>
        <a href="#kontak">Kontak</a>
    </nav>

    <main>
        <section id="biodata">
            <h2>Biodata</h2>
            <p>Halo, saya Budi Santoso dari Makassar. Saya sedang belajar
               menjadi web programmer dan bercita-cita membangun aplikasi sendiri.</p>
        </section>

        <section id="keahlian">
            <h2>Keahlian</h2>
            <table border="1">
                <thead>
                    <tr><th>Keahlian</th><th>Level</th></tr>
                </thead>
                <tbody>
                    <tr><td>HTML</td><td>Dasar</td></tr>
                    <tr><td>Microsoft Office</td><td>Mahir</td></tr>
                    <tr><td>Desain Grafis</td><td>Menengah</td></tr>
                </tbody>
            </table>
        </section>

        <section id="kontak">
            <h2>Kontak Saya</h2>
            <form>
                <p>
                    <label for="nama">Nama:</label>
                    <input type="text" id="nama" name="nama">
                </p>
                <p>
                    <label for="email">Email:</label>
                    <input type="email" id="email" name="email">
                </p>
                <p>
                    <label for="pesan">Pesan:</label>
                    <textarea id="pesan" name="pesan"></textarea>
                </p>
                <button type="submit">Kirim</button>
            </form>
        </section>
    </main>

    <footer>
        <p>&copy; 2026 Budi Santoso</p>
    </footer>
</body>
</html>
```

---

# SESI 5 — REVIEW & PENUTUP (16.30–17.00)

### Checklist Output Hari 1
Peserta dinyatakan tuntas bila `profil.html` memenuhi:
- [ ] Kerangka HTML lengkap (`<!DOCTYPE>`, `head`, `body`)
- [ ] Struktur semantik: `header`, `nav`, `main`, `section`, `footer`
- [ ] Ada `<h1>` (satu saja) + foto dengan `alt`
- [ ] Tabel keahlian minimal 3 baris
- [ ] Form kontak (nama, email, pesan, tombol)
- [ ] Footer dengan `&copy;` + tahun
- [ ] Tampil tanpa error di browser

### Titik Rawan Pemula (perhatian instruktur)
- **Lupa tag penutup** → halaman berantakan. Ajarkan Auto Rename Tag & indentasi rapi.
- **File belum di-save** → browser tak berubah. Biasakan Ctrl+S.
- **Path gambar salah** → gambar tidak muncul. Cek folder `img/` dan penulisan huruf besar/kecil.
- **Live Server tidak jalan** → pastikan folder dibuka lewat *Open Folder*, bukan file tunggal.
- **Menaruh konten di `<head>`** → tidak tampil. Ingatkan: yang tampil ada di `<body>`.
- **Pakai banyak `<h1>`** → jelaskan hierarki heading.
- Peserta cemas halaman "jelek" → tegaskan: **CSS besok** (Hari 2), hari ini fokus struktur.

### Tugas / Persiapan Hari 2
1. Rapikan `profil.html` masing-masing, pastikan lolos checklist.
2. Siapkan 1 file foto di folder `img/`.
3. Pikirkan 3 warna yang ingin dipakai untuk mempercantik halaman besok.

### Jembatan ke Hari 2
"Hari ini kita membangun kerangkanya. Besok kita 'cat dan hias' halaman profil ini dengan **CSS** supaya rapi, berwarna, dan responsif di HP."

---

*Modul ini bisa dibagikan ke peserta sebagai bahan bacaan, atau dipegang instruktur sebagai panduan mengajar. Kunci jawaban sebaiknya tidak dibagikan sebelum sesi latihan selesai.*
