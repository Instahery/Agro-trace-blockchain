# ️ Klumbayan Agro-Trace Blockchain: Project Roadmap

> **Sistem Traceability Pertanian Berbasis Blockchain & GIS**
> Dari Pembelian Petani hingga Product Passport yang Terverifikasi.


## 🏆 Milestone yang Tercapai

### 🟢 Maret 2026: Fase Fondasi & Akuisisi Data
- **Desain Database Relasional:** Membangun struktur tabel `trace_batches`, `nota_master`, `nota_detail`, dan `data_petani`.
- **Sistem Pembelian:** Mengambil data pembelian dari petani/pengepul dan generate `batch_id` awal.
- **Autentikasi & Role:** Implementasi login admin dan routing dasar menggunakan AdminLTE.

### 🟡 April 2026: Fase Geospatial & Traceability Dasar
- **Integrasi GIS:** Menambahkan pemetaan lahan petani menggunakan `Leaflet.js` dan format `GeoJSON`.
- **Fallback Data:** Sistem cerdas yang mengambil data petani dari GIS (`trip_lahan`) atau Nota (`nota_master`).
- **Halaman `trace.php` Awal:** Menampilkan informasi produk, foto petani, dan peta lahan untuk publik.

### 🟠 Mei 2026: Fase Rantai Pasok & Konsolidasi
- **Arsitektur Many-to-One:** Membuat tabel `batch_lineage` untuk melacak penggabungan batch (dari kg ke ton).
- **Sistem Input Log Terpisah:** 
  - `log-progres-awal.php`: Untuk tahap hulu (Proses Awal, Terima Gudang).
  - `log-progres-lanjut.php`: Untuk tahap hilir (Packing, Transport, Gudang Hub).
- **Optimasi Database:** Menyeragamkan collation ke `utf8mb4_unicode_ci` untuk mencegah error `UNION` dan `JOIN`.

### 🔴 Juni 2026: Fase Blockchain & Product Passport
- **Smart Contract Design:** Membuat contract `KlumbayanTraceability.sol` di Remix IDE untuk Polygon Amoy.
- **Message Signature:** Integrasi MetaMask untuk menandatangani hash data batch (*Zero-gas verification*).
- **Unified `verify.php`:** Membuat "Smart Router" yang otomatis mendeteksi apakah batch adalah "Batch Petani" (tampil GIS) atau "Batch Konsolidasi" (tampil Komposisi Induk).
- **Product Passport Final:** Halaman publik lengkap dengan timeline, bukti blockchain, dan peta interaktif.

---

## 🛠️ Tech Stack

| Kategori | Teknologi |
| :--- | :--- |
| **Backend** | PHP 8.x, PDO, MySQL/MariaDB |
| **Frontend** | Bootstrap 5, AdminLTE, jQuery, AJAX |
| **Geospatial** | Leaflet.js, GeoJSON, ArcGIS Tiles |
| **Blockchain** | Solidity ^0.8.20, Ethers.js, MetaMask, Polygon (Amoy/Mainnet) |
| **Tools** | Remix IDE, Git/GitHub, cPanel |
---

## 🏗️ Infografis Arsitektur Sistem

```mermaid
graph TD
    A[👨‍🌾 Petani / Pengepul] -->|1. Data Pembelian| B[(MySQL Database)]
    B -->|2. GIS & GeoJSON| C[🗺️ Leaflet Maps]
    B -->|3. Batch Lineage| D[🔄 Konsolidasi Many-to-One]
    D -->|4. Process Logs| E[📋 Input Progres Lapangan]
    E -->|5. SHA-256 Hash| F[🦊 MetaMask Wallet]
    F -->|6. Smart Contract| G[️ Polygon Blockchain]
    G -->|7. Verifikasi Publik| H[📱 Product Passport / QR Code]
    H -->|8. Transparansi| I[🌍 Buyer & Auditor]
    
    style A fill:#f9f,stroke:#333,stroke-width:2px
    style G fill:#8247e5,stroke:#333,stroke-width:2px,color:#fff
    style H fill:#2d6a4f,stroke:#333,stroke-width:2px,color:#fff
    style I fill:#ff9800,stroke:#333,stroke-width:2px,color:#fff

