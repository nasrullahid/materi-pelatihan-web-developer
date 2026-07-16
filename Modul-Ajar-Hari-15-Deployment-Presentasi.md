# MODUL AJAR — HARI 15
## Finalisasi, Deployment & Presentasi

*Bagian dari Pelatihan Web Programmer Dasar — Berbasis Laravel (15 Hari) — **HARI TERAKHIR***

---

## INFORMASI SESI

| Item | Keterangan |
|---|---|
| **Hari** | 15 dari 15 |
| **Fase** | Fase 3 — Laravel & Proyek (penutup) |
| **Topik** | Menyelesaikan, men-deploy ke internet, dan mempresentasikan proyek |
| **Durasi** | 8 jam |
| **Prasyarat** | Hari 14 (proyek sudah 70–80%) |
| **Output** | Aplikasi Laravel **online (deployed)** + presentasi + evaluasi akhir |

### Tujuan Hari Ini
Di akhir hari, setiap peserta:
1. Menyelesaikan & menyempurnakan aplikasi (bug diperbaiki).
2. Mengonfigurasi aplikasi untuk produksi (`.env`).
3. Men-deploy aplikasi ke shared hosting sehingga bisa diakses online.
4. Mampu mengatasi error deploy yang umum.
5. Mempresentasikan karyanya dengan demo langsung.
6. Menyelesaikan evaluasi akhir & memperoleh sertifikasi.

### Alat & Bahan
- Proyek Laravel dari Hari 14 (ter-commit di Git/GitHub)
- **Akun shared hosting (cPanel)** atau VPS — disediakan penyelenggara
- Terminal/SSH cPanel, browser

> **Catatan untuk instruktur:** siapkan akun hosting sebelum hari ini. Deploy Laravel di shared hosting punya beberapa jebakan (document root, permission, `.env`) — dampingi peserta satu per satu. Sisakan waktu cukup untuk presentasi & momen penutupan yang bermakna.

---

## PETA WAKTU HARI INI

| Waktu | Sesi | Fokus |
|---|---|---|
| 08.00–10.00 | Sesi 1 | Finalisasi & persiapan produksi |
| 10.00–10.15 | Istirahat | |
| 10.15–12.00 | Sesi 2 | Deploy ke shared hosting |
| 12.00–13.00 | ISHOMA | |
| 13.00–15.00 | Sesi 3 | Deploy via Git & troubleshooting |
| 15.00–15.15 | Istirahat | |
| 15.15–16.30 | Sesi 4 | Persiapan & latihan presentasi |
| 16.30–17.00 | Sesi 5 | Presentasi, evaluasi & penutupan |

---

# SESI 1 — FINALISASI & PRODUKSI (08.00–10.00)

### 1.1 Penyempurnaan akhir
Sebelum deploy, pastikan aplikasi benar-benar siap:
- [ ] Uji semua fitur CRUD sekali lagi — tak ada error.
- [ ] Perbaiki bug yang tersisa dari kemarin.
- [ ] Rapikan tampilan: layout konsisten, tombol jelas.
- [ ] Cek validasi & flash message di semua form.
- [ ] Pastikan halaman terproteksi benar-benar butuh login.
- [ ] Commit versi final ke Git.

### 1.2 Konfigurasi produksi (.env)
Pengaturan untuk server publik berbeda dari lokal:
```
APP_NAME=Toko
APP_ENV=production
APP_DEBUG=false               # WAJIB false di server publik
APP_URL=https://domainku.com

DB_DATABASE=namauser_toko     # nama DB di hosting (sering berprefix)
DB_USERNAME=namauser_toko
DB_PASSWORD=passwordkuat
```
> **`APP_DEBUG=false`** penting: di server publik, mode debug yang menyala akan menampilkan detail sistem (path, kode, kredensial) kepada pengunjung saat terjadi error — celah keamanan serius.

Setelah `.env` siap, selalu jalankan (di server):
```bash
php artisan key:generate     # membuat APP_KEY unik
php artisan config:clear     # bersihkan cache konfigurasi lama
```

### ✅ Cek pemahaman Sesi 1
1. Kenapa `APP_DEBUG` harus `false` di produksi?
2. Apa fungsi `php artisan key:generate`?
3. Apa saja yang perlu diperiksa sebelum deploy?

---

# SESI 2 — DEPLOY KE SHARED HOSTING (10.15–12.00)

### 2.1 Konsep deploy
Selama ini aplikasi hanya berjalan di **localhost** (komputermu). **Deploy** memindahkannya ke **server hosting** yang online 24 jam, lalu menghubungkannya ke sebuah **domain** — sehingga bisa diakses siapa saja.

### 2.2 Langkah deploy ke cPanel
1. **Buat database + user** di cPanel (menu *MySQL Databases*). Catat nama DB, user, password (biasanya berprefix nama akun, mis. `namauser_toko`).
2. **Upload proyek**: `git clone` dari GitHub (disarankan), atau upload `.zip` lalu extract di File Manager.
3. **Arahkan document root** domain ke folder **`/public`** (lihat 2.3).
4. **Jalankan `composer install`** via Terminal cPanel (`composer install --no-dev`).
5. **Atur `.env`** (produksi) lalu `php artisan key:generate`.
6. **Migrasi & storage**:
   ```bash
   php artisan migrate --force
   php artisan storage:link
   ```

### 2.3 PENTING: document root harus ke /public
Domain **harus menunjuk ke folder `public/`** di dalam proyek Laravel — **bukan** folder proyek utama.

**Kenapa?** Folder `public/` adalah satu-satunya bagian yang boleh diakses publik. File sensitif (`.env`, kode aplikasi, konfigurasi database) berada **di luar** `public/` agar aman dari pengunjung.

Cara umum di cPanel:
- Buat domain/subdomain dan set *Document Root*-nya ke `.../proyek/public`, **atau**
- Taruh isi proyek di luar `public_html`, lalu arahkan `public_html` ke `public` proyek (via symlink) atau sesuaikan `index.php`.

> Ingat dari pembahasan hosting: proyek Laravel berisi ribuan file di `vendor/` (dari Composer), sehingga hosting harus punya **batas inode** yang memadai.

### 🔨 Latihan 2
Deploy proyek masing-masing ke akun hosting: buat database, upload, arahkan docroot ke `/public`, `composer install`, atur `.env`, `key:generate`, `migrate`. Buka domain — aplikasi harus tampil.

---

# SESI 3 — GIT DEPLOY & TROUBLESHOOTING (13.00–15.00)

### 3.1 Alur deploy dengan Git
Cara modern & rapi untuk deploy dan update:
```bash
# di komputer lokal
git add .
git commit -m "siap deploy"
git push origin main

# di server (Terminal cPanel / SSH)
git clone <url-repo>          # pertama kali
git pull                      # untuk update berikutnya
composer install --no-dev
php artisan migrate --force
```
> Dengan Git, memperbarui aplikasi cukup: **push** dari lokal → **pull** di server. Tak perlu upload manual berulang.

### 3.2 Troubleshooting deploy (referensi)
| Gejala | Kemungkinan & solusi |
|---|---|
| **Error 500 / blank** | Cek `storage/logs/laravel.log`. Sering karena `APP_KEY` belum digenerate. |
| **Halaman putih** | Sementara set `APP_DEBUG=true` untuk melihat pesan error, perbaiki, lalu **kembalikan ke false**. |
| **Permission denied** | Beri izin tulis ke `storage/` & `bootstrap/cache` (`chmod -R 775`). |
| **Gambar tidak tampil** | Jalankan `php artisan storage:link` di server. |
| **Koneksi DB gagal** | Cek nama database/user/password di `.env` (pakai prefix cPanel). |
| **CSS/JS berantakan** | Pastikan `npm run build` sudah dijalankan & aset ter-upload; cek `APP_URL`. |

### 3.3 Verifikasi akhir
Setelah online, uji langsung di domain:
- Register & login berfungsi.
- CRUD berjalan (tambah/tampil/edit/hapus).
- Gambar & fitur lanjutan tampil.
- Tak ada pesan error yang bocor.

### 🔨 Latihan 3
Selesaikan deploy hingga aplikasi **benar-benar berfungsi online**. Atasi error yang muncul dengan tabel troubleshooting di atas. Minta bantuan mentor bila buntu.

---

# SESI 4 — PERSIAPAN PRESENTASI (15.15–16.30)

### 4.1 Struktur presentasi (5–10 menit)
1. **Masalah & ide** — Aplikasi apa, untuk siapa, memecahkan masalah apa.
2. **Demo langsung** — Tunjukkan aplikasi **ONLINE**: login, CRUD, fitur unggulan.
3. **Tantangan & solusi** — Kesulitan terbesar & bagaimana mengatasinya.
4. **Rencana ke depan** — Fitur yang ingin ditambahkan berikutnya.

### 4.2 Tips presentasi
- **Siapkan data contoh** yang rapi sebelum demo (jangan tabel kosong).
- **Latih alur demo** dulu — tahu klik apa dulu, apa berikutnya.
- **Tetap tenang bila error** saat demo — jelaskan maksud fitur, itu wajar.
- **Ceritakan proses belajarnya**, bukan hanya hasil — apa yang paling menantang.
- **Sebutkan URL** aplikasi agar penilai bisa mencobanya.

### 4.3 Latihan mandiri
Setiap peserta/kelompok menyiapkan poin presentasi & berlatih alur demo (15–20 menit).

---

# SESI 5 — PRESENTASI, EVALUASI & PENUTUP (16.30–17.00)

### 5.1 Presentasi proyek
Setiap peserta/kelompok mempresentasikan aplikasinya secara bergiliran, dengan **demo langsung dari versi online**. Instruktur & peserta lain memberi apresiasi dan masukan singkat.

### 5.2 Evaluasi akhir — Checklist kompetensi
Peserta dinyatakan kompeten bila mampu:
- [ ] Menjelaskan cara kerja web & MVC
- [ ] Membuat tampilan HTML/CSS responsif
- [ ] Menulis logika dengan PHP OOP
- [ ] Merancang & mengoperasikan database
- [ ] Membuat CRUD di Laravel
- [ ] Menerapkan autentikasi
- [ ] Mengelola relasi data
- [ ] Membuat REST API sederhana
- [ ] Men-deploy aplikasi ke internet

### 5.3 Rubrik penilaian proyek akhir
| Kriteria | Bobot |
|---|---|
| Aplikasi berjalan tanpa error | 20% |
| CRUD lengkap & berfungsi | 25% |
| Autentikasi & proteksi halaman | 15% |
| Min. 2 tabel berelasi + validasi | 15% |
| Min. 1 fitur lanjutan | 10% |
| Tampilan rapi & konsisten | 10% |
| Git + presentasi jelas | 5% |

### 5.4 Penutupan pelatihan

**Selamat! Kamu kini seorang Web Programmer.**

Lihat kembali perjalanan 15 hari ini:
```
Hari 1–3   :  HTML · CSS · JavaScript      (fondasi tampilan)
Hari 4–6   :  PHP · OOP · Database SQL      (jembatan backend)
Hari 7–9   :  Laravel MVC · Blade · Eloquent
Hari 10–13 :  CRUD · Auth · Relasi · API
Hari 14–15 :  Proyek Akhir · Deploy · Presentasi
```
Dari bertanya *"apa itu HTML?"* di Hari 1 — hingga meluncurkan **aplikasi Laravel yang online** di Hari 15. Itu pencapaian besar.

**Langkah selanjutnya (teruslah membangun):**
- Perdalam Laravel: Livewire, testing, queue, notifikasi.
- Kuasai front-end modern: Vue / React / Tailwind.
- Bangun portofolio: unggah proyek ke GitHub, deploy beberapa aplikasi.
- Ikuti sertifikasi kompetensi (mis. BNSP Junior Web Developer).
- Terus berlatih — kemampuan coding tumbuh dari membangun, bukan menghafal.

> "Terima kasih telah menyelesaikan perjalanan ini. Kodingan pertamamu hari ini adalah awal dari banyak karya berikutnya. Teruslah membangun."
>
> — Tim Instruktur, PT LPK Mentorbox Indonesia

---

*Modul ini menutup rangkaian 15 hari Pelatihan Web Programmer Dasar berbasis Laravel. Selamat kepada seluruh peserta dan instruktur.*
