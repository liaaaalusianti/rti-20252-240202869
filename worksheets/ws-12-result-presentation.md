# WS-12: Result Presentation & Visualization

> **Bab 12 — Penyajian Hasil & Visualisasi**

---

## Ringkasan Materi

### Data → Insight Model

```
Validated Data → Structured Presentation → Visualization → Pattern Recognition → Insight
```

Penyajian **mendahului** analisis. Tabel dan grafik membantu peneliti "melihat" data sebelum menghitung. Langsung ke uji statistik tanpa visualisasi berisiko kesimpulan yang secara teknis benar tapi kontekstual salah (Anscombe's Quartet, 1973).

### Tabel = Presisi, Grafik = Pola

Keduanya **saling melengkapi**:
- Tabel: angka presisi, self-contained (dipahami tanpa teks), sortable
- Grafik: pola visual, tren, perbandingan cepat

### Jenis Grafik Berdasarkan Tujuan

| Tujuan | Jenis Grafik |
|--------|-------------|
| Perbandingan antar-skenario | Bar chart (grouped/stacked) |
| Distribusi per-skenario | Box plot / violin plot |
| Tren temporal | Line chart |
| Korelasi dua variabel | Scatter plot |
| Proporsi (total = 100%) | Pie chart (hati-hati!) |

### Contoh Tabel Hasil yang Baik

| Model | Accuracy (%) | F1-Score (%) | Training Time (min) |
|-------|-------------|-------------|---------------------|
| BERT | 88.4 ± 1.2 | 87.1 ± 1.4 | 45.2 ± 3.1 |
| LSTM | 86.1 ± 1.8 | 84.5 ± 2.0 | 12.8 ± 1.2 |
| SVM | 82.3 ± 0.9 | 80.7 ± 1.1 | 0.3 ± 0.1 |

*N=10 per model. Mean ± std. Diurutkan berdasarkan Accuracy.*

### Visualization Bias — Yang Harus Dihindari

| Bias | Deskripsi | Dampak |
|------|----------|--------|
| Truncated axis | Y tidak dari 0 | Memperbesar perbedaan kecil |
| Inconsistent scale | Dua grafik skala beda | Perbandingan menyesatkan |
| Cherry-picked data | Hanya tampilkan yang "menang" | Selektif, tidak jujur |
| 3D effects | Efek 3D tanpa dimensi data ke-3 | Distorsi tanpa informasi |
| Missing error bar | Tidak ada variabilitas | Menyembunyikan ketidakpastian |

### Engineering vs Research Presentation

| Aspek | Engineering | Research |
|-------|-----------|---------|
| Tujuan grafik | Dashboard monitoring | Mendukung argumen ilmiah |
| Informasi wajib | KPI, threshold | Mean, std, CI, N, p-value |
| Bias handling | Less critical | Wajib dihindari (peer-review) |

---

## Template A.12 — Result Presentation Plan

```
RESULT PRESENTATION PLAN

Research Question :
Bagaimana perbandingan performa YOLOv8 dan YOLOv5 dalam mendeteksi kendaraan pada rekaman CCTV di Kabupaten Kebumen berdasarkan waktu preprocess, inference, dan postprocess?

Metrik Utama :
Preprocess Time (ms), Inference Time (ms), dan Postprocess/NMS Time (ms)

Tabel Hasil:
| Model  | Preprocess (Mean ± SD) | Inference (Mean ± SD) | Postprocess (Mean ± SD) |  n |
| ------ | ---------------------: | --------------------: | ----------------------: | -: |
| YOLOv8 |     **3.27 ± 0.63 ms** | **106.07 ± 28.08 ms** |      **1.28 ± 0.25 ms** |  9 |
| YOLOv5 |     **1.14 ± 0.28 ms** | **219.84 ± 35.50 ms** |      **1.21 ± 0.15 ms** |  9 |

Visualisasi yang Direncanakan:
| No | Jenis Grafik | Pesan Utama                                                 | Metrik                |
| -- | ------------ | ----------------------------------------------------------- | --------------------- |
| 1  | Bar Chart    | Membandingkan rata-rata waktu preprocess YOLOv8 dan YOLOv5  | Mean Preprocess Time  |
| 2  | Bar Chart    | Membandingkan rata-rata waktu inference YOLOv8 dan YOLOv5   | Mean Inference Time   |
| 3  | Bar Chart    | Membandingkan rata-rata waktu postprocess YOLOv8 dan YOLOv5 | Mean Postprocess Time |


Bias Check:
[x] Y-axis dimulai dari 0
[x] Error bar (Standar Deviasi) ditampilkan
[x] Seluruh data eksperimen ditampilkan
[x] Tidak menggunakan grafik 3D
```

---

## Latihan 1 — Tabel Hasil

Buat tabel hasil eksperimen Anda (boleh dengan data simulasi jika belum punya data riil).

| Model  | Preprocess (Mean ± SD) | Inference (Mean ± SD) | Postprocess (Mean ± SD) |  n |
| ------ | ---------------------: | --------------------: | ----------------------: | -: |
| YOLOv8 |     **3.27 ± 0.63 ms** | **106.07 ± 28.08 ms** |      **1.28 ± 0.25 ms** |  9 |
| YOLOv5 |     **1.14 ± 0.28 ms** | **219.84 ± 35.50 ms** |      **1.21 ± 0.15 ms** |  9 |


**Checklist tabel:**
- [x] Self-contained (judul jelas, satuan ada, N tercantum)
- [x] Mean ± SD digunakan
- [x] Diurutkan berdasarkan metrik utama (Inference Time)
- [x] Format tabel konsisten

---

## Latihan 2 — Rencana Visualisasi

Rencanakan 2-3 grafik untuk menyajikan data dari Latihan 1. Setiap grafik = satu pesan.

| No | Jenis Grafik | Pesan                                                                  | Data                  |
| -- | ------------ | ---------------------------------------------------------------------- | --------------------- |
| 1  | Bar Chart    | YOLOv8 memiliki waktu preprocess sedikit lebih tinggi dibanding YOLOv5 | Mean Preprocess Time  |
| 2  | Bar Chart    | YOLOv8 memiliki waktu inference jauh lebih cepat dibanding YOLOv5      | Mean Inference Time   |
| 3  | Bar Chart    | Waktu postprocess kedua model relatif sama                             | Mean Postprocess Time |

Grafik yang telah dibuat pada penelitian ini berupa grafik batang (bar chart) untuk membandingkan nilai rata-rata preprocess, inference, dan postprocess antara YOLOv8 dan YOLOv5.

---

## Latihan 3 — Bias Detection

| Pertanyaan                        | Jawaban                                                                                                                 |
| --------------------------------- | ----------------------------------------------------------------------------------------------------------------------- |
| Apakah Y-axis menyesatkan?        | Tidak. Grafik menggunakan sumbu Y yang dimulai dari nol sehingga perbedaan antar model ditampilkan secara proporsional. |
| Apakah error bar ditampilkan?     | Ya. Error bar menggunakan standar deviasi untuk menunjukkan variasi hasil dari setiap model.                            |
| Apakah semua kondisi ditampilkan? | Ya. Seluruh hasil pengujian pada tiga video CCTV dan sembilan run untuk setiap model digunakan dalam perhitungan.       |
| Apa solusinya?                    | Menggunakan skala sumbu yang konsisten, menampilkan seluruh data eksperimen, serta menambahkan error bar pada grafik.   |


**Evaluasi grafik Anda sendiri dari Latihan 2:**
- [x] Semua bias check lulus
- [ ] Ada yang perlu diperbaiki: Tidak ada
---

## Refleksi

> Mengapa tabel dan grafik keduanya diperlukan — tidak cukup salah satu saja? Pernahkah Anda membuat grafik yang (tanpa sengaja) menyesatkan?

> Tabel dan grafik memiliki fungsi yang saling melengkapi. Tabel memberikan informasi numerik secara rinci dan presisi sehingga memudahkan pembaca melihat nilai rata-rata serta standar deviasi setiap metrik. Sementara itu, grafik membantu memperlihatkan pola dan perbedaan performa antar model secara visual sehingga interpretasi hasil menjadi lebih mudah. Pada penelitian ini, grafik disusun menggunakan skala yang konsisten, dimulai dari nol, dan menampilkan seluruh hasil eksperimen sehingga dapat mengurangi potensi bias dalam penyajian data.
