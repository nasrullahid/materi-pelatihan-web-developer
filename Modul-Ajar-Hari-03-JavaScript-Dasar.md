# MODUL AJAR — HARI 3
## JavaScript Dasar

*Bagian dari Pelatihan Web Programmer Dasar — Berbasis Laravel (15 Hari)*

---

## INFORMASI SESI

| Item | Keterangan |
|---|---|
| **Hari** | 3 dari 15 |
| **Fase** | Fase 1 — Fondasi Web |
| **Topik** | Logika pemrograman & interaksi halaman dengan JavaScript |
| **Durasi** | 8 jam |
| **Prasyarat** | Hari 1 (HTML) & Hari 2 (CSS) |
| **Output** | Aplikasi **To-Do List** interaktif (tambah & hapus item) |

### Tujuan Pembelajaran
Setelah menyelesaikan hari ini, peserta mampu:
1. Menyisipkan JavaScript ke halaman dan menggunakan `console.log()`.
2. Memakai variabel, tipe data, dan operator.
3. Mengatur alur program dengan `if/else`, `switch`, dan perulangan.
4. Membuat dan memanggil fungsi dengan parameter serta `return`.
5. Menyimpan data dengan array dan object.
6. Memanipulasi elemen halaman (DOM) dan merespons aksi pengguna (event).

### Alat & Bahan
- VS Code + Live Server, browser (Chrome/Firefox)
- Folder proyek `latihan-web/` dari hari sebelumnya
- **Console browser** (buka dengan tombol **F12** → tab **Console**)

---

## PETA WAKTU HARI INI

| Waktu | Sesi | Fokus |
|---|---|---|
| 08.00–10.00 | Sesi 1 — Konsep | Mengenal JS: variabel & operator |
| 10.00–10.15 | Istirahat | |
| 10.15–12.00 | Sesi 2 — Lab | Logika: kondisi, perulangan, fungsi |
| 12.00–13.00 | ISHOMA | |
| 13.00–15.00 | Sesi 3 — Lab | Array & object |
| 15.00–15.15 | Istirahat | |
| 15.15–16.30 | Sesi 4 — Mini-project | DOM, event & To-Do List |
| 16.30–17.00 | Sesi 5 — Review | Evaluasi & jembatan Hari 4 |

---

# SESI 1 — MENGENAL JAVASCRIPT (08.00–10.00)

> **Metode:** ceramah + guided. Tekankan bahwa hari ini halaman akan mulai "merespons" pengguna.

### 1.1 Apa itu JavaScript?
**JavaScript (JS)** adalah bahasa pemrograman yang membuat halaman **interaktif** — merespons klik, mengubah isi tanpa memuat ulang, memvalidasi form, dan banyak lagi.

Analogi rumah (lanjutan):
- **HTML** = kerangka rumah (Hari 1)
- **CSS** = cat & dekorasi (Hari 2)
- **JavaScript** = instalasi listrik & otomasi — lampu menyala saat sakelar ditekan, pintu terbuka otomatis (Hari 3)

### 1.2 Memasang JavaScript
```html
<!-- Cara 1: file terpisah (disarankan) -->
<script src="script.js"></script>

<!-- Cara 2: langsung di HTML -->
<script>
    console.log("Halo dari JavaScript!");
</script>
```
> **Penting:** letakkan `<script>` di **bagian bawah `<body>`** agar seluruh elemen HTML sudah termuat sebelum JS berjalan. Ini mencegah banyak error pemula.

### 1.3 console.log() & Console browser
`console.log()` mencetak pesan ke **Console** — alat utama untuk memeriksa nilai dan mencari kesalahan.
```javascript
console.log("Halo");
console.log(10 + 5);
```
Buka Console: tekan **F12** di browser → pilih tab **Console**.

### 1.4 Variabel & tipe data
Variabel adalah "wadah" untuk menyimpan nilai.
```javascript
let nama = "Budi";      // string (teks) — diapit tanda kutip
const umur = 25;        // number (angka)
let aktif = true;       // boolean (true / false)
```
| Kata kunci | Arti |
|---|---|
| `let` | variabel yang **bisa berubah** nilainya |
| `const` | nilai **tetap** (konstanta), tidak boleh diubah |

Tipe data dasar: **string** (teks), **number** (angka), **boolean** (benar/salah).

### 1.5 Operator
```javascript
// operator hitung
let total = 10 + 5;        // 15
let sisa = 10 - 3;         // 7

// menggabung teks
let sapaan = "Halo " + nama;   // "Halo Budi"

// operator perbandingan (menghasilkan true/false)
console.log(umur >= 18);   // true
console.log(5 == 5);       // true
console.log(3 > 10);       // false
```
| Kelompok | Operator |
|---|---|
| Hitung | `+  -  *  /  %` |
| Perbandingan | `==  !=  >  <  >=  <=` |

### 🔨 Latihan 1 (20 menit)
Buat `script.js`, hubungkan ke sebuah halaman HTML, lalu:
1. Simpan nama & umur ke variabel.
2. Cetak kalimat "Nama saya Budi, umur 25" ke Console (gabungkan variabel).
3. Cetak hasil `umur >= 17` (apakah sudah boleh punya KTP).

**Kunci (untuk instruktur):**
```javascript
let nama = "Budi";
let umur = 25;
console.log("Nama saya " + nama + ", umur " + umur);
console.log(umur >= 17);   // true
```

### ✅ Cek pemahaman Sesi 1
1. Apa beda `let` dan `const`?
2. Kenapa `<script>` sebaiknya di bawah `<body>`?
3. Apa hasil `"5" + 5` menurutmu? (diskusi: string vs number)

---

# SESI 2 — LOGIKA & ALUR PROGRAM (10.15–12.00)

> **Metode:** demo + lab. Banyak latihan kecil agar peserta terbiasa dengan sintaks.

### 2.1 Percabangan: if / else
Membuat program **mengambil keputusan**.
```javascript
let nilai = 80;

if (nilai >= 75) {
    console.log("Lulus");
} else {
    console.log("Belum lulus");
}
```
Bisa bertingkat dengan `else if`:
```javascript
if (nilai >= 85) {
    console.log("A");
} else if (nilai >= 70) {
    console.log("B");
} else {
    console.log("C");
}
```

### 2.2 switch
Alternatif untuk banyak pilihan dari satu nilai:
```javascript
let hari = "Senin";

switch (hari) {
    case "Sabtu":
    case "Minggu":
        console.log("Akhir pekan");
        break;
    default:
        console.log("Hari kerja");
}
```
> Jangan lupa `break;` di tiap `case`, dan `default` untuk nilai lainnya.

### 2.3 Perulangan: for
Menjalankan blok kode berkali-kali.
```javascript
// mencetak 1 sampai 5
for (let i = 1; i <= 5; i++) {
    console.log(i);
}
```
Tiga bagian `for`: **mulai** (`let i = 1`), **syarat** (`i <= 5`), **langkah** (`i++`).

### 2.4 Perulangan: while
```javascript
let n = 1;
while (n <= 5) {
    console.log(n);
    n++;    // WAJIB ada, agar tidak berulang selamanya
}
```
> **Peringatan:** lupa menaikkan nilai (`n++`) membuat perulangan tak berhenti (infinite loop) dan browser hang.

### 2.5 Fungsi
Blok kode yang diberi nama dan bisa **dipakai ulang**.
```javascript
function sapa(nama) {
    return "Halo, " + nama + "!";
}

console.log(sapa("Budi"));    // Halo, Budi!
console.log(sapa("Andi"));    // Halo, Andi!
```
- **parameter** (`nama`) = input yang diterima fungsi.
- **return** = hasil yang dikembalikan fungsi.
- **memanggil** = menjalankan fungsi, mis. `sapa("Budi")`.

### 🔨 Latihan 2 (35 menit)
1. Buat fungsi `cekGanjilGenap(angka)` yang mengembalikan "Ganjil" atau "Genap" (petunjuk: `angka % 2`).
2. Gunakan perulangan `for` untuk mencetak status 1–10.

**Kunci (untuk instruktur):**
```javascript
function cekGanjilGenap(angka) {
    if (angka % 2 === 0) {
        return "Genap";
    } else {
        return "Ganjil";
    }
}

for (let i = 1; i <= 10; i++) {
    console.log(i + ": " + cekGanjilGenap(i));
}
```

---

# SESI 3 — ARRAY & OBJECT (13.00–15.00)

> **Metode:** demo + lab. Ini fondasi untuk mengelola banyak data — penting untuk mini-project sore.

### 3.1 Array — daftar berurutan
```javascript
let buah = ["apel", "jeruk", "mangga"];

console.log(buah[0]);       // apel  (index mulai dari 0!)
console.log(buah[2]);       // mangga
console.log(buah.length);   // 3  (jumlah item)
```

### 3.2 Menambah & menghapus item
```javascript
buah.push("pisang");        // menambah di akhir
buah.splice(1, 1);          // menghapus 1 item pada index 1
```

### 3.3 Mengulang isi array
```javascript
buah.forEach(function (item) {
    console.log(item);
});
```
> `forEach` menjalankan fungsi untuk **setiap** item dalam array — pola yang akan dipakai untuk menampilkan daftar to-do.

### 3.4 Object — data berpasangan
```javascript
let siswa = {
    nama: "Budi",
    umur: 20,
    aktif: true
};

console.log(siswa.nama);    // Budi
siswa.umur = 21;            // mengubah nilai
```

### 3.5 Array vs Object
| | Array | Object |
|---|---|---|
| Bentuk | daftar berurutan | pasangan nama–nilai |
| Akses | lewat angka: `buah[0]` | lewat nama: `siswa.nama` |
| Cocok untuk | banyak item sejenis | satu entitas dengan banyak sifat |

Keduanya bisa digabung — array berisi banyak object:
```javascript
let daftar = [
    { nama: "Budi", umur: 20 },
    { nama: "Andi", umur: 22 }
];
console.log(daftar[0].nama);   // Budi
```

### 🔨 Latihan 3 (40 menit)
1. Buat array `angka` berisi 5 angka.
2. Gunakan perulangan untuk menghitung **totalnya**, lalu cetak.
3. Buat object `mobil` dengan properti `merk`, `tahun`, `warna`, lalu cetak salah satunya.

**Kunci (untuk instruktur):**
```javascript
let angka = [10, 20, 30, 40, 50];
let total = 0;
angka.forEach(function (n) {
    total = total + n;
});
console.log("Total: " + total);   // 150

let mobil = { merk: "Toyota", tahun: 2020, warna: "hitam" };
console.log(mobil.merk);          // Toyota
```

---

# SESI 4 — DOM, EVENT & MINI-PROJECT (15.15–16.30)

> **Metode:** demo singkat lalu kerja mandiri. Menghasilkan **output resmi Hari 3**.

### 4.1 DOM: menghubungkan JS dengan HTML
**DOM** (Document Object Model) adalah cara JavaScript "menyentuh" elemen HTML.
```javascript
// memilih elemen (memakai penulisan selector CSS)
let judul = document.querySelector("#judul");

// membaca & mengubah isi
judul.textContent = "Teks baru";

// mengubah gaya
judul.style.color = "red";
```
`querySelector` memakai selector seperti CSS: `"#id"`, `".class"`, `"tag"`.

### 4.2 Event: merespons aksi pengguna
```javascript
let tombol = document.querySelector("#tombol");

tombol.addEventListener("click", function () {
    alert("Tombol diklik!");
});
```
| Event | Terjadi saat |
|---|---|
| `click` | elemen diklik |
| `input` | isian teks berubah |
| `submit` | form dikirim |

### 4.3 Membuat elemen baru
```javascript
let li = document.createElement("li");   // buat elemen <li>
li.textContent = "Item baru";
document.querySelector("#daftar").appendChild(li);  // pasang ke halaman
```

### 📦 Brief Mini-project: To-Do List Interaktif
Buat aplikasi daftar tugas sederhana yang bisa **menambah** dan **menghapus** item.

**Wajib ada:**
1. Sebuah `<input>` teks dan tombol **"Tambah"**.
2. Klik "Tambah" → teks masuk ke daftar (`<ul>`).
3. Setiap item punya tombol **"Hapus"** yang menghilangkannya.
4. Data disimpan dalam sebuah **array**.
5. Gunakan **DOM + event** dari sesi ini.

**Kriteria lulus:**
- Menambah item berfungsi.
- Menghapus item berfungsi.
- Input kosong tidak menambah item (validasi sederhana).

### Kunci — Contoh Solusi Lengkap (untuk instruktur)

**`todo.html`**
```html
<!DOCTYPE html>
<html lang="id">
<head>
    <meta charset="UTF-8">
    <title>To-Do List</title>
</head>
<body>
    <h1>Daftar Tugas</h1>
    <input type="text" id="inputTugas" placeholder="Tulis tugas...">
    <button id="tombolTambah">Tambah</button>
    <ul id="daftarTugas"></ul>

    <script src="todo.js"></script>
</body>
</html>
```

**`todo.js`**
```javascript
let tugas = [];   // array penyimpan data

let input = document.querySelector("#inputTugas");
let tombol = document.querySelector("#tombolTambah");
let daftar = document.querySelector("#daftarTugas");

// fungsi menampilkan ulang seluruh daftar
function tampilkan() {
    daftar.innerHTML = "";          // kosongkan dulu
    tugas.forEach(function (item, index) {
        let li = document.createElement("li");
        li.textContent = item + " ";

        let hapus = document.createElement("button");
        hapus.textContent = "Hapus";
        hapus.addEventListener("click", function () {
            tugas.splice(index, 1);  // hapus dari array
            tampilkan();             // gambar ulang
        });

        li.appendChild(hapus);
        daftar.appendChild(li);
    });
}

// event tombol tambah
tombol.addEventListener("click", function () {
    let teks = input.value;
    if (teks === "") {              // validasi: jangan tambah yang kosong
        return;
    }
    tugas.push(teks);               // simpan ke array
    input.value = "";               // kosongkan input
    tampilkan();                    // tampilkan daftar terbaru
});
```
> Halaman ini sengaja belum diberi CSS. Peserta yang cepat bisa mempercantiknya dengan CSS Hari 2 sebagai tantangan tambahan.

---

# SESI 5 — REVIEW & PENUTUP (16.30–17.00)

### Checklist Output Hari 3
Aplikasi To-Do List peserta memenuhi:
- [ ] JS terhubung lewat `<script src="todo.js">`
- [ ] Menambah tugas berfungsi
- [ ] Menghapus tugas berfungsi
- [ ] Data tersimpan dalam array
- [ ] Input kosong tidak menambah item
- [ ] Tidak ada error merah di Console

### Titik Rawan Pemula (perhatian instruktur)
- **Salah huruf besar/kecil** — `querySelector` ≠ `queryselector`; JS sensitif huruf.
- **Lupa kurung/kurawal/titik koma** → error sintaks. Ajarkan membaca pesan error di Console.
- **`<script>` di atas HTML** → elemen belum ada saat JS jalan (`null`). Taruh di bawah `<body>`.
- **Index array mulai dari 0**, bukan 1 — sumber kebingungan klasik.
- **Infinite loop** karena lupa menaikkan penghitung di `while`.
- **Lupa `.value`** saat mengambil isi input.
- Ajarkan kebiasaan **buka Console (F12)** setiap kali kode tidak jalan.

### Tugas / Persiapan Hari 4
1. Sempurnakan To-Do List hingga lolos checklist.
2. Tantangan: percantik dengan CSS Hari 2.
3. Renungkan: To-Do List ini masih **hilang saat halaman ditutup** (data hanya di browser). Bagaimana cara menyimpannya permanen? → itu peran **server & database**, mulai besok.

### Jembatan ke Hari 4
"Selama tiga hari kita bekerja di **front-end** (yang tampil di browser). Data To-Do tadi hilang begitu halaman ditutup, karena belum ada yang menyimpannya. Besok kita masuk **back-end** dengan **PHP** — bahasa yang berjalan di server dan bisa menyimpan serta memproses data. Ini langkah pertama menuju Laravel."

---

*Modul ini bisa dibagikan ke peserta sebagai bahan bacaan, atau dipegang instruktur sebagai panduan mengajar. Kunci jawaban sebaiknya tidak dibagikan sebelum sesi latihan selesai.*
