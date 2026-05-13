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
  Domain   :Internet of Things (IoT) 
  Konteks  :SISTEM PEMILAHAN SAMPAH ANORGANIK BERBASIS ESP32 MENGGUNAKAN SENSOR MULTIVARIABLE DENGAN NOTIFIKASI REAL-TIME VIA TELEGRAM


System Context
  Input       : Data sensor untuk mendeteksi jenis sampah anorganik (logam, plastik, kaca, dll.)
  Process     :ESP32 memproses data sensor multivariable untuk mengidentifikasi dan memilah jenis sampah

  Output      : ESP32 memproses data sensor multivariable untuk mengidentifikasi dan memilah jenis sampah
  Outcome     : Proses pemilahan sampah menjadi lebih cepat, efisien, dan mengurangi kesalahan manual
  Constraints :Akurasi sensor, keterbatasan daya ESP32, kondisi lingkungan, koneksi internet
  Stakeholders: Pengelola bank sampah, masyarakat, peneliti IoT, petugas kebersihan
Fenomena → Problem
  Fenomena yang diamati             : Pemilahan sampah anorganik masih dilakukan secara manual dan sering tidak akurat
  Gejala (symptom) yang terukur     : Tingkat kesalahan pemilahan sampah tinggi dan proses membutuhkan waktu lama
  Masalah yang didiagnosis          : Sistem manual tidak mampu melakukan identifikasi sampah secara konsisten dan real-time
  Masalah riset (researchable)      : Belum terdapat implementasi sistem pemilahan sampah anorganik berbasis ESP32 menggunakan sensor multivariable dengan integrasi notifikasi real-time Telegram yang diuji pada aspek akurasi dan respons sistem
  Variabel yang terukur             : Akurasi klasifikasi sampah, waktu respons sistem, keberhasilan notifikasi Telegram, dan konsumsi daya ESP32

Problem Quality Check
  [✓ ] Clarity — Apakah satu orang membaca akan paham?
  [✓ ] Measurability — Apakah ada metrik kuantitatif?
  [✓ ] Relevance — Apakah penting untuk domain?
  [✓] Testability — Apakah bisa gagal?
  [✓ ] Impact — Apakah ada kontribusi jika terjawab?

Problem Statement (1 paragraf):
 Pemilahan sampah anorganik di lingkungan masyarakat masih banyak dilakukan secara manual sehingga sering menimbulkan kesalahan klasifikasi dan membutuhkan waktu yang relatif lama. Kondisi ini menyebabkan proses pengelolaan sampah menjadi kurang efisien dan berpotensi mengurangi efektivitas daur ulang. Meskipun teknologi Internet of Things (IoT) telah banyak diterapkan dalam sistem otomasi, belum banyak penelitian yang mengimplementasikan sistem pemilahan sampah anorganik berbasis ESP32 menggunakan sensor multivariable dengan notifikasi real-time melalui Telegram. Oleh karena itu, penelitian ini bertujuan untuk merancang dan menganalisis performa sistem pemilahan sampah otomatis berdasarkan tingkat akurasi identifikasi, waktu respons sistem, keberhasilan pengiriman notifikasi, serta efisiensi penggunaan perangkat ESP32.
```

---

## Latihan 1 — Dari Topik ke Masalah Riset

Pilih satu topik di bidang TI yang diminati. Transformasikan melalui 5 tahap Problem Formation Model.

**Topik awal:** Sistem pemilahan sampah anorganik berbasis ESP32 menggunakan sensor multivariable dengan notifikasi Telegram
| Tahap | Hasil |
|-------|-------|
| Reality | *Contoh: Aplikasi e-commerce sering ditinggalkan saat checkout* |
| Observed Issue (Symptom) | *Contoh: Bounce rate checkout 68%* |
| Diagnosed Problem (Root Cause) | |
| Researchable Problem | |
| Measurable Variable | |

**Apakah terjebak solution-first thinking?** [ ] Ya /  [x] Tidak
> Jika ya, kembali ke tahap mana? ________________________

---

## Latihan 2 — System Context Decomposition

Gambarkan konteks sistem dari masalah riset di Latihan 1.

| Komponen | Deskripsi |
|----------|----------|
| Input | Data dari sensor multivariable untuk mendeteksi jenis sampah anorganik |
| Process |ESP32 memproses data sensor dan mengontrol mekanisme pemilahan sampah serta pengiriman notifikasi Telegram |
| Output |Sampah berhasil dipilah sesuai jenisnya dan notifikasi terkirim secara real-time |
| Outcome | Meningkatkan efisiensi dan akurasi proses pemilahan sampah anorganik|
| Constraints |Akurasi sensor, keterbatasan daya ESP32, koneksi internet, dan kondisi lingkungan |
| Stakeholders |Pengelola bank sampah, petugas kebersihan, masyarakat, dan peneliti IoT |

**Komponen mana yang paling relevan dengan masalah riset?** Proses dan Output

---

## Latihan 3 — Problem Quality Check

Evaluasi problem statement yang sudah dibuat menggunakan 5 kriteria.

| Kriteria | Skor (1-5) | Justifikasi |
|----------|-----------|-------------|
| Clarity | Problem statement sudah spesifik dan mudah dipahami | |
| Measurability |Variabel seperti akurasi sensor, waktu respons, dan notifikasi dapat diukur | 
| Relevance |Sangat relevan dengan bidang IoT dan pengelolaan sampah | |
| Testability |Sistem dapat diuji melalui implementasi dan eksperimen perangkat | |
| Impact |Penelitian berpotensi meningkatkan efisiensi pemilahan sampah otomatis | |

**Skor total:** 24 / 25

**Problem statement versi final (1 paragraf):**
> > Pemilahan sampah anorganik yang masih dilakukan secara manual sering menyebabkan kesalahan klasifikasi dan membutuhkan waktu yang lama sehingga proses pengelolaan sampah menjadi kurang efisien. Hingga saat ini, belum banyak penelitian yang mengimplementasikan sistem pemilahan sampah otomatis berbasis ESP32 menggunakan sensor multivariable dengan integrasi notifikasi real-time melalui Telegram. Oleh karena itu, penelitian ini dilakukan untuk menganalisis performa sistem berdasarkan tingkat akurasi identifikasi sampah, waktu respons sistem, keberhasilan pengiriman notifikasi, dan efisiensi penggunaan perangkat ESP32 dalam proses pemilahan sampah anorganik.

>

---

## Refleksi

> Bandingkan "masalah" yang biasa ditemui saat coding (bug, error) dengan masalah riset. Apa perbedaan fundamental dalam cara mendefinisikan dan mendekati keduanya?

**Jawaban:**
> Masalah saat coding biasanya berupa bug, error, atau fungsi sistem yang tidak berjalan sesuai harapan sehingga fokus utamanya adalah memperbaiki program agar kembali normal. S
> Sedangkan masalah riset berfokus pada kesenjangan pengetahuan atau keterbatasan solusi yang sudah ada, sehingga tujuannya bukan hanya membuat sistem bekerja tetapi juga menghasilkan bukti, analisis, dan pengetahuan baru yang dapat diuji serta dipertanggungjawabkan secara ilmiah.