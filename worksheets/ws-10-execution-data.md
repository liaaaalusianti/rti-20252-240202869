# WS-10: Experiment Execution & Data Collection

> **Bab 10 — Eksekusi Eksperimen & Pengumpulan Data**

---

## Ringkasan Materi

### Experiment Execution Pipeline

```
Design → Execution Plan → Controlled Execution → Data Collection → Data Logging → Dataset for Analysis
```

### Multiple Run = Non-Negotiable

Single run **tidak pernah cukup** untuk klaim ilmiah. Minimum 5-10 run per skenario dengan seed berbeda. Multiple run menghasilkan:
- Mean, std, confidence interval
- Distribusi hasil → uji statistik
- Variabilitas → error bar di grafik

### Execution Plan

Setiap eksperimen harus memiliki plan sebelum eksekusi:
- Daftar skenario
- Jumlah run per skenario
- Random seed per run (pre-determined!)
- Urutan eksekusi (randomisasi/counterbalancing)
- Pre-execution checklist

### Data Logging Komprehensif

Setiap run menghasilkan log terstruktur:
1. **Identitas** — Run ID, timestamp, skenario
2. **Konfigurasi** — Semua parameter, seed, code version
3. **Hasil** — Semua metrik, output detail
4. **Metadata** — Waktu eksekusi, resource usage, warning/error

Format: CSV/JSON/database — **bukan stdout yang di-copy-paste**.

### Engineering vs Research Execution

| Aspek | Engineering | Research |
|-------|-----------|---------|
| Run | Sekali (deploy) | Multiple (min 5-10, seed berbeda) |
| Logging | Error log, access log | Semua parameter, metrik, metadata |
| Anomali | Bug → fix → redeploy | Investigasi → dokumentasi → analisis |
| Urutan | Tidak penting | Bisa bias — perlu randomisasi |

### Anomali = Dokumentasi, Bukan Hapus

Run gagal/anomali tidak boleh dihapus tanpa dokumentasi. Bisa jadi:
- **Bug** → fix & re-run (dokumentasikan!)
- **Batas kemampuan metode** → DNF = temuan
- **Data yang bias** jika hanya simpan run "berhasil"

### Jebakan Kognitif

1. "Satu angka cukup" → tanpa distribusi, tidak bisa diuji
2. "Seed tidak penting" → bahkan algoritma deterministik bisa dipengaruhi library stokastik
3. "Run gagal langsung hapus" → kehilangan temuan potensial
4. "Semua run harus hari ini" → thermal throttling, fatigue

---

## Template A.10 — Execution Plan & Data Log

```
EXECUTION PLAN

| Run | Model  | Video         | Parameter            | Status    | Output             |
| --- | ------ | ------------- | -------------------- | --------- | ------------------ |
| 1   | YOLOv8 | depan_dprd    | imgsz=640, conf=0.25 | Completed | depan_dprd_run1    |
| 2   | YOLOv8 | depan_dprd    | imgsz=640, conf=0.25 | Completed | depan_dprd_run2    |
| 3   | YOLOv8 | depan_dprd    | imgsz=640, conf=0.25 | Completed | depan_dprd_run3    |
| 4   | YOLOv8 | depan_pendopo | imgsz=640, conf=0.25 | Completed | depan_pendopo_run1 |
| 5   | YOLOv8 | depan_pendopo | imgsz=640, conf=0.25 | Completed | depan_pendopo_run2 |
| 6   | YOLOv8 | depan_pendopo | imgsz=640, conf=0.25 | Completed | depan_pendopo_run3 |
| 7   | YOLOv8 | merdeka_timur | imgsz=640, conf=0.25 | Completed | merdeka_timur_run1 |
| 8   | YOLOv8 | merdeka_timur | imgsz=640, conf=0.25 | Completed | merdeka_timur_run2 |
| 9   | YOLOv8 | merdeka_timur | imgsz=640, conf=0.25 | Completed | merdeka_timur_run3 |
| 10  | YOLOv5 | depan_dprd    | imgsz=640, conf=0.25 | Completed | depan_dprd_run1    |
| 11  | YOLOv5 | depan_dprd    | imgsz=640, conf=0.25 | Completed | depan_dprd_run2    |
| 12  | YOLOv5 | depan_dprd    | imgsz=640, conf=0.25 | Completed | depan_dprd_run3    |
| 13  | YOLOv5 | depan_pendopo | imgsz=640, conf=0.25 | Completed | depan_pendopo_run1 |
| 14  | YOLOv5 | depan_pendopo | imgsz=640, conf=0.25 | Completed | depan_pendopo_run2 |
| 15  | YOLOv5 | depan_pendopo | imgsz=640, conf=0.25 | Completed | depan_pendopo_run3 |
| 16  | YOLOv5 | merdeka_timur | imgsz=640, conf=0.25 | Completed | merdeka_timur_run1 |
| 17  | YOLOv5 | merdeka_timur | imgsz=640, conf=0.25 | Completed | merdeka_timur_run2 |
| 18  | YOLOv5 | merdeka_timur | imgsz=640, conf=0.25 | Completed | merdeka_timur_run3 |


Jumlah model            : 2
Jumlah video            : 3
Run setiap video        : 3

Total eksperimen        : 18 run
```

---

## Latihan 1 — Execution Plan

Susun execution plan untuk eksperimen Anda. Tentukan skenario, jumlah run, dan seed sebelum eksekusi.

| Run | Model  | Video         | Parameter            | Status    |
| --- | ------ | ------------- | -------------------- | --------- |
| 1   | YOLOv8 | depan_dprd    | imgsz=640, conf=0.25 | Completed |
| 2   | YOLOv8 | depan_pendopo | imgsz=640, conf=0.25 | Completed |
| 3   | YOLOv8 | merdeka_timur | imgsz=640, conf=0.25 | Completed |
| 4   | YOLOv5 | depan_dprd    | imgsz=640, conf=0.25 | Completed |
| 5   | YOLOv5 | depan_pendopo | imgsz=640, conf=0.25 | Completed |
| 6   | YOLOv5 | merdeka_timur | imgsz=640, conf=0.25 | Completed |


Total model: 2 (YOLOv8 dan YOLOv5)
Jumlah video: 3
Run per video: 3
Total eksperimen: 18 run

---

## Latihan 2 — Data Log Terstruktur

Desain format data log untuk eksperimen Anda. Tentukan field apa saja yang akan dicatat.

**Identitas:**
| Field     | Contoh                         |
| --------- | ------------------------------ |
| Run ID    | run-001                        |
| Timestamp | 2026-06-26T10:15:00            |
| Model     | YOLOv8                         |
| Dataset   | Rekaman CCTV Kabupaten Kebumen |


**Konfigurasi:**
| Field                | Contoh          |
| -------------------- | --------------- |
| Model                | YOLOv8 / YOLOv5 |
| Image Size           | 640             |
| Confidence Threshold | 0.25            |
| Device               | CPU             |
| Source               | Video CCTV      |

**Hasil**
| Metrik                | Tipe    |
| --------------------- | ------- |
| Preprocess Time (ms)  | float   |
| Inference Time (ms)   | float   |
| Postprocess Time (ms) | float   |
| Total Kendaraan       | integer |
| Mobil                 | integer |
| Motor                 | integer |
| Bus                   | integer |
| Truk                  | integer |



**Format output:** [x ] CSV / [] JSON / [ ] Database / [ ] Lainnya: ____

---

## Latihan 3 — Anomaly Protocol

Rencanakan bagaimana menangani anomali. Untuk setiap jenis, tentukan langkah yang diambil.

| Jenis Anomali                    | Contoh                                                                | Tindakan                                                                                                  |
| -------------------------------- | --------------------------------------------------------------------- | --------------------------------------------------------------------------------------------------------- |
| **False Positive**               | Batu atau objek diam di tepi jalan terdeteksi sebagai mobil           | Dicatat sebagai kesalahan deteksi (false positive) dan dianalisis sebagai keterbatasan model.             |
| **False Negative**               | Kendaraan yang melintas tidak terdeteksi oleh model                   | Dicatat pada data log dan dibandingkan dengan hasil deteksi model lain.                                   |
| **Waktu inferensi tidak stabil** | Waktu inferensi meningkat karena CPU sedang menjalankan aplikasi lain | Menutup aplikasi lain, mengulangi pengujian, dan mencatat perubahan pada data log.                        |
| **Video bermasalah**             | Frame video rusak atau tidak terbaca pada bagian akhir video          | Mencatat peringatan (warning), memastikan hasil tetap tersimpan, dan mengulang pengujian jika diperlukan. |



---

## Refleksi

> Pernahkah Anda melaporkan hasil riset/tugas dari single run? Apa risikonya? Bagaimana multiple run mengubah kepercayaan terhadap hasil?

**Pengalaman sebelumnya:**
>Pada tugas atau proyek sebelumnya, hasil sering dilaporkan berdasarkan satu kali pengujian. Pendekatan tersebut berisiko menghasilkan kesimpulan yang kurang akurat karena tidak memperhitungkan variasi hasil akibat kondisi lingkungan maupun karakteristik data uji.

**Yang akan dilakukan berbeda:**
>Pada penelitian ini, model YOLOv8 dan YOLOv5 diuji menggunakan tiga video CCTV yang berbeda di Kabupaten Kebumen. Setiap video dijalankan sebanyak tiga kali dengan konfigurasi yang sama sehingga diperoleh 18 kali eksperimen. Seluruh hasil inferensi dicatat ke dalam file Excel dan CSV agar dapat dibandingkan berdasarkan waktu inferensi serta jumlah kendaraan yang berhasil dideteksi.
---

## Susunan yang Konsisten dengan WS-09

Untuk konsistensi dengan `WS-09: Implementation & Environment`, saya merapikan struktur supaya mudah diisi dan direproduksi: Ringkasan Materi, Template Eksekusi, Latihan (1–3), dan Refleksi. Perubahan inti:
- Menyamakan judul template menjadi `Template A.10` dan format checklist latihan seperti pada `WS-09`.
- Menambahkan checklist reproducibility singkat di bagian akhir.

## Checklist Reproducibility (singkat)

- [x] Semua run terdokumentasi (Run ID, model, video, konfigurasi)
- [x] Output disimpan dalam format CSV
- [x] Versi kode tercatat melalui GitHub
- [x] Anomali didokumentasikan pada data log

---

## Petunjuk Singkat Pengisian
- Execution Plan: mencatat seluruh kombinasi model, video uji, dan jumlah run yang akan dilakukan.
- Data Log: menyimpan hasil inferensi setiap run dalam format CSV agar mudah dianalisis.
- Anomaly Protocol: mendokumentasikan setiap kesalahan deteksi (false positive, false negative) maupun kendala selama proses inferensi.

---

## Contoh Ringkas (copyable)

```
Run ID          : YOLOv8-DD-01
Timestamp       : 2026-07-12T20:15:00+07:00
Model           : YOLOv8
Video           : depan_dprd.mp4
Image Size      : 640
Confidence      : 0.25
Device          : CPU
Inference Time  : 157.8 ms
Output          : Video hasil deteksi dan data jumlah kendaraan
Anomali         : False positive (batu di tepi jalan terdeteksi sebagai mobil)
Catatan         : Hasil tetap digunakan untuk analisis performa model.
```

