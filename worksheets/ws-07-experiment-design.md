# WS-07: Experimental Design & Validity

> **Bab 7 — Experimental Design & Validity**

---

## Ringkasan Materi

### Correlation ≠ Causality

Kausalitas membutuhkan 3 syarat:
1. **Covariance** — X dan Y bergerak bersama
2. **Temporal precedence** — X berubah sebelum Y
3. **Elimination of alternatives** — Tidak ada faktor lain yang menjelaskan Y

Controlled experiment adalah satu-satunya metode yang bisa membuktikan kausalitas.

### Empat Jenis Validitas

| Jenis | Pertanyaan | Ancaman Umum |
|-------|-----------|-------------|
| **Internal** | Apakah hubungan IV→DV nyata? | Confounding variable, selection bias |
| **External** | Apakah bisa digeneralisasi? | Dataset terlalu spesifik |
| **Construct** | Apakah mengukur konsep yang benar? | Metrik tidak sesuai |
| **Conclusion** | Apakah kesimpulan statistik valid? | Sample size kecil, uji salah |

Internal dan external validity sering berkonflik: semakin terkontrol (internal kuat) → semakin artificial (external lemah).

### Tiga Tipe Eksperimen dalam Riset TI

| Tipe | Deskripsi | Kapan Digunakan |
|------|----------|----------------|
| **Comparison Study** | Metode A vs B pada kondisi identik | Membandingkan pendekatan berbeda |
| **Ablation Study** | Full system → lepas komponen satu per satu | Mengukur kontribusi tiap komponen |
| **Parameter Study** | Variasikan satu parameter, amati dampak | Uji sensitifitas/robustness |

### Fairness dalam Perbandingan

Perbandingan yang adil = **kondisi identik** untuk semua metode: dataset sama, preprocessing sama, tuning effort sebanding, environment sama, metrik sama.

Contoh tidak adil: Transformer (30 fitur tambahan + Bayesian optimization) vs RF (default params) → hasilnya misleading.

### Threats to Validity = Diidentifikasi Sebelum Eksperimen

Ancaman validitas harus diidentifikasi **sebelum** eksperimen dan mitigasinya dirancang sebagai bagian dari desain — bukan ditulis sebagai boilerplate setelah selesai.

### Research vs Engineering

| Aspek | Engineering | Research |
|-------|------------|----------|
| Tujuan testing | Memastikan sistem memenuhi requirement | Membuktikan hubungan kausal antar variabel |
| Baseline | Versi sebelumnya (last release) | Metode tervalidasi dari literatur |
| Kegagalan | Bug → fix → release | H₀ tidak ditolak → tetap kontribusi ilmiah |
| Sukses | 100% test pass | Evidence valid — mendukung atau menolak hipotesis |

### Istilah Penting

- **Causality** — Hubungan sebab-akibat (covariance + temporal + elimination)
- **Controlled Experiment** — Ubah satu variabel, kontrol sisanya, amati efek
- **Fairness** — Semua metode diuji pada kondisi yang benar-benar identik
- **Threats to Validity** — Faktor yang bisa melemahkan kesimpulan jika tidak dimitigasi
- **Conclusion Validity** — Validitas statistik: power, sample size, uji yang tepat

---

## Template A.7 — Desain Eksperimen Lengkap

```
EXPERIMENT DESIGN

Research Question : Bagaimana kinerja sistem keamanan berbasis Artificial Intelligence menggunakan metode deteksi objek berbasis computer vision dalam meningkatkan akurasi deteksi dan waktu respon dibandingkan sistem CCTV konvensional melalui simulasi menggunakan dataset video publik untuk mendukung transformasi smart city di Kabupaten Kebumen?
Hypothesis        : Sistem keamanan berbasis Artificial Intelligence memiliki performa lebih baik dibandingkan sistem CCTV konvensional dalam hal akurasi deteksi dan waktu respon.
Tipe Eksperimen   : [x] Comparison  [ ] Ablation  [ ] Parameter

Kondisi Eksperimen:
| Kondisi | Deskripsi | IV Value | CV Settings |
|---------|-----------|----------|-------------|
| Control  |Sistem baseline |CCTV konvensional          |dataset sama, preprocessing sama, seed 42|
| Treatment|Sistem usulan   |AI berbasis computer vision|dataset sama, preprocessing sama, seed 42|

Fairness Checklist:
  [x] Dataset identik untuk semua kondisi
  [x] Preprocessing setara
  [x] Tuning effort setara
  [x] Environment identik
  [x] Metrik evaluasi sama

Threat Analysis:
| Threat Type | Ancaman Spesifik | Mitigasi |
|-------------|-----------------|----------|
| Internal    |Data leakage antara train-test|gunakan train-test split yang benar         |
| External    |Dataset terlalu spesifik      |gunakan dataset publik yang beragam         |
| Construct   |Accuracy saja tidak cukup     |tambah Precision, Recall, F1, Latency       |
| Conclusion  |Sampel terlalu kecil          |gunakan cukup banyak video dan repeated runs|

Statistical Plan:
  Uji statistik   : Independent t-test
  Justifikasi      : Karena membandingkan dua kelompok independen (AI vs CCTV)
  Alpha            : 0.05
  Effect size min  : 0.2 (small effect)
```

---

## Latihan 1 — Desain Eksperimen

Susun desain eksperimen berdasarkan RQ, variabel, dan sistem dari WS-04 sampai WS-06.

**RQ:** 
**Tipe eksperimen:** [ ] Comparison / [ ] Ablation / [ ] Parameter

| Kondisi | Deskripsi | IV Value | CV Settings |
|---------|-----------|----------|-------------|
| Control   |baseline dari sistem tradisional|CCTV konvensional|dataset sama, seed 42|
| Treatment |sistem usulan                   |AI detection     |dataset sama, seed 42|

---

## Latihan 2 — Fairness Checklist

Evaluasi apakah desain eksperimen di Latihan 1 sudah fair.

| Kriteria | Status | Detail |
|----------|--------|--------|
| Dataset identik      |✅|menggunakan dataset video publik yang sama |
| Preprocessing setara |✅|resize dan cleaning sama                   |
| Tuning effort setara |✅|parameter diuji secara adil                |
| Environment identik  |✅|hardware/software sama                     |
| Metrik evaluasi sama |✅|accuracy, precision, recall, F1, latency   |

**Ada yang tidak fair?** [ ] Ya / [x] Tidak
> Jika ya, bagaimana cara memperbaikinya? ________________

---

## Latihan 3 — Threat Analysis

Identifikasi ancaman validitas untuk desain eksperimen ini.

| Threat Type | Ancaman Spesifik | Mitigasi |
|-------------|-----------------|----------|
| Internal   |data leakage                           |validasi split               |
| External   |dataset tidak mewakili kondisi Kebumen |gunakan dataset yang beragam |
| Construct  |metrik kurang representatif            |multi-metric evaluation      |
| Conclusion |terlalu sedikit sampel                 |tambah jumlah eksperimen     |

**Ancaman mana yang paling sulit dimitigasi?** External validity
**Mengapa?**
> Karena penelitian menggunakan dataset publik sehingga kondisi nyata Kabupaten Kebumen mungkin tidak sepenuhnya terwakili

---

## Refleksi

> Sebuah paper melaporkan "metode kami mengalahkan semua baseline." Apa 3 pertanyaan pertama yang harus diajukan untuk mengevaluasi klaim ini?

**Jawaban:**
1. Apakah semua baseline diuji pada kondisi yang sama?
2. Apakah metrik evaluasi yang digunakan adil dan relevan?
3. Apakah hasilnya signifikan secara statistik?
