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

EXECUTION PLAN

| Run # | Skenario | Seed | Parameter | Status | Waktu | Output File |
|-------|----------|------|-----------|--------|-------|-------------|
| 1 | YOLOv8 | 42 | imgsz=640, epochs=50, conf=0.25 | Planned | - | yolo_run01.csv |
| 2 | YOLOv8 | 123 | imgsz=640, epochs=50, conf=0.25 | Planned | - | yolo_run02.csv |
| 3 | SSD | 42 | imgsz=640, epochs=50, conf=0.25 | Planned | - | ssd_run01.csv |
| 4 | SSD | 123 | imgsz=640, epochs=50, conf=0.25 | Planned | - | ssd_run02.csv |
| ... | ... | ... | ... | ... | ... | ... |

Jumlah runs per skenario : 20

Total runs               : 40

DATA LOG (per run):
Run ID      : run-001
Timestamp   : 2026-06-26 10:15 WIB
Skenario    : YOLOv8
Input       : Rekaman CCTV kendaraan Kabupaten Kebumen
Output      : mAP@50, Precision, Recall, FPS, hasil deteksi kendaraan
Anomali     : Tidak ada
Catatan     : Semua parameter sesuai konfigurasi awal
```

---

## Latihan 1 — Execution Plan

Susun execution plan untuk eksperimen Anda. Tentukan skenario, jumlah run, dan seed sebelum eksekusi.

| Run # | Skenario | Seed | Parameter Kunci                | Status  |
| ----- | -------- | ---- | ------------------------------ | ------- |
| 1     | YOLOv8   | 42   | imgsz=640, epoch=50, conf=0.25 | Planned |
| 2     | YOLOv8   | 123  | imgsz=640, epoch=50, conf=0.25 | Planned |
| 3     | YOLOv8   | 999  | imgsz=640, epoch=50, conf=0.25 | Planned |
| 4     | SSD      | 42   | imgsz=640, epoch=50, conf=0.25 | Planned |
| 5     | SSD      | 123  | imgsz=640, epoch=50, conf=0.25 | Planned |


Total skenario: 2 (YOLOv8 dan SSD)
Run per skenario: 20
Total run keseluruhan: 40

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
| Field                | Contoh         |
| -------------------- | -------------- |
| Seed                 | 42             |
| Code Version         | commit a3d5c9f |
| Epoch                | 50             |
| Image Size           | 640 × 640      |
| Confidence Threshold | 0.25           |


**Hasil:**
| Metrik    | Tipe Data | Range Valid |
| --------- | --------- | ----------- |
| mAP@50    | float     | 0.0–1.0     |
| Precision | float     | 0.0–1.0     |
| Recall    | float     | 0.0–1.0     |
| FPS       | float     | >0          |


**Format output:** [x ] CSV / [x ] JSON / [ ] Database / [ ] Lainnya: ____

---

## Latihan 3 — Anomaly Protocol

Rencanakan bagaimana menangani anomali. Untuk setiap jenis, tentukan langkah yang diambil.

| Jenis Anomali                 | Contoh                                                      | Tindakan                                                                                        |
| ----------------------------- | ----------------------------------------------------------- | ----------------------------------------------------------------------------------------------- |
| Run gagal (crash)             | Program berhenti saat proses inferensi                      | Dokumentasikan error, periksa konfigurasi, kemudian jalankan ulang dengan konfigurasi yang sama |
| Hasil ekstrem                 | Nilai mAP jauh lebih rendah dibanding run lain              | Periksa kualitas dataset, seed, dan parameter; ulangi eksperimen jika diperlukan                |
| Waktu eksekusi anomali        | FPS turun drastis karena CPU sedang digunakan aplikasi lain | Tutup aplikasi lain, ulangi pengujian, dan catat perubahan                                      |
| Inkonsistensi dengan run lain | Precision berbeda jauh pada seed yang sama                  | Verifikasi konfigurasi, versi library, dan dataset; lakukan re-run apabila ditemukan perbedaan  |


---

## Refleksi

> Pernahkah Anda melaporkan hasil riset/tugas dari single run? Apa risikonya? Bagaimana multiple run mengubah kepercayaan terhadap hasil?

**Pengalaman sebelumnya:**
>Pada tugas atau proyek sebelumnya, hasil sering dilaporkan berdasarkan satu kali pengujian. Pendekatan tersebut berisiko menghasilkan kesimpulan yang kurang akurat karena tidak memperhitungkan variasi hasil akibat faktor acak maupun kondisi lingkungan pengujian.

**Yang akan dilakukan berbeda:**
>Pada penelitian ini, setiap model (YOLOv8 dan SSD) akan diuji sebanyak 20 kali dengan random seed yang telah ditentukan sehingga total terdapat 40 kali pengujian. Seluruh hasil akan dicatat dalam data log terstruktur dan dianalisis menggunakan metrik yang sama agar perbandingan kedua model lebih objektif, konsisten, dan dapat direproduksi.
---

## Susunan yang Konsisten dengan WS-09

Untuk konsistensi dengan `WS-09: Implementation & Environment`, saya merapikan struktur supaya mudah diisi dan direproduksi: Ringkasan Materi, Template Eksekusi, Latihan (1–3), dan Refleksi. Perubahan inti:
- Menyamakan judul template menjadi `Template A.10` dan format checklist latihan seperti pada `WS-09`.
- Menambahkan checklist reproducibility singkat di bagian akhir.

## Checklist Reproducibility (singkat)

- [ ] Semua run terdokumentasi (Run ID, seed, config)
- [ ] Output disimpan dalam format terstruktur (CSV/JSON/DB)
- [ ] Versi kode tercatat (commit hash)
- [ ] Anomali didokumentasikan, tidak dihapus

---

## Petunjuk Singkat Pengisian

- **Execution Plan:** isi tabel dengan semua skenario dan seed sebelum mulai.
- **Data Log:** gunakan satu format konsisten; rekomendasi: CSV untuk metrik + JSON untuk metadata.
- **Anomaly Protocol:** catat penyebab, tindakan, dan apakah re-run diperlukan.

---

## Contoh Ringkas (copyable)

```
Run ID: run-2026-06-24-01
Timestamp: 2026-06-24T14:05:00+07:00
Skenario: BERT-base, DS-1
Seed: 42
Config: {"lr":2e-5, "epochs":10}
Metrics: {"accuracy":0.843, "loss":0.512}
Anomali: None
Notes: Baseline run
```

