# WS-03: Literature Mapping & Gap

> **Bab 3 — Literature Review, Research Gap & Baseline**

---

## Ringkasan Materi

### Literature Review = Positioning, Bukan Ringkasan

Literature review bukan merangkum paper satu per satu. Pendekatan yang benar adalah **concept-centric** — organisasi berdasarkan tema, metode, atau variabel. Tujuan: menemukan **pola, kontradiksi, dan gap**.

**Perbandingan pendekatan Author-centric vs Concept-centric:**

| Aspek | Author-centric (Hindari) | Concept-centric (Gunakan) |
|-------|--------------------------|---------------------------|
| Struktur | Per penulis/paper ("Rahman et al. menyatakan...") | Per konsep/metode ("Pendekatan berbasis transformer") |
| Tujuan | Ringkasan isi paper | Perbandingan metode & identifikasi gap |
| Contoh paragraph | "Rahman (2023) pakai CNN. Lee (2022) pakai LSTM. Zhang (2021) pakai RF." | "Tiga pendekatan dominan: CNN digunakan oleh 4 paper untuk representasi fitur visual; LSTM untuk data sekuensial; RF sebagai baseline klasik." |
| Hasil akhir | Daftar paper | Peta pengetahuan + gap yang teridentifikasi |

### Empat Jenis Research Gap

| Jenis Gap | Deskripsi | Contoh |
|-----------|----------|--------|
| **Performance Gap** | Performa belum memadai | Akurasi deteksi hanya 78% pada kasus tertentu |
| **Method Gap** | Pendekatan belum diterapkan | Belum ada yang pakai transformer untuk task ini |
| **Data Gap** | Dataset terbatas/tidak representatif | Semua studi pakai dataset sintetis |
| **Context Gap** | Belum diuji pada konteks berbeda | Belum ada evaluasi di negara berkembang |

Gap terkuat = kombinasi 2+ jenis.

### Systematic Search Strategy

1. **Database utama**: IEEE Xplore, ACM DL, Scopus
   - Akses IEEE/ACM melalui jaringan kampus atau VPN institusi
   - Alternatif bebas biaya: Google Scholar, ResearchGate ([researchgate.net](https://www.researchgate.net)), arXiv ([arxiv.org](https://arxiv.org))
2. **Boolean query** yang terdokumentasi eksplisit
   - Contoh: `("anomaly detection" OR "intrusion detection") AND ("deep learning" OR "neural network") NOT ("medical imaging")`
   - Gunakan tanda kutip untuk frasa eksak; AND/OR/NOT mengontrol scope
3. **Snowballing** — dua arah:
   - **Backward snowballing**: buka daftar referensi di paper kunci → telusuri paper yang dikutip
   - **Forward snowballing**: di Google Scholar, klik "Cited by" di bawah paper kunci → temukan paper yang mengutipnya
   - Ulangi 1–2 tingkat untuk membangun cakupan komprehensif
4. Klaim "belum ada penelitian" harus didukung **bukti pencarian**

### Baseline Selection — 3 Kriteria

| Kriteria | Pertanyaan | 
|----------|-----------|
| **Relevan** | Apakah menyelesaikan masalah yang sama? |
| **Representatif** | Apakah mewakili common practice? |
| **State-of-the-Art** | Apakah terbaru/terbaik? |

Membandingkan deep learning 2024 dengan decision tree sederhana tanpa justifikasi = **straw man comparison** (perbandingan tidak jujur).

### Research vs Engineering

| Aspek | Engineering | Research |
|-------|------------|----------|
| Tujuan baca literatur | Mencari solusi yang sudah ada | Memahami apa yang belum terjawab |
| Cara membaca paper | Tutorial, how-to | Metode, limitasi, gap |
| Baseline | Framework terpopuler | State-of-the-art yang rigorous |
| Dokumentasi pencarian | Tidak diperlukan | Wajib (reproducible) |

### Istilah Penting

- **Concept-centric** — Organisasi literatur berdasarkan konsep/metode, bukan per penulis
- **Snowballing** — Backward (telusuri referensi) + Forward (cari yang mengutip paper kunci)
- **Research Position** — Pernyataan eksplisit posisi riset terhadap studi sebelumnya
- **Straw man comparison** — Memilih baseline lemah agar metode sendiri terlihat lebih baik

---

## A.3 — Literature Mapping & Gap Identification

```
LITERATURE MAPPING

Topik      : Implementasi AI dalam Sistem Keamanan Kota (IKN) 
Database   : Google Scholar/Portal Jurnal Nasional (.ac.id)
Query      : Artifical Intelligence city security, AI keamanan kota, AI smart city scurity.
Tahun      : 2020-2024
Hasil awal : ±20 paper → Screening → 5-7 paper final

Literature Matrix (concept-centric):

| Study | Tahun | Method | Data | Result | Limitation |
|-------|-------|--------|------|--------|------------|
|Rahmawati et al.       |2024       |literature Review    |jurnal& refrensi skunder   |AI meningkatkan deteksi kejahatan & respon     |Privasi, biaya, keandalan          |
|Lubis|2021| Implementasi AI| Data Manufaktur| AI meningkatkan efisiensi sistem| Tidak fokus ke keamanan kota|
|Zsazsa & Sitepu|2023| Studi AI publik| Data Pelayanan Publik| AI meningkatkan kualitas layanan|Kurang spesifik keamanan|
|ITI Report|2023| Review| Data Skunder| AI punya potensi besar| Tantangan SDM & teknologi|
|Purnama & Chotib|2022| Analisis kebijakan| Data Kebijakan| Dukungan pemerintah penting| Tidak bahas teknis AI|
Pola yang ditemukan:
  Metode dominan     : Literature Review & Analisis konseptual
  Dataset umum       : Data sekunder(jurnal, laporan, kebijakan)
  Limitasi berulang  : 1. Privasi data 
                       2. Biaya implementasi tinggi
                       3. SDM belum siap
                       4. keandalan sistem AI
GAP IDENTIFICATION

Gap 1: [Jenis:method / impementation]
  Deskripsi    : Penelitian masih dominan berupa literature review, belum banyak implementasi sistem nyata.
  Bukti        : Dalam jurnal hanya menggunakan metode literature review, tidak menyertakan prototipe sistem. 
  Signifikansi : Memerlukan penelitian berbasis implementasi agar solusi bisa diterapkan, bukan hanya teori.

Gap 2: [Jenis:context/integration]
  Deskripsi    : Belum ada integrasi AI dengan sistem real-time berbasis IoT secara optimal.
  Bukti        : dalam jurnal disebutkan bahwa AI masih menghadapi masalah keandalan dan integrasi sistem.
  Signifikansi : integrasi penting untuk monitoring langsung(real-time) di smart city.

Baseline Selection:
| Baseline | Relevansi | Representatif | Source |
|----------|-----------|---------------|--------|
| AI Video Surveillance         |digunakan untuk deteksi aktivitas mencurigakan pada keamanan kota            |  digunakan secara luas dalam peneliatian dan implementasi smart city berbasis AI             |  Rahmawati et al., 2024
|conventional CCTV | sistem keamanan dasar tanpa AI | merupakan sistem standar yang digunakan sebelum AI | sistem umum|
|IoT Monitoring System | digunakan untuk monitoring real -time | banyak digunakan dalam sistem monitoring modrn berbasis IoT | Literatur IoT |    |
```

---

## Latihan 1 — Concept-Centric Literature Table

Gunakan topik riset dari WS-02. Cari minimal 5 paper relevan menggunakan database akademik.

> **Panduan pencarian:**
> - Database: IEEE Xplore, ACM DL, Google Scholar, atau ResearchGate
> - Tulis query Boolean yang digunakan: contoh `("object detection" OR "image classification") AND ("edge computing") NOT ("medical")`. Dokumentasikan query secara eksplisit.
> - Akses gratis: buka Google Scholar → cari judul paper → klik [PDF] jika tersedia, atau akses lewat campus VPN

**Topik riset:** Rancang Bangun Sistem Monitoring dan Otomasi Hidroponik Berbasis IoT dan Panel Surya.
**Query pencarian:** ("Internet of Things" OR "IoT") AND ("Hydroponic" OR "Agriculture") AND ("Solar Panel" OR "Renewable Energy")
**Database:** _Google Scholar / IEEE Xplore.

| # | Study | Tahun | Method | Dataset | Result | Limitasi |
|---|-------|-------|--------|---------|--------|----------|
| 1 | *Contoh: Rahman et al.* | *2023* | *CNN* | *ImageNet subset* | *Acc 91%* | *Hanya 3 kelas* |
| 2 |Fachrizal et al. |2025 |Arduino + DHT22 + Solar Panel |Solar Panel	Real-time sensor log |Prototipe fungsional & mandiri energi |Belum diuji saat cuaca ekstrem (mendung lama) |
| 3 |Pratama et al. |2024 |IoT Cloud + Hybrid Architecture |Architecture	SME Transaction logs |Efisiensi operasional naik 20% |Fokus pada data manajemen, bukan otomasi fisik |
| 4 |Sari & Wijaya |2023 |Fuzzy Logic + NodeMCU |NodeMCU	Sensor pH & TDS |Kontrol nutrisi lebih presisi |Konsumsi daya tinggi, tidak pakai panel surya |
| 5 |Budiman et al. |2024 |ESP32 + LoRa |Long-range sensor data |Transmisi data hingga 2km |Throughput data kecil, tidak cocok untuk video |

**Pola yang terlihat — Metode dominan:** Penggunaan mikrokontroler (Arduino/ESP32) yang dikombinasikan dengan platform Cloud untuk visualisasi data.
**Limitasi yang berulang:** Ketergantungan pada stabilitas energi (baterai) dan akurasi sensor kelas hobi (low-cost) dalam kondisi lapangan.

---

## Latihan 2 — Gap Identification

Berdasarkan tabel di Latihan 1, identifikasi gap.

| Jenis Gap | Ditemukan? | Gap Statement |
|-----------|-----------|---------------|
| Performance Gap | [ x] Ya / [ ] Tidak |Penurunan performa sistem IoT saat tegangan panel surya turun di bawah ambang batas operasional.|
| Method Gap | [ x] Ya / [ ] Tidak |Jarangnya penggunaan algoritma manajemen daya (sleep mode) untuk memperpanjang umur baterai pada hidroponik. |
| Data Gap | [ ] Ya / [x ] Tidak |Data sensor suhu/kelembapan sudah sangat banyak tersedia. |
| Context Gap | [ x] Ya / [ ] Tidak |Minimnya riset yang menguji durabilitas sistem pada lingkungan pertanian dengan kelembapan ekstrem tinggi. |

**Gap utama yang dipilih:** Method Gap & Performance Gap pada manajemen energi.
**Mengapa gap ini penting (bukan sekadar "belum ada yang meneliti")?**
>Karena sistem IoT pertanian yang "cerdas" menjadi tidak berguna jika mati saat tidak ada matahari. Mengoptimalkan cara sistem bekerja berdasarkan sisa daya baterai (manajemen energi) jauh lebih krusial untuk keberlanjutan panen daripada sekadar menambah sensor baru.

---

## Latihan 3 — Baseline Selection

Pilih 2 baseline dari literatur yang sudah dibaca.

| # | Baseline | Mengapa Relevan | Mengapa Representatif | Apakah SOTA? | Sumber |
|---|----------|----------------|----------------------|-------------|--------|
| 1 | Fuzzy Logic Control |Sama-sama mengontrol aktuator (pompa). |Standar untuk kontrol otomatis yang halus. | Ya, untuk kelas mikrokontroler. |Sari & Wijaya (2023) |
| 2 |Sistem Kontrol On/Off Statis |Sama-sama menggunakan threshold suhu. |Metode paling standar di DIY IoT. |Bukan (Metode Dasar) |Fachrizal et al. (2025) |

**Apakah pemilihan baseline ini bisa dianggap straw man?** [ ] Ya / [ x] Tidak
> Justifikasi: Baseline yang dipilih mencakup metode standar (On/Off) dan metode cerdas (Fuzzy), sehingga riset tidak membandingkan diri dengan sistem yang sengaja dibuat lemah, melainkan dengan standar industri dan akademis saat ini.

---

## Refleksi

> Apa perbedaan antara "belum ada yang meneliti ini" (klaim tanpa bukti) dengan research gap yang valid? Bagaimana cara membuktikan bahwa sebuah gap benar-benar ada?

**Jawaban:**
> Perbedaan fundamentalnya terletak pada bukti. Klaim "belum ada yang meneliti" seringkali hanya asumsi karena peneliti malas mencari. Sedangkan research gap yang valid dibuktikan melalui tabel literatur (Latihan 1) yang menunjukkan bahwa meski banyak riset di bidang tersebut, ada aspek spesifik (seperti efisiensi daya pada cuaca ekstrem) yang belum terselesaikan secara optimal. Cara membuktikannya adalah dengan menunjukkan keterbatasan (limitasi) dari penelitian-penelitian terdahulu secara sistematis.
