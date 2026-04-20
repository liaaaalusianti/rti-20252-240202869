# WS-02: Problem Statement

> **Bab 2 — Problem Formulation & System Context**

---

## Ringkasan Materi

### Problem Formation Model

Masalah riset melewati 5 tahap transformasi. Melompat langsung dari Reality ke Variable adalah kesalahan paling umum.

```
Reality → Observed Issue (Symptom) → Diagnosed Problem (Root Cause)
→ Researchable Problem (Scoped) → Measurable Variable (Operationalized)
```

### Topic ≠ Problem ≠ Research Problem

| Level | Contoh | Status |
|-------|--------|--------|
| **Topik** | Keamanan IoT | Terlalu luas, tidak bisa diuji |
| **Problem** | MQTT tidak terenkripsi | Spesifik tapi belum riset |
| **Research Problem** | Belum ada studi membandingkan overhead TLS 1.3 vs DTLS pada MQTT di IoT RAM < 64KB | Bisa dirancang eksperimennya |

### Symptom vs Root Cause

Apa yang diamati (gejala) ≠ mengapa terjadi (akar masalah). Gunakan **5 Whys** atau **Fishbone Diagram** untuk menggali.

Contoh: "User meninggalkan checkout" (symptom) → "Waktu loading > 8 detik karena API call sequential" (root cause).

### System Thinking

Setiap masalah riset TI harus terikat pada komponen sistem: **Input → Process → Output → Outcome → Constraints → Stakeholders**.

### Problem Quality Check

Masalah riset yang layak harus memenuhi 5 kriteria:
- **Clarity** — Satu orang membaca akan paham
- **Measurability** — Ada metrik kuantitatif
- **Relevance** — Penting untuk domain
- **Testability** — Bisa gagal (falsifiable)
- **Impact** — Ada kontribusi jika terjawab

### Research vs Engineering

| Aspek | Engineering | Research |
|-------|------------|----------|
| Tujuan | Menyelesaikan masalah (*solve*) | Memahami dan membuktikan (*understand & prove*) |
| Masalah | Bug, error, fitur belum ada | Gap dalam pengetahuan |
| Scope | Selesaikan semua yang perlu | Batasi agar bisa dibuktikan |
| Output | Working system | Evidence, paper, replicable findings |

### Istilah Penting

- **Problem Statement** — Formulasi tertulis: konteks sistem + gap + dampak + justifikasi
- **System Context** — Deskripsi lengkap: input, proses, output, outcome, constraints, stakeholders
- **Problem Drift** — Masalah "bermutasi" dari pendahuluan ke metodologi karena statement awal tidak presisi
- **Solution-First Thinking** — Memulai dari solusi tanpa masalah yang jelas — berbahaya dalam riset
- **Operational Definition** — Definisi variabel yang cukup jelas agar peneliti lain bisa mengukur hal yang sama

---

## Template A.2 — Problem Statement Builder

```
PROBLEM STATEMENT BUILDER

Domain & Konteks
  Domain   : Internet of Things (IoT) & Smart Agriculture
  Konteks  : Otomasi sistem pertanian hidroponik pada lingkungan dengan akses listrik terbatas.

System Context
  Input       : Data suhu dan kelembapan dari sensor DHT22, energi dari panel surya.
  Process     : Pengolahan data oleh Arduino Uno untuk menentukan aktivasi pompa/kipas.
  Output      : Status aktivasi perangkat (on/off), data yang dikirim ke dashboard IoT.
  Outcome     : Stabilitas suhu dan kelembapan pada lingkungan tanaman hidroponik.
  Constraints : Kapasitas baterai terbatas, ketergantungan pada cuaca, biaya sensor.
  Stakeholders: Petani urban, pengembang sistem IoT, peneliti pertanian cerdas.

Fenomena → Problem
  Fenomena yang diamati             : Kegagalan panen hidroponik akibat fluktuasi suhu dan kelalaian penyiraman manual.
  Gejala (symptom) yang terukur     : Angka kematian bibit mencapai 30% pada kondisi cuaca ekstrem.
  Masalah yang didiagnosis          : Kurangnya pemantauan real-time dan sistem respon otomatis yang mandiri energi.
  Masalah riset (researchable)      : Bagaimana efektivitas integrasi sensor DHT22 dan algoritma thresholding pada sistem bertenaga surya dalam menjaga kestabilan parameter lingkungan hidroponik?
  Variabel yang terukur             : Akurasi pembacaan sensor (Celsius/%RH), konsumsi daya (Watt), dan waktu respon sistem (detik).

Problem Quality Check
  [x ] Clarity — Apakah satu orang membaca akan paham? Pernyataan masalah sudah jelas menghubungkan antara kendala energi (panel surya) dengan kebutuhan otomasi suhu pada hidroponik. Satu orang pembaca dapat langsung memahami bahwa fokus riset adalah kemandirian sistem dalam menjaga lingkungan tanaman.
  [ x] Measurability — Apakah ada metrik kuantitatif? Ada metrik yang jelas dan dapat dihitung, yaitu derajat fluktuasi suhu (°C), persentase kelembapan (%RH), dan durasi ketersediaan daya baterai (jam).
  [ x] Relevance — Apakah penting untuk domain? Sangat relevan bagi domain Smart Agriculture dan IoT, terutama untuk mencari solusi pertanian di lokasi yang tidak terjangkau jaringan listrik PLN (off-grid).
  [ x] Testability — Apakah bisa gagal? Riset ini bersifat falsifiable (bisa dibuktikan salah). Sistem bisa dianggap gagal jika panel surya tidak mampu mengisi daya baterai dengan cukup atau jika suhu lingkungan tetap berada di luar ambang batas ideal tanaman meskipun pompa sudah aktif.
  [ x] Impact — Apakah ada kontribusi jika terjawab? Jika terjawab, riset ini berkontribusi memberikan model teknis prototipe hidroponik yang efisien dan murah untuk diterapkan oleh petani lokal atau UMKM di sektor pertanian.

Problem Statement (1 paragraf):
Sistem pertanian hidroponik seringkali mengalami kegagalan akibat ketidakstabilan parameter lingkungan dan keterbatasan akses energi listrik di lokasi lahan. Penelitian ini bertujuan untuk mengatasi masalah tersebut melalui rancang bangun sistem IoT berbasis Arduino yang mengintegrasikan energi terbarukan panel surya dan otomasi sensor DHT22. Fokus riset adalah menguji sejauh mana sistem ini dapat secara konsisten menjaga ambang batas suhu dan kelembapan secara mandiri tanpa intervensi manual yang berkelanjutan.
```

---

## Latihan 1 — Dari Topik ke Masalah Riset

Pilih satu topik di bidang TI yang diminati. Transformasikan melalui 5 tahap Problem Formation Model.

**Topik awal:** Otomasi IoT di Sektor Pertanian

| Tahap | Hasil |
|-------|-------|
| Reality |Tanaman hidroponik membutuhkan pengawasan ketat terhadap suhu dan air. |
| Observed Issue (Symptom) |Tanaman layu karena suhu di atas 30°C yang tidak segera ditangani secara manual. |
| Diagnosed Problem (Root Cause) |Tidak adanya mekanisme pendinginan otomatis yang bekerja 24 jam karena kendala daya listrik lokal.|
| Researchable Problem |Analisis performa sistem kontrol otomatis berbasis IoT dalam menstabilkan suhu mikro lingkungan hidroponik. |
| Measurable Variable |Derajat fluktuasi suhu (°C) dan durasi ketersediaan daya baterai panel surya (jam). |

**Apakah terjebak solution-first thinking?** [ ] Ya / [ x] Tidak
> Jika ya, kembali ke tahap mana? 

---

## Latihan 2 — System Context Decomposition

Gambarkan konteks sistem dari masalah riset di Latihan 1.

| Komponen | Deskripsi |
|----------|----------|
| Input | Data suhu/kelembapan udara, intensitas cahaya matahari, tegangan baterai. |
| Process |Logika perbandingan (IF-THEN) pada mikrokontroler untuk kendali aktuator. |
| Output |Tampilan data pada layar LCD atau aplikasi, semprotan air/kipas yang menyala. |
| Outcome |Lingkungan tumbuh tanaman yang optimal secara otomatis. |
| Constraints |Keakuratan sensor yang terbatas dan fluktuasi cuaca yang menghambat pengisian daya. |
| Stakeholders |Pemilik kebun hidroponik, penyedia solusi teknologi pertanian cerdas. |

**Komponen mana yang paling relevan dengan masalah riset?** Process (Logika otomasi) dan Constraints (Energi terbatas).

---

## Latihan 3 — Problem Quality Check

Evaluasi problem statement yang sudah dibuat menggunakan 5 kriteria.

| Kriteria | Skor (1-5) | Justifikasi |
|----------|-----------|-------------|
| Clarity |5 |Sangat jelas antara variabel input (IoT/Panel surya) dan output (stabilitas hidroponik). |
| Measurability | 5|Menggunakan angka eksak untuk suhu, kelembapan, dan daya listrik.|
| Relevance |4 |Sangat relevan dengan isu smart farming dan energi hijau saat ini. |
| Testability |5 |Hasilnya bisa terukur gagal jika sistem mati atau suhu tetap tinggi. |
| Impact | 4|Memberikan bukti nyata efisiensi teknologi IoT untuk UMKM tani. |

**Skor total:** 23 / 25

**Problem statement versi final (1 paragraf):**
> Ketidakmampuan menjaga parameter lingkungan secara real-time menjadi penyebab utama rendahnya produktivitas hidroponik, terutama di area yang kekurangan infrastruktur listrik. Riset ini mengusulkan solusi berupa sistem otomasi cerdas berbasis IoT yang ditenagai panel surya untuk memastikan kontrol suhu dan kelembapan berjalan secara otonom. Melalui pengujian fungsionalitas artefak, penelitian ini akan membuktikan apakah integrasi teknologi ini dapat menurunkan fluktuasi suhu lingkungan tanaman sekaligus mempertahankan ketersediaan daya sistem secara berkelanjutan.

---

## Refleksi

> Bandingkan "masalah" yang biasa ditemui saat coding (bug, error) dengan masalah riset. Apa perbedaan fundamental dalam cara mendefinisikan dan mendekati keduanya?

**Jawaban:**
> Perbedaan fundamentalnya terletak pada tujuan akhirnya. Saat coding (engineering), masalah didefinisikan sebagai "bug" yang harus segera diperbaiki agar sistem jalan. Namun dalam riset, masalah didefinisikan sebagai "gap" atau ketidaktahuan. Saat coding kita bertanya "Bagaimana cara menyambungkan sensor ini ke Arduino?", sedangkan dalam riset kita bertanya "Apakah sensor ini cukup akurat dan stabil untuk menjaga ekosistem tanaman dalam jangka panjang?". Riset mencari bukti ilmiah, bukan sekadar memperbaiki fungsi.
