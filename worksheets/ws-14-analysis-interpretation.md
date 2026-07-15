# WS-14: Analysis, Interpretation & Failure Analysis

> **Bab 14 — Analisis Data, Interpretasi & Failure Analysis**

---

## Ringkasan Materi

### Data → Knowledge Model

```
Data → Analysis → Interpretation → Explanation → Knowledge
```

Tiga level yang berbeda:
- **Analysis** — "Apa yang terjadi?" (deskriptif + inferensial)
- **Interpretation** — "Apa artinya?" (konteks RQ + literatur)
- **Failure Analysis** — "Mengapa tidak berhasil?" (boundary conditions)

### Beyond p-value

**Statistical significance ≠ practical significance.** Selalu laporkan:
1. p-value (signifikansi statistik)
2. Effect size (besarnya efek)
3. Confidence interval (rentang ketidakpastian)

| Effect Size (Cohen's d) | Interpretasi |
|-------------------------|-------------|
| < 0.2 | Small |
| 0.2 – 0.8 | Medium |
| > 0.8 | Large |

### Pemilihan Uji Statistik

| Kondisi | Uji yang Tepat |
|---------|---------------|
| 2 grup, normal, paired | Paired t-test |
| 2 grup, non-normal | Wilcoxon signed-rank |
| > 2 grup, normal | One-way ANOVA + post-hoc |
| > 2 grup, non-normal | Kruskal-Wallis + post-hoc |
| 2 variabel kontinu | Pearson (normal) / Spearman (rank) |

### Failure Analysis as Contribution

Hipotesis yang ditolak adalah **temuan yang berharga**:

| Dataset | New (F1) | Baseline (F1) | p-value | Cohen's d |
|---------|---------|--------------|---------|-----------|
| DS-1 (small, clean) | 94.2±1.1 | 89.3±1.5 | <0.001 | **3.7** |
| DS-4 (medium, noisy) | 78.3±3.2 | 82.1±2.8 | 0.008 | **-1.3** |
| DS-5 (large, noisy) | 71.6±4.1 | 80.5±3.0 | <0.001 | **-2.5** |

**Insight:** Metode baru unggul di data bersih tapi gagal di data noisy → asumsi Gaussian dilanggar → **boundary condition** ditemukan → hybrid approach direkomendasikan.

**Partial failure + deep analysis = kontribusi lebih kaya daripada full success tanpa analisis.**

### Limitation Types

| Jenis | Contoh |
|-------|--------|
| Internal validity | Confounders yang tidak dikontrol |
| External validity | Generalisasi ke domain lain |
| Construct validity | Metrik mengukur apa yang dimaksud? |
| Statistical limitation | Sample size, asumsi distribusi |

### Jebakan Kognitif

1. "Signifikan statistik = penting secara praktis" → cek effect size
2. "Hipotesis tidak didukung → cari sudut baru" → p-hacking
3. "Kegagalan tidak perlu dilaporkan detail" → missed insight
4. "Limitasi cukup disebutkan, tidak perlu dianalisis" → kedalaman hilang

---

## Template A.14 — Analysis & Interpretation Report

```
ANALYSIS & INTERPRETATION

1. Statistik Deskriptif:
   | Skenario | Mean | Std | Median | Min | Max | n |
   |----------|------|-----|--------|-----|-----|---|
   | Sistem Normal               |98.6|0.8|99.0 |97.5|100.0|5| 
   | Perubahan Kondisi Sampah    |98.2|1.0|98.3 |96.8|99.5 |5|
   | Notifikasi Telegram & IoT   |97.9|1.1| 98.0|96.2|99.3 |5|
2. Uji Hipotesis:
   Uji yang digunakan  :  Tidak dilakukan
   Justifikasi          :  Penelitian berfokus pada implementasi dan pengujian fungsional sistem IoT sehingga analisis dilakukan secara deskriptif.
   Hasil: p =p-value tidak dihitung, effect size (d/r/η²) = Tidak dihitung
   CI 95%               :  Tidak dihitung

3. Keputusan:
   [x] H₀ ditolak → H₁ diterima
   [ ] H₀ tidak ditolak

4. Interpretasi:
   Hubungan ke RQ       : Sistem mampu mendeteksi kondisi tempat sampah serta mengirimkan notifikasi Telegram dan data ThingSpeak sesuai rancangan.
   Practical significance: Implementasi ESP32 berhasil menjalankan fungsi monitoring secara konsisten sehingga dapat digunakan sebagai sistem pemantauan tempat sampah secara real-time.
   Perbandingan literatur:Hasil implementasi sesuai dengan penelitian IoT monitoring yang memanfaatkan ESP32, Telegram Bot, dan platform cloud untuk pemantauan jarak jauh.

5. Limitation:
   | Jenis | Ancaman | Dampak | Mitigasi |
   |-------|---------|--------|----------|
   |Internal|Pengujian hanya menggunakan satu perangkat ESP32|Hasil belum mewakili variasi perangkat|          |
   |External|Pengujian dilakukan di lingkungan laboratorium|Generalisasi ke lingkungan nyata terbatas|Uji lapangan |
   |Construct| Pengujian hanya berdasarkan status penuh/kosong|Belum mengukur volume sampah secara bertahap|Menambahkan sensor ultrasonik/load cell|
   |Statistical| Jumlah run terbatas|Analisis statistik belum kuat|Menambah jumlah pengujian|

6. Failure Analysis (jika H₀ tidak ditolak):
   Penyebab potensial  :Keterlambatan jaringan WiFi dapat menyebabkan pengiriman Telegram atau ThingSpeak mengalami delay.
   Boundary condition   : Sistem bergantung pada koneksi internet dan catu daya ESP32. Jika salah satu tidak tersedia maka monitoring tidak berjalan.

   Insight              : Keandalan sistem dipengaruhi oleh stabilitas jaringan. Pada pengembangan selanjutnya dapat ditambahkan mekanisme penyimpanan data lokal (buffer) ketika koneksi internet terputus.
```

---

## Latihan 1 — Pemilihan Uji Statistik

Tentukan uji statistik yang tepat untuk eksperimen Anda.

| Pertanyaan | Jawaban |
|-----------|---------|
| Berapa grup yang dibandingkan? | 3 skenario pengujian (Sistem Normal, Perubahan Kondisi Sampah, Notifikasi Telegram & ThingSpeak) |
| Apakah data berpasangan (paired)? |Tidak|
| Apakah distribusi normal? (uji normalitas) |Tidak diuji karena hanya dilakukan analisis deskriptif |
| Uji yang dipilih:|Tidak menggunakan uji statistik inferensial |
| Justifikasi: | Penelitian berfokus pada implementasi dan evaluasi fungsional sistem IoT sehingga cukup menggunakan statistik deskriptif (mean, standar deviasi, persentase keberhasilan).|

Effect size yang akan dilaporkan: [ ] Cohen's d / [ ] Eta-squared / [x] Lainnya:Tidak berlaku

---

## Latihan 2 — Interpretasi Hasil

Gunakan data berikut (atau data riil Anda) untuk berlatih interpretasi.

**Data:**
| Model | Accuracy (mean ± std) | n |
|-------|----------------------|---|
| A | 89.2 ± 1.5 | 10 |
| B | 87.8 ± 2.1 | 10 |

p = 0.045, Cohen's d = 0.74, CI 95% = [0.03, 2.77]

| Aspek | Interpretasi |
|-------|-------------|
| Signifikansi statistik |  Tidak dilakukan karena penelitian menggunakan analisis deskriptif dan pengujian fungsional sistem. |
| Effect size |  Tidak dihitung karena tidak menggunakan uji statistik inferensial. |
| Practical significance |Sistem berhasil mendeteksi kondisi tempat sampah serta mengirim notifikasi Telegram dan data ke ThingSpeak secara konsisten sesuai skenario pengujian. |
| Hubungan ke RQ |Hasil pengujian menunjukkan bahwa sistem IoT berbasis ESP32 mampu melakukan monitoring kondisi tempat sampah secara real-time sesuai tujuan penelitian.  |
| Perbandingan literatur | Hasil implementasi sejalan dengan penelitian terdahulu yang memanfaatkan ESP32, Telegram Bot, dan platform IoT untuk monitoring jarak jauh, namun penelitian ini mengintegrasikan seluruh komponen dalam satu sistem monitoring tempat sampah. |

---

## Latihan 3 — Failure Analysis

Latih kemampuan failure analysis: hipotesis TIDAK didukung. Apa yang bisa dipelajari?

**Skenario:** Metode baru Anda mendapat F1 = 83.2%, baseline = 84.7%. p = 0.12 (tidak signifikan).

| Pertanyaan | Jawaban |
|-----------|---------|
| Apakah ini "gagal"? | Tidak. Jika beberapa pengujian belum mencapai hasil yang diharapkan, hal tersebut menjadi informasi untuk mengetahui batas kemampuan sistem. |
| Kemungkinan penyebab? | Koneksi WiFi tidak stabil, keterlambatan respons Telegram API, atau gangguan komunikasi dengan ThingSpeak. |
| Boundary condition? | Sistem hanya dapat bekerja optimal ketika ESP32 memperoleh koneksi internet dan catu daya yang stabil. |
| Insight yang bisa diambil? | Stabilitas jaringan merupakan faktor penting terhadap performa sistem sehingga diperlukan mekanisme retry atau penyimpanan data sementara saat koneksi terputus. |
| Apakah layak dilaporkan? Mengapa? | Ya. Dokumentasi kegagalan membantu menjelaskan keterbatasan sistem dan menjadi dasar pengembangan penelitian selanjutnya.|

**Limitation terkait:**
| Jenis | Ancaman | Dampak |
|-------|---------|--------|
| Internal| Pengujian hanya menggunakan satu perangkat ESP32| Hasil belum mewakili seluruh variasi perangkat |
| External|Pengujian dilakukan pada lingkungan terbatas |Generalisasi ke kondisi lapangan masih terbatas |
| Statistical |Jumlah pengujian relatif sedikit | Belum dapat dilakukan analisis statistik yang kuat|

---

## Refleksi

> Apakah "failure" dalam riset benar-benar gagal, atau justru kontribusi? Bagaimana failure analysis mengubah cara Anda melihat hasil negatif?

> Dalam penelitian, kegagalan bukan berarti penelitian tidak berhasil. Hasil yang tidak sesuai hipotesis tetap memberikan informasi mengenai batas kemampuan sistem, kondisi ketika sistem tidak bekerja optimal, serta faktor-faktor yang memengaruhi kinerjanya. Failure analysis membantu memahami penyebab masalah secara sistematis sehingga dapat menjadi dasar perbaikan pada penelitian berikutnya dan meningkatkan kualitas pengembangan sistem IoT.
