**Langkah-langkah membuat backend CodeIgniter 4 untuk studi kasus Perpustakaan**

---

````markdown
# 📚 Backend Perpustakaan - CodeIgniter 4

Repositori ini berisi REST API backend sederhana untuk manajemen data **buku** dan **peminjaman** di sistem perpustakaan. Dibuat menggunakan **CodeIgniter 4**.

---

## 🧾 Struktur Tabel (SQL)

Silakan import SQL berikut ke database MySQL Anda:

```sql
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
````

> Kedua tabel **tidak memiliki relasi** (sengaja dipisah untuk penyederhanaan).

---

## ⚙️ Langkah Instalasi Backend

### 1. Clone Repo & Masuk Folder

```bash
git clone https://github.com/username/backend_perpustakaan.git
cd backend_perpustakaan
```

### 2. Install Dependency

```bash
composer install
```

### 3. Salin & Edit File `.env`

```bash
cp env .env
```

Edit bagian database pada `.env`:

```dotenv
database.default.hostname = localhost
database.default.database = db_perpus_[NIM_ANDA]
database.default.username = root
database.default.password =
```

### 4. Jalankan Server

```bash
php spark serve
```

---

## 📮 Endpoint REST API

### 🔸 Buku

| Method | Endpoint   | Deskripsi             |
| ------ | ---------- | --------------------- |
| GET    | /buku      | Ambil semua data buku |
| GET    | /buku/{id} | Ambil detail buku     |
| POST   | /buku      | Tambah data buku      |
| PUT    | /buku/{id} | Ubah data buku        |
| DELETE | /buku/{id} | Hapus data buku       |

### 🔸 Peminjaman

| Method | Endpoint         | Deskripsi               |
| ------ | ---------------- | ----------------------- |
| GET    | /peminjaman      | Ambil semua data pinjam |
| GET    | /peminjaman/{id} | Ambil detail peminjaman |
| POST   | /peminjaman      | Tambah data peminjaman  |
| PUT    | /peminjaman/{id} | Ubah data peminjaman    |
| DELETE | /peminjaman/{id} | Hapus data peminjaman   |

---

## 📁 Struktur Folder Penting

```
app/
├── Controllers/
│   ├── Buku.php
│   └── Peminjaman.php
├── Models/
│   ├── BukuModel.php
│   └── PeminjamanModel.php
├── Config/
│   └── Routes.php
```

---

## 🧪 Testing API dengan Postman

1. Buat Collection:

   * `uas_buku` untuk endpoint `/buku`
   * `uas_peminjaman` untuk endpoint `/peminjaman`

2. Tambahkan Request:

   * `GET`, `POST`, `PUT`, `DELETE` sesuai tabel

3. Contoh Body JSON `POST /peminjaman`:

```json
{
  "nama_peminjam": "Rina Kusuma",
  "judul_buku": "Pemrograman Web",
  "tanggal_pinjam": "2025-05-20",
  "tanggal_kembali": "2025-05-27"
}
```

---

## 🔧 Contoh Kode Controller

### 📂 app/Controllers/Buku.php

```php
<?php namespace App\Controllers;
use CodeIgniter\RESTful\ResourceController;

class Buku extends ResourceController {
    protected $modelName = 'App\\Models\\BukuModel';
    protected $format    = 'json';
}
```

### 📂 app/Controllers/Peminjaman.php

```php
<?php namespace App\Controllers;
use CodeIgniter\RESTful\ResourceController;

class Peminjaman extends ResourceController {
    protected $modelName = 'App\\Models\\PeminjamanModel';
    protected $format    = 'json';
}
```

---

## 💾 Contoh Kode Model

### 📂 app/Models/BukuModel.php

```php
<?php namespace App\Models;
use CodeIgniter\Model;

class BukuModel extends Model {
    protected $table = 'buku';
    protected $primaryKey = 'id';
    protected $allowedFields = ['judul', 'pengarang', 'penerbit', 'tahun_terbit'];
}
```

### 📂 app/Models/PeminjamanModel.php

```php
<?php namespace App\Models;
use CodeIgniter\Model;

class PeminjamanModel extends Model {
    protected $table = 'peminjaman';
    protected $primaryKey = 'id';
    protected $allowedFields = ['nama_peminjam', 'judul_buku', 'tanggal_pinjam', 'tanggal_kembali'];
}
```

---

## 📍 Tambahkan Routing di `app/Config/Routes.php`

```php
$routes->resource('buku');
$routes->resource('peminjaman');
```

## 📚 Dibuat Oleh

**Prih Diantono Abda'u, M.Kom**
UAS Praktikum Pemrograman Berbasis Framework
Politeknik Negeri Cilacap – Semester Genap 2024/2025

