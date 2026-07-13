# Tahap 1 — Perancangan Arsitektur & Skema Database

**Status:** Selesai

---

## 1. Komponen Sistem

Sistem deteksi kendaraan yang dikembangkan terdiri atas beberapa komponen utama sebagai berikut.

1. Input Video
   - Berupa tiga video CCTV lalu lintas Kabupaten Kebumen:
      - depan_dprd.mp4
      - depan_pendopo.mp4
      - merdeka_timur.mp4
2. Preprocessing
   - Membaca setiap frame video menggunakan OpenCV.
   - Mengubah frame menjadi ukuran input 640 × 640 piksel sesuai kebutuhan model YOLO.
3. Model Deteksi Objek
   - YOLOv8 sebagai metode utama.
   - YOLOv5 sebagai metode pembanding (baseline).
4. Output Deteksi
   - Bounding box kendaraan.
   - Label kelas kendaraan.
   - Confidence score hasil deteksi.
5. Performance Logger
   - Mencatat waktu:
      - Preprocess
      - Inference
      - Postprocess
   - Data disimpan ke dalam file CSV untuk analisis.

## 2. Alur Sistem

```
Video CCTV
      │
      ▼
Membaca Frame Video
      │
      ▼
Preprocessing
(Resize 640 × 640)
      │
      ▼
YOLOv8 / YOLOv5
(Object Detection)
      │
      ▼
Bounding Box + Label
      │
      ▼
Performance Logger
      │
      ▼
CSV Hasil Pengujian

```

Catatan: Seluruh proses dilakukan menggunakan parameter yang sama agar perbandingan antara YOLOv8 dan YOLOv5 bersifat fair comparison.

## 3. Dataset Penelitian
Dataset yang digunakan terdiri atas tiga video CCTV lalu lintas Kabupaten Kebumen.

| Nama Video        | Lokasi                                |
| ----------------- | ------------------------------------- |
| depan_dprd.mp4    | Depan DPRD Kabupaten Kebumen          |
| depan_pendopo.mp4 | Depan Pendopo Kabupaten Kebumen       |
| merdeka_timur.mp4 | Jalan Merdeka Timur Kabupaten Kebumen |

Ketiga video digunakan pada kedua model sehingga tidak terdapat perbedaan dataset selama eksperimen.

## 4. Parameter Pengujian

| Parameter            | Nilai           |
| -------------------- | --------------- |
| Image Size           | 640 × 640       |
| Confidence Threshold | 0.25            |
| Device               | CPU             |
| Framework            | Python          |
| Library              | OpenCV          |
| Model                | YOLOv8 & YOLOv5 |


## 5. Skenario Eksperimen

Eksperimen dilakukan menggunakan dua model deteksi objek.

| Model  | Video         | Jumlah Run |
| ------ | ------------- | ---------- |
| YOLOv8 | depan_dprd    | 3          |
| YOLOv8 | depan_pendopo | 3          |
| YOLOv8 | merdeka_timur | 3          |
| YOLOv5 | depan_dprd    | 3          |
| YOLOv5 | depan_pendopo | 3          |
| YOLOv5 | merdeka_timur | 3          |

Total eksperimen yang dilakukan adalah 18 run.

## 6. Metrik Evaluasi
Penelitian mengevaluasi performa model menggunakan metrik berikut.

| Metrik              | Keterangan                                            |
| ------------------- | ----------------------------------------------------- |
| Preprocess Time     | Waktu persiapan frame sebelum deteksi (ms)            |
| Inference Time      | Waktu proses deteksi objek oleh model (ms)            |
| Postprocess Time    | Waktu pemrosesan hasil deteksi (ms)                   |
| Total Pipeline Time | Total waktu preprocess + inference + postprocess (ms) |

## 7. Keputusan Teknis (Final)
1. Menggunakan YOLOv8 sebagai metode utama dan YOLOv5 sebagai baseline.
2. Seluruh eksperimen menggunakan dataset CCTV yang sama.
3. Parameter pengujian dibuat identik (image size, confidence threshold, device, dan environment) untuk memastikan perbandingan yang adil.
4. Setiap kombinasi model dan video diuji sebanyak 3 kali, sehingga diperoleh 18 data eksperimen.
5. Hasil eksperimen direkam ke dalam file CSV, kemudian dihitung nilai mean, standar deviasi, dan total pipeline time sebagai dasar analisis performa.