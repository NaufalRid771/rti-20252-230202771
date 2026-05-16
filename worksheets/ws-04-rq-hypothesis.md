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

Gap Statement  : Belum banyak penelitian yang mengintegrasikan multisensor berbasis ESP32 untuk pemilahan sampah anorganik dengan notifikasi real-time yang hemat biaya dan hemat daya.
Research Question:
  Tipe         :  [☑] Comparison  [☑] Improvement  [ ] Exploratory
  Formulasi    :Apakah sistem pemilahan sampah anorganik berbasis ESP32 menggunakan sensor multivariable menghasilkan akurasi klasifikasi dan kecepatan notifikasi real-time yang lebih baik dibanding sistem smart bin berbasis sensor tunggal?
  Variabel IV  : Jenis sistem sensor (sensor tunggal vs multisensor)
  Variabel DV  : Akurasi klasifikasi sampah dan waktu delay notifikasi Telegram
  Metrik       : Accuracy (%)
  Dataset      : Data hasil pengujian prototype smart waste bin pada sampah anorganik (plastik, kaleng, kaca)
  Baseline     : ESP32 + ultrasonic sensor pada penelitian smart bin sebelumnya

Quality Check RQ:
  [ ☑ ] Variabel spesifik
  [ ☑] Metrik jelas
  [ ☑ ] Baseline ada
  [ ☑ ] Konteks disebutkan
  [ ☑ ] Memerlukan eksperimen (bukan hanya survei literatur)

Contribution Statement:
  Apa yang baru diketahui :Penggunaan multisensor pada ESP32 dapat meningkatkan akurasi pemilahan sampah dan mempertahankan sistem notifikasi real-time dengan biaya rendah.
  Jenis kontribusi        : [☑] Improvement  [☑] Comparison  [ ] Novel approach
  Gap yang diisi          : Keterbatasan penelitian smart waste sebelumnya yang hanya menggunakan sensor tunggal dan belum optimal pada implementasi low-cost.

Hypothesis Pair:
  H₀ :Tidak ada perbedaan signifikan pada akurasi klasifikasi dan delay notifikasi antara sistem smart waste berbasis sensor tunggal dan multisensor pada ESP32.
  H₁ : Sistem smart waste berbasis multisensor pada ESP32 menghasilkan akurasi klasifikasi lebih tinggi dan delay notifikasi lebih rendah dibanding sistem sensor tunggal.
  Threshold              : 
  Akurasi meningkat minimal 10%
  Delay notifikasi ≤ 2 detik
  Justifikasi threshold  : Threshold ditentukan berdasarkan rata-rata performa penelitian smart bin sebelumnya yang memiliki akurasi sekitar 80–85% dan delay notifikasi 2–3 detik.

---

## Latihan 1 — Dari Gap ke RQ

Gunakan gap yang ditemukan di WS-03. Transformasikan menjadi Research Question.

**Gap dari WS-03:** 
Belum ada sistem smart waste low-cost berbasis ESP32 yang mengintegrasikan multisensor untuk meningkatkan akurasi pemilahan sampah anorganik secara real-time.

**RQ versi pertama (tulis bebas):**
> Apakah penggunaan multisensor pada ESP32 dapat meningkatkan performa smart waste sorting?

**Evaluasi RQ:**

| Komponen | Ada? | Isi |
|----------|------|-----|
| Metode spesifik |  Ya |Sensor tunggal vs multisensor |
| Metrik terukur |Ya |Accuracy dan delay |
| Baseline |Ya |Smart bin sensor tunggal |
| Dataset/konteks |Ya |Sampah anorganik pada prototype IoT |

**Tipe RQ:** [ ☑] Comparison / [ ☑] Improvement / [ ] Exploratory

**RQ versi revisi (setelah evaluasi):**
> Apakah sistem pemilahan sampah anorganik berbasis ESP32 menggunakan sensor multivariable menghasilkan accuracy lebih tinggi dan delay notifikasi lebih rendah dibanding sistem smart bin berbasis sensor tunggal?
---

## Latihan 2 — Hypothesis Pair

Rumuskan pasangan hipotesis dari RQ di Latihan 1.

| Komponen | Isi |
|----------|-----|
| H₀ | Tidak ada perbedaan signifikan accuracy dan delay antara sistem sensor tunggal dan multisensor|
| H₁ | Sistem multisensor menghasilkan accuracy lebih tinggi dan delay lebih rendah|
| Metrik |Accuracy (%) dan delay (detik) |
| Threshold |Accuracy naik ≥10%, delay ≤2 detik |
| Justifikasi threshold | Berdasarkan performa rata-rata penelitian smart bin sebelumnya|

**Apakah hipotesis ini falsifiable?** [ ✓ ] Ya / [ ] Tidak
> Bagaimana cara membuktikannya salah? Dengan melakukan eksperimen pada kedua sistem
(sensor tunggal dan multisensor) menggunakan dataset
dan kondisi pengujian yang sama.
Jika hasil statistik menunjukkan tidak ada peningkatan
signifikan pada accuracy atau delay,
maka H₁ ditolak dan H₀ diterima.
---

## Latihan 3 — Rantai Operasionalisasi

Lengkapi rantai dari RQ hingga metode analisis.

| Tahap | Isi |
|-------|-----|
| RQ | Apakah multisensor ESP32 menghasilkan accuracy lebih tinggi dibanding sensor tunggal? |
| Variable (IV) | *Contoh: Jenis algoritma (CNN vs RF)* |Jenis sistem sensor (sensor tunggal vs multisensor) |
| Variable (DV) |Jenis sistem sensor (sensor tunggal vs multisensor) | 
| Metric | |
| Data source | |
| Analysis method | |

**Apakah rantai lengkap?** [☑ ] Ya / [ ] Tidak
> Jika tidak, tahap mana yang perlu direvisi? ______________

---

## Refleksi

> Ambil satu judul skripsi/paper yang pernah dibaca. Coba ekstrak RQ-nya. Apakah RQ tersebut memenuhi semua komponen (metode, metrik, baseline, konteks)? Jika tidak, apa yang hilang?

**Judul:** 
Smart Waste Bin Berbasis ESP32 dengan Notifikasi Telegram
**RQ yang diekstrak:**
 Apakah sistem smart waste berbasis ESP32 mampu melakukan monitoring kapasitas tempat sampah secara real-time?
**Komponen yang hilang:** 
Belum ada baseline pembanding, metrik performa yang jelas, dan belum ada evaluasi accuracy klasifikasi sampah.