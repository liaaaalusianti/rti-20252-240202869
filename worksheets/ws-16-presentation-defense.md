# WS-16: Presentation & Defense (UAS)

> **Bab 16 — Presentasi & Pertahanan Ilmiah**

---

## Ringkasan Materi

### Scientific Defense Model

```
Research Work → Presentation → Questioning → Defense → Evaluation → Acceptance
```

### Presentasi ≠ Ringkasan Paper

| Paper | Presentasi |
|-------|-----------|
| Dibaca (self-paced) | Didengar (presenter-paced) |
| Detail lengkap | Ide kunci + highlight |
| Tabel numerik detail | Grafik visual + angka kunci |
| Pembaca bisa re-read | Audiens dengar sekali |

**Prinsip:** Presentasi membutuhkan **reformulasi**, bukan kompresi. Medium berbeda = pendekatan berbeda.

### Claim-Evidence-Reasoning (CER)

Setiap jawaban defense harus memiliki:
1. **Claim** — Pernyataan yang dijawab
2. **Evidence** — Data/fakta pendukung
3. **Reasoning** — Logika yang menghubungkan evidence ke claim

**Contoh:**
| Pertanyaan | Bad Answer | Good Answer (CER) |
|-----------|-----------|-------------------|
| "Kenapa hanya 3 dataset?" | "Tiga sudah cukup" | "3 dataset mewakili variasi: small-clean, medium-clean, medium-noisy [E]. Generalisasi perlu validasi lanjut — listed as limitation [R]" |
| "Hasil DS-3 menurun?" | "Itu outlier" | "Ya, karena distribusi heavy-tail melanggar asumsi Gaussian [E]. Ini menunjukkan boundary condition metode [R]" |
| "Effect size?" | "p=0.003, jadi signifikan" | "Cohen's d=1.2 (large effect) [E] — bukan hanya signifikan tapi substansial [R]" |

### Slide Design — One Slide, One Message

**Optimal 9-Slide Plan (15 menit):**

| # | Slide | Waktu | Pesan |
|---|-------|-------|-------|
| 1 | Title + context | 1 min | Apa ini tentang apa |
| 2 | Problem + motivation | 2 min | Mengapa penting |
| 3 | Gap + RQ | 1.5 min | Apa yang belum terjawab |
| 4 | Method overview | 2 min | Bagaimana dijawab (diagram) |
| 5 | Key result — tabel | 2 min | Temuan utama |
| 6 | Key result — grafik | 2 min | Pola visual |
| 7 | Interpretation + failure | 2 min | Apa artinya |
| 8 | Limitation + future | 1.5 min | Batasan & arah |
| 9 | Conclusion + contribution | 1 min | Closing message |

### Anticipatory Defense

Prediksi pertanyaan berdasarkan kategori:

| Kategori | Contoh Pertanyaan |
|---------|------------------|
| Problem | "Mengapa masalah ini penting?" |
| Gap | "Bagaimana dengan studi X yang sudah menjawab ini?" |
| Method | "Mengapa metode ini, bukan Y?" |
| Results | "Bagaimana menjelaskan anomali di DS-3?" |
| Generalization | "Apakah bisa diterapkan di domain lain?" |

### Tiga Prinsip Jawaban

1. **Direct** — Jawab dulu, elaborasi kemudian
2. **Data-based** — Tunjuk evidence spesifik
3. **Honest** — Akui limitasi jika memang ada

### Jebakan Kognitif

1. "Presentasi = semua yang ada di paper" → terlalu padat
2. "Slide cantik = presentasi bagus" → konten > estetika
3. "Tidak bisa jawab = gagal" → "I don't know, but..." menunjukkan kejujuran
4. "Tidak perlu latihan — saya paham riset saya" → latihan = menemukan celah

---

## A.16 — Defense Preparation Sheet

DEFENSE PREPARATION

Slide Deck Plan:
Total slides : 10 (9 konten + 1 penutup)
Time per slide : ±1,5 menit
Total time : ±15 menit

Slide Outline:
| # | Pesan Utama                                                       | Visual                                                             | Waktu     |
| - | ----------------------------------------------------------------- | ------------------------------------------------------------------ | --------- |
| 1 | Judul penelitian dan identitas                                    | Cover + logo kampus                                                | 1 menit   |
| 2 | Latar belakang Smart City dan Smart Mobility di Kabupaten Kebumen | Ilustrasi Smart City + CCTV                                        | 2 menit   |
| 3 | Research Gap, Research Question, dan Hipotesis                    | Diagram research gap                                               | 1,5 menit |
| 4 | Metodologi penelitian                                             | Diagram alur eksperimen YOLOv8 vs YOLOv5                           | 2 menit   |
| 5 | Dataset dan skenario pengujian                                    | Tabel dataset dan flow eksperimen                                  | 1,5 menit |
| 6 | Hasil eksperimen                                                  | Tabel rata-rata preprocess, inference, postprocess, total pipeline | 2 menit   |
| 7 | Visualisasi hasil                                                 | Grafik perbandingan YOLOv8 dan YOLOv5                              | 2 menit   |
| 8 | Interpretasi hasil, keterbatasan penelitian, dan future work      | Diagram atau bullet point                                          | 2 menit   |
| 9 | Kesimpulan dan kontribusi penelitian                              | Ringkasan poin utama                                               | 1 menit   |


Anticipatory Defense Matrix:
| Kategori       | Pertanyaan Potensial                            | Jawaban (CER)                                                                                                                                                                                                                                                                                                                                     |
| -------------- | ----------------------------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| Problem        | Mengapa memilih topik deteksi kendaraan?        | **Claim:** Deteksi kendaraan merupakan bagian penting Smart Mobility. **Evidence:** CCTV telah tersedia namun belum dimanfaatkan secara otomatis. **Reasoning:** Computer Vision dapat membantu monitoring lalu lintas secara real-time.                                                                                                          |
| Gap            | Mengapa membandingkan YOLOv8 dengan YOLOv5?     | **Claim:** YOLOv5 merupakan baseline yang masih banyak digunakan. **Evidence:** Banyak penelitian sebelumnya menggunakan YOLOv5 sebagai pembanding. **Reasoning:** Perbandingan menunjukkan peningkatan performa generasi terbaru secara objektif.                                                                                                |
| Method         | Mengapa hanya menggunakan tiga video CCTV?      | **Claim:** Tiga video mewakili tiga lokasi lalu lintas berbeda di Kabupaten Kebumen. **Evidence:** Dataset berasal dari depan DPRD, depan Pendopo, dan Jalan Merdeka Timur dengan masing-masing tiga kali pengujian. **Reasoning:** Dataset cukup untuk melakukan eksperimen komparatif awal meskipun belum mewakili seluruh kondisi lalu lintas. |
| Results        | Mengapa YOLOv8 lebih cepat?                     | **Claim:** YOLOv8 memiliki waktu inferensi lebih rendah. **Evidence:** Rata-rata inference sekitar 106 ms, sedangkan YOLOv5 sekitar 209 ms. **Reasoning:** Arsitektur YOLOv8 lebih efisien sehingga proses deteksi lebih cepat pada perangkat CPU.                                                                                                |
| Generalization | Apakah hasil ini dapat diterapkan di kota lain? | **Claim:** Dapat diterapkan dengan penyesuaian. **Evidence:** Model menggunakan dataset CCTV umum dan framework YOLO yang bersifat universal. **Reasoning:** Perlu validasi menggunakan dataset dari daerah lain untuk memastikan kemampuan generalisasi.                                                                                         |


Latihan:
Latihan 1: Simulasi presentasi mandiri
Catatan: Mengukur durasi presentasi dan memperbaiki alur penyampaian.

Latihan 2: Simulasi dengan teman
Catatan: Menerima masukan mengenai kejelasan metode dan hasil penelitian.

Latihan 3: Gladi bersih
Catatan: Presentasi berjalan sesuai waktu, materi sudah siap, dan mampu menjawab pertanyaan utama.


---

## Latihan 1 — Slide Outline

Rencanakan presentasi 15 menit untuk riset Anda.
| # | Pesan Utama                             | Visual yang Digunakan                                     | Waktu     |
| - | --------------------------------------- | --------------------------------------------------------- | --------- |
| 1 | Judul penelitian                        | Cover penelitian                                          | 1 menit   |
| 2 | Permasalahan lalu lintas dan Smart City | Foto CCTV dan Smart City                                  | 2 menit   |
| 3 | Gap penelitian dan Research Question    | Diagram Gap Analysis                                      | 1,5 menit |
| 4 | Metode penelitian                       | Flowchart penelitian                                      | 2 menit   |
| 5 | Dataset dan skenario eksperimen         | Tabel dataset                                             | 1,5 menit |
| 6 | Hasil pengujian                         | Tabel hasil eksperimen                                    | 2 menit   |
| 7 | Grafik perbandingan performa            | Grafik preprocess, inference, postprocess, total pipeline | 2 menit   |
| 8 | Interpretasi hasil dan keterbatasan     | Bullet point                                              | 2 menit   |
| 9 | Kesimpulan dan kontribusi               | Ringkasan                                                 | 1 menit   |


**Total waktu estimasi:** 15 menit

---

## Latihan 2 — Anticipatory Defense

Prediksi 5 pertanyaan yang mungkin diajukan penguji, lalu siapkan jawaban CER.

| # | Kategori    | Pertanyaan                     | Claim                                                      | Evidence                                                | Reasoning                                      |
| - | ----------- | ------------------------------ | ---------------------------------------------------------- | ------------------------------------------------------- | ---------------------------------------------- |
| 1 | Problem     | Mengapa memilih YOLO?          | YOLO merupakan algoritma deteksi objek real-time.          | Digunakan luas pada Intelligent Transportation System.  | Sesuai untuk aplikasi Smart Mobility.          |
| 2 | Method      | Mengapa hanya tiga video?      | Tiga video mewakili tiga lokasi berbeda.                   | 18 eksperimen dilakukan (2 model × 3 video × 3 run).    | Sudah cukup untuk studi komparatif awal.       |
| 3 | Method      | Mengapa hanya menggunakan CPU? | Penelitian bertujuan melihat performa pada perangkat umum. | Semua eksperimen dilakukan pada environment yang sama.  | Perbandingan menjadi adil dan reproducible.    |
| 4 | Results     | Apa hasil utama penelitian?    | YOLOv8 lebih cepat dibanding YOLOv5.                       | Inference YOLOv8 sekitar 106 ms, YOLOv5 sekitar 209 ms. | YOLOv8 lebih efisien untuk aplikasi real-time. |
| 5 | Future Work | Apa pengembangan selanjutnya?  | Menambah dataset dan menggunakan GPU.                      | Dataset penelitian masih terbatas.                      | Akurasi dan generalisasi dapat ditingkatkan.   |


---

## Latihan 3 — Simulasi Q&A

Minta teman/kolega mengajukan 3 pertanyaan tentang riset Anda. Catat pertanyaan dan evaluasi jawaban Anda.

| # | Pertanyaan                                     | Jawaban Saya                                                                                                                                                   | Evaluasi                       |
| - | ---------------------------------------------- | -------------------------------------------------------------------------------------------------------------------------------------------------------------- | ------------------------------ |
| 1 | Mengapa menggunakan YOLOv5 sebagai pembanding? | Karena YOLOv5 merupakan baseline yang banyak digunakan sehingga hasil perbandingan lebih objektif.                                                             | ☑ Direct ☑ Data-based ☑ Honest |
| 2 | Mengapa tidak menghitung Precision dan Recall? | Fokus penelitian adalah membandingkan performa waktu pemrosesan (preprocess, inference, postprocess) menggunakan model pretrained tanpa ground truth berlabel. | ☑ Direct ☑ Data-based ☑ Honest |
| 3 | Mengapa hanya menggunakan tiga video?          | Karena penelitian merupakan studi komparatif awal dan keterbatasan dataset. Hal ini telah dicantumkan sebagai keterbatasan penelitian.                         | ☑ Direct ☑ Data-based ☑ Honest |


**Pertanyaan yang paling sulit dijawab:**
> Bagaimana performa YOLOv8 jika diuji pada kondisi malam hari atau cuaca buruk?
**Apa yang perlu disiapkan lebih baik:**
> Menyiapkan dataset tambahan pada berbagai kondisi pencahayaan, cuaca, dan kepadatan lalu lintas agar hasil penelitian memiliki tingkat generalisasi yang lebih tinggi.
---

## Refleksi

> Dari seluruh proses WS-01 sampai WS-16 — dari paradigma riset hingga presentasi — bagian mana yang paling mengubah cara Anda berpikir tentang riset? Apa satu hal yang akan selalu Anda terapkan di riset berikutnya?

**Insight terbesar:**
> Seluruh proses penelitian menunjukkan bahwa keberhasilan riset tidak hanya bergantung pada implementasi algoritma, tetapi juga pada perencanaan eksperimen, validasi data, analisis hasil, dan kemampuan menginterpretasikan temuan secara ilmiah. Dokumentasi yang sistematis membuat penelitian lebih mudah direproduksi dan dipertanggungjawabkan.
**Yang akan selalu diterapkan:**
> Pada penelitian berikutnya, saya akan selalu menyusun Research Question yang jelas, mendokumentasikan seluruh proses eksperimen secara lengkap, melakukan validasi data sebelum analisis, serta menyajikan hasil menggunakan tabel dan visualisasi yang objektif sehingga kesimpulan yang diperoleh dapat dipertanggungjawabkan secara ilmiah.
