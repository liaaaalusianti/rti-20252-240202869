# WS-06: System-Experiment Mapping

> **Bab 6 — System Design sebagai Experimental Artifact**

---

## Ringkasan Materi

### Sistem = Instrumen Pengujian, Bukan Produk

Seorang engineer bertanya "apakah sistem bekerja?" — seorang peneliti bertanya "apa yang bisa dibuktikan sistem ini?" Sistem dalam riset adalah **artifact** — objek yang sengaja dibuat untuk menguji klaim spesifik.

### System as Experiment Model

```
RQ → Variable → System Component → Experimental Setup → Output
```

Setiap komponen sistem harus bisa ditelusuri ke variabel riset (top-down), dan setiap pengukuran harus menjawab RQ (bottom-up).

### Mapping Variabel ke Komponen

| Tipe Variabel | Peran di Sistem | Contoh |
|---------------|----------------|--------|
| **IV** (Independent) | Modul yang bisa di-toggle/swap | Algoritma A vs B |
| **DV** (Dependent) | Modul pengukuran | Logger, metrics collector |
| **CV** (Control) | Config yang dikunci | Dataset, parameter tetap |

Jika variabel tidak bisa di-map ke komponen apapun → arsitektur perlu didesain ulang.

### 4 Prinsip Desain Eksperimental

| Prinsip | Pertanyaan Kunci |
|---------|-----------------|
| **Traceability** | Komponen ini melayani variabel yang mana? |
| **Modularity** | Bisakah IV diubah tanpa memengaruhi yang lain? |
| **Controllability** | Apakah CV dieksternalisasi ke config file? |
| **Measurability** | Apakah sistem otomatis menghasilkan data yang dibutuhkan? |

### Variable Isolation melalui Arsitektur

- **Modular architecture** — Pisahkan berdasarkan variabel
- **Configuration-driven** — Ubah config (YAML/JSON), bukan code
- **Feature toggles** — On/off flag untuk ablation study

  Contoh config YAML dengan feature toggles:
  ```yaml
  model:
    type: cnn          # IV: ganti "rf" untuk kondisi baseline
  features:
    use_temporal: true  # toggle komponen temporal
    use_normalization: true  # toggle preprocessing
  experiment:
    seed: 42
    runs: 5
  ```
  Dengan pendekatan ini, berbeda kondisi eksperimen = berbeda satu baris config, **tanpa mengubah kode**.

### Research vs Engineering

| Aspek | Engineering | Research |
|-------|------------|----------|
| Tujuan sistem | Memenuhi kebutuhan user | Menguji hipotesis, menghasilkan bukti |
| Arsitektur | Optimasi performa & skalabilitas | Optimasi isolasi variabel & reprodusibilitas |
| Konfigurasi | Sering hardcoded | Dieksternalisasi ke config file |
| Fitur tambahan | Menambah nilai user | Menambah noise jika tidak terkait RQ |

### Istilah Penting

- **Artifact** — Objek yang sengaja dibuat untuk memecahkan masalah atau menguji proposisi
- **Traceability** — Kemampuan menelusuri hubungan RQ → variabel → komponen → output
- **Variable Isolation** — Mengubah hanya satu variabel sambil menahan yang lain konstan
- **Ablation Study** — Menguji kontribusi tiap komponen dengan melepasnya satu per satu
- **Configuration-driven Execution** — Semua parameter di config file, bukan hardcoded

---

## Template A.6 — Mapping RQ ke Arsitektur Sistem

```
SYSTEM-EXPERIMENT MAPPING

Research Question: Bagaimana kinerja sistem keamanan berbasis Artificial Intelligence menggunakan metode deteksi objek berbasis computer vision dalam meningkatkan akurasi deteksi dan waktu respon dibandingkan sistem CCTV konvensional melalui simulasi menggunakan dataset video publik untuk mendukung transformasi smart city di Kabupaten Kebumen?
Variable → Component Mapping:
| Variabel | Tipe | Komponen Sistem | Cara Manipulasi/Pengukuran |
|----------|------|-----------------|---------------------------|
|Jenis sistem keamanan| IV   |Modul deteksi objek   |Mengganti model AI ↔ baseline CCTV konvensional melalui config|
|Kinerja sistem       | DV   |Metrics evaluator     |Menghitung Accuracy, Precision, Recall, F1-score              |
|Waktu respon         | DV   |Timer / latency logger|Mengukur waktu proses tiap video (ms)                         |
|Riset TI yang Relevan| CV   |Input dataset manager |Menggunakan dataset yang sama pada semua eksperimen           |
4 Prinsip Desain:
  [X] Traceability — Setiap komponen bisa ditelusuri ke variabel
  [X] Variable Isolation — IV bisa diubah tanpa mengubah CV
  [X] Measurement Integration — Pengukuran DV built-in
  [X] Reproducibility — Setup bisa direkonstruksi

Experimental Setup:
  Input data     : Dataset video pengawasan publik (public surveillance dataset)
  Parameter      : 1. model_type = AI / conventional
                   2. video_source = same dataset
                   3. number_of_runs = 5
  Output format  : Tabel hasil Accuracy, Precision, Recall, F1-score, dan Latency
```

---

## Latihan 1 — Variable-to-Component Mapping

Gunakan RQ dan variabel dari WS-05. Petakan ke komponen sistem.

**RQ:** Bagaimana kinerja sistem keamanan berbasis AI dibandingkan CCTV konvensional melalui simulasi menggunakan dataset video publik?

| Variabel | Tipe | Komponen Sistem | Cara Manipulasi / Pengukuran |
|----------|------|-----------------|---------------------------|
|Jenis sistem   | IV |Detection module |Ubah model_type         |
|Kinerja sistem | DV |Evaluation module|Hitung confusion matrix |
|Waktu respon   | CV |Timer logger     |Catat latency           |
|Dataset        | CV |Dataset loader   |Gunakan dataset sama    |

**Apakah semua variabel bisa di-map?** [X] Ya / [ ] Tidak
> Jika tidak, komponen apa yang perlu ditambahkan? _________

---

## Latihan 2 — 4 Prinsip Desain

Evaluasi desain sistem terhadap 4 prinsip.

| Prinsip | Status | Bukti / Penjelasan |
|---------|--------|-------------------|
| Traceability    |✅ |Semua modul terkait langsung ke variabel    |
| Modularity      |✅ |Modul AI dapat diganti tanpa ubah modul lain|
| Controllability |✅ |Parameter eksperimen disimpan di config     |
| Measurability   |✅ |Output metrik otomatis dihasilkan           |

**Prinsip mana yang paling sulit dipenuhi?** Controllability
**Strategi untuk mengatasinya:**
> Menggunakan file konfigurasi (config.yaml) agar parameter eksperimen dapat diubah tanpa mengubah kode program.
---

## Latihan 3 — Ablation Study Planning

Jika sistem memiliki 3 komponen utama, rencanakan ablation study.

> **Panduan jumlah kondisi:** Untuk 3 komponen (A, B, C), kondisi minimal yang direkomendasikan:
> Full + (-A) + (-B) + (-C) = **4 kondisi dasar**. Jika waktu memungkinkan, tambahkan kombinasi ganda: (-A,-B), (-A,-C), (-B,-C) = **7 kondisi**. Sesuaikan dengan *computational cost* dan tenggat waktu penelitian.

| Kondisi | Komponen A | Komponen B | Komponen C | Hasil yang Diharapkan |
|---------|-----------|-----------|-----------|----------------------|
| Full |✅             | ✅                  | ✅                     |performa terbaik          |
| – A  | ❌ (ganti RF) | ✅                  | ✅                     |performa turun            |
| – B  | ✅            | ❌ (tanpa temporal) | ✅                     |akurasi menurun           |
| – C  | ✅            | ✅                  | ❌ (tanpa normalisasi) |metrik tidak dapat diukur |
**Komponen mana yang diprediksi paling berkontribusi?** AI Detection Model
**Mengapa?**
> Karena komponen ini merupakan inti sistem yang secara langsung menentukan kemampuan deteksi objek dan membedakan performa dengan baseline.
---

## Refleksi

> Apa risiko jika sistem dibangun seperti produk (monolitik, fitur lengkap) lalu baru dilakukan eksperimen? Mengapa arsitektur modular penting untuk riset?

**Jawaban:**
> Jika sistem dibangun secara monolitik, perubahan satu komponen dapat memengaruhi seluruh sistem sehingga sulit mengisolasi variabel penelitian. Hal ini membuat hasil eksperimen sulit direproduksi dan mengurangi validitas penelitian.
> Karena arsitektur modular memungkinkan perubahan hanya pada variabel yang diuji tanpa memengaruhi komponen lain, sehingga eksperimen lebih terkontrol dan hasil lebih valid.
