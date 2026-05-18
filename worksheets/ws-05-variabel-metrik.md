# WS-05: Variabel & Metrik

> **Bab 5 — Metric, Measurement & Data**

---

## Ringkasan Materi

### Measurement Alignment Model

Setiap pengukuran yang valid harus bisa ditelusuri melalui rantai ini tanpa lompatan logis:

```
Problem → Concept → Variable → Metric → Data → Result
```

### Operationalization = Keputusan Desain

Menerjemahkan konsep abstrak menjadi variabel terukur bukan proses mekanis. "Code quality" yang diukur via SonarQube code smells membawa asumsi implisit. Setiap operasionalisasi harus didokumentasikan dan dijustifikasi.

### Empat Tipe Data (NOIR)

| Tipe | Ciri | Contoh | Operasi Valid |
|------|------|--------|---------------|
| **Nominal** | Kategori, tanpa urutan | Jenis algoritma (RF, SVM, CNN) | Modus, chi-square |
| **Ordinal** | Urutan, interval tidak sama | Skala Likert (1-5) | Median, Spearman |
| **Interval** | Jarak bermakna, tanpa nol absolut | Suhu Celsius | Mean, Pearson, t-test |
| **Ratio** | Jarak bermakna + nol absolut | Waktu eksekusi (ms) | Semua operasi |

Tipe data menentukan uji statistik yang valid. Kebanyakan metrik performa TI = ratio; persepsi pengguna = ordinal.

### Kriteria Pemilihan Metrik

- **Representative** — Mewakili konsep yang diteliti
- **Sensitive** — Cukup peka menangkap perbedaan bermakna (hindari ceiling effect)
- **Feasible** — Bisa dikumpulkan dalam batasan waktu dan biaya

### Pre-registration

Metrik harus ditentukan **sebelum** eksperimen. Memilih metrik setelah melihat data = **p-hacking**. Metrik tambahan yang ditemukan kemudian dilaporkan sebagai *exploratory*, bukan *confirmatory*.

### Primary vs Secondary Metric

- **Primary Metric** — Langsung terikat ke hipotesis, menentukan kesimpulan
- **Secondary Metric** — Pendukung, dilaporkan di samping primary; statusnya suplementer

### Research vs Engineering

| Aspek | Engineering | Research |
|-------|------------|----------|
| Pemilihan metrik | Berdasarkan kebiasaan/tool yang ada | Berdasarkan construct validity |
| Anomali | Dihapus untuk laporan bersih | Diinvestigasi — bisa jadi temuan |
| Kapan dipilih | Setelah sistem jadi (monitoring) | Sebelum eksperimen (by design) |

### Istilah Penting

- **Operationalization** — Transformasi konsep abstrak menjadi variabel terukur
- **Construct Validity** — Sejauh mana pengukuran benar-benar mengukur konsep yang dimaksud
- **Measurement Scale** — Klasifikasi data (NOIR) yang menentukan analisis valid
- **Multi-metric Evaluation** — Menggunakan beberapa metrik untuk menangkap konsep kompleks

---

## Template A.5 — Definisi Variabel, Metrik & Justifikasi

```
VARIABLE & METRIC DEFINITION

Research Question: Bagaimana kinerja sistem keamanan berbasis Artificial Intelligence menggunakan metode deteksi objek berbasis computer vision dalam meningkatkan akurasi deteksi dan waktu respon dibandingkan sistem CCTV konvensional melalui simulasi menggunakan dataset video publik, untuk mendukung transformasi smart city di Kabupaten Kebumen?

| Variabel | Tipe | Konsep | Metrik | Skala | Satuan | Cara Mengukur | Justifikasi |
|----------|------|--------|--------|-------|--------|---------------|-------------|
|Jenis sistem keamanan| IV   |Pendekatan sistem keamanan  |AI-based vs CCTV konvensional         |Nominal |- |Membandingkan dua metode sistem melalui simulasi    |Variabel utama penelitian       |
|Kinerja Sistem       | DV   |Efektivitas sistem          |Accuracy, Precision, Recall, F1-score |Ratio   |% |Dihitung dari confusion matrix hasil simulasi       |Mengukur kualitas deteksi objek |
|Waktu respon         | DV   |Kecepatan sistem            |Latency                               |Ratio   |ms|Mengukur waktu pemrosesan video selama simulasi     |Mengukur efisiensi sistem       |
| Dataset Video Publik| CV   |Konsistensi input           |Dataset sama untuk semua metode       |Nominal |- |Menggunakan dataset identik pada seluruh eksperimen |Menjaga fairness                |
Alignment Check:
  RQ → Concept → Variable → Metric → Data → Result
  [x ] Setiap langkah terdokumentasi
  [x] Tidak ada "lompatan logis"
  [x] Metrik mengukur apa yang dimaksud (construct validity)
```

---

## Latihan 1 — Operationalization Chain

Gunakan RQ dari WS-04. Definisikan variabel dan metriknya.

**RQ:** Bagaimana kinerja sistem keamanan berbasis AI dibandingkan CCTV konvensional melalui simulasi menggunakan dataset video publik untuk mendukung smart city di Kebumen?

| Variabel | Tipe | Konsep Abstrak | Metrik Konkret | Skala (NOIR) | Satuan |
|----------|------|---------------|----------------|-------------|--------|
|Jenis sistem   |IV |Pendekatan keamanan |AI vs CCTV                           |Nominal |- |
|Kinerja sistem |DV |Efektivitas         |Accuracy, Precision, Recall, F1-score|Ratio   |% |
|Waktu respon   |CV |Kecepatan           |Latency                              |Ratio   |ms|
|Dataset        |CV |Konsistensi input   |Dataset video publik yang sama       |Nominal |- |
**Apakah ada lompatan logis dalam rantai?** [ ] Ya / [x] Tidak
> Jika ya, di mana? ____________________________________

---

## Latihan 2 — Evaluasi Metrik

Evaluasi metrik DV yang dipilih di Latihan 1 menggunakan 3 kriteria.

| Kriteria | Skor (1-5) | Justifikasi |
|----------|-----------|-------------|
| Representative |5|Accuracy & F1-score mewakili performa deteksi|
| Sensitive      |4|Dapat menangkap perbedaan kecil antar metode |
| Feasible       |5|Mudah dhitung dari dataset                   |

**Apakah perlu secondary metric?** [x] Ya / [ ] Tidak
> Jika ya, apa dan mengapa? Karena selain akurasi, sistem keamanan harus cepat memberi respon.

**Contoh kasus ceiling effect untuk metrik ini:**
> Jika kedua sistem sama-sama memiliki accuracy >98%, accuracy saja tidak cukup membedakan performa; perlu F1-score dan latency.

---

## Latihan 3 — Data Quality Check

Bayangkan data yang akan dikumpulkan dari eksperimen. Evaluasi 4 dimensi kualitas data.

| Dimensi | Pertanyaan | Jawaban | Strategi Mitigasi |
|---------|-----------|---------|------------------|
| Completeness       |*Apakah semua data point terkumpul?*        |ya     |cek semua video diproses      |
| Consistency        |*Apakah ada kontradiksi internal?*          |mungkin|standarisasi preprocessing    |
| Validity           |*Apakah benar-benar mengukur yang dimaksud?*|ya     |gunakan metrik standar        |
| Representativeness |*Apakah sampel mewakili populasi target?*   |cukup  |gunakan dataset publik beragam|

---

## Refleksi

> Mengapa memilih metrik setelah melihat data dianggap p-hacking? Apa bedanya dengan eksplorasi data yang sah?

**Jawaban:**
> Karena peneliti bisa memilih hanya metrik yang menguntungkan hasil penelitiannya sehingga menghasilkan bias dan menurunkan validitas penelitian. Berbeda dengan eksplorasi data yang sah, di mana analisis tambahan dilakukan setelah eksperimen dan dilaporkan sebagai temuan eksploratif, bukan untuk membuktikan hipotesis utama.