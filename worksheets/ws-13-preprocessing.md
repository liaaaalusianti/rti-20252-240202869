# WS-13: Data Preprocessing

> **Bab 13 — Preprocessing & Persiapan Data untuk Analisis**

---

## Ringkasan Materi

### Data Refinement Pipeline

```
Raw Data → Cleaning → Transformation → Normalization → Processed Data → Analysis Ready
```

Setiap tahap memiliki tujuan berbeda. **Preprocessing bukan langkah teknis biasa** — setiap keputusan preprocessing adalah keputusan riset yang bisa mengubah kesimpulan.

### Empat Prinsip Preprocessing

| Prinsip | Deskripsi |
|---------|----------|
| **Consistency** | Metode sama untuk data yang sama |
| **Transparency** | Setiap langkah terdokumentasi |
| **Reproducibility** | Orang lain bisa mengulang dengan hasil sama |
| **Minimal Distortion** | Ubah sesedikit mungkin; jika normalisasi tidak perlu, jangan lakukan |

### Cleaning Triad

| Masalah | Strategi | Risiko |
|---------|---------|--------|
| **Missing values** | | |
| — Listwise deletion | Missing < 5%, random | Data loss |
| — Mean/median imputation | Sedikit missing, dist. normal | Mengurangi variabilitas |
| — Model-based imputation | Banyak missing, pola sistematis | Introduces dependency |
| — Flag & separate | Missing karena alasan substantif | Kompleksitas analisis |
| **Duplikat** | Identifikasi → verifikasi → hapus | False positive (data mirip ≠ duplikat) |
| **Error format** | Standardisasi tipe, encoding | Kehilangan informasi saat konversi |

### Normalisasi — Kapan & Metode Mana

| Metode | Formula | Output | Sensitif Outlier? |
|--------|---------|--------|-------------------|
| Min-max | (x-min)/(max-min) | [0, 1] | Ya |
| Z-score | (x-mean)/std | Unbounded | Lebih robust |
| Robust scaling | (x-median)/IQR | Unbounded | Paling robust |

**Kunci:** Parameter normalisasi harus dihitung dari **training set saja** — bukan seluruh data. Pelanggaran = **data leakage**.

### Data Leakage Prevention

Data leakage terjadi ketika informasi dari test set "bocor" ke preprocessing:
- Normalisasi parameter dari seluruh dataset ← **SALAH**
- Cross-validation dilakukan sebelum split ← **SALAH**
- Feature selection menggunakan label test set ← **SALAH**

### Jebakan Kognitif

1. "Preprocessing cuma teknis — tidak perlu detail" → bisa ubah kesimpulan
2. "Lebih banyak preprocessing = lebih bersih = lebih baik" → over-processing distorsi data
3. "Normalisasi selalu diperlukan" → belum tentu, tergantung metode analisis
4. "Imputation sama untuk semua situasi" → strategi harus sesuai konteks

---

## A.13 — Preprocessing Documentation Log

PREPROCESSING LOG

Dataset           : Rekaman CCTV kendaraan Kabupaten Kebumen
Jumlah data awal  : 3 video CCTV

Cleaning:
| Masalah      | Jumlah Kasus | Penanganan                                    | Justifikasi                                |
| ------------ | -----------: | --------------------------------------------- | ------------------------------------------ |
| Missing data |            0 | Tidak ada tindakan                            | Seluruh video dapat diproses               |
| Duplikat     |            0 | Tidak ada tindakan                            | Setiap video merupakan lokasi yang berbeda |
| Error format |            0 | Seluruh video diseragamkan menjadi format MP4 | Menjaga konsistensi proses deteksi         |


Transformation:
| Transformasi         | Variabel      | Detail           | Alasan                                           |
| -------------------- | ------------- | ---------------- | ------------------------------------------------ |
| Resize frame         | Image Size    | 640 × 640 piksel | Menyamakan ukuran input pada kedua model         |
| Confidence Threshold | Deteksi objek | 0,25             | Menyamakan parameter pengujian YOLOv8 dan YOLOv5 |


Normalization:
Metode    : Tidak dilakukan
Alasan    : Penelitian menggunakan model YOLO pretrained untuk inferensi sehingga tidak memerlukan normalisasi tambahan pada data hasil pengujian.
Parameter : Tidak ada

Leakage Check:
  [x] Tidak ada data training dan testing
  [x] Tidak ada informasi yang bocor antar pengujian
  [x] Seluruh eksperimen menggunakan konfigurasi yang sama

Jumlah data akhir : 3 video CCTV
Script tersedia   : [x] Ya → YOLOv8 dan YOLOv5 Python Script


---

## Latihan 1 — Cleaning Plan

| Masalah      | Jumlah Kasus | Penanganan                              | Justifikasi                              |
| ------------ | -----------: | --------------------------------------- | ---------------------------------------- |
| Missing data |            0 | Tidak ada                               | Seluruh video dapat diproses             |
| Duplikat     |            0 | Tidak ada                               | Setiap video berasal dari lokasi berbeda |
| Error format |            0 | Format MP4 digunakan pada seluruh video | Konsisten untuk seluruh eksperimen       |


**Jumlah data sebelum cleaning:** 3 video
**Jumlah data setelah cleaning:** 3 video
**Persentase data yang hilang/berubah:** 0%

---

## Latihan 2 — Normalisasi Decision

Tentukan apakah data Anda perlu normalisasi, dan jika ya, metode apa yang tepat.

| Variabel         | Range Asli    | Distribusi | Outlier | Metode          | Alasan                             |
| ---------------- | ------------- | ---------- | ------- | --------------- | ---------------------------------- |
| Preprocess Time  | 0,8–4,6 ms    | Normal     | Tidak   | Tidak dilakukan | Digunakan sebagai hasil pengukuran |
| Inference Time   | 77,1–313,6 ms | Normal     | Tidak   | Tidak dilakukan | Digunakan langsung untuk analisis  |
| Postprocess Time | 1,0–1,9 ms    | Normal     | Tidak   | Tidak dilakukan | Tidak memerlukan normalisasi       |

**Apakah normalisasi diperlukan?** [ ] Ya / [x] Tidak
**Justifikasi:**
> Penelitian ini membandingkan performa YOLOv8 dan YOLOv5 berdasarkan waktu preprocess, inference, dan postprocess. Nilai yang diperoleh merupakan hasil pengukuran langsung dari proses inferensi sehingga tidak memerlukan normalisasi tambahan. Analisis dilakukan menggunakan nilai asli agar perbandingan performa kedua model tetap merepresentasikan kondisi sebenarnya.

**Leakage check:**
- [✓]Tidak terdapat proses training dan testing.
- [✓]Tidak dilakukan normalisasi sehingga tidak terjadi data leakage.
---

## Latihan 3 — Preprocessing Report

Buat ringkasan preprocessing lengkap — dokumentasi yang cukup bagi orang lain untuk mereplikasi.

```
PREPROCESSING SUMMARY

1. Dataset:
   Rekaman CCTV kendaraan Kabupaten Kebumen
   (depan_dprd.mp4, depan_pendopo.mp4, merdeka_timur.mp4)

2. Data awal:
   3 video CCTV

3. Cleaning:
   - Missing values : 0 kasus
   - Duplikat       : 0 kasus
   - Error format   : 0 kasus

4. Transformation:
   - Seluruh video diproses menggunakan image size 640 × 640 piksel
   - Confidence threshold ditetapkan sebesar 0,25
   - Device yang digunakan adalah CPU

5. Normalisasi:
   Tidak dilakukan karena penelitian hanya membandingkan performa inferensi kedua model menggunakan data hasil pengukuran asli.

6. Data akhir:
   3 video CCTV yang menghasilkan total 18 run pengujian.

7. Leakage check:
   ☑ Lulus

```

---

## Refleksi

> Apakah Anda pernah melakukan normalisasi "karena biasa dilakukan" tanpa mempertimbangkan apakah benar-benar diperlukan? Apa risiko over-preprocessing?

> Pada penelitian ini, normalisasi tidak dilakukan hanya karena merupakan langkah yang umum digunakan. Keputusan preprocessing disesuaikan dengan tujuan penelitian, yaitu membandingkan waktu preprocess, inference, dan postprocess antara YOLOv8 dan YOLOv5. Melakukan normalisasi tanpa kebutuhan yang jelas dapat mengubah karakteristik data asli sehingga hasil analisis menjadi kurang merepresentasikan performa sebenarnya. Oleh karena itu, preprocessing dilakukan seminimal mungkin dengan tetap menjaga konsistensi dan reproduktibilitas eksperimen.