Markdown

# Dokumentasi Arsitektur Sistem - Enterprise Knowledge Management (EKM)

Dokumen ini menjelaskan arsitektur data, alur kerja (pipeline), dan interaksi komponen di dalam Sistem Laporan Otomatis berbasis Kecerdasan Buatan (AI) pada **PT Klumbayan Gold Farm**.

---

## 1. Topologi Alur Data (Data Pipeline)

Sistem ini mengadopsi arsitektur *Linear Pipeline with Dynamic Feedback Loop*, di mana data mentah dari lapangan diproses secara bertahap hingga menjadi produk pengetahuan siap cetak bagi eksekutif.

[ Google Drive Storage ]
│
▼ (Proses 1: Extraction Script)
[ Google Drive API Sync / PDF Parser ]
│
▼
[ MySQL: Tabel document_text (Raw Text/Narrative) ] & [ Tabel climate_daily (Physical Data) ]
│
▼ (Proses 2: Aggregator Script - generate_weekly_summary2.php)
[ Filter URL Parameter: ?type=weekly | monthly ]
│
▼
[ Pembuatan System Prompt Berbasis Persona (CFO, CEO, Scientist) ]
│
▼ (Proses 3: LLM Engine Processing via API)
[ Smart JSON Parsing & Sanitation (```json Guard) ]
│
▼ (Proses 4: DB Helper - converter_json_mysql_helper.php)
[ MySQL: Tabel ai_analyses (Multi-Column JSON Storage) ]
│
▼ (Proses 5: UI Renderer - cetak_jurnal_html.php)
[ Adaptive HTML Content Rendering & PDF Print Engine ]


---

## 2. Penjelasan Detail Komponen Komponen Utama

### A. Lapisan Akuisisi Data (Data Acquisition Layer)
1. **Google Drive Cloud Scanner**: Skrip yang mendengarkan atau memindai folder repositori laporan lapangan di Google Drive.
2. **Text Extractor & Parser**: Mengonversi berkas dokumen (PDF/DOCX) dari lapangan menjadi teks mentah (*string*) dan membersihkan karakter-karakter non-standar.
3. **Database Ingestion**: Hasil ekstraksi disimpan ke dalam dua tabel dasar:
   - `document_text`: Menyimpan narasi aktivitas mingguan (`week_id`, `year`, `full_text`).
   - `climate_daily`: Menyimpan metrik cuaca harian per desa (`village`, `temp_mean`, `rainfall`, `soil_moisture`, dll).

### B. Lapisan Agregasi & Kontrol Konten (Aggregation & Control Layer)
Lapisan ini diatur secara dinamis oleh skrip `generate_weekly_summary2.php`.
- **Dual-Mode Handler**: Menggunakan kontrol variabel `$type = $_GET['type'] ?? 'weekly';` untuk menentukan apakah kueri database harus mengagregasi data berdasarkan rentang mingguan atau bulanan secara otomatis.
- **Cache Isolation**: Hasil penarikan data sementara disimpan ke dalam berkas *cache* terpisah (`testknowledge_weekly.json` atau `testknowledge_monthly.json`) agar aliran data mingguan dan bulanan tidak saling menimpa (*race condition*).

### C. Lapisan Kecerdasan Buatan (AI Processing Layer)
- **Persona Alignment**: Sistem menyuntikkan instruksi khusus (*System Prompt*) sebelum teks dikirim ke LLM. 
  * *Contoh Persona CFO*: Memaksa AI untuk menerjemahkan data fisik (seperti penurunan kelembaban tanah atau kematian bibit) menjadi indikator devaluasi aset, risiko finansial operasional (*overbudgeting*), dan pemenuhan kepatuhan donor (*donor compliance*).
- **Structured Output Guarantees**: Prompt memaksa LLM mengembalikan data dalam format JSON murni dengan struktur kunci (*key*) yang telah ditentukan secara baku.

### D. Lapisan Penyimpanan Pengetahuan (Enterprise Knowledge Layer)
Diproses oleh `converter_json_mysql_helper.php`.
- **JSON Sanitation**: Skrip secara otomatis mendeteksi dan membersihkan pembungkus *markdown block* (seperti ` ```json ... ``` `) yang sering dihasilkan oleh LLM.
- **Relational Mapping to Columnar JSON**: Objek JSON utama didekonstruksi dan didistribusikan ke 27 kolom spesifik pada tabel `ai_analyses` (misal kolom `cfo_analysis`, `agro_climate_weather`, `risks`, dll) menggunakan mekanisme `INSERT ... ON DUPLICATE KEY UPDATE` untuk menjamin efisiensi ruang dan pembaruan data yang cepat.

### E. Lapisan Presentasi Dinamis (Dynamic Presentation Layer)
Diproses oleh `cetak_jurnal_html.php`.
- **Dynamic Content Sniffing**: Halaman cetak HTML tidak lagi dikunci (*hardcoded*) untuk satu persona saja. Kode PHP menggunakan logika `!empty($row['nama_kolom'])` untuk mendeteksi ketersediaan data di database.
- **Adaptive Layout rendering**:
  * Jika kolom `cfo_analysis` terisi, komponen visual laporan keuangan korporat akan otomatis dirender dengan aksen warna formal (*slate blue*).
  * Jika kolom data agroklimat (`agro_climate_weather` / `soil`) terisi, sistem otomatis memunculkan tabel infografis ringkasan kondisi cuaca lapangan lengkap dengan indikator warna (*soft-heatmap table*) tanpa memerlukan modul kanvas JavaScript pihak ketiga.
- **Print & PDF Engine**: Menggunakan media kueri CSS `@media print` untuk menyembunyikan elemen UI kontrol browser (seperti tombol cetak) dan memformat tata letak agar pas dengan ukuran kertas standar internasional A4 (210mm x 297mm) tanpa terpotong secara canggung di tengah halaman (*page-break safety*).

---

## 3. Desain Skema Tabel Utama (`ai_analyses`)

Penyimpanan akhir dari seluruh kecerdasan sistem berpusat pada tabel ini dengan struktur hibrida (Relasional + JSON asli):

| Nama Kolom | Tipe Data | Peran / Deskripsi |
| :--- | :--- | :--- |
| `analysis_id` | VARCHAR(50) [UNIQUE] | Kunci utama bisnis (Format: KGF-CFO-YYYYMMDD-XXX) |
| `executive_title` | VARCHAR(255) | Judul utama dokumen hasil perumusan AI |
| `executive_summary` | TEXT | Ringkasan eksekutif tingkat tinggi |
| `findings` | JSON | Kumpulan array temuan teknis umum lapangan |
| `cfo_analysis` | JSON | Blok analisis khusus keuangan, tata kelola, dan SROI |
| `agro_climate_weather`| JSON | Array data cuaca harian terstruktur per desa |
| `agro_climate_soil` | JSON | Array parameter kelembaban dan suhu tanah terstruktur |

---
