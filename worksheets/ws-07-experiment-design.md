# WS-07: Experimental Design & Validity

> **Bab 7 — Experimental Design & Validity**

---

## Ringkasan Materi

### Correlation ≠ Causality

Kausalitas membutuhkan 3 syarat:
1. **Covariance** — X dan Y bergerak bersama
2. **Temporal precedence** — X berubah sebelum Y
3. **Elimination of alternatives** — Tidak ada faktor lain yang menjelaskan Y

Controlled experiment adalah satu-satunya metode yang bisa membuktikan kausalitas.

### Empat Jenis Validitas

| Jenis | Pertanyaan | Ancaman Umum |
|-------|-----------|-------------|
| **Internal** | Apakah hubungan IV→DV nyata? | Confounding variable, selection bias |
| **External** | Apakah bisa digeneralisasi? | Dataset terlalu spesifik |
| **Construct** | Apakah mengukur konsep yang benar? | Metrik tidak sesuai |
| **Conclusion** | Apakah kesimpulan statistik valid? | Sample size kecil, uji salah |

Internal dan external validity sering berkonflik: semakin terkontrol (internal kuat) → semakin artificial (external lemah).

### Tiga Tipe Eksperimen dalam Riset TI

| Tipe | Deskripsi | Kapan Digunakan |
|------|----------|----------------|
| **Comparison Study** | Metode A vs B pada kondisi identik | Membandingkan pendekatan berbeda |
| **Ablation Study** | Full system → lepas komponen satu per satu | Mengukur kontribusi tiap komponen |
| **Parameter Study** | Variasikan satu parameter, amati dampak | Uji sensitifitas/robustness |

### Fairness dalam Perbandingan

Perbandingan yang adil = **kondisi identik** untuk semua metode: dataset sama, preprocessing sama, tuning effort sebanding, environment sama, metrik sama.

Contoh tidak adil: Transformer (30 fitur tambahan + Bayesian optimization) vs RF (default params) → hasilnya misleading.

### Threats to Validity = Diidentifikasi Sebelum Eksperimen

Ancaman validitas harus diidentifikasi **sebelum** eksperimen dan mitigasinya dirancang sebagai bagian dari desain — bukan ditulis sebagai boilerplate setelah selesai.

### Research vs Engineering

| Aspek | Engineering | Research |
|-------|------------|----------|
| Tujuan testing | Memastikan sistem memenuhi requirement | Membuktikan hubungan kausal antar variabel |
| Baseline | Versi sebelumnya (last release) | Metode tervalidasi dari literatur |
| Kegagalan | Bug → fix → release | H₀ tidak ditolak → tetap kontribusi ilmiah |
| Sukses | 100% test pass | Evidence valid — mendukung atau menolak hipotesis |

### Istilah Penting

- **Causality** — Hubungan sebab-akibat (covariance + temporal + elimination)
- **Controlled Experiment** — Ubah satu variabel, kontrol sisanya, amati efek
- **Fairness** — Semua metode diuji pada kondisi yang benar-benar identik
- **Threats to Validity** — Faktor yang bisa melemahkan kesimpulan jika tidak dimitigasi
- **Conclusion Validity** — Validitas statistik: power, sample size, uji yang tepat

---

## Template A.7 — Desain Eksperimen Lengkap

EXPERIMENT DESIGN

Research Question : Apakah sistem pemilahan sampah anorganik berbasis ESP32 menggunakan sensor multivariable menghasilkan accuracy klasifikasi dan delay notifikasi yang lebih baik dibanding sistem sensor tunggal?  
Hypothesis        : Sistem multisensor berbasis ESP32 menghasilkan accuracy lebih tinggi dan delay notifikasi lebih rendah dibanding sistem sensor tunggal.  
Tipe Eksperimen   : [✓] Comparison  [✓] Ablation  [ ] Parameter  

Kondisi Eksperimen:
| Kondisi | Deskripsi | IV Value | CV Settings |
|---------|-----------|----------|-------------|
| Control | Sistem smart bin dengan sensor tunggal | Single sensor | Jenis sampah sama, jaringan sama, ESP32 sama |
| Treatment | Jenis sampah sama, jaringan sama, ESP32 sama | Multisensor | Jenis sampah sama, jaringan sama, ESP32 sama |

Fairness Checklist:
  [✓] Dataset identik untuk semua kondisi  
  [✓] Preprocessing setara  
  [✓] Tuning effort setara  
  [✓] Environment identik  
  [✓] Metrik evaluasi sama  

Threat Analysis:
| Threat Type | Ancaman Spesifik | Mitigasi |
|-------------|-----------------|----------|
| Internal    | Kondisi jaringan berubah saat eksperimen | Gunakan jaringan WiFi yang sama |
| External    | Pengujian hanya pada skala laboratorium | Tambahkan pengujian pada lingkungan nyata |
| Construct   | Accuracy belum sepenuhnya menggambarkan kualitas sistem | Tambahkan precision dan recall |
| Conclusion  | Jumlah sampel terlalu sedikit | Lakukan pengujian berulang |

Statistical Plan:
  Uji statistik    : Perbandingan rata-rata accuracy dan delay  
  Justifikasi      : Untuk melihat apakah multisensor memberikan peningkatan performa dibanding baseline sensor tunggal.  
  Alpha            : 0.05  
  Effect size min  : Peningkatan accuracy minimal 10%  

---

## Latihan 1 — Desain Eksperimen

Susun desain eksperimen berdasarkan RQ, variabel, dan sistem dari WS-04 sampai WS-06.

**RQ:** Apakah sistem multisensor berbasis ESP32 meningkatkan accuracy klasifikasi sampah dan mengurangi delay notifikasi dibanding sensor tunggal?  
**Tipe eksperimen:** [✓] Comparison / [✓] Ablation / [ ] Parameter  

| Kondisi | Deskripsi | IV Value | CV Settings |
|---------|-----------|----------|-------------|
| Control | Sistem smart bin sensor tunggal | Single sensor | Sampah sama, WiFi sama, ESP32 sama |
| Treatment | Sistem smart bin multisensor | Multisensor | Sampah sama, WiFi sama, ESP32 sama |

---

## Latihan 2 — Fairness Checklist

Evaluasi apakah desain eksperimen di Latihan 1 sudah fair.

| Kriteria | Status | Detail |
|----------|--------|--------|
| Dataset identik | ✓ | Menggunakan jenis sampah yang sama |
| Preprocessing setara | ✓ | Kondisi pengujian sama |
| Tuning effort setara | ✓ | Tidak ada optimasi khusus pada salah satu metode |
| Environment identik | ✓ | Menggunakan perangkat dan jaringan yang sama |
| Metrik evaluasi sama | ✓ | Sama-sama menggunakan accuracy dan delay |

**Ada yang tidak fair?** [ ] Ya / [✓] Tidak
> Jika ya, bagaimana cara memperbaikinya? ________________

---

## Latihan 3 — Threat Analysis

Identifikasi ancaman validitas untuk desain eksperimen ini.

| Threat Type | Ancaman Spesifik | Mitigasi |
|-------------|-----------------|----------|
| Internal | Delay dipengaruhi koneksi internet | Gunakan jaringan stabil dan sama |
| External | Hanya diuji pada sedikit jenis sampah | Tambah variasi sampah |
| Construct | Accuracy saja belum cukup | Tambahkan precision dan recall |
| Conclusion | Sampel pengujian terlalu sedikit | Perbanyak jumlah eksperimen |

**Ancaman mana yang paling sulit dimitigasi?** External validity
**Mengapa?**
> Karena kondisi dunia nyata sangat beragam sehingga sulit memastikan sistem bekerja sama baiknya di semua lingkungan.

---

## Refleksi

> Sebuah paper melaporkan "metode kami mengalahkan semua baseline." Apa 3 pertanyaan pertama yang harus diajukan untuk mengevaluasi klaim ini?

**Jawaban:**
1. Apakah baseline dibandingkan secara fair dengan kondisi yang sama?  
2. Apakah metrik evaluasi yang digunakan sudah sesuai dan jelas?  
3. Apakah jumlah data dan eksperimen cukup untuk mendukung kesimpulan?  