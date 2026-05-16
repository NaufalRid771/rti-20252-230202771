# WS-05: Variabel & Metrik

> **Bab 5 — Metric, Measurement & Data**

---

## Ringkasan Materi

### Measurement Alignment Model

Setiap pengukuran yang valid harus bisa ditelusuri melalui rantai ini tanpa lompatan logis:

```
Problem → Concept → Variable → Metric → Data → Result
```

### Operationalization = Keputusan Desain

Menerjemahkan konsep abstrak menjadi variabel terukur bukan proses mekanis. "Code quality" yang diukur via SonarQube code smells membawa asumsi implisit. Setiap operasionalisasi harus didokumentasikan dan dijustifikasi.

### Empat Tipe Data (NOIR)

| Tipe | Ciri | Contoh | Operasi Valid |
|------|------|--------|---------------|
| **Nominal** | Kategori, tanpa urutan | Jenis algoritma (RF, SVM, CNN) | Modus, chi-square |
| **Ordinal** | Urutan, interval tidak sama | Skala Likert (1-5) | Median, Spearman |
| **Interval** | Jarak bermakna, tanpa nol absolut | Suhu Celsius | Mean, Pearson, t-test |
| **Ratio** | Jarak bermakna + nol absolut | Waktu eksekusi (ms) | Semua operasi |

Tipe data menentukan uji statistik yang valid. Kebanyakan metrik performa TI = ratio; persepsi pengguna = ordinal.

### Kriteria Pemilihan Metrik

- **Representative** — Mewakili konsep yang diteliti
- **Sensitive** — Cukup peka menangkap perbedaan bermakna (hindari ceiling effect)
- **Feasible** — Bisa dikumpulkan dalam batasan waktu dan biaya

### Pre-registration

Metrik harus ditentukan **sebelum** eksperimen. Memilih metrik setelah melihat data = **p-hacking**. Metrik tambahan yang ditemukan kemudian dilaporkan sebagai *exploratory*, bukan *confirmatory*.

### Primary vs Secondary Metric

- **Primary Metric** — Langsung terikat ke hipotesis, menentukan kesimpulan
- **Secondary Metric** — Pendukung, dilaporkan di samping primary; statusnya suplementer

### Research vs Engineering

| Aspek | Engineering | Research |
|-------|------------|----------|
| Pemilihan metrik | Berdasarkan kebiasaan/tool yang ada | Berdasarkan construct validity |
| Anomali | Dihapus untuk laporan bersih | Diinvestigasi — bisa jadi temuan |
| Kapan dipilih | Setelah sistem jadi (monitoring) | Sebelum eksperimen (by design) |

### Istilah Penting

- **Operationalization** — Transformasi konsep abstrak menjadi variabel terukur
- **Construct Validity** — Sejauh mana pengukuran benar-benar mengukur konsep yang dimaksud
- **Measurement Scale** — Klasifikasi data (NOIR) yang menentukan analisis valid
- **Multi-metric Evaluation** — Menggunakan beberapa metrik untuk menangkap konsep kompleks

---

## Template A.5 — Definisi Variabel, Metrik & Justifikasi

```
VARIABLE & METRIC DEFINITION

Research Question:Apakah sistem pemilahan sampah anorganik berbasis ESP32 menggunakan sensor multivariable menghasilkan akurasi klasifikasi dan delay notifikasi yang lebih baik dibanding sistem sensor tunggal?

| Variabel | Tipe | Konsep | Metrik | Skala | Satuan | Cara Mengukur | Justifikasi |
|----------|------|--------|--------|-------|--------|---------------|-------------|
|          | IV  |Pendekatan sistem klasifikasi     | Sensor tunggal vs multisensor       |Nominal       |  —      |Membandingkan konfigurasi sensor pada prototype               |  Variabel utama yang memengaruhi performa sistem           |
|          | DV   | Ketepatan pemilahan sampah       | Accuracy (%)       | Ratio      | Persen (%)       | Jumlah klasifikasi benar ÷ total pengujian × 100%              |  Accuracy mewakili performa utama sistem           |
|          | CV   | Karakteristik objek uji       |  Plastik, kaca, kaleng      | Nominal      | —       | 
|Mengontrol jenis sampah yang diuji|   Agar hasil pengujian konsisten            | 
Alignment Check:
  RQ → Concept → Variable → Metric → Data → Result
  [ ☑ ] Setiap langkah terdokumentasi
  [ ☑ ] Tidak ada "lompatan logis"
  [ ☑ ] Metrik mengukur apa yang dimaksud (construct validity)
```

---

## Latihan 1 — Operationalization Chain

Gunakan RQ dari WS-04. Definisikan variabel dan metriknya.

**RQ:** 
Apakah sistem pemilahan sampah anorganik berbasis ESP32 menggunakan sensor multivariable menghasilkan akurasi klasifikasi dan delay notifikasi yang lebih baik dibanding sistem sensor tunggal?

| Variabel | Tipe | Konsep Abstrak | Metrik Konkret | Skala (NOIR) | Satuan |
|----------|------|---------------|----------------|-------------|--------|
| *Contoh: Jenis model* | *IV* | *Pendekatan klasifikasi* | *Categorical: CNN vs RF* | *Nominal* | *—* |
| Akurasi klasifikasi| DV | Ketepatan pemilahan sampah|Accuracy (%) | Ratio| Persen (%)|
|Jenis sampah | CV |Karakteristik objek pengujian |Plastik, kaca, kaleng |Nominal |—|

**Apakah ada lompatan logis dalam rantai?** [ ] Ya / [ ☑ ] Tidak
> Jika ya, di mana? Tidak ada, karena semua konsep abstrak sudah diterjemahkan menjadi variabel dan metrik yang dapat diukur langsung.
---

## Latihan 2 — Evaluasi Metrik

Evaluasi metrik DV yang dipilih di Latihan 1 menggunakan 3 kriteria.

| Kriteria | Skor (1-5) | Justifikasi |
|----------|-----------|-------------|
| Representative | 5 |Accuracy dan delay langsung mewakili performa sistem smart waste |
| Sensitive | 4|Perubahan kecil pada performa masih dapat terdeteksi |
| Feasible | 5| Data dapat dikumpulkan langsung dari prototype dan Telegram|

**Apakah perlu secondary metric?** [ ☑] Ya / [ ] Tidak
> Jika ya, apa dan mengapa? Precision dan recall dapat digunakan sebagai secondary metric untuk melihat performa klasifikasi tiap jenis sampah secara lebih detail.

**Contoh kasus ceiling effect untuk metrik ini:**
>Jika accuracy seluruh sistem sudah mendekati 100%, maka perbedaan performa antar metode menjadi sulit terlihat hanya dari accuracy saja.

---

## Latihan 3 — Data Quality Check

Bayangkan data yang akan dikumpulkan dari eksperimen. Evaluasi 4 dimensi kualitas data.

| Dimensi | Pertanyaan | Jawaban | Strategi Mitigasi |
|---------|-----------|---------|------------------|
| Completeness | *Apakah semua data point terkumpul?* |Bisa terjadi data hilang saat koneksi internet putus |Menyimpan log lokal pada ESP32 |
| Consistency | *Apakah ada kontradiksi internal?* | Kemungkinan delay berbeda pada tiap pengujian|Melakukan pengujian berulang |
| Validity | *Apakah benar-benar mengukur yang dimaksud?* | Accuracy sudah sesuai tujuan klasifikasi|Menggunakan skenario uji yang sama |
| Representativeness | *Apakah sampel mewakili populasi target?* | Sampel sampah masih terbatas|Menambah variasi jenis sampah |

---

## Refleksi

> Mengapa memilih metrik setelah melihat data dianggap p-hacking? Apa bedanya dengan eksplorasi data yang sah?

**Jawaban:**
> Memilih metrik setelah melihat data dianggap p-hacking karena peneliti dapat memilih metrik yang paling menguntungkan hasil penelitian sehingga kesimpulan menjadi bias. 
> Hal ini berbeda dengan eksplorasi data yang sah, karena eksplorasi dilakukan untuk menemukan pola tambahan dan hasilnya dilaporkan sebagai exploratory, bukan sebagai bukti utama untuk menerima hipotesis.
