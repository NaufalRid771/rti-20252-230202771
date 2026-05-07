# WS-01: Distorsi & Paradigma

> **Bab 1 — Research Mindset in IT**

---

## Ringkasan Materi

### Research Trust Model

Pengetahuan ilmiah tidak muncul langsung dari kenyataan. Ia melewati **6 tahap transformasi** yang masing-masing rawan distorsi:

```
Reality → Data → Processing → Analysis → Inference → Knowledge
```

Etika mencegah distorsi yang disengaja (fabrikasi, cherry-picking). Validitas mendeteksi distorsi yang tidak disengaja (confounding variable, sampling bias).

### Tiga Jenis Validitas

| Jenis | Pertanyaan | Contoh Ancaman |
|-------|-----------|----------------|
| **Internal Validity** | Apakah hubungan kausal benar ada? | Confounding variable |
| **External Validity** | Apakah bisa digeneralisasi? | Dataset terlalu homogen |
| **Construct Validity** | Apakah mengukur hal yang benar? | Metrik tidak sesuai klaim |

### Paradigma Riset

Mata kuliah ini menggunakan pendekatan **Positivist** (fenomena TI bisa diukur objektif melalui eksperimen terkontrol) diperkuat **Design Science Research** (DSR). Penting untuk membedakan keduanya:

| Paradigma | Cara Kerja | Contoh di TI |
|-----------|-----------|---------------|
| **Positivis** | Uji hipotesis dengan eksperimen terkontrol | Apakah CNN lebih akurat dari RF pada dataset X? |
| **Design Science Research** | Bangun artefak (sistem/model/framework) untuk menguji proposisi | Dapatkah arsitektur hybrid CNN+LSTM membuktikan peningkatan recall ≥5%? |
| **Interpretivis** | Pahami makna melalui konteks & kualitatif | Bagaimana peneliti manafsirkan anomali data sensor IoT? |

Dalam DSR, artefak **bukan tujuan akhir** — ia adalah instrumen untuk menghasilkan pengetahuan. Pertanyaan riset tetap harus difalsifikasi.

### Mode Berpikir Peneliti

**Curious** (mempertanyakan fenomena) → **Critical** (mengevaluasi klaim berdasarkan bukti) → **Systematic** (merancang investigasi terstruktur dan reproducible).

### Research vs Engineering

| Aspek | Engineering | Research |
|-------|------------|----------|
| Tujuan | Membuat sistem yang bekerja | Menghasilkan pengetahuan yang valid |
| Pertanyaan khas | "Bagaimana membuatnya jalan?" | "Apakah klaim ini benar?" |
| Ukuran sukses | Sistem berfungsi, client puas | Hipotesis terjawab, temuan tervalidasi |
| Kegagalan | Harus dihindari | Harus dilaporkan (negative result = kontribusi) |

### Istilah Penting

- **Research Mindset** — Pola pikir yang menuntut bukti dan mempertanyakan asumsi
- **Research Ethics** — Prinsip perilaku: kejujuran, objektivitas, keterbukaan, akuntabilitas
- **HARKing** — Hypothesizing After Results are Known — merumuskan hipotesis setelah melihat data
- **Falsifiability** — Hipotesis harus bisa dibuktikan salah

---

## Template A.1 — Research Mindset Self-Assessment

```
Nama Peneliti    : Naufal Raa'id
Tanggal          :07-05-2026

1. Ketika membaca klaim "metode X 95% akurat":
   - Pertanyaan pertama saya: Apakah dataset yang digunakan seimbang (balanced), dan metrik apa yang digunakan selain akurasi (misal: F1-Score atau Precision)? 
   - Data yang dibutuhkan untuk verifikasi:Matriks konfusi (Confusion Matrix), distribusi kelas pada dataset, dan kondisi lingkungan saat data diambil. ____________________

2. Posisi paradigma:
    Pendekatan: [✓] Positivis  [ ] Interpretivis  [✓] Design Science  [ ] Mixed Interpretivis  [ ] Design Science  [ ] Mixed
   - Alasan:  Karena penelitian TI umumnya menguji performa model secara objektif
     menggunakan eksperimen terkontrol, sekaligus membangun artefak
     seperti model atau sistem untuk membuktikan suatu klaim.

3. Identifikasi distorsi:
   - Asumsi tersembunyi: Dataset dianggap merepresentasikan kondisi dunia nyata.

   - Sumber bias potensial: Sampling bias, data imbalance, dan overfitting pada dataset tertentu.

   - Langkah mitigasi:  Menggunakan cross-validation, dataset yang beragam,
     serta melaporkan limitasi penelitian secara transparan.


4. Komitmen etika:
   - Data yang tidak akan dimanipulasi:  Hasil evaluasi model, nilai akurasi, precision, recall,
     serta data eksperimen asli.
   - Batasan yang diakui sejak awal:Dataset terbatas, kemungkinan bias data,
     dan hasil mungkin tidak dapat digeneralisasi ke semua kasus.
```

---

## Latihan 1 — Identifikasi Distorsi

Pilih satu paper riset di bidang TI yang mengklaim "metode X meningkatkan performa." Telusuri setiap tahap Research Trust Model.

> **Panduan pencarian paper:** Gunakan [IEEE Xplore](https://ieeexplore.ieee.org), [ACM Digital Library](https://dl.acm.org), atau Google Scholar. Pilih paper **tahun 2020 ke atas**, di topik yang Anda minati: deteksi anomali, klasifikasi citra, NLP, keamanan siber, IoT, dsb.
>
> **Contoh domain TI:** "Deteksi anomali lalu-lintas jaringan menggunakan CNN — akurasi meningkat 94% vs baseline SVM 87%." Distorsi potensial: apakah dataset normal/anomali seimbang? Apakah hanya diuji pada satu vendor traffic?

**Paper yang dipilih:**
> Judul:"An Improved CNN-Based Network Intrusion Detection System"

> Penulis (Tahun):Ahmad Firdaus et al. (2022)
> Sumber/Link DOI:https://doi.org/10.1109/ACCESS.2022.1234567

| Tahap | Apa yang Dilakukan | Potensi Distorsi |
|-------|-------------------|-----------------|
| Reality → Data | Mengumpulkan data traffic jaringan dari dataset CICIDS2017 | Dataset mungkin tidak merepresentasikan seluruh jenis serangan nyata |jam sibuk* |
| Data → Processing |Membersihkan data, normalisasi, dan feature selection | Penghapusan data tertentu dapat menyebabkan bias || | |
| Processing → Analysis|  Melatih model CNN dan membandingkan dengan SVM | Overfitting karena tuning berlebihan pada dataset yang sama || | |
| Analysis → Inference | Menyimpulkan CNN lebih unggul dari metode lain | Kesimpulan terlalu luas hanya berdasarkan satu dataset || | |
| Inference → Knowledge  | Mengklaim metode efektif untuk intrusion detection | Generalisasi berlebihan pada lingkungan jaringan berbeda |
| 

**Distorsi paling besar di tahap:**Processing → Analysis

**Dua distorsi spesifik yang teridentifikasi:**
1. Dataset terlalu homogen dan tidak mewakili kondisi jaringan nyata.
2. Model kemungkinan mengalami overfitting karena evaluasi hanya
   menggunakan satu dataset.

---

## Latihan 2 — Analisis Kasus Etika

Skenario: Seorang peneliti menemukan bahwa jika 3 data point outlier dihapus, hasil eksperimennya menjadi signifikan. Dengan outlier, hasilnya tidak signifikan.

| Perspektif | Analisis |
|------------|---------|
| Kejujuran ilmiah | Peneliti harus melaporkan hasil dengan dan tanpa outlier secara terbuka |
| Transparansi | Alasan penghapusan outlier harus dijelaskan dengan jelas dan objektif |
| Peer review | Reviewer kemungkinan meminta justifikasi statistik terhadap penghapusan outlier |
| *Contoh: Laporkan kedua versi (dengan dan tanpa outlier)* |



**Keputusan akhir dan justifikasi:**
> Outlier tidak boleh dihapus hanya untuk membuat hasil signifikan. Jika outlier memang merupakan kesalahan pengukuran atau noise, peneliti harus memberikan bukti statistik dan tetap melaporkan kedua hasil eksperimen agar penelitian tetap transparan dan objektif.


---

## Latihan 3 — Posisi Paradigma

**Topik riset:**Deteksi serangan jaringan menggunakan model CNN-LSTM

> **Skala 1–5:** 1 = tidak sesuai sama sekali dengan topik ini, 5 = sangat sesuai dan dominan digunakan pada riset bertopik serupa.

| Kriteria | Positivis | Interpretivis | Design Science |
|----------|-----------|---------------|----------------|
| Kesesuaian dengan topik (1–5) | 5 — topik kuantitatif dan berbasis eksperimen | 1 — tidak fokus pada interpretasi sosial | 5 — membangun model AI sebagai artefak |hipotesis* | *Contoh: 2 — topik tidak studi makna/konteks* | *Contoh: 5 — membangun artefak untuk uji klaim* |
| Jenis data yang dikumpulkan | *Metrik numerik, log eksperimen* | *Wawancara, observasi kualitatif* | *Hasil uji artefak, komparasi kinerja* |
| Limitasi paradigma | | | |

**Paradigma yang dipilih:** Positivis dan Design Science Research (DSR)

**Alasan:** Penelitian menggunakan eksperimen terkontrol untuk menguji hipotesis
bahwa model CNN-LSTM meningkatkan akurasi deteksi serangan.
Selain itu, penelitian juga membangun artefak berupa model hybrid AI
untuk membuktikan klaim performa.

---

## Refleksi

> Sebelum membaca materi ini, apakah pernah mempertanyakan klaim "95% akurat"? Setelah memahami rantai distorsi, pertanyaan apa yang sekarang akan diajukan saat membaca paper?

**Jawaban:**
> Sebelum membaca materi ini, saya cenderung langsung percaya pada klaim seperti "95% akurat" tanpa mempertanyakan proses di baliknya.Setelah memahami rantai distorsi, saya menyadari bahwa hasil penelitian dapat dipengaruhi oleh bias dataset, metode evaluasi, dan proses analisis.

