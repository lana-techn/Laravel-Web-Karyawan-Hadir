# 🏢 Maulana Employee Attendance App

Sistem manajemen kehadiran karyawan berbasis web yang modern dan responsif, dibangun dengan **Laravel 10** dan **Tailwind CSS**.

---

## 📋 Daftar Isi

- [Fitur Utama](#fitur-utama)
- [Teknologi yang Digunakan](#teknologi-yang-digunakan)
- [Prasyarat Instalasi](#prasyarat-instalasi)
- [Instalasi](#instalasi)
- [Konfigurasi](#konfigurasi)
- [Penggunaan](#penggunaan)
- [Screenshot](#screenshot)
- [Struktur Database](#struktur-database)
- [Akun Default](#akun-default)
- [Fitur Lanjutan](#fitur-lanjutan)
- [Kontribusi](#kontribusi)

---

## ✨ Fitur Utama

### Untuk Karyawan:
- ✅ **Absensi Masuk & Keluar** - Catat waktu masuk dan keluar dengan mudah
- 📍 **Geolokasi** - Verifikasi lokasi saat melakukan absensi
- 📅 **Riwayat Absensi** - Lihat histori kehadiran lengkap
- 🏥 **Izin & Sakit** - Pengajuan izin dan surat izin sakit
- 📊 **Laporan Personal** - Unduh laporan kehadiran dalam format PDF/Excel
- 👤 **Profil Karyawan** - Edit data profil dan informasi pribadi
- 📱 **Interface Responsif** - Dapat diakses dari desktop, tablet, dan mobile

### Untuk Admin/Manager:
- 🎯 **Dashboard Admin** - Monitoring kehadiran real-time
- 👥 **Manajemen Karyawan** - Tambah, edit, dan hapus data karyawan
- 📈 **Laporan Rekap** - Laporan komprehensif per periode
- 🗺️ **Monitor Lokasi** - Lihat sebaran lokasi absensi karyawan
- ✔️ **Persetujuan Izin** - Setujui atau tolak pengajuan izin
- 📮 **Integrasi Telegram** - Notifikasi otomatis via Telegram Bot
- 🔐 **Kontrol Akses** - Manajemen hak akses berbasis role

---

## 🛠️ Teknologi yang Digunakan

| Kategori | Teknologi |
|----------|-----------|
| **Backend** | Laravel 10 (PHP 8.1+) |
| **Frontend** | Tailwind CSS, Alpine.js |
| **Database** | MySQL 8.0+ |
| **Build Tool** | Vite |
| **Authentication** | Laravel Breeze |
| **Integrasi** | Telegram Bot SDK |
| **API** | RESTful API dengan Sanctum |

---

## 📦 Prasyarat Instalasi

Sebelum memulai, pastikan Anda memiliki:

- **PHP** 8.1 atau lebih tinggi
- **MySQL** 8.0 atau lebih tinggi
- **Composer** (untuk manajemen dependencies PHP)
- **Node.js** & **npm** (untuk build frontend assets)
- **Git** (untuk version control)
- **XAMPP** atau web server lainnya (optional)

### Cek Versi:
```bash
php -v
mysql --version
composer --version
node -v
npm -v
```

---

## 🚀 Instalasi

### 1. Clone Repository
```bash
git clone https://github.com/yourusername/maulana-attendance-app.git
cd "Maulana Employee Attendance App"
```

### 2. Install Dependencies PHP
```bash
composer install
```

### 3. Setup Environment File
```bash
cp .env.example .env
php artisan key:generate
```

### 4. Konfigurasi Database
Edit file `.env` dan atur konfigurasi database:
```env
DB_CONNECTION=mysql
DB_HOST=127.0.0.1
DB_PORT=3306
DB_DATABASE=laravel_absen
DB_USERNAME=root
DB_PASSWORD=
```

### 5. Install Dependencies Frontend
```bash
npm install
```

### 6. Migrasi Database
```bash
php artisan migrate:fresh
```

### 7. Seed Database (Data Awal)
```bash
php artisan db:seed
```

### 8. Build Frontend Assets
```bash
npm run build
```

---

## ⚙️ Konfigurasi

### Telegram Bot Integration (Opsional)
Untuk mengaktifkan notifikasi Telegram, atur di `.env`:
```env
TELEGRAM_BOT_TOKEN=your_bot_token_here
TELEGRAM_CHAT_ID=your_chat_id_here
```

### Environment Variables Penting
```env
APP_NAME="Maulana Attendance"
APP_ENV=local
APP_DEBUG=true
APP_URL=http://localhost:8000

MAIL_DRIVER=smtp
MAIL_HOST=smtp.mailtrap.io
MAIL_PORT=465
```

---

## 📖 Penggunaan

### Jalankan Development Server
```bash
php artisan serve
```

Server akan berjalan di `http://localhost:8000`

### Watch Mode untuk Frontend Development
```bash
npm run dev
```

### Production Build
```bash
npm run build
```

---

## 📸 Screenshot

### Dashboard Karyawan
![Dashboard Karyawan](assets/Screenshot%202025-11-27%20at%2020.50.22.png)

### Halaman Absensi Masuk
![Absensi Masuk](assets/Screenshot%202025-11-27%20at%2020.50.40.png)

### Halaman Absensi Keluar
![Absensi Keluar](assets/Screenshot%202025-11-27%20at%2020.50.49.png)

### Halaman Izin & Sakit
![Izin & Sakit](assets/Screenshot%202025-11-27%20at%2020.51.03.png)

### Histori Absensi
![Histori Absensi](assets/Screenshot%202025-11-27%20at%2020.51.09.png)

### Laporan Kehadiran
![Laporan](assets/Screenshot%202025-11-27%20at%2020.51.17.png)

### Dashboard Admin
![Dashboard Admin](assets/Screenshot%202025-11-27%20at%2020.51.54.png)

### Manajemen Karyawan
![Manajemen Karyawan](assets/Screenshot%202025-11-27%20at%2020.52.21.png)

---

## 🗄️ Struktur Database

### Tabel Utama

#### Users
Menyimpan data karyawan dan admin

```sql
CREATE TABLE users (
  id BIGINT PRIMARY KEY,
  perner VARCHAR(20) UNIQUE,
  nama VARCHAR(100),
  email VARCHAR(100) UNIQUE,
  password VARCHAR(255),
  jabatan VARCHAR(100),
  id_telegram VARCHAR(50),
  created_at TIMESTAMP,
  updated_at TIMESTAMP
);
```

#### Absensi (Absensis)
Menyimpan record absensi masuk dan keluar

```sql
CREATE TABLE absensis (
  id BIGINT PRIMARY KEY,
  id_user BIGINT,
  tanggal DATE,
  jam_masuk TIME,
  jam_keluar TIME,
  lokasi_masuk VARCHAR(255),
  lokasi_keluar VARCHAR(255),
  latitude_masuk DECIMAL(10, 8),
  longitude_masuk DECIMAL(11, 8),
  latitude_keluar DECIMAL(10, 8),
  longitude_keluar DECIMAL(11, 8),
  keterangan TEXT,
  created_at TIMESTAMP,
  updated_at TIMESTAMP,
  FOREIGN KEY (id_user) REFERENCES users(id)
);
```

#### Pengajuan Izin
Menyimpan data pengajuan izin dan sakit

```sql
CREATE TABLE pengajuan_izins (
  id BIGINT PRIMARY KEY,
  id_user BIGINT,
  jenis_izin VARCHAR(50),
  tanggal_mulai DATE,
  tanggal_selesai DATE,
  keterangan TEXT,
  status ENUM('pending', 'approved', 'rejected'),
  disetujui_oleh BIGINT,
  created_at TIMESTAMP,
  updated_at TIMESTAMP,
  FOREIGN KEY (id_user) REFERENCES users(id),
  FOREIGN KEY (disetujui_oleh) REFERENCES users(id)
);
```

#### Jabatan
Data struktur organisasi

```sql
CREATE TABLE jabatans (
  id BIGINT PRIMARY KEY,
  nama_jabatan VARCHAR(100),
  deskripsi TEXT,
  created_at TIMESTAMP,
  updated_at TIMESTAMP
);
```

---

## 🔑 Akun Default

Setelah menjalankan seeders, tersedia akun default:

### Admin
```
Email: admin@example.com
Password: password
Role: SUPERADMIN
```

### Karyawan Sampel
Sistem sudah membuat 322+ user karyawan dengan email:
```
karyawan1@example.com (password: password)
karyawan2@example.com (password: password)
... dst
```

---

## 🚀 Fitur Lanjutan

### 1. Geolokasi dan Verifikasi Lokasi
- Sistem menggunakan Geolocation API untuk mendapatkan koordinat akurat
- Admin dapat mengatur radius kerja yang diizinkan
- Pencegahan fraud dengan verifikasi lokasi

### 2. Integrasi Telegram Bot
- Notifikasi otomatis ketika karyawan absensi
- Reminder pengajuan izin
- Alert jika ada keterlambatan

### 3. Export Data
- Laporan dalam format PDF
- Export ke Excel untuk analisis lebih lanjut
- Rekap bulanan dan tahunan

### 4. Sistem Role & Permission
- **SUPERADMIN**: Akses penuh ke semua fitur
- **ADMIN**: Manajemen karyawan dan laporan
- **TEAM WAGNER**: Level manager
- **USER**: Akses dasar absensi

### 5. Real-time Monitoring
- Dashboard live karyawan yang sedang absensi
- Map view lokasi absensi
- Chart analytics kehadiran

---

## 📝 API Endpoints

### Authentication
```
POST   /login          - Login user
POST   /logout         - Logout user
POST   /register       - Registrasi user baru
```

### Absensi
```
GET    /api/absen                 - Get daftar absensi
POST   /api/absen                 - Create absensi baru
GET    /api/absen/{id}            - Get detail absensi
PUT    /api/absen/{id}            - Update absensi
DELETE /api/absen/{id}            - Hapus absensi
```

### Izin
```
POST   /api/izin                  - Buat pengajuan izin
GET    /api/izin/{id}             - Get detail izin
PUT    /api/izin/{id}/approve     - Approve izin
PUT    /api/izin/{id}/reject      - Reject izin
```

---

## 🐛 Troubleshooting

### 1. Error "SQLSTATE[HY000]: General error"
```bash
php artisan migrate:fresh --seed
```

### 2. Assets tidak tampil
```bash
npm run build
php artisan storage:link
```

### 3. Permission denied pada storage
```bash
chmod -R 775 storage bootstrap/cache
```

### 4. Database connection error
Pastikan MySQL running dan konfigurasi `.env` benar

---

## 🔒 Keamanan

- ✅ Password hashing dengan bcrypt
- ✅ CSRF protection
- ✅ XSS prevention
- ✅ SQL injection protection
- ✅ Rate limiting
- ✅ API token authentication (Sanctum)

---

## 📄 Lisensi

Project ini dilisensikan di bawah **MIT License** - lihat file [LICENSE](LICENSE) untuk detail.

---

## 👥 Kontribusi

Kami menerima kontribusi! Silakan:

1. Fork repository ini
2. Buat branch fitur (`git checkout -b feature/AmazingFeature`)
3. Commit perubahan (`git commit -m 'Add AmazingFeature'`)
4. Push ke branch (`git push origin feature/AmazingFeature`)
5. Buat Pull Request

---

## 📞 Kontak & Support

- **Email**: support@maulana.com
- **Telegram**: @maulana_support
- **Issues**: Gunakan GitHub Issues untuk bug reports

---

## 🙏 Ucapan Terima Kasih

Terima kasih kepada:
- Komunitas Laravel
- Tailwind CSS
- Semua kontributor yang telah membantu

---

**Dibuat dengan ❤️ oleh Tim Maulana**

*Last Updated: November 27, 2025*
