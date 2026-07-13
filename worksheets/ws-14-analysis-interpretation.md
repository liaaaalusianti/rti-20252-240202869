# WS-14: Analysis, Interpretation & Failure Analysis

> **Bab 14 — Analisis Data, Interpretasi & Failure Analysis**

---

## Ringkasan Materi

### Data → Knowledge Model

```
Data → Analysis → Interpretation → Explanation → Knowledge
```

Tiga level yang berbeda:
- **Analysis** — "Apa yang terjadi?" (deskriptif + inferensial)
- **Interpretation** — "Apa artinya?" (konteks RQ + literatur)
- **Failure Analysis** — "Mengapa tidak berhasil?" (boundary conditions)

### Beyond p-value

**Statistical significance ≠ practical significance.** Selalu laporkan:
1. p-value (signifikansi statistik)
2. Effect size (besarnya efek)
3. Confidence interval (rentang ketidakpastian)

| Effect Size (Cohen's d) | Interpretasi |
|-------------------------|-------------|
| < 0.2 | Small |
| 0.2 – 0.8 | Medium |
| > 0.8 | Large |

### Pemilihan Uji Statistik

| Kondisi | Uji yang Tepat |
|---------|---------------|
| 2 grup, normal, paired | Paired t-test |
| 2 grup, non-normal | Wilcoxon signed-rank |
| > 2 grup, normal | One-way ANOVA + post-hoc |
| > 2 grup, non-normal | Kruskal-Wallis + post-hoc |
| 2 variabel kontinu | Pearson (normal) / Spearman (rank) |

### Failure Analysis as Contribution

Hipotesis yang ditolak adalah **temuan yang berharga**:

| Dataset | New (F1) | Baseline (F1) | p-value | Cohen's d |
|---------|---------|--------------|---------|-----------|
| DS-1 (small, clean) | 94.2±1.1 | 89.3±1.5 | <0.001 | **3.7** |
| DS-4 (medium, noisy) | 78.3±3.2 | 82.1±2.8 | 0.008 | **-1.3** |
| DS-5 (large, noisy) | 71.6±4.1 | 80.5±3.0 | <0.001 | **-2.5** |

**Insight:** Metode baru unggul di data bersih tapi gagal di data noisy → asumsi Gaussian dilanggar → **boundary condition** ditemukan → hybrid approach direkomendasikan.

**Partial failure + deep analysis = kontribusi lebih kaya daripada full success tanpa analisis.**

### Limitation Types

| Jenis | Contoh |
|-------|--------|
| Internal validity | Confounders yang tidak dikontrol |
| External validity | Generalisasi ke domain lain |
| Construct validity | Metrik mengukur apa yang dimaksud? |
| Statistical limitation | Sample size, asumsi distribusi |

### Jebakan Kognitif

1. "Signifikan statistik = penting secara praktis" → cek effect size
2. "Hipotesis tidak didukung → cari sudut baru" → p-hacking
3. "Kegagalan tidak perlu dilaporkan detail" → missed insight
4. "Limitasi cukup disebutkan, tidak perlu dianalisis" → kedalaman hilang

---

## Template A.14 — Analysis & Interpretation Report

ANALYSIS & INTERPRETATION

1. Statistik Deskriptif

| Model  | Mean Inference (ms) | Std (ms) | Median (ms) | Min (ms) | Max (ms) | n |
|--------|--------------------:|---------:|------------:|---------:|---------:|--:|
| YOLOv8 | 106,07 | 30,73 | 101,20 | 77,10 | 157,80 | 9 |
| YOLOv5 | 219,84 | 35,07 | 208,20 | 202,00 | 313,60 | 9 |

2. Uji Hipotesis

Uji yang digunakan : Belum dilakukan (analisis deskriptif)

Justifikasi :
Penelitian ini berfokus pada analisis deskriptif terhadap waktu preprocess, inference, dan postprocess menggunakan rata-rata dan standar deviasi. Pengujian inferensial belum dilakukan karena penelitian bertujuan membandingkan performa kedua model berdasarkan hasil eksperimen.

Hasil :
p-value : Belum dihitung
Effect size : Belum dihitung
Confidence Interval : Belum dihitung

3. Keputusan

☑ YOLOv8 memiliki rata-rata waktu inference lebih rendah dibandingkan YOLOv5.

4. Interpretasi

Hubungan ke Research Question :
Berdasarkan hasil eksperimen, YOLOv8 menunjukkan performa inferensi yang lebih cepat dibandingkan YOLOv5 pada ketiga video CCTV Kabupaten Kebumen.

Practical significance :
Kecepatan inferensi yang lebih rendah membuat YOLOv8 lebih sesuai diterapkan pada sistem pemantauan lalu lintas secara real-time.

Perbandingan literatur :
Hasil penelitian sejalan dengan beberapa penelitian terdahulu yang melaporkan bahwa YOLOv8 memiliki efisiensi inferensi yang lebih baik dibandingkan YOLOv5 pada tugas deteksi objek.

5. Limitation

| Jenis | Ancaman | Dampak | Mitigasi |
|-------|----------|---------|----------|
| Internal Validity | Dataset hanya terdiri dari tiga video CCTV | Hasil mungkin belum mewakili seluruh kondisi lalu lintas | Menambah jumlah video pada penelitian berikutnya |
| External Validity | Pengujian hanya menggunakan CPU | Hasil dapat berbeda jika menggunakan GPU | Pengujian ulang pada perangkat berbeda |
| Statistical | Jumlah eksperimen hanya 18 run | Analisis statistik inferensial belum dilakukan | Menambah jumlah run pada penelitian selanjutnya |

6. Failure Analysis

Selama pengujian ditemukan beberapa false positive, yaitu objek statis seperti batu terdeteksi sebagai kendaraan. Selain itu, YOLOv5 memiliki waktu inferensi yang relatif lebih lama dibandingkan YOLOv8.

Penyebab potensial :
- Kemiripan bentuk objek dengan kendaraan.
- Sudut pengambilan CCTV.
- Kondisi pencahayaan dan kualitas video.

Boundary condition :
Model masih dapat mengalami kesalahan ketika objek memiliki bentuk menyerupai kendaraan atau ketika kualitas rekaman CCTV menurun.

Insight :
Walaupun masih ditemukan false positive, YOLOv8 tetap memberikan waktu inferensi yang lebih cepat sehingga lebih sesuai digunakan untuk sistem pemantauan lalu lintas berbasis CCTV.


---

## Latihan 1 — Pemilihan Uji Statistik

Tentukan uji statistik yang tepat untuk eksperimen Anda.

| Pertanyaan                        | Jawaban                                                                                          |
| --------------------------------- | ------------------------------------------------------------------------------------------------ |
| Berapa grup yang dibandingkan?    | 2 (YOLOv8 dan YOLOv5)                                                                            |
| Apakah data berpasangan (paired)? | Ya, kedua model diuji pada video dan skenario yang sama                                          |
| Apakah distribusi normal?         | Belum dilakukan uji normalitas                                                                   |
| **Uji yang dipilih**              | Paired t-test (jika data normal) atau Wilcoxon Signed-Rank Test (jika data tidak normal)         |
| **Justifikasi**                   | Kedua model diuji menggunakan dataset dan skenario yang sama sehingga data bersifat berpasangan. |

**Effect size yang akan dilaporkan:** [✓] Cohen's d / [ ] Eta-squared / [ ] Lainnya: ____

---

## Latihan 2 — Interpretasi Hasil

| Aspek                         | Interpretasi                                                                                                                                                              |
| ----------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| Signifikansi statistik        | Belum dihitung karena penelitian masih menggunakan analisis deskriptif.                                                                                                   |
| Effect size                   | Belum dihitung.                                                                                                                                                           |
| Practical significance        | YOLOv8 memiliki waktu inferensi lebih rendah sehingga lebih efisien untuk aplikasi pemantauan lalu lintas secara real-time.                                               |
| Hubungan ke Research Question | Hasil menunjukkan bahwa YOLOv8 memiliki performa inferensi lebih cepat dibandingkan YOLOv5 pada rekaman CCTV Kabupaten Kebumen.                                           |
| Perbandingan literatur        | Temuan ini konsisten dengan penelitian sebelumnya yang menyatakan bahwa YOLOv8 memiliki efisiensi inferensi yang lebih baik dibandingkan YOLOv5 pada tugas deteksi objek. |

---

## Latihan 3 — Failure Analysis

Latih kemampuan failure analysis: hipotesis TIDAK didukung. Apa yang bisa dipelajari?

| Pertanyaan                        | Jawaban                                                                                                                                   |
| --------------------------------- | ----------------------------------------------------------------------------------------------------------------------------------------- |
| Apakah ini gagal?                 | Tidak. Kedua model berhasil mendeteksi kendaraan, meskipun masih ditemukan beberapa kesalahan deteksi.                                    |
| Kemungkinan penyebab?             | False positive terjadi karena objek statis memiliki bentuk yang menyerupai kendaraan dan dipengaruhi oleh kualitas video CCTV.            |
| Boundary condition?               | Model dapat mengalami penurunan performa pada kondisi pencahayaan rendah atau ketika terdapat objek dengan bentuk yang mirip kendaraan.   |
| Insight yang bisa diambil?        | YOLOv8 tetap menjadi model yang lebih efisien dari sisi waktu inferensi meskipun masih memiliki beberapa false positive.                  |
| Apakah layak dilaporkan? Mengapa? | Ya. False positive merupakan bagian dari evaluasi performa model dan menjadi informasi penting untuk pengembangan penelitian selanjutnya. |


**Limitation terkait:**
| Jenis             | Ancaman                  | Dampak                                 |
| ----------------- | ------------------------ | -------------------------------------- |
| Internal Validity | Jumlah video hanya tiga  | Generalisasi hasil masih terbatas      |
| Statistical       | Jumlah run sebanyak 18   | Analisis inferensial belum dilakukan   |
| External Validity | Pengujian hanya pada CPU | Hasil dapat berbeda pada perangkat GPU |


---

## Refleksi

> Apakah "failure" dalam riset benar-benar gagal, atau justru kontribusi? Bagaimana failure analysis mengubah cara Anda melihat hasil negatif?

> Penelitian yang tidak sepenuhnya sesuai dengan hipotesis bukan berarti gagal. Hasil negatif maupun kesalahan deteksi tetap memberikan informasi penting mengenai batas kemampuan model pada kondisi tertentu. Melalui failure analysis, peneliti dapat mengetahui penyebab terjadinya kesalahan, mengidentifikasi kondisi yang memengaruhi performa model, serta memberikan rekomendasi untuk penelitian selanjutnya agar hasil yang diperoleh semakin baik.
