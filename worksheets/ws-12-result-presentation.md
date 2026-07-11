# WS-12: Result Presentation & Visualization

> **Bab 12 — Penyajian Hasil & Visualisasi**

---

## Ringkasan Materi

### Data → Insight Model

```
Validated Data → Structured Presentation → Visualization → Pattern Recognition → Insight
```

Penyajian **mendahului** analisis. Tabel dan grafik membantu peneliti "melihat" data sebelum menghitung. Langsung ke uji statistik tanpa visualisasi berisiko kesimpulan yang secara teknis benar tapi kontekstual salah (Anscombe's Quartet, 1973).

### Tabel = Presisi, Grafik = Pola

Keduanya **saling melengkapi**:
- Tabel: angka presisi, self-contained (dipahami tanpa teks), sortable
- Grafik: pola visual, tren, perbandingan cepat

### Jenis Grafik Berdasarkan Tujuan

| Tujuan | Jenis Grafik |
|--------|-------------|
| Perbandingan antar-skenario | Bar chart (grouped/stacked) |
| Distribusi per-skenario | Box plot / violin plot |
| Tren temporal | Line chart |
| Korelasi dua variabel | Scatter plot |
| Proporsi (total = 100%) | Pie chart (hati-hati!) |

### Contoh Tabel Hasil yang Baik

| Model | Accuracy (%) | F1-Score (%) | Training Time (min) |
|-------|-------------|-------------|---------------------|
| BERT | 88.4 ± 1.2 | 87.1 ± 1.4 | 45.2 ± 3.1 |
| LSTM | 86.1 ± 1.8 | 84.5 ± 2.0 | 12.8 ± 1.2 |
| SVM | 82.3 ± 0.9 | 80.7 ± 1.1 | 0.3 ± 0.1 |

*N=10 per model. Mean ± std. Diurutkan berdasarkan Accuracy.*

### Visualization Bias — Yang Harus Dihindari

| Bias | Deskripsi | Dampak |
|------|----------|--------|
| Truncated axis | Y tidak dari 0 | Memperbesar perbedaan kecil |
| Inconsistent scale | Dua grafik skala beda | Perbandingan menyesatkan |
| Cherry-picked data | Hanya tampilkan yang "menang" | Selektif, tidak jujur |
| 3D effects | Efek 3D tanpa dimensi data ke-3 | Distorsi tanpa informasi |
| Missing error bar | Tidak ada variabilitas | Menyembunyikan ketidakpastian |

### Engineering vs Research Presentation

| Aspek | Engineering | Research |
|-------|-----------|---------|
| Tujuan grafik | Dashboard monitoring | Mendukung argumen ilmiah |
| Informasi wajib | KPI, threshold | Mean, std, CI, N, p-value |
| Bias handling | Less critical | Wajib dihindari (peer-review) |

---

## Template A.12 — Result Presentation Plan

```
RESULT PRESENTATION PLAN

Research Question : Apakah sistem pemilahan sampah anorganik berbasis ESP32 menggunakan sensor multivariable mampu mendeteksi kondisi tempat sampah secara akurat serta mengirimkan notifikasi Telegram secara real-time?  
Metrik Utama: 
1. Akurasi deteksi sensor (%)
2. Waktu respon notifikasi Telegram (detik)

Tabel Hasil:
| Skenario | Metrik 1 (mean ± std) | Metrik 2 (mean ± std) | n |
|----------|----------------------|----------------------|---|
|Sistem Normal|    98.4 ± 0.6 %   | 1.21 ± 0.15 detik    | 5 |
|Kondisi Penuh|    97.8 ± 0.8 %   | 1.34 ± 0.18 detik    | 5 | 
|Notifikasi Telegram| 100 ± 0.0 % | 1.42 ± 0.22 detik    | 5 |
|Sistem Terintegrasi|98.7 ± 0.5 % | 1.30 ± 0.17 detik    |10 |

Visualisasi yang Direncanakan:
| # | Jenis Grafik | Pesan Utama | Metrik |
|---|-------------|-------------|--------|
| 1 | Bar Chart + Error Bar | Akurasi tiap skenario | Akurasi (%)|
| 2 | Line Chart            | Waktu respon tiap skenario         |  Waktu (detik) |

Waktu respon tiap skenario 
```

---

## Latihan 1 — Tabel Hasil

Buat tabel hasil eksperimen Anda (boleh dengan data simulasi jika belum punya data riil).

| Skenario | Metrik 1 (mean ± std) | Metrik 2 (mean ± std) | n |
|----------|----------------------|----------------------|---|
| Sistem Terintegrasi|98.7 ± 0.5 % |1.30 ± 0.17 detik | 10|
| Sistem Normal      |98.4 ± 0.6 % |1.21 ± 0.15 detik | 5 |
| Kondisi Penuh      |97.8 ± 0.8 % |1.34 ± 0.18 detik | 5 |
| Notifikasi Telegram|100 ± 0.0 %  |1.42 ± 0.22 detik | 5 |

**Checklist tabel:**
- [✔️] Self-contained (judul jelas, satuan ada, N tercantum)
- [✔️] Mean ± std (bukan single number)
- [✔️] Diurutkan berdasarkan metrik utama
- [✔️] Format konsisten di semua baris

---

## Latihan 2 — Rencana Visualisasi

Rencanakan 2-3 grafik untuk menyajikan data dari Latihan 1. Setiap grafik = satu pesan.

| # | Jenis Grafik | Pesan | Data yang Digunakan |
|---|-------------|-------|---------------------|
| 1 | Bar Chart + Error Bar | Membandingkan akurasi deteksi pada setiap skenario pengujian | Mean akurasi ± standar deviasi |
| 2 | Line Chart | Menunjukkan perubahan waktu respon notifikasi Telegram pada setiap skenario | Mean waktu respon |
| 3 | Pie Chart | Menampilkan persentase keberhasilan dan kegagalan pengiriman notifikasi Telegram |Jumlah notifikasi berhasil dan gagal |

---

## Latihan 3 — Bias Detection

Evaluasi visualisasi berikut untuk bias (skenario dari contoh):

**Skenario:** Metode A = 91.2%, Metode B = 90.8%. Bar chart dengan Y-axis mulai dari 90%.

| Pertanyaan | Jawaban |
|-----------|---------|
| Apakah Y-axis menyesatkan? | Ya. Perbedaan terlihat jauh lebih besar daripada kondisi sebenarnya karena sumbu Y tidak dimulai|
| Apakah error bar ditampilkan? | Ya, error bar harus ditampilkan agar variasi hasil setiap pengujian terlihat.|
| Apakah semua kondisi ditampilkan? |Ya, seluruh skenario pengujian harus ditampilkan agar tidak terjadi cherry-picking data. |
| Apa solusinya? |Gunakan sumbu Y yang dimulai dari nol atau berikan alasan yang jelas jika menggunakan skala lain, serta tampilkan error bar pada setiap grafik. |

**Evaluasi grafik Anda sendiri dari Latihan 2:**
- [v] Semua bias check lulus
- [ ] Ada yang perlu diperbaiki: -
---

## Refleksi

> Mengapa tabel dan grafik keduanya diperlukan — tidak cukup salah satu saja? Pernahkah Anda membuat grafik yang (tanpa sengaja) menyesatkan?

> Tabel diperlukan untuk menyajikan nilai hasil eksperimen secara rinci dan presisi, sedangkan grafik membantu memperlihatkan pola, tren, dan perbandingan antar skenario dengan lebih cepat.
> Keduanya saling melengkapi sehingga pembaca dapat memahami hasil penelitian secara menyeluruh. Saya pernah membuat grafik batang dengan skala sumbu Y yang terlalu sempit sehingga perbedaan nilai terlihat lebih besar dari kondisi sebenarnya. Setelah mempelajari materi ini, saya memahami pentingnya menggunakan skala yang tepat, menampilkan seluruh data, serta menambahkan error bar agar visualisasi tidak menyesatkan.