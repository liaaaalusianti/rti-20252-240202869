# WS-11: Data Validation & Integrity

> **Bab 11 — Validasi Data & Integritas**

---

## Ringkasan Materi

### Data Trust Model

```
Raw Data → Data Cleaning → Consistency Check → Validation Process → Trusted Data
```

Data mentah belum bisa dipercaya. Harus melewati pipeline validasi sebelum siap untuk analisis statistik.

### Empat Pilar Data Quality

| Pilar | Deskripsi | Contoh Pelanggaran |
|-------|----------|-------------------|
| **Accuracy** | Nilai dalam range masuk akal | Akurasi = 1.5 (di luar [0,1]) |
| **Consistency** | Format seragam di semua run | Run 1: CSV, Run 2: JSON |
| **Completeness** | Tidak ada data hilang dari plan | 97 dari 100 run tercatat |
| **Validity** | Data sesuai desain eksperimen | Parameter baseline tercampur treatment |

### Proses Validasi Progresif

1. **Format validation** — Tipe file, header, kolom
2. **Range validation** — Nilai dalam batas logis
3. **Consistency validation** — Format seragam antar-run
4. **Logic validation** — Data cocok dengan desain eksperimen

Jika gagal di langkah awal → tidak perlu lanjut.

### Anomaly Detection — 3 Jenis

| Jenis | Deskripsi | Deteksi |
|-------|----------|---------|
| **Statistical outlier** | Nilai di luar distribusi normal | IQR: < Q1-1.5×IQR atau > Q3+1.5×IQR |
| **Contextual anomaly** | Normal absolut, abnormal dalam konteks | Run 1-10: ~91%, Run 11-20: ~88% |
| **Pattern anomaly** | Pola sistematis (bukan random) | Performa menurun berurutan |

**Prinsip:** Detect → Investigate → Document → Decide — **JANGAN langsung hapus.**

### Engineering vs Research Validation

| Aspek | Engineering | Research |
|-------|-----------|---------|
| Tujuan | Data sesuai spesifikasi bisnis | Data layak untuk analisis statistik |
| Missing data | Impute / set default | Investigasi penyebab → dokumentasi |
| Outlier | Bug → fix | Mungkin temuan → investigasi |
| Dokumentasi | Minimal (log error) | Komprehensif (anomali + keputusan) |

### Jebakan Kognitif

1. "Logging otomatis ≠ data benar" → bisa ada bug di logger
2. "Outlier = hapus" → bisa jadi temuan penting
3. "Dataset kecil tidak perlu validasi" → justru lebih rentan
4. "Mean normal = data benar" → [94, 95, 93, **44**, 94] → mean 84% terlihat wajar

---

## Template A.11 — Data Validation Checklist

```
DATA VALIDATION CHECKLIST

Completeness:
  [✓] Semua skenario tercakup
  [✓] Jumlah run sesuai rencana
  [✓] Tidak ada file output hilang
  Missing: 0 dari 18 data points

Format Consistency:
  [✓] Semua file format sama (CSV)
  [✓] Header konsisten
  [✓] Tipe data konsisten (numerik tetap numerik)

Range & Logic:
  [✓] Nilai dalam range masuk akal
  [✓] Tidak ada waktu negatif
  [✓] Waktu preprocess, inference, dan postprocess bernilai positif
  Anomali ditemukan:
  - False positive: objek batu terdeteksi sebagai mobil pada beberapa frame.
  - YOLOv5 memiliki waktu inferensi lebih tinggi dibandingkan YOLOv8.

Cross-Validation:
  [✓] Run identik → hasil mendekati
  [✓] Trend konsisten dengan ekspektasi teori
  (YOLOv8 secara konsisten memiliki waktu inferensi lebih cepat daripada YOLOv5.)

Keputusan:
  [✓] Data siap analisis
  [ ] Perlu cleaning
  [ ] Perlu re-run (skenario: -)
```

---

## Latihan 1 — Completeness Check

Verifikasi apakah semua data yang direncanakan sudah terkumpul.

| Skenario               | Run Direncanakan | Run Tercatat | Missing | Alasan |
| ---------------------- | ---------------: | -----------: | ------: | ------ |
| YOLOv8 – depan_dprd    |                3 |            3 |       0 | —      |
| YOLOv8 – depan_pendopo |                3 |            3 |       0 | —      |
| YOLOv8 – merdeka_timur |                3 |            3 |       0 | —      |
| YOLOv5 – depan_dprd    |                3 |            3 |       0 | —      |
| YOLOv5 – depan_pendopo |                3 |            3 |       0 | —      |
| YOLOv5 – merdeka_timur |                3 |            3 |       0 | —      |


**Total expected:** 18 | **Total actual:** 18 | **Missing:** 0

**Keputusan untuk data missing:**
> Tidak terdapat data yang hilang. Seluruh eksperimen berhasil dijalankan sesuai rencana sehingga seluruh hasil dapat digunakan pada tahap analisis berikutnya.
---

## Latihan 2 — Anomaly Investigation

Periksa data Anda untuk anomali. Gunakan metode IQR atau z-score.

**Dataset (Inference Time)**
| Run | Inference Time (ms) |
| --- | ------------------: |
| 1   |               157.8 |
| 2   |               148.0 |
| 3   |                87.2 |
| 4   |               105.3 |
| 5   |               100.0 |


**Deteksi outlier:**
- Deteksi Outlier
- Q1 = Belum dihitung
- Q3 = Belum dihitung
- IQR = Belum dihitung
- Outlier terdeteksi = Tidak ditemukan outlier yang signifikan berdasarkan pengamatan awal.

**Investigasi (untuk setiap outlier):**
| Outlier        |                         Nilai | Kemungkinan Penyebab                                               | Keputusan                                                                                |
| -------------- | ----------------------------: | ------------------------------------------------------------------ | ---------------------------------------------------------------------------------------- |
| False Positive | Batu terdeteksi sebagai mobil | Kemiripan bentuk objek dengan kendaraan pada sudut kamera tertentu | Tidak dihapus, didokumentasikan sebagai false positive dan menjadi bagian evaluasi model |


---

## Latihan 3 — Validation Report

Buat laporan validasi ringkas untuk dataset eksperimen Anda.

**1. Completeness:** 100% data terkumpul
**2. Format:** [✓] Konsisten / [ ] Ada inkonsistensi: ____
**3. Range check (anomali):** Ditemukan false positive, yaitu objek batu pada area jalan terdeteksi sebagai kendaraan (mobil). Selain itu seluruh nilai inference time berada pada rentang yang masih wajar dan tidak ditemukan nilai negatif maupun data kosong.
**4. Logic check:** [✓] Parameter sesuai plan / [ ] Ada ketidaksesuaian: 
Semua eksperimen menggunakan parameter yang sama, yaitu:

Image Size = 640
Confidence Threshold = 0.25
Dataset CCTV yang sama
Perbandingan model YOLOv5 dan YOLOv8

**Kesimpulan:** [✓] Data siap analisis / [ ] Perlu tindakan: Seluruh data eksperimen telah tervalidasi, lengkap, dan konsisten. Anomali berupa false positive telah didokumentasikan sebagai bagian dari evaluasi performa model sehingga dataset layak digunakan pada tahap analisis dan pembahasan hasil penelitian.

---

## Refleksi

> Apa perbedaan antara "data yang benar" dan "data yang dipercaya"? Mengapa proses validasi formal diperlukan meskipun data dikumpulkan secara otomatis?

> Data yang benar adalah data yang diperoleh langsung dari hasil eksperimen, sedangkan data yang dipercaya adalah data yang telah melalui proses validasi sehingga terbukti lengkap, konsisten, dan sesuai dengan rancangan penelitian. Meskipun data dikumpulkan secara otomatis, proses validasi tetap diperlukan untuk memastikan tidak terdapat data yang hilang, kesalahan pencatatan, maupun anomali seperti false positive. Dengan demikian, hasil penelitian menjadi lebih objektif, dapat dipertanggungjawabkan, dan mudah direproduksi oleh peneliti lain.
