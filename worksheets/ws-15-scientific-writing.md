# WS-15: Scientific Writing

> **Bab 15 — Penulisan Ilmiah**

---

## Ringkasan Materi

### Scientific Argument Flow

```
Problem → Gap → RQ → Method → Result → Analysis → Conclusion → Contribution
```

Paper ilmiah adalah **satu argumen utuh** dari masalah ke kontribusi. Setiap node harus terhubung logis ke node sebelum dan sesudahnya.

### Struktur IMRAD

| Section | Peran | Pertanyaan Kunci |
|---------|-------|-----------------|
| **Introduction** | Motivasi + frame | Why is this needed? |
| **Method** | Deskripsi (reproducible) | How was it done? |
| **Results** | Laporan objektif | What was found? |
| **Discussion** | Interpretasi + refleksi | What does it mean? |
| **Conclusion** | Ringkasan + kontribusi | So what? |

### Logical Flow — "Red Thread"

Setiap paragraf menjawab satu pertanyaan dan memicu pertanyaan berikutnya. Alur logis ini harus terasa di tiga level:
1. **Antar-kalimat** dalam paragraf
2. **Antar-paragraf** dalam section
3. **Antar-section** dalam paper

### Internal Consistency

Setiap elemen yang dijanjikan di Introduction harus hadir di Discussion/Conclusion.

**Consistency Matrix:**
```
           Intro  Method  Result  Discuss  Conclude
RQ1          ✓      ✓       ✓       ✓        ✓
RQ2          ✓      ✓       ✓       ✗ ←      ✓
Metrik-X     ✗      ✗       ✓ ←     ✗        ✗
```
**Masalah:** RQ2 dibahas di semua bagian kecuali Discussion. Metrik-X muncul di Result tapi tidak diperkenalkan di Method.

### Writing Quality Triad

| Kualitas | Deskripsi | Contoh Buruk → Baik |
|----------|----------|---------------------|
| **Clarity** | Dipahami sekali baca | "Performa meningkat" → "Accuracy meningkat dari 85.3% ke 89.7%" |
| **Precision** | Istilah eksak, tanpa ambiguitas | "signifikan" → "signifikan secara statistik (p=0.003, d=1.2)" |
| **Conciseness** | Setiap kata menambah informasi | Hapus kalimat redundan, filler words |

### Urutan Penulisan yang Disarankan

1. **Method & Results** — paling stabil, tulis pertama
2. **Discussion** — interpretasi berdasarkan hasil
3. **Introduction** — frame sesuai temuan aktual
4. **Abstract & Conclusion** — terakhir

### Target Jumlah Kata

| Section | Target |
|---------|--------|
| Introduction | 500–700 |
| Related Work | 700–1000 |
| Method | 800–1200 |
| Results | 500–800 |
| Discussion | 600–900 |
| Conclusion | 200–400 |

### Jebakan Kognitif

1. "Lebih panjang = lebih lengkap" → conciseness lebih berharga
2. "Introduction harus ditulis pertama" → justru ditulis terakhir
3. "Jargon teknis = lebih ilmiah" → clarity lebih penting
4. "Discussion = ringkasan Results" → Discussion = interpretasi + konteks

---

## A.15 — Paper Structure Checklist

PAPER STRUCTURE CHECKLIST

Title   : Perbandingan YOLOv8 dan YOLOv5 dalam Deteksi Kendaraan pada Rekaman CCTV untuk Mendukung Smart City di Kabupaten Kebumen
Target  : [ ] Jurnal  [ ] Konferensi  [✓] Laporan

Section Check:
  [✓] Abstract — masalah, metode, hasil utama, kontribusi (max 250 kata)
  [✓] Introduction — konteks → gap → RQ → kontribusi → struktur paper
  [✓] Related Work — concept-centric, gap positioning
  [✓] Method — reproducible: desain, variabel, metrik, setup, prosedur
  [✓] Results — tabel + grafik + observasi (tanpa interpretasi)
  [✓] Discussion — interpretasi, perbandingan, implikasi, limitation
  [✓] Conclusion — jawaban RQ, kontribusi, future work

Consistency Matrix:
  [✓] RQ di Introduction = RQ di Method = RQ di Conclusion
  [✓] Variabel di Method = variabel di Results
  [✓] Klaim di Discussion didukung data di Results
  [✓] Limitasi di Discussion di-address di Conclusion/Future Work

Writing Quality:
  [✓] Clarity — mudah dipahami tanpa re-read
  [✓] Precision — tidak ada istilah ambigu
  [✓] Conciseness — tidak ada kalimat redundan


---

## Latihan 1 — Paper Outline

Buat outline paper untuk riset Anda menggunakan struktur IMRAD.

| Section          | Konten Utama                                                                                                                                                                                                                                                                                                                                                                        | Target Kata |
| ---------------- | ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ----------- |
| **Abstract**     | Penelitian membandingkan performa YOLOv8 dan YOLOv5 dalam mendeteksi kendaraan pada rekaman CCTV di Kabupaten Kebumen. Pengujian dilakukan menggunakan tiga video CCTV dengan masing-masing tiga kali pengujian pada setiap model. Hasil menunjukkan bahwa YOLOv8 memiliki waktu inference lebih cepat dibandingkan YOLOv5 sehingga lebih sesuai untuk implementasi smart mobility. | 200–250     |
| **Introduction** | Menjelaskan konsep Smart City dan Smart Mobility, pentingnya deteksi kendaraan otomatis menggunakan CCTV, keterbatasan penelitian sebelumnya, research gap, Research Question, hipotesis, dan kontribusi penelitian.                                                                                                                                                                | 500–700     |
| **Related Work** | Membahas penelitian terdahulu mengenai YOLOv5, YOLOv8, computer vision, intelligent transportation system, dan implementasi smart city. Menunjukkan gap bahwa penelitian komparatif pada CCTV Kabupaten Kebumen masih terbatas.                                                                                                                                                     | 700–1000    |
| **Method**       | Menjelaskan metode eksperimen, dataset tiga video CCTV, dua model (YOLOv8 dan YOLOv5), spesifikasi perangkat, variabel penelitian, prosedur eksperimen sebanyak 18 run, metrik preprocess, inference, postprocess, total pipeline, serta teknik analisis deskriptif.                                                                                                                | 800–1200    |
| **Results**      | Menampilkan tabel hasil rata-rata, standar deviasi, grafik perbandingan preprocess, inference, postprocess, dan total pipeline antara YOLOv8 dan YOLOv5 tanpa interpretasi.                                                                                                                                                                                                         | 500–800     |
| **Discussion**   | Menginterpretasikan hasil bahwa YOLOv8 memiliki inference lebih cepat daripada YOLOv5 sehingga lebih sesuai digunakan pada sistem monitoring lalu lintas berbasis CCTV. Membahas penyebab perbedaan performa dan membandingkan dengan penelitian terdahulu.                                                                                                                         | 600–900     |
| **Conclusion**   | Menjawab Research Question, menyimpulkan bahwa YOLOv8 lebih efisien dibandingkan YOLOv5 berdasarkan waktu inferensi dan total pipeline, serta memberikan saran penelitian lanjutan menggunakan GPU dan dataset yang lebih besar.                                                                                                                                                    | 200–400     |

---

## Latihan 2 — Consistency Matrix

Buat consistency matrix untuk memverifikasi internal consistency paper Anda.

| Komponen                                               | Intro | Method | Result | Discussion | Conclusion |
| ------------------------------------------------------ | :---: | :----: | :----: | :--------: | :--------: |
| Research Question                                      |   ✓   |    ✓   |    ✓   |      ✓     |      ✓     |
| Hipotesis                                              |   ✓   |    ✓   |    ✓   |      ✓     |      ✓     |
| Variabel Independen (Model YOLO)                       |   ✓   |    ✓   |    ✓   |      ✓     |      ✓     |
| Variabel Dependen (Preprocess, Inference, Postprocess) |   ✓   |    ✓   |    ✓   |      ✓     |      ✓     |
| Dataset CCTV                                           |   ✓   |    ✓   |    ✓   |      ✓     |      ✓     |
| Grafik Perbandingan                                    |   ✗   |    ✓   |    ✓   |      ✓     |      ✓     |
| Kontribusi Penelitian                                  |   ✓   |    ✗   |    ✓   |      ✓     |      ✓     |


**Isi setiap sel:** ✓ (ada & konsisten), ✗ (missing), ~ (ada tapi inkonsisten)

**Inkonsistensi yang ditemukan**
> Tidak terdapat inkonsistensi yang signifikan. Semua Research Question, variabel penelitian, metode, dan hasil telah konsisten dari pendahuluan hingga kesimpulan.

**Tindakan Perbaikan**
>Menambahkan referensi terhadap grafik hasil pada bagian Discussion agar interpretasi lebih kuat serta memastikan seluruh gambar dan tabel diberi nomor dan penjelasan.

---

## Latihan 3 — Writing Quality Check

Ambil satu paragraf dari tulisan Anda (atau tulis paragraf baru) dan evaluasi kualitasnya.

**Paragraf asli:**
> Penelitian ini membandingkan YOLOv8 dan YOLOv5 untuk mendeteksi kendaraan pada CCTV Kabupaten Kebumen. Pengujian dilakukan menggunakan tiga video CCTV dan hasilnya menunjukkan bahwa YOLOv8 lebih cepat daripada YOLOv5.

| Kriteria    | Evaluasi                                                               | Perbaikan                                         |
| ----------- | ---------------------------------------------------------------------- | ------------------------------------------------- |
| Clarity     | Sudah jelas tetapi belum menjelaskan bagaimana perbandingan dilakukan. | Tambahkan jumlah video dan jumlah run eksperimen. |
| Precision   | Belum menyebutkan metrik yang digunakan.                               | Sebutkan preprocess, inference, dan postprocess.  |
| Conciseness | Sudah cukup ringkas.                                                   | Tidak perlu perubahan besar.                      |

**Paragraf setelah perbaikan:**
> Penelitian ini membandingkan performa YOLOv8 dan YOLOv5 dalam mendeteksi kendaraan pada tiga rekaman CCTV di Kabupaten Kebumen. Pengujian dilakukan sebanyak tiga kali pada setiap video untuk masing-masing model sehingga diperoleh 18 run eksperimen. Evaluasi dilakukan berdasarkan waktu preprocess, inference, postprocess, dan total pipeline. Hasil eksperimen menunjukkan bahwa YOLOv8 memiliki rata-rata waktu inference dan total pipeline yang lebih rendah dibandingkan YOLOv5 sehingga lebih sesuai untuk implementasi sistem pemantauan lalu lintas berbasis smart mobility.
---

## Refleksi

> Apa perbedaan antara menulis "tentang" riset dan menulis sebagai "argumen" riset? Bagaimana urutan penulisan (Method → Discussion → Introduction) mengubah kualitas tulisan?

> Menulis "tentang" riset hanya menjelaskan apa yang dilakukan, sedangkan menulis sebagai "argumen" riset berarti setiap bagian tulisan harus mendukung jawaban terhadap Research Question. Pendekatan ini membuat alur penelitian menjadi lebih logis karena setiap metode, hasil, dan pembahasan saling berkaitan untuk memperkuat kesimpulan.
> Menulis dengan urutan Method → Results → Discussion → Introduction → Conclusion membantu menghasilkan tulisan yang lebih konsisten karena seluruh bagian pendahuluan dan kesimpulan disusun berdasarkan hasil eksperimen yang benar-benar diperoleh, sehingga mengurangi inkonsistensi antara tujuan penelitian dan hasil yang dilaporkan.
