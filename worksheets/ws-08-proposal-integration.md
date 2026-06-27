# WS-08: Proposal Integration (UTS)

> **Bab 8 — Proposal & Checkpoint**

---

## Ringkasan Materi

### Proposal = Satu Argumen Utuh

Proposal riset bukan kumpulan bab yang independen. Ia adalah **satu argumen** yang mengalir dari masalah ke rencana solusi. Jika satu koneksi putus, seluruh proposal kehilangan koherensi.

### Integration Map — 6 Koneksi Kritis

```
Problem (Bab 2) → Gap (Bab 3) → RQ & H (Bab 4) → Metrik (Bab 5) → Sistem (Bab 6) → Eksperimen (Bab 7)
```

| Koneksi | Pertanyaan Verifikasi |
|---------|----------------------|
| Problem → Gap | Apakah gap muncul dari analisis literatur terhadap masalah? |
| Gap → RQ | Apakah RQ langsung menjawab gap yang teridentifikasi? |
| RQ → Metrik | Apakah setiap variabel di RQ punya metrik terdefinisi? |
| Metrik → Sistem | Apakah setiap metrik bisa diukur oleh komponen sistem? |
| Sistem → Eksperimen | Apakah desain eksperimen menggunakan sistem sebagai instrumen? |

### Koherensi Vertikal + Horizontal

- **Vertikal** — Alur logis atas-ke-bawah (problem → experiment). Setiap section menjawab pertanyaan yang diangkat section sebelumnya dan memunculkan pertanyaan baru.
- **Horizontal** — Konsistensi terminologi (nama variabel di RQ = di hipotesis = di metrik = di desain)

**Operasionalisasi Red Thread** (benang merah):
```
Bab 2 (Problem) → | memperkenalkan masalah X + evidensi |
                          ↓ menimbulkan pertanyaan: "apa akar gap-nya?"
Bab 3 (Gap)     → | menjawab pertanyaan tadi + membuka "lalu apa yang perlu diteliti?" |
                          ↓
Bab 4 (RQ/H)    → | menjawab gap dengan pertanyaan spesifik + prediksi terukur |
                          ↓
Bab 5-7 (Method)→ | menjawab RQ melalui desain eksperimen yang tepat |
```
Jika ada lompatan (section B tidak menjawab pertanyaan section A), red thread putus.

### Jebakan Kognitif

| Jebakan | Deskripsi |
|---------|----------|
| "Selling" Introduction | Menulis promosi, bukan menyajikan data dan gap |
| Copy-paste Methodology | Menyalin deskripsi tekstbook tanpa menyesuaikan ke RQ |
| Optimistic Timeline | Meremehkan waktu implementasi; selalu tambah buffer 30-50% |
| No Possibility of Failure | Mengimplikasikan hasil pasti sukses — proposal jujur mengakui H₀ mungkin tidak ditolak |

### Struktur Proposal

1. **Pendahuluan** — Latar belakang + problem statement (Bab 1-2)
2. **Tinjauan Pustaka** — Literature review + gap + baseline (Bab 3)
3. **RQ / Kontribusi / Hipotesis** — (Bab 4)
4. **Metodologi** — Metrik + sistem + desain eksperimen (Bab 5-7)
5. **Timeline & Output**

### Istilah Penting

- **Integration Map** — Diagram 6 koneksi kritis antar komponen proposal
- **Vertical Coherence** — Alur logis atas-ke-bawah
- **Horizontal Coherence** — Konsistensi terminologi di semua bagian
- **Checkpoint** — Titik self-assessment sebelum transisi dari desain ke eksekusi

---

## Template A.8 — Integration Checklist

```
PROPOSAL INTEGRATION CHECKLIST

Koneksi Vertikal (Flow Atas-Bawah):
  [ ] Problem → Gap: masalah terdokumentasi di literatur
  [ ] Gap → RQ: pertanyaan menjawab gap spesifik
  [ ] RQ → Hypothesis: hipotesis memprediksi jawaban
  [ ] Hypothesis → Metric: metrik mengukur variabel dalam hipotesis
  [ ] Metric → System: komponen sistem menghasilkan/mengukur metrik
  [ ] System → Experiment: desain eksperimen menggunakan sistem

Koneksi Horizontal (Konsistensi):
  [ ] Istilah sama di semua bagian
  [ ] Variabel di RQ = variabel di hipotesis = metrik di desain
  [ ] Scope tidak berubah dari masalah ke eksperimen

Cognitive Trap Checklist:
  [ ] Tidak ada paragraf "promosi" di pendahuluan (hanya data & gap)
  [ ] Metodologi disesuaikan ke RQ, bukan copy-paste textbook
  [ ] Timeline sudah ditambah buffer 30-50% dari estimasi awal
  [ ] Proposal mengakui kemungkinan H0 tidak ditolak (honest uncertainty)
  [ ] Tidak ada klaim "pasti berhasil" atau "meningkatkan signifikan"

Rubrik Self-Assessment:
| Kriteria     | 1 (Lemah)                                        | 2 (Cukup)                                     | 3 (Baik)                                           | Skor |
|------------- |--------------------------------------------------|-----------------------------------------------|----------------------------------------------------|------|
| Koherensi    | >2 koneksi vertikal terputus                     | 1-2 koneksi lemah, argumen masih bisa diikuti | Semua 6 koneksi terhubung, red thread jelas        |      |
| Specificity  | Variabel/metrik masih abstrak, tidak ada angka   | Sebagian metrik terdefinisi numerik           | Semua metrik + threshold + unit pengukuran jelas   |      |
| Feasibility  | Timeline >6 bulan tanpa memperhitungkan sumber   | Timeline 3-6 bulan dengan asumsi tertentu     | Timeline 1-3 bulan realistis dengan rencana detail |      |
| Rigor        | Baseline tidak jelas atau straw man              | 1-2 baseline dengan justifikasi partial       | 2+ baseline SOTA + justifikasi pemilihan lengkap   |      |
```

---

## Latihan 1 — Kompilasi Proposal Mini

Kumpulkan hasil dari WS-02 sampai WS-07 menjadi satu ringkasan proposal.

| Komponen | Sumber | Isi (1-2 kalimat) |
|----------|--------|-------------------|
| Problem Statement | WS-02 | Pengelolaan sampah masih banyak dilakukan secara manual sehingga proses pemilahan sampah anorganik kurang efisien dan sering terjadi kesalahan klasifikasi. Sistem berbasis IoT diperlukan untuk membantu proses pemilahan secara otomatis dan real-time.|
| Gap | WS-03 | Sebagian besar penelitian hanya menggunakan sensor tunggal dan belum banyak mengintegrasikan multisensor dengan notifikasi Telegram real-time untuk meningkatkan akurasi klasifikasi dan monitoring.|
| RQ | WS-04 | Apakah sistem pemilahan sampah anorganik berbasis ESP32 menggunakan sensor multivariable menghasilkan akurasi klasifikasi dan delay notifikasi yang lebih baik dibanding sistem sensor tunggal? |
| Hipotesis | WS-04 | H₁: Sistem multisensor berbasis ESP32 menghasilkan accuracy lebih tinggi dan delay notifikasi lebih rendah dibanding sistem sensor tunggal. |
| Variabel & Metrik | WS-05 | IV = jenis sensor (single sensor vs multisensor). DV = accuracy klasifikasi (%) dan delay notifikasi (detik). CV = jenis sampah dan kondisi jaringan. |
| Sistem | WS-06 |Sistem terdiri dari ESP32, sensor multivariable, modul klasifikasi sampah, WiFi, dan Telegram Bot untuk notifikasi real-time. |
| Desain Eksperimen | WS-07 |Comparison study antara sensor tunggal dan multisensor menggunakan kondisi pengujian yang sama, dengan metrik accuracy dan delay notifikasi. |

---

## Latihan 2 — Integration Checklist

Verifikasi 6 koneksi kritis. Isi dengan merujuk tabel di Latihan 1.

| Koneksi | Status | Bukti |
|---------|--------|-------|
| Problem → Gap |✅ Literatur menunjukkan sistem pemilahan otomatis masih memiliki keterbatasan pada penggunaan sensor tunggal dan monitoring real-time. | |
| Gap → RQ |✅ RQ secara langsung menguji apakah multisensor dapat mengatasi keterbatasan tersebut.| |
| RQ → Hypothesis |✅ Hipotesis memprediksi peningkatan accuracy dan penurunan delay notifikasi.| |
| Hypothesis → Metric |✅ | Accuracy (%) dan delay (detik) digunakan untuk menguji hipotesis.|
| Metric → System |✅ | ESP32 dan Telegram Bot menghasilkan data accuracy dan delay yang dapat diukur.|
| System → Experiment | ✅|Sistem digunakan sebagai alat eksperimen untuk membandingkan dua kondisi sensor. |

**Koneksi mana yang paling lemah?**
Problem → Gap
 Menambahkan lebih banyak referensi jurnal terbaru yang menunjukkan keterbatasan sistem pemilahan sampah berbasis sensor tunggal sehingga research gap menjadi lebih valid dan memiliki dasar literatur yang kuat.
**Bagaimana cara memperkuatnya?**
> Menambahkan lebih banyak referensi penelitian yang menunjukkan keterbatasan sensor tunggal sehingga gap menjadi lebih kuat dan berbasis bukti.

**Konsistensi horizontal — apakah istilah dan scope konsisten?** [☑ ] Ya / [ ] Tidak
> Jika tidak, di bagian mana terjadi inkonsistensi? _________

---

## Latihan 3 — Rubrik Self-Assessment

Evaluasi proposal mini menggunakan rubrik.

| Kriteria | Skor (1-3) | Justifikasi |
|----------|-----------|-------------|
| Koherensi | 3 Semua koneksi dari problem hingga eksperimen saling terhubung. | |
| Specificity | 3 Variabel, metrik, dan satuan pengukuran sudah jelas (accuracy %, delay detik). | |
| Feasibility | 3 | Sistem dapat dibuat menggunakan ESP32 dan sensor yang tersedia dengan waktu pengerjaan skripsi normal.|
| Rigor | 2 |Baseline sudah ada (sensor tunggal), namun masih perlu dukungan literatur yang lebih kuat. |

**Skor total:** 11 / 12

**Apakah proposal siap untuk fase eksekusi?** [ ☑] Ya / [ ] Belum
> Jika belum, apa yang perlu diperbaiki? __________________

---

## Refleksi

> Dari seluruh proses WS-01 sampai WS-08, bagian mana yang paling mudah dan paling sulit? Mengapa? Apa yang akan dilakukan berbeda jika mengulang dari awal?

**Bagian termudah:** 
Menentukan variabel, metrik, dan desain sistem karena langsung berasal dari kebutuhan prototype yang dibuat.
**Bagian tersulit:** 
Menentukan research gap dan menyusun research question yang benar-benar didukung oleh literatur.
**Yang akan dilakukan berbeda:**
> Melakukan pencarian literatur lebih sistematis sejak awal sehingga proses identifikasi gap menjadi lebih mudah. Selain itu, dokumentasi paper akan dibuat lebih rapi agar hubungan antara gap, RQ, hipotesis, dan eksperimen lebih jelas.
> ___________________________________________________
