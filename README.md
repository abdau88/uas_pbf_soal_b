**Langkah-langkah membuat backend CodeIgniter 4 untuk studi kasus Perpustakaan**

Berikut ini adalah README backend **CodeIgniter 4** untuk **kasus Perpustakaan** dengan entitas `buku` dan `peminjaman` (tanpa relasi), disusun sesuai struktur yang Anda minta:

---

````markdown
# 📚 Backend Perpustakaan - CodeIgniter 4

Repositori ini berisi proyek backend REST API menggunakan **CodeIgniter 4** untuk sistem informasi perpustakaan dengan dua entitas utama: `buku` dan `peminjaman`.

---

## ⚙️ LANGKAH-LANGKAH PEMBUATAN BACKEND

### 1. Persiapan Awal

Pastikan perangkat Anda telah terinstal:
- PHP >= 8.1
- Composer
- MySQL/MariaDB
- Git

### 2. Buat Proyek CodeIgniter 4 Baru

```bash
composer create-project codeigniter4/appstarter backend_perpustakaan
cd backend_perpustakaan
```

### 3. Konfigurasi Database

#### a. Salin file `.env`

```bash
cp env .env
```

#### b. Edit konfigurasi database di `.env`

```dotenv
database.default.hostname = localhost
database.default.database = db_perpus_[NIM_ANDA]
database.default.username = root
database.default.password =
```

### 4. Buat Database dan Tabel

Login ke phpMyAdmin atau terminal SQL, lalu jalankan query berikut:

```sql
CREATE DATABASE db_perpus_[NIM_ANDA];
USE db_perpus_[NIM_ANDA];

CREATE TABLE buku (
  id INT AUTO_INCREMENT PRIMARY KEY,
  judul VARCHAR(100),
  pengarang VARCHAR(100),
  penerbit VARCHAR(100),
  tahun_terbit INT
);

CREATE TABLE peminjaman (
  id INT AUTO_INCREMENT PRIMARY KEY,
  nama_peminjam VARCHAR(100),
  judul_buku VARCHAR(100),
  tanggal_pinjam DATE,
  tanggal_kembali DATE
);
```

---

## 🛠️ Pembuatan Model

### 📁 app/Models/BukuModel.php

```php
<?php namespace App\Models;
use CodeIgniter\Model;

class BukuModel extends Model {
    protected $table = 'buku';
    protected $primaryKey = 'id';
    protected $allowedFields = ['judul', 'pengarang', 'penerbit', 'tahun_terbit'];
    protected $useTimestamps = false;
}
```

### 📁 app/Models/PeminjamanModel.php

```php
<?php namespace App\Models;
use CodeIgniter\Model;

class PeminjamanModel extends Model {
    protected $table = 'peminjaman';
    protected $primaryKey = 'id';
    protected $allowedFields = ['nama_peminjam', 'judul_buku', 'tanggal_pinjam', 'tanggal_kembali'];
    protected $useTimestamps = false;
}
```

---

## 🎮 Pembuatan Controller (REST API)

Gunakan ResourceController bawaan CI4 untuk RESTful API.

### 📁 app/Controllers/Buku.php

```php
<?php namespace App\Controllers;
use CodeIgniter\RESTful\ResourceController;

class Buku extends ResourceController {
    protected $modelName = 'App\\Models\\BukuModel';
    protected $format    = 'json';
}
```

### 📁 app/Controllers/Peminjaman.php

```php
<?php namespace App\Controllers;
use CodeIgniter\RESTful\ResourceController;

class Peminjaman extends ResourceController {
    protected $modelName = 'App\\Models\\PeminjamanModel';
    protected $format    = 'json';
}
```

---

## 🛣️ Routing

Tambahkan routing ke `app/Config/Routes.php`:

```php
$routes->resource('buku');
$routes->resource('peminjaman');
```

---

## 🚀 Menjalankan Server

```bash
php spark serve
```

Akses melalui browser atau Postman:

- [http://localhost:8080/buku](http://localhost:8080/buku)
- [http://localhost:8080/peminjaman](http://localhost:8080/peminjaman)

---

## 🧪 Pengujian dengan Postman

Buat Collection Postman:

- Nama: `uas_buku` dan `uas_peminjaman`
- Tambahkan endpoint:

  - GET `/buku` – ambil semua buku
  - POST `/buku` – tambah buku
  - PUT `/buku/{id}` – ubah buku
  - DELETE `/buku/{id}` – hapus buku

  - GET `/peminjaman` – ambil semua peminjaman
  - POST `/peminjaman` – tambah data peminjaman
  - PUT `/peminjaman/{id}` – ubah peminjaman
  - DELETE `/peminjaman/{id}` – hapus peminjaman

Gunakan body JSON saat POST dan PUT. Contoh:

```json
{
  "nama_peminjam": "Ahmad Fauzi",
  "judul_buku": "Dasar-Dasar Laravel",
  "tanggal_pinjam": "2025-05-25",
  "tanggal_kembali": "2025-06-02"
}
```

---

## 📮 Endpoint API Lengkap

### 🔹 Buku

| Method | Endpoint     | Deskripsi           |
|--------|--------------|---------------------|
| GET    | `/buku`      | Ambil semua buku    |
| GET    | `/buku/{id}` | Detail buku         |
| POST   | `/buku`      | Tambah buku         |
| PUT    | `/buku/{id}` | Ubah data buku      |
| DELETE | `/buku/{id}` | Hapus data buku     |

### 🔹 Peminjaman

| Method | Endpoint           | Deskripsi               |
|--------|--------------------|--------------------------|
| GET    | `/peminjaman`      | Ambil semua peminjaman   |
| GET    | `/peminjaman/{id}` | Detail peminjaman        |
| POST   | `/peminjaman`      | Tambah peminjaman        |
| PUT    | `/peminjaman/{id}` | Ubah data peminjaman     |
| DELETE | `/peminjaman/{id}` | Hapus data peminjaman    |

---

## 🗂️ Struktur Folder Utama

```
backend_perpustakaan/
├── app/
│   ├── Controllers/
│   │   ├── Buku.php
│   │   └── Peminjaman.php
│   ├── Models/
│   │   ├── BukuModel.php
│   │   └── PeminjamanModel.php
│   └── Config/
│       └── Routes.php
├── public/
├── .env
├── composer.json
└── README.md
```

---

## 💡 Catatan Tambahan

- Pastikan database MySQL sudah berjalan sebelum menjalankan `php spark serve`.
- Gunakan perintah `php spark routes` untuk melihat daftar routing aktif.

---

## 👨‍💻 Dibuat oleh

**Prih Diantono Abda’u, M.Kom**  
UAS Praktikum Pemrograman Berbasis Framework – Genap 2024/2025  
Politeknik Negeri Cilacap
````

---
