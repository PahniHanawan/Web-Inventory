# 📦 Web-Inventory — Sistem Informasi Inventaris & Peminjaman Barang

<p align="center">
  <img src="https://raw.githubusercontent.com/laravel/art/master/logo-lockup/5%20SVG/2%20CMYK/1%20Full%20Color/laravel-logolockup-cmyk-red.svg" width="320" alt="Laravel Logo">
</p>

<p align="center">
  <a href="https://laravel.com/"><img src="https://img.shields.io/badge/Laravel-5.8-FF2D20?style=for-the-badge&logo=laravel&logoColor=white" alt="Laravel 5.8"></a>
  <a href="https://www.php.net/"><img src="https://img.shields.io/badge/PHP-%5E7.1.3%20|%207.4-777BB4?style=for-the-badge&logo=php&logoColor=white" alt="PHP Version"></a>
  <a href="https://www.mysql.com/"><img src="https://img.shields.io/badge/MySQL-4479A1?style=for-the-badge&logo=mysql&logoColor=white" alt="MySQL"></a>
  <a href="https://adminlte.io/"><img src="https://img.shields.io/badge/Theme-AdminLTE%202.4-3c8dbc?style=for-the-badge" alt="AdminLTE"></a>
  <a href="LICENSE"><img src="https://img.shields.io/badge/License-MIT-green.svg?style=for-the-badge" alt="License MIT"></a>
</p>

---

## 📌 Tentang Proyek

**Web-Inventory** adalah aplikasi web manajemen inventaris dan sirkulasi peminjaman sarana & prasarana yang dibangun menggunakan framework **Laravel 5.8** dengan antarmuka **AdminLTE (Bootstrap 3)**.

Aplikasi ini dikembangkan pada tahun **2020** sebagai proyek **Praktik Kerja Lapangan (PKL)** untuk mempermudah pencatatan aset barang, pengelompokan berdasarkan gedung & ruangan, pengelolaan stok barang per merk, serta pemantauan riwayat peminjaman dan pembuatan laporan rekapitulasi secara otomatis.

---

## ✨ Fitur Utama

### 1. 📊 Dashboard & Statistik Interaktif
- Ringkasan total jumlah barang, ruangan, gedung, dan transaksi peminjaman.
- Visualisasi grafik data peminjaman per bulan secara dinamis menggunakan **ConsoleTVs/Charts**.

### 2. 🏢 Manajemen Master Data
- **Data Gedung**: Tambah, edit, hapus, serta export data gedung.
- **Data Ruangan**: Pengelompokan ruang yang terhubung dengan data gedung terkait.
- **Data Merk**: Manajemen data merk aset inventaris dengan server-side DataTables.

### 3. 📦 Manajemen Inventaris Barang
- Pencatatan barang dengan relasi ke ruangan dan merk (*many-to-many*).
- Pengelolaan rincian stok barang per merk secara terpisah.
- **Fitur Inline Editing**: Edit jumlah stok barang langsung pada tabel menggunakan **X-Editable**.
- Pencatatan kondisi barang (misal: jumlah rusak dan keterangan barang).
- Dukungan upload foto/gambar untuk dokumentasi visual barang.

### 4. 🔄 Transaksi Peminjaman Barang
- Form peminjaman barang mencakup nama peminjam, barang yang dipinjam, jumlah, tanggal pinjam, dan estimasi tanggal kembali.
- Pelacakan status peminjaman (dipinjam / dikembalikan).
- Filter riwayat peminjaman berdasarkan rentang tanggal tertentu.

### 5. 📑 Laporan & Ekspor Multi-Format
- **Export ke Excel (.xlsx)**: Menggunakan package `maatwebsite/excel` untuk rekapitulasi data barang, merk, gedung, ruang, dan peminjaman.
- **Export ke PDF**: Cetak dan unduh dokumen laporan resmi menggunakan package `barryvdh/laravel-dompdf`.

### 6. 🔐 Autentikasi & Multi-Role Akses
- Sistem Login dan Registrasi pengguna.
- Pemisahan hak akses menggunakan Middleware Role:
  - **Admin**: Akses penuh ke seluruh menu (Master Data, Inventaris, Transaksi Peminjaman, dan Cetak Laporan).
  - **User**: Akses dasar ke beranda dan pemantauan ringkasan data.

### 7. ⚡ Antarmuka & UX Responsif
- Integrasi **Yajra DataTables** untuk pengurutan, pencarian cepat, dan paginasi data berskala besar.
- Notifikasi interaktif menggunakan **SweetAlert2** dan feedback pesan sukses/gagal.

---

## 🛠️ Tech Stack & Dependensi

| Kategori | Teknologi / Library | Deskripsi |
| :--- | :--- | :--- |
| **Backend Framework** | [Laravel 5.8](https://laravel.com/) | Kerangka kerja PHP MVC |
| **Bahasa Pemrograman** | [PHP ^7.1.3](https://www.php.net/) | PHP 7.1 hingga 7.4 |
| **Database** | [MySQL / MariaDB](https://www.mysql.com/) | Penyimpanan data relasional |
| **Admin Template** | [AdminLTE 2.4](https://adminlte.io/) | Dashboard template berbasis Bootstrap 3 |
| **CSS & Frontend** | Bootstrap 3.3.7, Font Awesome, Ionicons | Desain antarmuka & ikon |
| **DataTables** | [yajra/laravel-datatables-oracle](https://github.com/yajra/laravel-datatables) (~9.0) | Pengelolaan tabel data dinamis |
| **Export Excel** | [maatwebsite/excel](https://laravel-excel.com/) (^3.1) | Import/Export spreadsheet |
| **Export PDF** | [barryvdh/laravel-dompdf](https://github.com/barryvdh/laravel-dompdf) (^0.8.7) | Konversi tampilan Blade menjadi PDF |
| **Charting** | [consoletvs/charts](https://github.com/ConsoleTVs/Charts) (5.*) | Visualisasi grafik data |
| **Inline Editor** | [X-editable](https://vitalets.github.io/x-editable/) (1.5.0) | Edit data di tempat (*in-place*) |
| **Notifikasi** | [SweetAlert2](https://sweetalert2.github.io/) | Dialog notifikasi pop-up modern |

---

## 🗄️ Struktur Basis Data

Entitas utama dan relasi yang terdapat dalam sistem:

```
[Gedung] 1 ──── < [Ruang] 1 ──── < [Barang] > ──── < [Barang_Merk] > ──── < [Merk]
                                      │ 1
                                      │
                                      ▼ <
                                [Peminjaman]
```

- **`users`**: Menyimpan kredensial pengguna, nama, email, dan `role` (`admin` / `user`).
- **`gedungs`**: Menyimpan daftar gedung inventaris (`nama_gedung`).
- **`ruangs`**: Menyimpan daftar ruangan yang berelasi dengan gedung (`gedung_id`).
- **`merks`**: Menyimpan daftar merk (`nama_merk`).
- **`barangs`**: Menyimpan data barang inventaris, foto (`gambar`), keterangan, kondisi fisik (`jumlah_rusak`), dan penempatan (`ruang_id`).
- **`barang_merk`**: Tabel perantara *Many-to-Many* antara Barang dan Merk untuk mencatat rincian stok (`jumlah`) per merk.
- **`peminjaman`**: Mencatat transaksi sirkulasi barang (`nama_peminjam`, `tanggal_pinjam`, `tanggal_kembali`, `jml_pinjam`, `status`, `keterangan`, `barang_id`).

---

## 🚀 Panduan Instalasi & Menjalankan

### 1. Prasyarat Sistem
Pastikan lingkungan lokal Anda telah terpasang:
- **PHP**: Versi **7.2**, **7.3**, atau **7.4** *(Catatan: Laravel 5.8 belum mendukung PHP 8.x secara langsung).*
- **Composer**: Dependency Manager PHP
- **MySQL / MariaDB** (melalui XAMPP, Laragon, Docker, atau instalasi standalone)
- **Web Server**: Apache / Nginx / PHP Built-in Server

### 2. Langkah-Langkah Instalasi

1. **Clone Repositori**
   ```bash
   git clone https://github.com/PahniHanawan/Web-Inventory.git
   cd Web-Inventory
   ```

2. **Install Dependensi Composer**
   ```bash
   composer install
   ```

3. **Salin File Konfigurasi Environment**
   ```bash
   # Di Windows (Command Prompt / PowerShell)
   copy .env.example .env

   # Atau di Linux / macOS
   cp .env.example .env
   ```

4. **Konfigurasi Database**
   Buka file `.env` dan sesuaikan pengaturan database Anda:
   ```env
   DB_CONNECTION=mysql
   DB_HOST=127.0.0.1
   DB_PORT=3306
   DB_DATABASE=db_web_inventory
   DB_USERNAME=root
   DB_PASSWORD=
   ```
   *Pastikan database dengan nama tersebut sudah dibuat di MySQL Anda.*

5. **Generate Application Key**
   ```bash
   php artisan key:generate
   ```

6. **Jalankan Migrasi Database**
   ```bash
   php artisan migrate
   ```

7. **Membuat Akun Admin**
   Untuk login sebagai `admin`, Anda dapat mendaftar melalui halaman registrasi (`/register`), lalu mengubah kolom `role` menjadi `admin` langsung di tabel `users` (via phpMyAdmin / DBeaver / Navicat), atau melalui Laravel Tinker:
   ```bash
   php artisan tinker
   ```
   Lalu masukkan perintah:
   ```php
   App\User::create([
       'name' => 'Administrator',
       'email' => 'admin@gmail.com',
       'role' => 'admin',
       'password' => bcrypt('password123')
   ]);
   exit
   ```

8. **Buat Symlink Storage (Jika Diperlukan untuk Gambar)**
   ```bash
   php artisan storage:link
   ```

9. **Jalankan Server Lokal**
   ```bash
   php artisan serve
   ```
   Buka peramban (browser) dan akses:
   ```text
   http://127.0.0.1:8000
   ```

---

## 📂 Struktur Direktori Utama

```text
├── app/
│   ├── Exports/            # Class konfigurasi export Excel (LaporanExport, dll.)
│   ├── Helpers/            # Helper global aplikasi (Global.php)
│   ├── Http/
│   │   ├── Controllers/    # Controller logika aplikasi (Barang, Merk, Gedung, Peminjaman, dll.)
│   │   └── Middleware/     # Middleware hak akses (CheckRole.php)
│   ├── Barang.php          # Model Eloquent data Barang
│   ├── Gedung.php          # Model Eloquent data Gedung
│   ├── Ruang.php           # Model Eloquent data Ruang
│   ├── Merk.php            # Model Eloquent data Merk
│   ├── Peminjaman.php      # Model Eloquent data Peminjaman
│   └── User.php            # Model Eloquent pengguna sistem
├── database/
│   └── migrations/         # Skema struktur tabel database
├── public/
│   ├── adminlte/           # Aset tema dashboard AdminLTE
│   └── images/             # Direktori aset gambar & upload foto barang
├── resources/
│   └── views/              # Template tampilan Blade (layouts, barang, peminjaman, laporan, dll.)
└── routes/
    ├── web.php             # Routing antarmuka web & middleware
    └── api.php             # Endpoint API internal (misal: inline edit jumlah barang)
```

---

## 💡 Catatan Tambahan (Proyek Arsip 2020)

Proyek ini merupakan arsip karya tahun **2020**. Jika Anda menjalankan proyek ini di lingkungan pengembangan modern:
- Disarankan menggunakan versi **PHP 7.4** (misalnya menggunakan multi-PHP version di **Laragon** atau **Docker**).
- Jika menggunakan Composer versi baru dan mengalami kendala dependensi lama, Anda dapat menambahkan flag `--ignore-platform-reqs`:
  ```bash
  composer install --ignore-platform-reqs
  ```

---

## 👨‍💻 Pengembang

- **Pahni Hanawan** — [*GitHub Profile*](https://github.com/PahniHanawan)

---

## 📄 Lisensi

Proyek ini dilisensikan di bawah lisensi [MIT License](LICENSE).
