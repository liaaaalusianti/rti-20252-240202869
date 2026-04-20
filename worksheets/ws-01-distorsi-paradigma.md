# WS-01: Distorsi & Paradigma

> **Bab 1 — Research Mindset in IT**

---

## Ringkasan Materi

### Research Trust Model

Pengetahuan ilmiah tidak muncul langsung dari kenyataan. Ia melewati **6 tahap transformasi** yang masing-masing rawan distorsi:

```
Reality → Data → Processing → Analysis → Inference → Knowledge
```

Etika mencegah distorsi yang disengaja (fabrikasi, cherry-picking). Validitas mendeteksi distorsi yang tidak disengaja (confounding variable, sampling bias).

### Tiga Jenis Validitas

| Jenis | Pertanyaan | Contoh Ancaman |
|-------|-----------|----------------|
| **Internal Validity** | Apakah hubungan kausal benar ada? | Confounding variable |
| **External Validity** | Apakah bisa digeneralisasi? | Dataset terlalu homogen |
| **Construct Validity** | Apakah mengukur hal yang benar? | Metrik tidak sesuai klaim |

### Paradigma Riset

Mata kuliah ini menggunakan pendekatan **Positivist** (fenomena TI bisa diukur objektif melalui eksperimen terkontrol) diperkuat **Design Science Research** (DSR). Penting untuk membedakan keduanya:

| Paradigma | Cara Kerja | Contoh di TI |
|-----------|-----------|---------------|
| **Positivis** | Uji hipotesis dengan eksperimen terkontrol | Apakah CNN lebih akurat dari RF pada dataset X? |
| **Design Science Research** | Bangun artefak (sistem/model/framework) untuk menguji proposisi | Dapatkah arsitektur hybrid CNN+LSTM membuktikan peningkatan recall ≥5%? |
| **Interpretivis** | Pahami makna melalui konteks & kualitatif | Bagaimana peneliti manafsirkan anomali data sensor IoT? |

Dalam DSR, artefak **bukan tujuan akhir** — ia adalah instrumen untuk menghasilkan pengetahuan. Pertanyaan riset tetap harus difalsifikasi.

### Mode Berpikir Peneliti

**Curious** (mempertanyakan fenomena) → **Critical** (mengevaluasi klaim berdasarkan bukti) → **Systematic** (merancang investigasi terstruktur dan reproducible).

### Research vs Engineering

| Aspek | Engineering | Research |
|-------|------------|----------|
| Tujuan | Membuat sistem yang bekerja | Menghasilkan pengetahuan yang valid |
| Pertanyaan khas | "Bagaimana membuatnya jalan?" | "Apakah klaim ini benar?" |
| Ukuran sukses | Sistem berfungsi, client puas | Hipotesis terjawab, temuan tervalidasi |
| Kegagalan | Harus dihindari | Harus dilaporkan (negative result = kontribusi) |

### Istilah Penting

- **Research Mindset** — Pola pikir yang menuntut bukti dan mempertanyakan asumsi
- **Research Ethics** — Prinsip perilaku: kejujuran, objektivitas, keterbukaan, akuntabilitas
- **HARKing** — Hypothesizing After Results are Known — merumuskan hipotesis setelah melihat data
- **Falsifiability** — Hipotesis harus bisa dibuktikan salah

---

## Template A.1 — Research Mindset Self-Assessment

```
Nama Peneliti    : Lia Lusianti
Tanggal          : 18 april 2026

1. Ketika membaca klaim "metode X 95% akurat":
   - Pertanyaan pertama saya: Bagaimana distribusi data yang digunakan untuk pengujian, dan apakah kondisi lingkungan saat pengambilan data sudah mencakup berbagai skenario ekstrem?
   - Data yang dibutuhkan untuk verifikasi: Matriks konfusi (confusion matrix), spesifikasi teknis sensor yang digunakan, serta log data mentah sebelum diproses.

2. Posisi paradigma:
   - Pendekatan: [ ] Positivis  [ ] Interpretivis  [ x] Design Science  [ ] Mixed
   - Alasan: Riset ini berfokus pada pembangunan sebuah artefak (sistem otomasi hidroponik) untuk membuktikan bahwa integrasi IoT dan energi terbarukan dapat memecahkan masalah efisiensi pertanian.

3. Identifikasi distorsi:
   - Asumsi tersembunyi: Sistem dianggap akan selalu mendapatkan paparan sinar matahari yang konstan untuk panel surya.
   - Sumber bias potensial: Penempatan sensor suhu yang mungkin terlalu dekat dengan komponen elektronik yang panas.
   - Langkah mitigasi: Melakukan kalibrasi sensor secara berkala dengan alat ukur standar industri dan menggunakan teknik shielding pada sensor.

4. Komitmen etika:
   - Data yang tidak akan dimanipulasi:Log waktu respons (latensi) pengiriman data dari sensor ke dashboard dan pembacaan asli parameter lingkungan.
   - Batasan yang diakui sejak awal: Keterbatasan kapasitas baterai pada panel surya yang mungkin mempengaruhi stabilitas sistem saat cuaca mendung berkepanjangan.
```

---

## Latihan 1 — Identifikasi Distorsi

Pilih satu paper riset di bidang TI yang mengklaim "metode X meningkatkan performa." Telusuri setiap tahap Research Trust Model.

> **Panduan pencarian paper:** Gunakan [IEEE Xplore](https://ieeexplore.ieee.org), [ACM Digital Library](https://dl.acm.org), atau Google Scholar. Pilih paper **tahun 2020 ke atas**, di topik yang Anda minati: deteksi anomali, klasifikasi citra, NLP, keamanan siber, IoT, dsb.
>
> **Contoh domain TI:** "Deteksi anomali lalu-lintas jaringan menggunakan CNN — akurasi meningkat 94% vs baseline SVM 87%." Distorsi potensial: apakah dataset normal/anomali seimbang? Apakah hanya diuji pada satu vendor traffic?

**Paper yang dipilih:**
> Judul: Desain dan Prototipe Integrasi IoT dalam Pertanian Hidroponik Cerdas Berbasis Energi Terbarukan
> Penulis (Tahun): M.R. Fachrizal, dkk. (2025)
> Sumber/Link DOI: (https://journal.stmiki.ac.id/index.php/jimik/article/view/1134)

| Tahap | Apa yang Dilakukan | Potensi Distorsi |
|-------|-------------------|-----------------|
| Reality → Data |Mengambil data suhu dan kelembapan udara melalui sensor DHT22 pada instalasi hidroponik.|Sensor Noise: Penempatan sensor yang terkena sinar matahari langsung dapat memberikan bacaan suhu lebih tinggi dari suhu nutrisi sebenarnya. |
| Data → Processing |Mengirimkan data dari Arduino Uno ke platform IoT untuk ditampilkan di dashboard.|Latency Distortion: Jika koneksi internet tidak stabil, data yang diproses bisa mengalami keterlambatan (delay), sehingga data tidak lagi bersifat real-time.|
| Processing → Analysis |Membandingkan data sensor dengan ambang batas (threshold) untuk menyalakan pompa/kipas secara otomatis. |Threshold Bias: Penentuan ambang batas yang terlalu kaku mungkin tidak cocok jika jenis tanaman hidroponiknya diganti (misal: selada vs cabai). |
| Analysis → Inference |Menyimpulkan bahwa penggunaan panel surya cukup untuk menggerakkan seluruh sistem IoT. |Contextual Bias: Kesimpulan ini mungkin hanya valid saat cuaca cerah; saat musim hujan, daya mungkin tidak mencukupi (tidak digeneralisasi). |
| Inference → Knowledge |Menyatakan bahwa sistem otomasi ini meningkatkan efisiensi pemeliharaan hidroponik secara signifikan. |Measurement Validity: Jika "efisiensi" tidak diukur dengan angka pertumbuhan tanaman, maka klaim ini bersifat subjektif. |

**Distorsi paling besar di tahap:** Reality → Data (Akurasi Sensor)

**Dua distorsi spesifik yang teridentifikasi:**
1. Environmental Bias: Selection Bias: Pengambilan data performa sistem hanya dilakukan pada durasi waktu tertentu yang optimal.
2. Sampling Rate Distortion: Penggunaan sensor kelas hobi (DHT22) mungkin memiliki margin error yang lebih besar dibandingkan sensor standar industri.

---

## Latihan 2 — Analisis Kasus Etika

Skenario: Seorang peneliti menemukan bahwa jika 3 data point outlier dihapus, hasil eksperimennya menjadi signifikan. Dengan outlier, hasilnya tidak signifikan.

| Perspektif | Analisis |
|------------|---------|
| Kejujuran ilmiah | Peneliti harus melaporkan keberadaan outlier tersebut karena itu adalah bagian dari realitas eksperimen yang mungkin disebabkan oleh kegagalan sensor atau gangguan daya.|
| Transparansi |Menjelaskan secara rinci alasan mengapa data tersebut dianggap sebagai outlier (misalnya karena gangguan teknis yang teridentifikasi). |
| Peer review |Menyembunyikan data demi hasil signifikan akan menyesatkan peneliti lain yang mencoba mereplikasi sistem ini. |

**Keputusan akhir dan justifikasi:**
> Melaporkan kedua hasil tersebut (dengan dan tanpa outlier) di dalam laporan. Jika outlier tersebut memang disebabkan oleh kerusakan teknis yang jelas, peneliti boleh mengeksklusinya namun tetap wajib memberikan catatan kaki atau penjelasan teknis mengenai pengecualian tersebut untuk menjaga integritas riset.

---

## Latihan 3 — Posisi Paradigma

**Topik riset:** Rancang Bangun Sistem Monitoring dan Otomasi Hidroponik Berbasis IoT dan Panel Surya.

> **Skala 1–5:** 1 = tidak sesuai sama sekali dengan topik ini, 5 = sangat sesuai dan dominan digunakan pada riset bertopik serupa.

| Kriteria | Positivis | Interpretivis | Design Science |
|----------|-----------|---------------|----------------|
| Kesesuaian dengan topik (1–5) |4|2|5|
| Jenis data yang dikumpulkan |Metrik akurasi sensor, efisiensi daya panel surya. |Persepsi petani terhadap kemudahan antarmuka sistem.|Keberhasilan fungsi otomasi dan performa artefak. |
| Limitasi paradigma |Kurang mengeksplorasi sisi sosial penerimaan teknologi. |Sulit mengukur keandalan sistem secara teknis/numerik. |Terlalu fokus pada "pembuatan alat" daripada teori mendasar. |

**Paradigma yang dipilih:** Design Science Research (DSR)
**Alasan:** Karena fokus utama riset ini adalah menciptakan solusi praktis berupa artefak teknologi untuk memecahkan masalah pertanian, di mana validasi dilakukan melalui pengujian performa artefak tersebut.
---

## Refleksi

> Sebelum membaca materi ini, apakah pernah mempertanyakan klaim "95% akurat"? Setelah memahami rantai distorsi, pertanyaan apa yang sekarang akan diajukan saat membaca paper?

**Jawaban:**
> Sebelum mempelajari materi ini, saya cenderung menganggap angka akurasi tinggi sebagai jaminan kualitas sebuah sistem. Setelah memahami rantai distorsi, saya menyadari bahwa angka tersebut bisa saja bias. Pertanyaan yang akan saya ajukan sekarang adalah: "Bagaimana kondisi lingkungan saat data diambil, dan apakah metrik yang digunakan benar-benar merepresentasikan keberhasilan sistem dalam kondisi dunia nyata yang tidak menentu?"

