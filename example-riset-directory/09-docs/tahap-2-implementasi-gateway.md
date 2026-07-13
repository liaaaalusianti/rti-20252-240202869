# Tahap 2 — Implementasi Sistem Deteksi Kendaraan

**Status:** Selesai
**Acuan arsitektur:** [tahap-1-arsitektur-dan-skema-database.md](tahap-1-arsitektur-dan-skema-database.md)
**Lokasi kode:** [../05-kode/gateway/](../05-kode/gateway/)

---

## Tujuan

Mengimplementasikan sistem deteksi kendaraan menggunakan dua model deep learning, yaitu YOLOv8 sebagai metode utama dan YOLOv5 sebagai metode pembanding (baseline). Implementasi dilakukan menggunakan Python dengan framework Ultralytics YOLO dan OpenCV untuk memproses rekaman CCTV Kabupaten Kebumen.

## Deliverable

 - [X] Implementasi model YOLOv8 untuk deteksi kendaraan.
 - [X] Implementasi model YOLOv5 sebagai metode pembanding.
 - [X] Modul pembacaan video menggunakan OpenCV.
 - [X] Modul preprocessing frame video (resize 640 × 640 piksel).
 - [X] Modul deteksi kendaraan secara otomatis.
 - [X] Modul pencatatan waktu preprocess, inference, dan postprocess.
 - [X] Penyimpanan hasil pengujian dalam format CSV.
 - [X] Dokumentasi kebutuhan perangkat lunak (requirements.txt).
 - [X] Struktur folder penelitian yang memisahkan dataset, source code, hasil eksperimen, dan visualisasi.

## Struktur Implementasi

```
Dataset CCTV
        │
        ▼
Video Reader (OpenCV)
        │
        ▼
Frame Preprocessing
(Resize 640×640)
        │
        ▼
YOLOv8 / YOLOv5
Object Detection
        │
        ▼
Vehicle Detection
(Bounding Box + Label)
        │
        ▼
Performance Logger
        │
        ▼
CSV Results

```
## Hasil Implementasi
Implementasi berhasil dijalankan menggunakan Python dengan library Ultralytics YOLO, OpenCV, NumPy, dan Pandas. Sistem mampu membaca ketiga video CCTV yang digunakan sebagai dataset penelitian kemudian melakukan proses deteksi kendaraan secara otomatis menggunakan model YOLOv8 maupun YOLOv5.

Output yang dihasilkan meliputi:

- Bounding box kendaraan.
- Label objek kendaraan.
- Nilai confidence setiap deteksi.
- Waktu preprocessing.
- Waktu inference.
- Waktu postprocessing.
- File CSV hasil pengujian.
- Video hasil deteksi.

## Hasil Verifikasi
Verifikasi implementasi dilakukan dengan menjalankan kedua model pada tiga video CCTV Kabupaten Kebumen.

Hasil pengujian menunjukkan bahwa:

- YOLOv8 berhasil melakukan deteksi kendaraan pada seluruh video pengujian.
- YOLOv5 juga berhasil mendeteksi kendaraan pada seluruh video sebagai model pembanding.
- Sistem berhasil mencatat waktu preprocess, inference, dan postprocess untuk setiap proses deteksi.
- Seluruh hasil eksperimen berhasil disimpan dalam file yolo_results.csv yang kemudian digunakan pada tahap analisis data dan visualisasi hasil penelitian.

## Konfigurasi Lingkungan

| Komponen             | Spesifikasi           |
| -------------------- | --------------------- |
| Bahasa Pemrograman   | Python 3.11           |
| Framework            | Ultralytics YOLO      |
| Library              | OpenCV, NumPy, Pandas |
| Model                | YOLOv8 dan YOLOv5     |
| Device               | CPU                   |
| Image Size           | 640 × 640             |
| Confidence Threshold | 0.25                  |
| Format Output        | CSV                   |

## Dataset 

| No | Nama Dataset      |
| -- | ----------------- |
| 1  | depan_dprd.mp4    |
| 2  | depan_pendopo.mp4 |
| 3  | merdeka_timur.mp4 |

Masing-masing video diuji menggunakan YOLOv8 dan YOLOv5 sebanyak 3 kali, sehingga diperoleh 18 kali eksperimen.

## Struktur Folder Implementasi
```
05-kode/
│
├── yolo_v8.py
├── yolo_v5.py
├── requirements.txt
├── utils.py
└── README.md
```

## Catatan Implementasi
1. Seluruh eksperimen dijalankan menggunakan konfigurasi perangkat keras dan perangkat lunak yang sama untuk menjaga konsistensi hasil pengujian.
2. Kedua model menggunakan parameter inferensi yang identik sehingga perbandingan performa dilakukan secara adil (fair comparison).
3. Dataset yang digunakan berupa tiga rekaman CCTV Kabupaten Kebumen dengan kondisi lalu lintas yang berbeda.
4. Hasil pengujian disimpan dalam format CSV sehingga dapat digunakan pada Tahap 3 (Eksekusi Eksperimen), Tahap 4 
(Analisis Data), serta Tahap 5 (Penyusunan Laporan Penelitian).


