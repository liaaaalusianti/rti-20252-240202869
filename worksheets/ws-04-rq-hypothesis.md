# WS-04: Research Question & Hypothesis

> **Bab 4 — Research Question, Contribution & Hypothesis**

---

## Ringkasan Materi

### RQ Bukan Pertanyaan Biasa

Research Question yang baik secara implisit mengandung cetak biru eksperimen: subjek, baseline, metrik, domain, dataset.

| Kualitas | Contoh |
|----------|--------|
| **Buruk** | "Bagaimana pengaruh deep learning terhadap deteksi malware?" |
| **Baik** | "Apakah CNN menghasilkan F1-Score lebih tinggi dari RF pada CIC-MalMem-2022?" |

Perbedaan: RQ yang baik menyebutkan **metode spesifik**, **metrik terukur**, **baseline**, dan **dataset**.

### Tiga Jenis RQ

| Jenis | Pola | Kebutuhan |
|-------|------|-----------|
| **Comparison** | A vs B → mana lebih baik? | ≥ 2 metode, metrik sama |
| **Improvement** | A' vs A → modifikasi lebih baik? | Pre/post, bukti perbaikan |
| **Exploratory** | Faktor X₁...Xₙ → pengaruh terhadap Y? | Multi-variabel, korelasi/regresi |

### Contribution Statement

Tiga jenis kontribusi: **Improvement** (metode terbukti lebih baik), **Comparison** (perbandingan sistematis yang belum ada), **Novel Approach** (pendekatan baru). Kontribusi harus terhubung langsung dengan gap — kontribusi tanpa gap = klaim tanpa justifikasi.

### Hypothesis H₀ / H₁

- **H₀** (Null) = Tidak ada perbedaan signifikan — asumsi default, harus dibuktikan salah
- **H₁** (Alternative) = Ada perbedaan signifikan — diterima hanya jika H₀ ditolak
- Harus **falsifiable**, mengandung **metrik terukur**, dirumuskan **SEBELUM eksperimen**

### Rantai Operasionalisasi

```
RQ → Variable → Metric → Data → Analysis
```

Jika rantai ini tidak lengkap, RQ belum mature. Bi-directional: RQ yang tidak bisa jadi hipotesis testable harus direvisi mundur.

### Research vs Engineering

| Aspek | Engineering | Research |
|-------|------------|----------|
| Tujuan pertanyaan | Apa yang harus dibangun? | Apa yang harus dibuktikan? |
| Bentuk jawaban | Sistem yang berfungsi | Bukti empiris terukur |
| Sukses diukur oleh | User satisfaction, uptime | Signifikansi statistik, effect size |
| Jika gagal | Debug dan perbaiki | Laporkan, analisis mengapa |

### Istilah Penting

- **Research Question (RQ)** — Pertanyaan spesifik: variabel terukur + metrik + konteks
- **Contribution Statement** — Apa yang diketahui setelah riset selesai yang sebelumnya belum ada
- **H₀ / H₁** — Null vs Alternative Hypothesis
- **Falsifiability** — Kondisi hipotesis ditolak harus bisa didefinisikan sebelum eksperimen
- **Operationalization** — Proses mewujudkan konsep abstrak menjadi variabel terukur

---

## Template A.4 — RQ-Contribution-Hypothesis

```
RQ-CONTRIBUTION-HYPOTHESIS

Gap Statement  : Sebagian besar penelitian terkait penerapan Artificial Intelligence dalam sistem keamanan perkotaan masih berfokus pada kota besar dan menggunakan pendekatan konseptual tanpa implementasi sistem nyata, sementara penerapan pada daerah berkembang seperti Kabupaten Kebumen masih minim dikaji.

Research Question:
  Tipe         : [x ] Comparison  [ ] Improvement  [ ] Exploratory
  Formulasi    : Bagaimana kinerja sistem keamanan berbasis Artificial Intelligence menggunakan metode deteksi objek berbasis computer vision dalam meningkatkan akurasi deteksi dan waktu respon dibandingkan sistem CCTV konvensional untuk mendukung transformasi smart city di Kabupaten Kebumen menggunakan dataset video pengawasan publik?
  Variabel IV  : Jenis sistem keamanan (AI berbasis computer vision vs CCTV konvensional)
  Variabel DV  : Kinerja sistem keamanan
  Metrik       : Accuracy
                 Precision
                 Recall
                 F1-score
                 Latency
  Dataset      : Dataset video pengawasan publik
  Baseline     : Sistem CCTV konvensional tanpa AI

Quality Check RQ:
  [x] Variabel spesifik
  [x] Metrik jelas
  [x] Baseline ada
  [x] Konteks disebutkan
  [x] Memerlukan eksperimen (bukan hanya survei literatur)

Contribution Statement:
  Apa yang baru diketahui : Penelitian ini memberikan bukti empiris mengenai efektivitas sistem keamanan berbasis Artificial Intelligence dibandingkan sistem CCTV konvensional dalam mendukung pengembangan smart city pada daerah berkembang seperti Kabupaten Kebumen.
  Jenis kontribusi        : [ ] Improvement  [x] Comparison  [ ] Novel approach
  Gap yang diisi          : Method Gap + Context Gap
Hypothesis Pair:
  H₀ : Tidak terdapat perbedaan signifikan pada akurasi deteksi dan waktu respon antara sistem keamanan berbasis Artificial Intelligence dan sistem CCTV konvensional dalam konteks smart city di Kabupaten Kebumen.
  H₁ : Terdapat perbedaan signifikan pada akurasi deteksi dan waktu respon, di mana sistem keamanan berbasis Artificial Intelligence memiliki performa lebih baik dibandingkan sistem CCTV konvensional dalam konteks smart city di Kabupaten Kebumen.
  Threshold              : p-value < 0.05
  Justifikasi threshold  : Nilai signifikansi 0.05 merupakan standar umum dalam penelitian kuantitatif untuk menentukan apakah hasil eksperimen signifikan secara statistik.
```

---

## Latihan 1 — Dari Gap ke RQ

Gunakan gap yang ditemukan di WS-03. Transformasikan menjadi Research Question.

**Gap dari WS-03:** Kurangnya implementasi sistem keamanan berbasis AI pada daerah berkembang serta minimnya evaluasi performa secara empiris.

**RQ versi pertama (tulis bebas):**
> Apakah sistem keamanan berbasis AI lebih baik daripada CCTV biasa untuk mendukung smart city di Kebumen?

**Evaluasi RQ:**

| Komponen | Ada? | Isi |
|----------|------|-----|
| Metode spesifik | ya |Computer Vision |
| Metrik terukur |ya |Accuracy, Precision, Recall, F1, Latency |
| Baseline |ya |CCTV konvensional |
| Dataset/konteks |ya |Dataset video pengawasan publik, Kebumen |

**Tipe RQ:** [x] Comparison / [ ] Improvement / [ ] Exploratory

**RQ versi revisi (setelah evaluasi):**
> Bagaimana kinerja sistem keamanan berbasis Artificial Intelligence menggunakan metode deteksi objek berbasis computer vision dalam meningkatkan akurasi deteksi dan waktu respon dibandingkan sistem CCTV konvensional untuk mendukung transformasi smart city di Kabupaten Kebumen?

---

## Latihan 2 — Hypothesis Pair

Rumuskan pasangan hipotesis dari RQ di Latihan 1.

| Komponen | Isi |
|----------|-----|
| H₀ |Tidak ada perbedaan signifikan antara AI dan CCTV|
| H₁ |Ada perbedaan signifikan; AI lebih baik |
| Metrik |Accuracy, Precision, Recall, F1, Latency |
| Threshold |p < 0.05 |
| Justifikasi threshold |standar penelitian kuantitatif |

**Apakah hipotesis ini falsifiable?** [x] Ya / [ ] Tidak
> Bagaimana cara membuktikannya salah? Jika hasil eksperimen menunjukkan p-value > 0.05 atau performa AI tidak lebih baik dari baseline.

---

## Latihan 3 — Rantai Operasionalisasi

Lengkapi rantai dari RQ hingga metode analisis.

| Tahap | Isi |
|-------|-----|
| RQ |Apakah AI lebih baik dari CCTV untuk smart city di Kebumen? |
| Variable (IV) |Jenis sistem keamanan|
| Variable (DV) |Kinerjam Sistem |
| Metric |Accuracy, Precision, Recall, F1, Latency |
| Data source |Dataset video pengawasan publik |
| Analysis method |Uji t-test / ANOVA |

**Apakah rantai lengkap?** [x] Ya / [ ] Tidak
> Jika tidak, tahap mana yang perlu direvisi? ______________

---

## Refleksi

> Ambil satu judul skripsi/paper yang pernah dibaca. Coba ekstrak RQ-nya. Apakah RQ tersebut memenuhi semua komponen (metode, metrik, baseline, konteks)? Jika tidak, apa yang hilang?

**Judul:** Implementasi Teknologi Artificial Intelligence dalam Sistem Keamanan Kota di Ibu Kota Nusantara (IKN)
**RQ yang diekstrak:** Bagaimana AI diterapkan untuk meningkatkan keamanan kota?
**Komponen yang hilang:** metode spesifik
                          baseline
                          metrik
                          dataset
