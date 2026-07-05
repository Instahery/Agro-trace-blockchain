# Changelog

Semua perubahan penting dalam proyek ini akan didokumentasikan dalam file ini.

## [Unreleased] - 2026-07-05

### Kegiatan Hari Ini: Optimasi Database, Ekstraksi Prompt Eksternal, Normalisasi JSON AI, dan Modul Cetak Jurnal

---

### 🚀 Added
- **Otomatisasi Kolom Waktu & Tahun (`climate_daily`):** - Menambahkan kolom `week_id` dan `year_id` pada tabel `climate_daily` untuk mempercepat kueri laporan mingguan/bulanan.
  - Membuat MySQL Trigger `before_insert_climate_date_fix` untuk mengisi nilai `week_id` dan `year_id` secara otomatis setiap kali ada data cuaca baru yang masuk.
- **Arsitektur Manajemen Prompt Eksternal (`prompts/`):**
  - Memisahkan instruksi peran kecerdasan buatan (`system_role.txt`) dan gaya laporan (`style_*.txt`) ke dalam file teks terpisah agar mudah dikonfigurasi tanpa menyentuh kode PHP utama.
- **Skema Hybrid Database Hasil AI (`ai_analyses`):**
  - Membuat tabel `ai_analyses` dengan tipe data kolom `JSON` untuk menampung struktur data bertingkat (*nested array/object*) dari *output* AI (seperti komponen *findings*, *risks*, dan *references*).
- **Modul Pembersih & Pengonversi Otomatis (`converter_helper.php`):**
  - Membuat fungsi pintar `insertAiAnalysisToMysql()` yang dapat dipanggil dari halaman mana saja untuk membaca, membersihkan, dan menyimpan file JSON hasil AI langsung ke database.
- **Halaman Cetak Jurnal Formal (`cetak_jurnal_html.php`):**
  - Membuat template cetak berbasis HTML murni dan CSS modern (`@media print`) yang mendukung cetak langsung ke kertas A4 atau *Save as PDF* dengan fitur anti-potong teks (`page-break-inside: avoid`).
- **Repositori Dashboard Laporan (`index_jurnal.php`):**
  - Membuat halaman tabel utama menggunakan Bootstrap 5 untuk menampilkan daftar dokumen analisis yang tersimpan di MySQL beserta tombol aksi untuk membuka tab cetak baru.

---

### 🔧 Fixed & Optimized
- **Perbaikan Syntax Error Trigger MySQL:** - Menghapus pembungkus `BEGIN ... END` yang berlebih pada saat deklarasi skrip trigger di phpMyAdmin.
- **Normalisasi Karakter Blok Markdown JSON:**
  - Menambahkan fungsi pembersihan berbasis `preg_replace` di backend PHP untuk menghapus otomatis penanda teks 
http://googleusercontent.com/immersive_entry_chip/0

### Tips Penggunaan di GitHub:
1. Buat file baru bernama `change_log.md` di root folder proyek Anda.
2. Salin teks di atas dan tempel (*paste*) ke dalam file tersebut.
3. Lakukan *commit* dengan pesan: `git commit -m "docs: update changelog for AI journal printing and DB optimization"`.
