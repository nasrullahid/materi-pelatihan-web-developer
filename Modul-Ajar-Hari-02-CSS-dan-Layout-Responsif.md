# MODUL AJAR — HARI 2
## CSS & Layout Responsif

*Bagian dari Pelatihan Web Programmer Dasar — Berbasis Laravel (15 Hari)*

---

## INFORMASI SESI

| Item | Keterangan |
|---|---|
| **Hari** | 2 dari 15 |
| **Fase** | Fase 1 — Fondasi Web |
| **Topik** | Mempercantik & menata halaman dengan CSS |
| **Durasi** | 8 jam |
| **Prasyarat** | Hari 1 (HTML) — peserta sudah punya `profil.html` |
| **Output** | `style.css` yang mempercantik `profil.html` menjadi rapi & responsif |

### Tujuan Pembelajaran
Setelah menyelesaikan hari ini, peserta mampu:
1. Menyisipkan CSS ke halaman dengan tiga cara (inline, internal, external).
2. Menggunakan selector (elemen, class, id) dan properti dasar.
3. Menjelaskan dan menerapkan box model (margin, border, padding, content).
4. Menata tata letak dengan Flexbox dan mengenal dasar Grid.
5. Membuat halaman responsif menggunakan unit relatif dan media query.
6. Mengenal konsep framework CSS berbasis utility class.

### Alat & Bahan
- File `profil.html` hasil Hari 1 (masing-masing peserta)
- VS Code + Live Server, browser
- Folder proyek `latihan-web/` dari Hari 1

---

## PETA WAKTU HARI INI

| Waktu | Sesi | Fokus |
|---|---|---|
| 08.00–10.00 | Sesi 1 — Konsep | Mengenal CSS & selector |
| 10.00–10.15 | Istirahat | |
| 10.15–12.00 | Sesi 2 — Guided | Box model & styling |
| 12.00–13.00 | ISHOMA | |
| 13.00–15.00 | Sesi 3 — Lab | Layout: Flexbox & Grid |
| 15.00–15.15 | Istirahat | |
| 15.15–16.30 | Sesi 4 — Mini-project | Responsif + percantik profil |
| 16.30–17.00 | Sesi 5 — Review | Framework, evaluasi, PR |

---

# SESI 1 — MENGENAL CSS (08.00–10.00)

> **Metode:** ceramah + guided. Buka `profil.html` Hari 1 yang masih polos sebagai titik awal — "hari ini kita akan menghidupkan tampilannya".

### 1.1 Apa itu CSS?
**CSS** (Cascading Style Sheets) adalah bahasa untuk mengatur **tampilan** halaman: warna, huruf, jarak, dan tata letak.

Analogi rumah (lanjutan Hari 1):
- **HTML** = kerangka bangunan (sudah dibuat kemarin).
- **CSS** = mengecat, memasang keramik, menata ruangan agar indah dan nyaman.

Penting: HTML-nya **tidak berubah** — CSS hanya mengubah cara halaman itu tampil.

### 1.2 Tiga cara menyisipkan CSS
```html
<!-- 1. Inline — langsung di tag (cepat, tapi sulit dikelola) -->
<p style="color: red;">Teks merah</p>

<!-- 2. Internal — di dalam <head> (untuk satu halaman) -->
<head>
    <style>
        p { color: red; }
    </style>
</head>

<!-- 3. External — file terpisah (RAPI & DISARANKAN) -->
<head>
    <link rel="stylesheet" href="style.css">
</head>
```
> **Kaidah utama:** gunakan **external CSS**. Satu file `style.css` bisa dipakai banyak halaman dan mudah dirawat. Mulai hari ini peserta memakai cara ini.

### 1.3 Membuat & menghubungkan file CSS
1. Di folder `latihan-web/`, buat file baru `style.css`.
2. Di `profil.html`, tambahkan di dalam `<head>`:
   ```html
   <link rel="stylesheet" href="style.css">
   ```
3. Uji: isi `style.css` dengan `body { background-color: #f4f4f5; }` lalu simpan — latar halaman harus berubah.
> Jika tidak berubah: cek nama file, lokasi file, dan penulisan `href` (huruf besar/kecil).

### 1.4 Anatomi aturan CSS
```css
selector {
    property: value;
}

/* contoh nyata */
h1 {
    color: navy;
    font-size: 32px;
}
```
- **selector** = elemen yang mau diatur.
- **property** = sifat yang diubah (warna, ukuran, dll).
- **value** = nilainya. Setiap baris diakhiri titik koma `;`.

### 1.5 Tiga jenis selector
```css
p        { color: gray; }     /* semua elemen <p> */
.judul   { color: navy; }     /* semua elemen ber-class "judul" */
#header  { background: #eee; }/* elemen ber-id "header" (unik) */
```
Cara memasang class/id di HTML:
```html
<p class="judul">Halo</p>
<div id="header">...</div>
```
> **Aturan praktis:** pakai **class** untuk gaya yang dipakai berulang; **id** untuk satu elemen unik.

### 1.6 Properti dasar (warna, font, teks)
```css
body {
    color: #333333;               /* warna teks */
    background-color: #ffffff;    /* warna latar */
    font-family: Arial, sans-serif;
    font-size: 16px;
    line-height: 1.6;             /* jarak antar baris */
    text-align: left;
}
```
> Warna bisa ditulis dengan nama (`navy`), kode hex (`#333333`), atau `rgb(51,51,51)`.

### 🔨 Latihan 1 (20 menit)
Pada `profil.html` masing-masing:
1. Buat file `style.css` dan hubungkan lewat `<link>`.
2. Atur `body`: warna teks abu gelap, font sans-serif, `line-height` 1.6.
3. Buat `<h1>` berwarna dan rata tengah.
4. Beri class `.kotak` pada salah satu section dan beri warna latar.

**Kunci (untuk instruktur) — `style.css`:**
```css
body {
    color: #333333;
    font-family: Arial, sans-serif;
    line-height: 1.6;
}
h1 {
    color: #A91D2A;
    text-align: center;
}
.kotak {
    background-color: #f4f4f5;
}
```

### ✅ Cek pemahaman Sesi 1
1. Sebutkan 3 cara memasang CSS — mana yang disarankan?
2. Apa beda selector `.judul` dan `#judul`?
3. Properti apa untuk mengubah warna teks vs warna latar?

---

# SESI 2 — BOX MODEL & STYLING (10.15–12.00)

> **Metode:** konsep singkat + banyak praktik. Ini fondasi tata letak.

### 2.1 Konsep Box Model
Setiap elemen HTML sebenarnya adalah sebuah **kotak**. Kotak itu punya 4 lapisan dari dalam ke luar:

```
┌───────────────── margin ─────────────────┐
│   ┌───────────── border ─────────────┐   │
│   │   ┌───────── padding ────────┐   │   │
│   │   │        content           │   │   │
│   │   └──────────────────────────┘   │   │
│   └──────────────────────────────────┘   │
└───────────────────────────────────────────┘
```
| Lapisan | Arti |
|---|---|
| **content** | isi elemen (teks/gambar) |
| **padding** | jarak **dalam**: antara isi dan border |
| **border** | garis tepi elemen |
| **margin** | jarak **luar**: antara elemen ini dan elemen lain |

Analogi: mengirim barang. **content** = barang, **padding** = bantalan/busa, **border** = dinding kardus, **margin** = jarak antar kardus di dalam truk.

### 2.2 margin & padding
```css
.kartu {
    margin: 20px;           /* semua sisi */
    padding: 16px;
}

/* per sisi */
.kartu {
    margin-top: 10px;
    margin-bottom: 20px;
    padding-left: 12px;
}

/* shorthand: atas-kanan-bawah-kiri (searah jarum jam) */
.kartu {
    padding: 10px 20px 10px 20px;
}
```

### 2.3 border & border-radius
```css
.kartu {
    border: 2px solid navy;   /* tebal - gaya - warna */
    border-radius: 8px;       /* sudut membulat */
}
```

### 2.4 background, width, dan pemusatan
```css
.kartu {
    background-color: #f4f4f5;
    width: 300px;
    max-width: 100%;          /* tidak melebihi lebar layar */
    margin: 0 auto;           /* memusatkan kotak secara horizontal */
}
```

### 2.5 Jebakan penting: box-sizing
Secara default, `width` hanya menghitung content — padding & border membuat kotak jadi **lebih lebar** dari yang ditulis. Perbaiki dengan:
```css
* {
    box-sizing: border-box;   /* width sudah termasuk padding & border */
}
```
> Letakkan aturan ini di paling atas `style.css`. Ini menghindari banyak pusing tata letak bagi pemula.

### 🔨 Latihan 2 (30 menit)
Buat sebuah "kartu profil kecil" (boleh di file `latihan-css.html`):
1. Satu `<div class="kartu">` berisi judul dan paragraf.
2. Beri `padding` 16px, `border` 1px, `border-radius` 8px.
3. Beri `background-color` terang dan `width` 300px, lalu pusatkan dengan `margin: 0 auto`.
4. Terapkan `box-sizing: border-box` di atas file.

**Kunci (untuk instruktur):**
```css
* { box-sizing: border-box; }

.kartu {
    width: 300px;
    max-width: 100%;
    margin: 24px auto;
    padding: 16px;
    border: 1px solid #d4d4d8;
    border-radius: 8px;
    background-color: #ffffff;
}
```

---

# SESI 3 — LAYOUT: FLEXBOX & GRID (13.00–15.00)

> **Metode:** demo + lab. Ini bagian yang paling terasa "wow" bagi pemula karena tata letak langsung terlihat.

### 3.1 Masalah yang dipecahkan
Secara default, elemen blok (`div`, `section`, `nav`) **menumpuk ke bawah**. Untuk menyusun elemen **berdampingan** (mis. menu navigasi), kita butuh Flexbox.

### 3.2 Flexbox
Cukup beri `display: flex` pada elemen **pembungkus**:
```css
.container {
    display: flex;
    justify-content: space-between;  /* posisi horizontal */
    align-items: center;             /* posisi vertikal */
    gap: 16px;                       /* jarak antar item */
}
```
| Properti | Fungsi | Nilai umum |
|---|---|---|
| `justify-content` | atur posisi mendatar | `flex-start`, `center`, `space-between` |
| `align-items` | atur posisi tegak | `flex-start`, `center`, `flex-end` |
| `gap` | jarak antar item | `8px`, `16px` |
| `flex-direction` | arah susunan | `row` (default), `column` |

### 3.3 Contoh: navigasi berjajar
```html
<nav class="navbar">
    <a href="#">Biodata</a>
    <a href="#">Keahlian</a>
    <a href="#">Kontak</a>
</nav>
```
```css
.navbar {
    display: flex;
    gap: 20px;
    justify-content: center;
}
```

### 3.4 Grid (sekilas)
Grid berguna untuk susunan **baris DAN kolom** (mis. galeri):
```css
.galeri {
    display: grid;
    grid-template-columns: 1fr 1fr 1fr;  /* 3 kolom sama lebar */
    gap: 16px;
}
```
`1fr` berarti "satu bagian" — `1fr 1fr 1fr` = tiga kolom yang membagi ruang secara merata.

### 3.5 Kapan pakai yang mana?
- **Flexbox** → susunan **satu arah** (satu baris atau satu kolom). Cocok untuk navbar, deretan tombol.
- **Grid** → susunan **dua arah** (baris + kolom). Cocok untuk galeri, dashboard.

### 🔨 Latihan 3 (45 menit)
1. Ubah `<nav>` di `profil.html` menjadi navigasi berjajar dengan Flexbox.
2. Buat `latihan-grid.html` berisi 6 kotak angka yang tersusun 3 kolom dengan Grid.

**Kunci (untuk instruktur):**
```css
/* nav flexbox */
nav {
    display: flex;
    gap: 20px;
    justify-content: center;
    padding: 12px;
    background-color: #18181b;
}
nav a {
    color: #ffffff;
    text-decoration: none;
}

/* grid */
.galeri {
    display: grid;
    grid-template-columns: 1fr 1fr 1fr;
    gap: 16px;
}
.galeri div {
    background-color: #A91D2A;
    color: #fff;
    padding: 24px;
    text-align: center;
    border-radius: 8px;
}
```

---

# SESI 4 — RESPONSIF & MINI-PROJECT (15.15–16.30)

> **Metode:** konsep singkat lalu kerja mandiri. Ini menghasilkan **output resmi Hari 2**.

### 4.1 Apa itu responsive design?
Halaman **responsif** menyesuaikan diri agar tetap enak dilihat di layar apa pun — HP, tablet, desktop.

### 4.2 Unit relatif (bukan px kaku)
```css
.container {
    width: 100%;          /* mengikuti lebar induk */
    max-width: 600px;     /* tapi tak lebih dari 600px */
    margin: 0 auto;
    font-size: 1.2rem;    /* rem = kelipatan ukuran dasar */
}
```
| Unit | Arti |
|---|---|
| `%` | persen dari elemen induk |
| `rem` | kelipatan ukuran font dasar (default 16px) |
| `vw` / `vh` | persen dari lebar/tinggi layar |
> Kombinasi `width: 100%` + `max-width` adalah pola paling penting untuk responsif.

### 4.3 Media query
Aturan khusus yang aktif pada ukuran layar tertentu:
```css
/* aturan ini hanya berlaku saat layar ≤ 768px (HP/tablet) */
@media (max-width: 768px) {
    nav {
        flex-direction: column;   /* menu menumpuk ke bawah */
    }
    h1 {
        font-size: 24px;
    }
}
```

### 4.4 Meta viewport (pengingat)
Pastikan baris ini ada di `<head>` (sudah dari Hari 1) — tanpa ini, media query tidak bekerja di HP:
```html
<meta name="viewport" content="width=device-width, initial-scale=1.0">
```

### 📦 Brief Mini-project: Percantik `profil.html`
Gunakan **satu file `style.css`** untuk menata `profil.html` Hari 1 hingga terlihat profesional dan responsif.

**Wajib ada:**
1. CSS external (`style.css`) yang terhubung ke `profil.html`.
2. `box-sizing: border-box` dan pemusatan konten (`max-width` + `margin: 0 auto`).
3. Pengaturan warna, font, dan `line-height` di `body`.
4. `<nav>` berjajar rapi menggunakan **Flexbox**.
5. Tabel keahlian dan form kontak diberi jarak (`padding`), `border`, dan warna.
6. Minimal satu **media query** agar rapi saat layar diperkecil.

**Kriteria lulus:**
- CSS terpisah di file sendiri (bukan inline).
- Tampilan rapi, berwarna, konsisten, dan punya jarak yang nyaman.
- Tidak berantakan saat jendela browser dikecilkan.

### Kunci — Contoh `style.css` Lengkap (untuk instruktur)
```css
/* ===== Dasar ===== */
* {
    box-sizing: border-box;
    margin: 0;
    padding: 0;
}
body {
    font-family: Arial, sans-serif;
    color: #333333;
    line-height: 1.6;
    background-color: #f4f4f5;
}
main, header, footer {
    max-width: 700px;
    margin: 0 auto;
    padding: 16px;
}

/* ===== Header ===== */
header {
    text-align: center;
    padding-top: 32px;
}
header h1 {
    color: #A91D2A;
    margin-bottom: 8px;
}
header img {
    border-radius: 50%;   /* foto jadi lingkaran */
}

/* ===== Navigasi (Flexbox) ===== */
nav {
    display: flex;
    justify-content: center;
    gap: 20px;
    padding: 12px;
    background-color: #18181b;
    border-radius: 8px;
}
nav a {
    color: #ffffff;
    text-decoration: none;
    font-weight: bold;
}
nav a:hover {
    color: #EF3B2D;
}

/* ===== Section ===== */
section {
    background-color: #ffffff;
    border-radius: 8px;
    padding: 20px;
    margin-bottom: 16px;
}
section h2 {
    color: #A91D2A;
    margin-bottom: 12px;
}

/* ===== Tabel ===== */
table {
    width: 100%;
    border-collapse: collapse;
}
th, td {
    border: 1px solid #d4d4d8;
    padding: 10px;
    text-align: left;
}
th {
    background-color: #A91D2A;
    color: #ffffff;
}

/* ===== Form ===== */
form label {
    display: block;
    margin-top: 12px;
    font-weight: bold;
}
form input,
form textarea {
    width: 100%;
    padding: 8px;
    margin-top: 4px;
    border: 1px solid #d4d4d8;
    border-radius: 4px;
}
form button {
    margin-top: 16px;
    padding: 10px 20px;
    background-color: #A91D2A;
    color: #ffffff;
    border: none;
    border-radius: 4px;
    cursor: pointer;
}

/* ===== Footer ===== */
footer {
    text-align: center;
    color: #71717a;
    padding: 24px 16px;
}

/* ===== Responsif ===== */
@media (max-width: 600px) {
    nav {
        flex-direction: column;
        text-align: center;
    }
    header h1 {
        font-size: 24px;
    }
}
```

---

# SESI 5 — FRAMEWORK, REVIEW & PENUTUP (16.30–17.00)

### 5.1 Sekilas Framework CSS (utility class)
Di dunia kerja, banyak developer memakai **framework CSS** seperti **Bootstrap** atau **Tailwind CSS** untuk mempercepat styling.
```html
<!-- Tailwind: styling langsung lewat "utility class" -->
<div class="flex gap-4 p-4 bg-gray-100">
    <h1 class="text-2xl font-bold">Judul</h1>
</div>
```
Setiap class mewakili satu aturan CSS (`p-4` = padding, `flex` = display flex, dst).
> **Pesan penting:** framework mempercepat kerja, **tetapi** memahami CSS dasar (yang dipelajari hari ini) tetap wajib — tanpa fondasi ini, framework hanya jadi hafalan. Framework akan disinggung lagi saat masuk Laravel.

### Checklist Output Hari 2
`profil.html` + `style.css` peserta memenuhi:
- [ ] CSS external terhubung (`<link>`)
- [ ] `box-sizing: border-box` diterapkan
- [ ] Konten dipusatkan (`max-width` + `margin: 0 auto`)
- [ ] Warna, font, dan jarak diatur rapi
- [ ] Navigasi berjajar dengan Flexbox
- [ ] Tabel & form tertata (border, padding)
- [ ] Ada minimal satu media query yang bekerja
- [ ] Tampilan tetap rapi saat layar diperkecil

### Titik Rawan Pemula (perhatian instruktur)
- **Lupa menghubungkan CSS** (`<link>` salah/kurang) → CSS tidak jalan. Ini penyebab #1.
- **Salah tanda selector** — `.` untuk class, `#` untuk id; sering tertukar.
- **Lupa satuan** — `font-size: 16` (salah) vs `16px` (benar).
- **Lupa titik koma** `;` → aturan berikutnya ikut rusak.
- **Bingung width membengkak** → ingatkan `box-sizing: border-box`.
- **Media query tidak jalan di HP** → cek meta viewport dari Hari 1.
- Peserta ingin langsung "cantik" seperti template jadi → tegaskan bahwa rapi dan konsisten lebih penting daripada ramai.

### Tugas / Persiapan Hari 3
1. Rapikan `profil.html` + `style.css` hingga lolos checklist.
2. Coba ubah satu warna tema dan lihat perubahannya.
3. Pikirkan: elemen apa di halaman yang ingin dibuat **interaktif** (mis. tombol yang memunculkan pesan)? Itu tugas JavaScript besok.

### Jembatan ke Hari 3
"Halaman kita sekarang sudah punya kerangka (HTML) dan tampilan (CSS). Besok kita buat halaman **hidup dan interaktif** dengan **JavaScript** — misalnya tombol yang merespons klik dan form yang bisa divalidasi."

---

*Modul ini bisa dibagikan ke peserta sebagai bahan bacaan, atau dipegang instruktur sebagai panduan mengajar. Kunci jawaban sebaiknya tidak dibagikan sebelum sesi latihan selesai.*
