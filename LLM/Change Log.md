📝 CHANGELOG - [04-07-2026]
🚀 Added

    Antarmuka Workspace Baru (reports2-V2.php): Mengganti tata letak lama 3-kolom menjadi 2-kolom modern bergaya NotebookLM (Area Hasil Laporan yang Luas & Panel Kontrol Kanan).
    Widget Kondisi Cuaca v2: Menyisipkan panel informasi cuaca premium (Suhu, Curah Hujan, Kelembapan, Kondisi) terintegrasi tepat di atas hasil teks laporan AI.
    Fitur Input Konteks Dinamis: Menambahkan area teks (textarea) adaptif yang otomatis muncul saat pengguna memilih jenis laporan Tabel CSV atau Infografis.
    Arsitektur Eksternal Prompt (prompts/): Memisahkan instruksi peran sistem (system_role.txt) dan gaya penulisan laporan (style_*.txt) ke dalam file teks terpisah agar mudah diedit tanpa mengubah kode PHP.
    Otomatisasi Database (Trigger): Menambahkan skema trigger before_insert_climate_date_fix pada tabel climate_daily untuk pengisian kolom week_id dan year_id secara otomatis pada setiap data baru.

🔧 Fixed / Optimized
    Perbaikan Duplikasi AJAX Submit (reports2.php): Menghapus event listener ganda yang menyebabkan parameter bulan/tahun terkunci (hardcoded) dan selalu memanggil laporan mingguan.
    Dinamis URL Routing: Memastikan form mendeteksi pilihan Weekly/Monthly dan melempar request ke berkas backend yang tepat (generate_weekly_summary2.php atau generate_monthly_summary.php).
    Penyempurnaan Normalisasi Bridge AI: Memperbarui penanganan respons JSON agar kompatibel dengan standar format OpenAI/GitHub Models (choices[0].message.content) dan Gemini secara bersamaan.
    Skema Indeks Tabel climate_daily: Menambahkan kolom week_id, year_id, serta indeks kombinasi untuk mengoptimalkan kecepatan query hingga di bawah 5 milidetik.
    Visual Restyling index.php: Mengubah wajah dashboard utama menggunakan tema Modern Dark-Light Contrast (Sidebar Sleek Charcoal & Main Pane Isolated Scrolling).
