# MODUL AJAR — MATERI TAMBAHAN (BONUS)
## CSS Framework: Tailwind CSS
### Implementasi ke Mini-Project `profil.html`

*Bagian dari Pelatihan Web Programmer Dasar — Berbasis Laravel (15 Hari)*

---

## INFORMASI SESI

| Item | Keterangan |
|---|---|
| **Sifat** | Materi tambahan / bonus (opsional) |
| **Topik** | Mempercantik halaman lebih cepat dengan CSS framework (Tailwind CSS) |
| **Durasi** | Fleksibel (~3–4 jam) |
| **Penempatan** | Paling cocok **setelah Hari 2** (CSS & Layout Responsif) |
| **Prasyarat** | Hari 1 (HTML + `profil.html`), Hari 2 (CSS dasar) |
| **Output** | `profil.html` versi modern & responsif memakai Tailwind CSS |

### Tujuan Pembelajaran
Setelah menyelesaikan materi ini, peserta mampu:
1. Menjelaskan apa itu CSS framework dan kapan memakainya.
2. Membedakan pendekatan utility-first (Tailwind) dan component-based (Bootstrap).
3. Memasang Tailwind CSS dengan cepat lewat CDN.
4. Memakai utility class dasar: layout, spacing, tipografi, warna, efek.
5. Membuat tampilan responsif dengan prefix (`sm:`, `md:`, `lg:`).
6. Menerapkan Tailwind untuk mempercantik `profil.html`.

### Kenapa materi ini penting?
Laravel (Breeze, Hari 11) memakai **Tailwind CSS** secara bawaan. Menguasainya sejak awal membuat peserta lebih siap saat masuk fase Laravel — sekaligus mempercepat pembuatan tampilan di proyek akhir.

### Alat & Bahan
- File `profil.html` dari Hari 1, VS Code + Live Server, browser
- Koneksi internet (untuk CDN Tailwind)

---

## PETA MATERI

| Bagian | Fokus |
|---|---|
| Bagian 1 | Mengenal CSS framework (Tailwind vs Bootstrap) |
| Bagian 2 | Memasang Tailwind (CDN) |
| Bagian 3 | Utility class dasar & responsive |
| Bagian 4 | Implementasi ke `profil.html` (mini-project) |

---

# BAGIAN 1 — MENGENAL CSS FRAMEWORK

### 1.1 Kenapa pakai CSS framework?
Di Hari 2, kita menulis semua CSS sendiri: warna, spacing, layout, responsive — semua manual di file `.css` terpisah. Cara ini bagus untuk memahami dasar, tapi **lambat dan berulang** untuk proyek nyata.

**CSS framework** menyediakan style siap pakai. **Tailwind CSS** menyediakannya dalam bentuk **utility class** — banyak class kecil yang masing-masing melakukan satu hal, dirakit langsung di HTML.

### 1.2 Tailwind vs Bootstrap
| | **Tailwind CSS** | **Bootstrap** |
|---|---|---|
| Pendekatan | utility-first | component-based |
| Cara pakai | rakit class kecil di HTML | pakai komponen jadi (btn, card) |
| Fleksibilitas | sangat tinggi & kustom | cepat untuk tampilan standar |
| Kustomisasi | mudah & bebas | lebih terbatas |
| Kaitan pelatihan | **dipakai Laravel Breeze** | alternatif populer |

Kita fokus **Tailwind** karena dipakai Laravel. Bootstrap diperkenalkan sebagai alternatif (lihat bagian akhir).

Contoh perbedaan gaya:
```html
<!-- Tailwind: rakit sendiri dari utility -->
<button class="bg-red-600 text-white px-4 py-2 rounded">Kirim</button>

<!-- Bootstrap: pakai komponen jadi -->
<button class="btn btn-danger">Kirim</button>
```

---

# BAGIAN 2 — MEMASANG TAILWIND (CDN)

Cara tercepat — cocok untuk belajar & file statis seperti `profil.html`. Cukup satu baris di dalam `<head>`:
```html
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Profil Saya</title>
    <script src="https://cdn.tailwindcss.com"></script>
</head>
```
Setelah ini, kita cukup menambahkan class Tailwind langsung ke elemen HTML — **tanpa file `.css` terpisah**.

> **Catatan:** CDN (Play CDN) sempurna untuk latihan & prototipe. Untuk **proyek produksi** (termasuk Laravel), Tailwind dipasang lewat proses build (npm) agar hasil lebih ringan. Untuk materi ini, CDN sudah lebih dari cukup.

---

# BAGIAN 3 — UTILITY CLASS DASAR

Prinsipnya: **satu class = satu efek**. Kita gabungkan beberapa class untuk membentuk tampilan.

### 3.1 Layout & spacing
```html
<!-- menata elemen berdampingan -->
<div class="flex items-center gap-4"> ... </div>

<!-- grid 2 kolom -->
<div class="grid grid-cols-2 gap-6"> ... </div>

<!-- padding (dalam) & margin (luar) -->
<div class="p-6 mt-8 mx-auto"> ... </div>
```
| Class | Fungsi |
|---|---|
| `flex` / `grid` | mode penataan |
| `items-center` | rata tengah vertikal |
| `justify-between` | sebar horizontal |
| `gap-4` | jarak antar item |
| `p-6` `px-4` `py-2` | padding (all / horizontal / vertikal) |
| `m-4` `mt-8` `mx-auto` | margin (mx-auto = tengah) |

> Angka menunjukkan ukuran: `p-2` (kecil) → `p-8` (besar), kelipatan 0.25rem.

### 3.2 Tipografi & warna
```html
<h1 class="text-3xl font-bold text-center text-gray-800">Budi Santoso</h1>

<span class="bg-red-600 text-white px-3 py-1 rounded">Web Developer</span>
```
| Class | Fungsi |
|---|---|
| `text-xl` `text-2xl` `text-3xl` | ukuran teks |
| `font-bold` `font-semibold` | ketebalan |
| `text-center` | rata tengah |
| `text-gray-800` | warna teks |
| `bg-red-600` | warna latar |
| `text-white` | teks putih |

> Warna: `{warna}-{intensitas}`, mis. `red-600`, `gray-800`, `blue-500`. Intensitas 50 (terang) → 900 (gelap).

### 3.3 Efek: border, rounded, shadow
```html
<div class="rounded-xl shadow-lg p-6 border"> kartu </div>

<img class="w-40 h-40 rounded-full" src="foto.jpg">
```
| Class | Fungsi |
|---|---|
| `rounded-lg` `rounded-full` | sudut membulat |
| `shadow` `shadow-lg` | bayangan |
| `border` | garis tepi |
| `w-40` `h-40` `w-full` | ukuran lebar/tinggi |
| `max-w-2xl` | lebar maksimal |

### 3.4 Responsive dengan prefix layar
Tambahkan prefix ukuran layar di depan class agar berlaku hanya pada layar itu ke atas:
```html
<!-- 1 kolom di HP, 2 kolom di layar sedang ke atas -->
<div class="grid grid-cols-1 md:grid-cols-2 gap-6"> ... </div>
```
| Prefix | Berlaku pada |
|---|---|
| (tanpa prefix) | semua ukuran (mobile-first) |
| `sm:` | ≥ 640px |
| `md:` | ≥ 768px (tablet) |
| `lg:` | ≥ 1024px (desktop) |

> **Mobile-first:** tulis tampilan HP dulu (tanpa prefix), lalu tambahkan `md:` / `lg:` untuk layar besar.

### 🔨 Latihan singkat
Buat satu kartu sederhana: sebuah `<div>` dengan `bg-white rounded-xl shadow-lg p-6 max-w-md mx-auto` berisi judul (`text-xl font-bold`) dan paragraf (`text-gray-600 mt-2`). Amati hasilnya di browser.

---

# BAGIAN 4 — IMPLEMENTASI KE `profil.html`

### 4.1 Sebelum → sesudah
Struktur HTML tetap sama — kita hanya **menambahkan class**.
```html
<!-- SEBELUM (HTML polos) -->
<img src="foto.jpg">
<h1>Budi Santoso</h1>
<p>Web Developer</p>

<!-- SESUDAH (dengan Tailwind) -->
<img src="foto.jpg" class="w-40 h-40 rounded-full mx-auto shadow-lg">
<h1 class="text-3xl font-bold text-center text-gray-800">Budi Santoso</h1>
<p class="text-center text-red-600 font-medium">Web Developer</p>
```

### 📦 Brief Mini-project: `profil.html` versi modern
Ubah `profil.html` (Hari 1) menjadi CV online yang modern & responsif dengan Tailwind.

**Wajib ada:**
1. Pasang Tailwind via CDN.
2. Foto profil bulat + shadow, di tengah.
3. Kartu biodata (`rounded-xl shadow-lg p-6`).
4. Tabel keahlian yang rapi & berwarna.
5. Form kontak yang rapi.
6. Layout responsif: 1 kolom di HP, 2 kolom di layar besar (`md:grid-cols-2`).

**Kriteria lulus:**
- Tailwind termuat (tampilan berubah tanpa file `.css` terpisah).
- Foto bulat, kartu ber-shadow, warna konsisten.
- Layout menyesuaikan saat jendela diperkecil (responsif).

### Kunci — Contoh Solusi Lengkap (`profil.html`)
```html
<!DOCTYPE html>
<html lang="id">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Profil — Budi Santoso</title>
    <script src="https://cdn.tailwindcss.com"></script>
</head>
<body class="bg-gray-100 text-gray-800">

    <!-- Header profil -->
    <header class="bg-red-700 text-white py-10 text-center">
        <img src="foto.jpg" alt="Foto Budi"
             class="w-36 h-36 rounded-full mx-auto shadow-lg border-4 border-white object-cover">
        <h1 class="text-3xl font-bold mt-4">Budi Santoso</h1>
        <p class="text-red-100 mt-1">Calon Web Developer</p>
    </header>

    <!-- Konten utama -->
    <main class="max-w-3xl mx-auto p-4 -mt-8">

        <!-- Grid: biodata + keahlian -->
        <div class="grid grid-cols-1 md:grid-cols-2 gap-6">

            <!-- Kartu biodata -->
            <section class="bg-white rounded-xl shadow-lg p-6">
                <h2 class="text-xl font-bold text-red-700 mb-3">Biodata</h2>
                <ul class="space-y-2 text-gray-700">
                    <li><span class="font-semibold">Nama:</span> Budi Santoso</li>
                    <li><span class="font-semibold">Kota:</span> Makassar</li>
                    <li><span class="font-semibold">Email:</span> budi@email.com</li>
                    <li><span class="font-semibold">Hobi:</span> Coding, Futsal</li>
                </ul>
            </section>

            <!-- Kartu keahlian -->
            <section class="bg-white rounded-xl shadow-lg p-6">
                <h2 class="text-xl font-bold text-red-700 mb-3">Keahlian</h2>
                <table class="w-full text-left">
                    <thead>
                        <tr class="bg-red-700 text-white">
                            <th class="p-2 rounded-l">Skill</th>
                            <th class="p-2 rounded-r">Level</th>
                        </tr>
                    </thead>
                    <tbody>
                        <tr class="border-b"><td class="p-2">HTML</td><td class="p-2">Mahir</td></tr>
                        <tr class="border-b"><td class="p-2">CSS</td><td class="p-2">Mahir</td></tr>
                        <tr><td class="p-2">JavaScript</td><td class="p-2">Menengah</td></tr>
                    </tbody>
                </table>
            </section>
        </div>

        <!-- Form kontak -->
        <section class="bg-white rounded-xl shadow-lg p-6 mt-6">
            <h2 class="text-xl font-bold text-red-700 mb-4">Hubungi Saya</h2>
            <form class="space-y-4">
                <input type="text" placeholder="Nama"
                       class="w-full border rounded-lg px-4 py-2 focus:outline-none focus:ring-2 focus:ring-red-500">
                <input type="email" placeholder="Email"
                       class="w-full border rounded-lg px-4 py-2 focus:outline-none focus:ring-2 focus:ring-red-500">
                <textarea placeholder="Pesan" rows="3"
                          class="w-full border rounded-lg px-4 py-2 focus:outline-none focus:ring-2 focus:ring-red-500"></textarea>
                <button type="submit"
                        class="bg-red-700 text-white px-6 py-2 rounded-lg hover:bg-red-800 transition">
                    Kirim
                </button>
            </form>
        </section>
    </main>

    <footer class="text-center text-gray-500 text-sm py-6">
        &copy; 2026 Budi Santoso — dibuat dengan Tailwind CSS
    </footer>
</body>
</html>
```
> **Tips warna brand:** contoh ini memakai `red-700` (dekat dengan merah Magau). Untuk warna kustom persis, Tailwind CDN bisa dikonfigurasi:
> ```html
> <script>
>   tailwind.config = { theme: { extend: { colors: { magau: '#A91D2A' } } } }
> </script>
> ```
> lalu pakai `bg-magau`, `text-magau`, dst.

---

## TITIK RAWAN PEMULA (perhatian instruktur)
- **Lupa memuat CDN** di `<head>` → semua class Tailwind tidak berefek.
- **Salah nama class** (mis. `rounded-xxl` tak ada) → efek tak muncul; cek dokumentasi.
- **Bingung mobile-first** — class tanpa prefix berlaku untuk HP; `md:` untuk layar besar, bukan sebaliknya.
- **Terlalu banyak class** hingga sulit dibaca — kelompokkan logis (layout, spacing, warna) dan rapikan.
- **`w-40 h-40` pada foto** tanpa `object-cover` → gambar bisa gepeng. Tambahkan `object-cover`.
- **Mengira CDN untuk produksi** — untuk aplikasi nyata, pasang Tailwind via build (npm).

## KAITAN KE MATERI UTAMA
- **Hari 2 (CSS):** ini "jalan cepat" dari konsep yang sama (box model, flex, grid, responsive) — kini lewat class siap pakai.
- **Hari 8 (Blade):** class Tailwind bisa langsung dipakai di file `.blade.php`.
- **Hari 11 (Breeze):** Laravel Breeze sudah memakai Tailwind — tampilannya akan terasa familiar.
- **Proyek Akhir (Hari 14–15):** pakai Tailwind agar tampilan proyek rapi & cepat.

## TANTANGAN LANJUTAN (opsional)
1. Tambahkan warna brand kustom (`magau`) lewat `tailwind.config`.
2. Buat navbar responsif di atas halaman.
3. Terapkan Tailwind ke salah satu halaman Laravel di proyek akhir.

---

*Materi tambahan ini melengkapi Hari 2 dan menyiapkan peserta untuk tampilan berbasis Tailwind di fase Laravel. Kunci jawaban sebaiknya diberikan setelah peserta mencoba sendiri.*
