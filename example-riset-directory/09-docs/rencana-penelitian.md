# Rencana Penelitian: Perbandingan YOLOv8 dan YOLOv5 dalam Deteksi Kendaraan pada Rekaman CCTV untuk Mendukung Smart City di Kabupaten Kebumen

## 1. Ringkasan

| Item                 | Keterangan                                                                                                                                                                         |
| -------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| **Judul**            | Perbandingan YOLOv8 dan YOLOv5 dalam Deteksi Kendaraan pada Rekaman CCTV untuk Mendukung Smart City di Kabupaten Kebumen                                                           |
| **Target Publikasi** | Seminar Nasional / Jurnal SINTA                                                                                                                                                    |
| **Metode**           | Comparison Study                                                                                                                                                                   |
| **Framework**        | Ultralytics YOLOv8, YOLOv5, OpenCV, Python                                                                                                                                         |
| **Dataset**          | Tiga video CCTV Kabupaten Kebumen (depan_dprd.mp4, depan_pendopo.mp4, merdeka_timur.mp4)                                                                                           |
| **Masalah**          | Sistem pemantauan lalu lintas masih bergantung pada observasi manual sehingga kurang efisien dalam menghasilkan informasi secara real-time.                                        |
| **Solusi**           | Membandingkan performa YOLOv8 dan YOLOv5 untuk mengetahui model yang memiliki waktu pemrosesan paling cepat pada deteksi kendaraan berbasis CCTV sebagai pendukung Smart Mobility. |


## 2. Alur Kerja (Roadmap)

Setiap tahap memiliki file rencana detail tersendiri agar lebih rapi:

- [✓] **Tahap 1** — Studi Literatur dan Identifikasi Masalah — Selesai
- [✓] **Tahap 2** — Penyusunan Proposal Penelitian dan Research Question — Selesai
- [✓] **Tahap 3** — Persiapan Dataset CCTV dan Lingkungan Eksperimen — Selesai
- [✓] **Tahap 4** — Implementasi YOLOv8 dan YOLOv5 — Selesai
- [✓] **Tahap 5** — Pelaksanaan Eksperimen (18 Run) — Selesai
- [✓] **Tahap 6** — Pengumpulan dan Validasi Data — Selesai
- [✓] **Tahap 7** — Analisis Data, Perhitungan Mean dan Standar Deviasi — Selesai
- [✓] **Tahap 8** — Pembuatan Grafik dan Interpretasi Hasil — Selesai
- [✓] **Tahap 9** — Penyusunan Proposal dan Laporan Penelitian — Selesai
---

## 3. Catatan

Penelitian ini menggunakan pendekatan kuantitatif eksperimental dengan desain comparison study. Pengujian dilakukan menggunakan dua model deteksi objek, yaitu YOLOv8 sebagai metode utama dan YOLOv5 sebagai baseline. Eksperimen menggunakan tiga video CCTV Kabupaten Kebumen, masing-masing diuji sebanyak tiga kali pada setiap model sehingga menghasilkan 18 kali eksperimen. Parameter pengujian dibuat identik, yaitu image size 640, confidence threshold 0,25, device CPU, dan dataset yang sama, sehingga hasil perbandingan bersifat adil (fair comparison). Data yang dianalisis meliputi waktu preprocess, inference, postprocess, dan total pipeline, kemudian dihitung nilai rata-rata serta standar deviasinya sebagai dasar evaluasi performa kedua model
