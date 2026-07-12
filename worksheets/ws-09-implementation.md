# WS-09: Implementation & Environment

> **Bab 9 — Implementasi Riset & Kontrol Lingkungan**

---

## Ringkasan Materi

### Implementasi Riset ≠ Coding Biasa

Tujuan implementasi riset bukan membuat software yang berfungsi, melainkan membangun **instrumen pengukuran yang konsisten**. Setiap modul harus di-mapping ke variabel (dari Bab 6), parameter harus config-driven, dan logging aktif dari hari pertama.

> **Mengapa reproducibility penting?** Sains dibangun di atas prinsip verifikasi — temuan harus bisa dikonfirmasi oleh peneliti lain. _Replicability crisis_ yang terjadi di banyak paper riset ML/AI disebabkan oleh environment tidak terdokumentasi: orang lain tidak bisa reproduksi, hasil diragukan, kepercayaan terhadap temuan hilang. Prinsip: **dokumentasi environment = snapshot kredibilitas riset Anda.**

### Reproducible Implementation Model

```
Design → Implementation → Environment Setup → Execution Consistency → Reproducibility → Trustworthy Result
```

Setiap transisi memiliki syarat:
- Design → Implementation: kode sesuai mapping variabel-ke-komponen
- Implementation → Environment: versi, dependency, seed, path, OS eksplisit
- Environment → Consistency: seed terkunci, urutan deterministik
- Consistency → Reproducibility: dokumentasi lengkap
- Reproducibility → Trust: siapa pun ikuti dokumentasi → hasil sama/serupa

### Repeatability vs Reproducibility

| Level | Peneliti | Environment | Hasil |
|-------|---------|-------------|-------|
| **Repeatability** | Sama | Sama | Sama persis |
| **Reproducibility** | Berbeda | Berbeda (ikuti docs) | Sama/serupa |

Capai **repeatability** dulu, baru **reproducibility**.

### Engineering vs Research Perspective

| Aspek | Engineering | Research |
|-------|-----------|---------|
| Tujuan | Sistem berfungsi untuk user | Instrumen pengukuran konsisten |
| Dependency | Update ke terbaru | Lock di versi spesifik |
| Testing | Unit, integration, E2E | Repeatability test (run ulang → sama?) |
| Dokumentasi | User guide, API docs | Environment spec, execution steps, expected output |
| Config | Default masuk akal | Setiap parameter eksplisit & adjustable |

### Jebakan Kognitif

1. Menunda environment setup → bug sulit dilacak
2. Tidak pakai version control → hasil tidak bisa direkonstruksi
3. Menolak Docker/container → "di laptop saya bisa" saat review
   - **Docker** = teknologi container yang "membungkus" aplikasi beserta seluruh dependency-nya dalam satu unit terisolasi. Hasilnya: kode berjalan identik di laptop, server, maupun reviewer lain. Intro singkat: `docker run -v $(pwd):/workspace environment-image python run_experiment.py`
4. 3× hasil sama ≠ repeatable (bisa cache/state tersimpan)

### Dependency Locking

Mengandalkan "install library terbaru" berbahaya: versi berbeda = perilaku berbeda = hasil tidak reproducible. Praktik:
- **Python**: buat `requirements.txt` dengan versi eksplisit: `scikit-learn==1.3.2`, lalu kunci dengan `pip freeze > requirements.txt`
- **Conda**: gunakan `conda env export > environment.yml` untuk snapshot lengkap
- **Node.js/R/Julia**: gunakan `package-lock.json` / `renv.lock` / `Project.toml` — semua fungsi serupa: lock versi + hash

### Istilah Penting

- **Environment Specification** — Deskripsi lengkap: hardware, OS, runtime, library + versi, config, seed
- **Dependency** — Komponen eksternal yang harus di-lock versinya
- **Config-driven** — Parameter dieksternalisasi ke file konfigurasi, bukan hardcode

---

## Template A.9 — Dokumentasi Setup Eksperimen

```
EXPERIMENT SETUP DOCUMENTATION

Hardware
CPU      : AMD Ryzen 3 7320U with Radeon Graphics (2.40 GHz)
RAM      : 8 GB
GPU      : AMD Radeon 610M
Storage  : SSD 477 GB

Software
OS        : Windows 11 Home 64-bit
Runtime   : Python 3.12
Framework : YOLOv8 (Ultralytics), YOLOv5, PyTorch, OpenCV

Dependencies:
| Library     | Version |
| ----------- | ------- |
| Python      | 3.12.x  |
| Ultralytics | 8.4.89  |
| PyTorch     | 2.12.1  |
| Torchvision | 0.27.1  |
| OpenCV      | 5.0.0   |
| NumPy       | 2.5.1   |


Konfigurasi:
Image Size      : 640
Confidence      : 0.25
Device          : CPU
Random Seed     : 42
Model           : YOLOv8 & YOLOv5

Reproducibility Check:
[x] Dependency terdokumentasi
[x] requirements.txt tersedia
[x] Source code di GitHub
[x] Parameter eksperimen tetap
[x] Dataset tetap
```

---

## Latihan 1 — Environment Specification

Dokumentasikan environment untuk eksperimen Anda (boleh environment saat ini atau yang direncanakan).

| Komponen    | Spesifikasi                            |
| ----------- | -------------------------------------- |
| CPU         | AMD Ryzen 3 7320U with Radeon Graphics |
| RAM         | 8 GB                                   |
| GPU         | AMD Radeon 610M                        |
| OS          | Windows 11 Home 64-bit                 |
| Runtime     | Python 3.12                            |
| Framework   | Ultralytics YOLOv8, YOLOv5             |
| Random Seed | 42                                     |
                                          |

**Dependencies (minimal 5):**

| Library     | Version | Alasan                   |
| ----------- | ------- | ------------------------ |
| Python      | 3.12.x  | Bahasa pemrograman utama |
| Ultralytics | 8.4.89  | Framework YOLOv8         |
| PyTorch     | 2.12.1  | Framework Deep Learning  |
| Torchvision | 0.27.1  | Mendukung model YOLOv5   |
| OpenCV      | 5.0.0   | Pemrosesan video CCTV    |
| NumPy       | 2.5.1   | Operasi numerik          |





---

## Latihan 2 — Repeatability Test Plan

Eksperimen dijalankan sebanyak 3 kali untuk setiap video pada kedua model dengan konfigurasi yang sama.

| Run | Model  | Video      | Metrik Utama   | Hasil    |
| --- | ------ | ---------- | -------------- | -------- |
| 1   | YOLOv8 | depan_dprd | Inference Time | Berhasil |
| 2   | YOLOv8 | depan_dprd | Inference Time | Berhasil |
| 3   | YOLOv8 | depan_dprd | Inference Time | Berhasil |


**Jika hasil berbeda, kemungkinan penyebab:**

> Beban CPU berubah selama proses inferensi.
> Versi library berubah.
> Dataset mengalami perubahan.
> Konfigurasi model tidak sama.
> Proses lain berjalan di background.

___________________________________________________

**Checklist kontrol yang sudah diterapkan:**
- [✓] Random seed digunakan
- [✓] Dataset sama
- [✓] Parameter sama
- [✓] Environment sama
- [✓] Model yang digunakan sama
---

## Latihan 3 — README Eksperimen

Tulis README minimum untuk eksperimen Anda (6 komponen wajib).

```
# Judul Eksperimen

# Perbandingan YOLOv8 dan YOLOv5 dalam Deteksi Kendaraan pada Rekaman CCTV untuk Mendukung Smart City di Kabupaten Kebumen
## 1. Environment

CPU : AMD Ryzen 3 7320U

RAM : 8 GB

GPU : AMD Radeon 610M

OS : Windows 11 Home

Python : 3.12

## 2. Installation

pip install ultralytics

pip install torch torchvision

pip install opencv-python

## 3. Data

Dataset menggunakan tiga video CCTV Kabupaten Kebumen:

- depan_dprd.mp4
- depan_pendopo.mp4
- merdeka_timur.mp4

## 4. Execution

YOLOv8

python scripts/run_yolo.py

YOLOv5

python detect.py --weights yolov5s.pt --source dataset/videos/depan_dprd.mp4

## 5. Configuration

Image Size : 640

Confidence Threshold : 0.25

Device : CPU

Seed : 42

## 6. Expected Output

- Video hasil deteksi
- Jumlah kendaraan
- Inference Time
- FPS
- Perbandingan performa YOLOv8 dan YOLOv5
```

---

## Refleksi

> Apakah eksperimen Anda saat ini bisa direproduksi oleh orang lain tanpa bantuan Anda? Komponen apa yang masih hilang?

**Level saat ini:** [x] Repeatability / [ ] Reproducibility / [ ] Belum keduanya
**Komponen yang belum terdokumentasi:**
> Dataset CCTV belum dipublikasikan secara terbuka.
> File requirements.txt perlu disertakan pada repositori GitHub.
> README masih perlu dilengkapi dengan langkah reproduksi eksperimen yang lebih rinci.
> Hasil eksperimen (CSV dan Excel) akan disertakan sebagai data pendukung penelitian.
