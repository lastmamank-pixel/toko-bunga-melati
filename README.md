#  Toko Bunga Melati — Sistem Reservasi & Manajemen Toko Bunga

UAS Pemrograman Web Lanjut — Aplikasi manajemen toko bunga dengan fitur katalog produk,
pemesanan, reservasi acara (pernikahan/ulang tahun/dll), autentikasi dengan verifikasi email,
role Admin & User, dashboard statistik, export laporan PDF, dan REST API.

## Identitas

- Nama: Luthan Asthalariq
- NIM: 240170208

## Fitur

-  Login & Register + verifikasi email (Laravel Breeze)
-  CRUD lengkap (Kategori, Produk, kelola status Pesanan)
-  Role Admin & User dengan hak akses berbeda
-  Tampilan responsif (Tailwind CSS)
-  Dashboard admin (statistik produk, pesanan, pendapatan, produk terlaris)
-  Export laporan pesanan ke PDF
-  REST API (produk, kategori, pesanan, login) dengan autentikasi token (Laravel Sanctum), siap ditest di Postman

## Tech Stack

- Laravel 11 (PHP)
- Laravel Breeze (autentikasi + verifikasi email)
- Laravel Sanctum (autentikasi token untuk REST API)
- MySQL
- Tailwind CSS (CDN)
- barryvdh/laravel-dompdf (export PDF)

---

## Cara Instalasi & Menjalankan Aplikasi

### 1. Clone repository

```bash
git clone https://github.com/lastmamank-pixel/toko-bunga-melati
cd toko-bunga-melati
```

### 2. Install dependency PHP & JS

```bash
composer install
npm install
```

### 3. Konfigurasi environment

```bash
cp .env.example .env
php artisan key:generate
```

### 4. Migrasi database & storage link

```bash
php artisan migrate
php artisan db:seed
php artisan storage:link
```

### 5. Build asset frontend

```bash
npm run build
```

### 6. Jalankan aplikasi

```bash
php artisan serve
```

Buka `http://localhost:8000`

---

## Akun Demo

| Admin | admin@tokobungamelati.test | password |
| User | user@tokobungamelati.test | password |

*(Akun demo di atas dibuat otomatis lewat `php artisan db:seed` dengan status email sudah terverifikasi.)*

---

## REST API & Pengujian di Postman

Aplikasi ini menyediakan REST API sederhana dengan autentikasi token (Laravel Sanctum).
File collection Postman tersedia di `postman_collection.json`.

### Daftar Endpoint

| Method | Endpoint | Keterangan | Auth |
|---|---|---|---|
| POST | `/api/login` | Login, mengembalikan Bearer token | Tidak |
| GET | `/api/user` | Data user yang sedang login | Ya |
| POST | `/api/logout` | Logout (cabut token) | Ya |
| GET | `/api/categories` | List kategori | Tidak |
| GET | `/api/categories/{id}` | Detail kategori | Tidak |
| POST | `/api/categories` | Tambah kategori | Ya (Admin) |
| PUT | `/api/categories/{id}` | Update kategori | Ya (Admin) |
| DELETE | `/api/categories/{id}` | Hapus kategori | Ya (Admin) |
| GET | `/api/products` | List produk (support `?search=` & `?category_id=`) | Tidak |
| GET | `/api/products/{id}` | Detail produk | Tidak |
| POST | `/api/products` | Tambah produk | Ya (Admin) |
| PUT | `/api/products/{id}` | Update produk | Ya (Admin) |
| DELETE | `/api/products/{id}` | Hapus produk | Ya (Admin) |
| GET | `/api/orders` | List pesanan (milik sendiri, atau semua jika admin) | Ya |
| GET | `/api/orders/{id}` | Detail pesanan | Ya |
| POST | `/api/orders` | Buat pesanan baru | Ya |

### Cara Testing di Postman

1. Import `postman_collection.json` ke Postman.
2. Buka request **Login**, isi email & password akun demo, klik **Send**, copy `token` dari response.
3. Klik nama collection → tab **Variables** → paste token ke variable `token` → **Save**.
4. Sekarang semua request yang butuh login bisa langsung dites.

**Bukti pengujian:**

**1. Login (token keluar)**

![Login Postman](screenshots/postman-login.png)

**2. Create Product (Admin)**

![Create Product Postman](screenshots/postman-create-product.png)

**3. List Orders**

![List Orders Postman](screenshots/postman-list-orders.png)

---

## Dokumentasi Screenshot

### Login / Register

![Login](screenshots/login.png)
![Register](screenshots/register.png)

### Verifikasi Email

![Verifikasi Email](screenshots/verifikasi-email.png)

### Dashboard Admin

![Dashboard Admin](screenshots/dashboard-admin.png)

### CRUD Kategori & Produk

![CRUD Kategori](screenshots/crud-kategori.png)
![CRUD Produk](screenshots/crud-produk.png)

### Pengujian REST API di Postman

*(lihat bagian REST API di atas)*

### Perbedaan Menu Admin vs User

**Admin:**
![Navbar Admin](screenshots/navbar-admin.png)

**User:**
![Navbar User](screenshots/navbar-user.png)

### Tampilan Responsive

**Desktop:**
![Responsive Desktop](screenshots/responsive-desktop.png)

**Mobile:**
![Responsive Mobile](screenshots/responsive-mobile.png)

### Export PDF

![Export PDF](screenshots/export-pdf.png)

---

## Struktur Role

- **Admin**: kelola kategori, kelola produk, kelola status pesanan, lihat dashboard, export laporan, akses REST API penuh
- **User**: melihat katalog, memesan produk, mengajukan reservasi acara, melihat riwayat pesanan/reservasi sendiri, akses REST API terbatas (order miliknya sendiri)
