# Tahap 3 — Pelaksanaan Eksperimen Deteksi Kendaraan

**Status:** Selesai 
**Bergantung pada:** [tahap-2-implementasi-gateway.md](tahap-2-implementasi-gateway.md)
**Lokasi kode:** [../05-kode/k6](../05-kode/k6)

---

## Tujuan

Melaksanakan eksperimen untuk membandingkan performa model YOLOv8 dan YOLOv5 dalam mendeteksi kendaraan pada rekaman CCTV Kabupaten Kebumen berdasarkan waktu komputasi dan jumlah objek yang berhasil dideteksi.
## Deliverable

-[x] Pelaksanaan pengujian menggunakan model YOLOv8.
-[x] Pelaksanaan pengujian menggunakan model YOLOv5.
-[x] Pengujian pada tiga video CCTV Kabupaten Kebumen.
-[x] Pengulangan eksperimen sebanyak 3 kali pada setiap video.
-[x] Pencatatan waktu preprocess, inference, dan postprocess.
-[x] Penyimpanan hasil eksperimen dalam format CSV.
-[x] Dokumentasi konfigurasi eksperimen.

## Desain Eksperimen

Eksperimen dilakukan menggunakan dua model object detection dengan dataset yang sama sehingga hasil yang diperoleh dapat dibandingkan secara adil (fair comparison).

## Variabel Penelitian
| Variabel    | Keterangan                     |
| ----------- | ------------------------------ |
| Model       | YOLOv8, YOLOv5                 |
| Dataset     | 3 Video CCTV Kabupaten Kebumen |
| Pengulangan | 3 kali setiap video            |
| Image Size  | 640 × 640                      |
| Device      | CPU                            |
| Confidence  | 0.25                           |


## Dataset

| No | Nama Video        |
| -- | ----------------- |
| 1  | depan_dprd.mp4    |
| 2  | depan_pendopo.mp4 |
| 3  | merdeka_timur.mp4 |

## Jumlah Eksperimen

| Model  | Video | Pengulangan | Total |
| ------ | ----- | ----------- | ----- |
| YOLOv8 | 3     | 3           | 9     |
| YOLOv5 | 3     | 3           | 9     |

Total eksperimen yang dilakukan adalah 18 kali pengujian.

### Alur Eksperimen
```
Dataset CCTV
        │
        ▼
Load Video
        │
        ▼
Frame Extraction
        │
        ▼
YOLO Detection
(YOLOv8 / YOLOv5)
        │
        ▼
Vehicle Detection
        │
        ▼
Performance Logging
        │
        ▼
CSV Results
```

### Parameter yang Dicatat

| Parameter                   | Satuan |
| --------------------------- | ------ |
| Preprocess Time             | ms     |
| Inference Time              | ms     |
| Postprocess Time            | ms     |
| Total Pipeline              | ms     |
| Jumlah Kendaraan Terdeteksi | Objek  |

## Struktur Dataset Hasil

seluruh data di simpan dalam file :
```
04-data/yolo_results.csv
```
```
04-data/

├── yolo_results.csv
├── preprocess_results.csv
├── inference_results.csv
├── postprocess_results.csv
└── pipeline_results.csv
```

## Hasil Pelaksanaan
Eksperimen berhasil dijalankan menggunakan dua model YOLO pada tiga video CCTV Kabupaten Kebumen.

Seluruh proses berhasil menghasilkan:

- data preprocess,
- data inference,
- data postprocess,
- total waktu pipeline,
- jumlah kendaraan yang berhasil dideteksi.

Seluruh data kemudian digunakan pada Tahap 4 untuk analisis statistik dan visualisasi hasil penelitian.

## Ringkasan Eksperimen

| Model  | Jumlah Pengujian |
| ------ | ---------------- |
| YOLOv8 | 9                |
| YOLOv5 | 9                |

## Catatan Lingkungan

Eksperimen dijalankan menggunakan konfigurasi perangkat keras dan perangkat lunak yang sama agar hasil pengujian bersifat konsisten. Kedua model menggunakan parameter inferensi yang identik sehingga perbandingan performa dilakukan secara objektif. Dataset yang digunakan merupakan tiga rekaman CCTV Kabupaten Kebumen dengan kondisi lalu lintas yang berbeda.