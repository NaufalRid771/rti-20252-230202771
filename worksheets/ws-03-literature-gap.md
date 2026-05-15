# WS-03: Literature Mapping & Gap

> **Bab 3 — Literature Review, Research Gap & Baseline**

---

## Ringkasan Materi

### Literature Review = Positioning, Bukan Ringkasan

Literature review bukan merangkum paper satu per satu. Pendekatan yang benar adalah **concept-centric** — organisasi berdasarkan tema, metode, atau variabel. Tujuan: menemukan **pola, kontradiksi, dan gap**.

**Perbandingan pendekatan Author-centric vs Concept-centric:**

| Aspek | Author-centric (Hindari) | Concept-centric (Gunakan) |
|-------|--------------------------|---------------------------|
| Struktur | Per penulis/paper ("Rahman et al. menyatakan...") | Per konsep/metode ("Pendekatan berbasis transformer") |
| Tujuan | Ringkasan isi paper | Perbandingan metode & identifikasi gap |
| Contoh paragraph | "Rahman (2023) pakai CNN. Lee (2022) pakai LSTM. Zhang (2021) pakai RF." | "Tiga pendekatan dominan: CNN digunakan oleh 4 paper untuk representasi fitur visual; LSTM untuk data sekuensial; RF sebagai baseline klasik." |
| Hasil akhir | Daftar paper | Peta pengetahuan + gap yang teridentifikasi |

### Empat Jenis Research Gap

| Jenis Gap | Deskripsi | Contoh |
|-----------|----------|--------|
| **Performance Gap** | Performa belum memadai | Akurasi deteksi hanya 78% pada kasus tertentu |
| **Method Gap** | Pendekatan belum diterapkan | Belum ada yang pakai transformer untuk task ini |
| **Data Gap** | Dataset terbatas/tidak representatif | Semua studi pakai dataset sintetis |
| **Context Gap** | Belum diuji pada konteks berbeda | Belum ada evaluasi di negara berkembang |

Gap terkuat = kombinasi 2+ jenis.

### Systematic Search Strategy

1. **Database utama**: IEEE Xplore, ACM DL, Scopus
   - Akses IEEE/ACM melalui jaringan kampus atau VPN institusi
   - Alternatif bebas biaya: Google Scholar, ResearchGate ([researchgate.net](https://www.researchgate.net)), arXiv ([arxiv.org](https://arxiv.org))
2. **Boolean query** yang terdokumentasi eksplisit
   - Contoh: `("anomaly detection" OR "intrusion detection") AND ("deep learning" OR "neural network") NOT ("medical imaging")`
   - Gunakan tanda kutip untuk frasa eksak; AND/OR/NOT mengontrol scope
3. **Snowballing** — dua arah:
   - **Backward snowballing**: buka daftar referensi di paper kunci → telusuri paper yang dikutip
   - **Forward snowballing**: di Google Scholar, klik "Cited by" di bawah paper kunci → temukan paper yang mengutipnya
   - Ulangi 1–2 tingkat untuk membangun cakupan komprehensif
4. Klaim "belum ada penelitian" harus didukung **bukti pencarian**

### Baseline Selection — 3 Kriteria

| Kriteria | Pertanyaan |
|----------|-----------|
| **Relevan** | Apakah menyelesaikan masalah yang sama? |
| **Representatif** | Apakah mewakili common practice? |
| **State-of-the-Art** | Apakah terbaru/terbaik? |

Membandingkan deep learning 2024 dengan decision tree sederhana tanpa justifikasi = **straw man comparison** (perbandingan tidak jujur).

### Research vs Engineering

| Aspek | Engineering | Research |
|-------|------------|----------|
| Tujuan baca literatur | Mencari solusi yang sudah ada | Memahami apa yang belum terjawab |
| Cara membaca paper | Tutorial, how-to | Metode, limitasi, gap |
| Baseline | Framework terpopuler | State-of-the-art yang rigorous |
| Dokumentasi pencarian | Tidak diperlukan | Wajib (reproducible) |

### Istilah Penting

- **Concept-centric** — Organisasi literatur berdasarkan konsep/metode, bukan per penulis
- **Snowballing** — Backward (telusuri referensi) + Forward (cari yang mengutip paper kunci)
- **Research Position** — Pernyataan eksplisit posisi riset terhadap studi sebelumnya
- **Straw man comparison** — Memilih baseline lemah agar metode sendiri terlihat lebih baik

---

## Template A.3 — Literature Mapping & Gap Identification

```
LITERATURE MAPPING

Topik      : Sistem Pemilahan Sampah Anorganik Berbasis ESP32 Menggunakan Sensor Multivariable dengan Notifikasi Real-Time via Telegram
Database   : Google Scholar, IEEE Xplore, ResearchGate
Query      : ("smart waste sorting" OR "automatic waste classification") AND ("ESP32" OR "IoT") AND ("sensor" OR "multisensor") AND ("Telegram notification")
Tahun      : 2020–2025
Hasil awal : 28 paper → Screening → 5 paper final

Literature Matrix (concept-centric):

| Study | Tahun | Method | Data | Result | Limitation |
|-------|-------|--------|------|--------|------------|
|       |       |        |      |        |            |

Pola yang ditemukan:
  Metode dominan     : ESP32/ESP8266 berbasis IoT
  Dataset umum       :Prototype laboratorium
  Limitasi berulang  :Belum banyak sistem multisensor

GAP IDENTIFICATION

Gap 1: [Jenis: performance / method / data / context]
  Deskripsi    : Sebagian besar penelitian hanya menggunakan satu sensor atau hanya monitoring kapasitas tanpa klasifikasi berbasis multisensor.
  Bukti        :Penelitian Putra et al. dan Damayanti & Noer fokus pada monitoring serta notifikasi Telegram, bukan pemilahan otomatis multisensor.
  Signifikansi : Multisensor dapat meningkatkan akurasi pemilahan dengan biaya lebih murah dibanding sistem berbasis kamera/AI.

Gap 2: [Jenis:Context + Performance Gap]
  Deskripsi    : istem AI memiliki akurasi tinggi tetapi membutuhkan perangkat mahal dan konsumsi daya besar.
  Bukti        : White et al. menggunakan CNN dengan Jetson Nano untuk mencapai akurasi tinggi.
  Signifikansi :ESP32 lebih murah dan hemat daya sehingga lebih cocok diterapkan di sekolah, rumah tangga, dan lingkungan masyarakat Indonesia.
Baseline Selection:
| Baseline | Relevansi    | Representatif | Source |



|ESP32     |Sama" smart -|Dipakai pada banyak penelitian IoT                              |--------|
|          |waste monitor
           |               |        |
```

---

## Latihan 1 — Concept-Centric Literature Table

Gunakan topik riset dari WS-02. Cari minimal 5 paper relevan menggunakan database akademik.

> **Panduan pencarian:**
> - Database: IEEE Xplore, ACM DL, Google Scholar, atau ResearchGate
> - Tulis query Boolean yang digunakan: contoh `("object detection" OR "image classification") AND ("edge computing") NOT ("medical")`. Dokumentasikan query secara eksplisit.
> - Akses gratis: buka Google Scholar → cari judul paper → klik [PDF] jika tersedia, atau akses lewat campus VPN

**Topik riset:** Sistem Pemilahan Sampah Anorganik Berbasis ESP32 Menggunakan Sensor Multivariable dengan Notifikasi Real-Time via Telegram

**Query pencarian:** ("smart waste sorting" OR "automatic waste classification") AND ("ESP32" OR "IoT") AND ("sensor" OR "multisensor") AND ("Telegram notification")

**Database:** 
google Scholar, IEEE Xplore, ResearchGate

| # | Study | Tahun | Method | Dataset | Result | Limitasi |
|---|-------|-------|--------|---------|--------|----------|
| 1 | Damayanti & Noer | *2025* | *Smart Dustbin IoT + Telegram* | *Prototype smart bin* | *Notifikasi real-time berhasil* | *Hanya 2 kategori sampah* |
| 2 |Lianawati et al. |2024 |ESP32 + sensor berat |Sampah organik/plastik |Akurasi 86,67% |Belum multisensor |
| 3 | Putra et al.|2024 | ESP32 + infrared + Telegram|Monitoring kapasitas tempat sampah |Sistem stabil real-time |Tidak ada klasifikasi sampah |
| 4 |White et al. | 2020| CNN + Edge AI|Dataset 6 kelas sampah | Akurasi 97%| Hardware mahal|
| 5 | Lam et al.|2022 |AI + IoT Smart Bin |Dataset visual waste |Akurasi 90% | Konsumsi daya tinggi|

**Pola yang terlihat — Metode dominan:** 
IoT berbasis ESP32 dengan sensor ultrasonik dan notifikasi Telegram.
**Limitasi yang berulang:** 
Belum ada integrasi multisensor low-cost untuk klasifikasi sampah anorganik secara real-time.
---

## Latihan 2 — Gap Identification

Berdasarkan tabel di Latihan 1, identifikasi gap.

| Jenis Gap | Ditemukan? | Gap Statement |
|-----------|-----------|---------------|
| Performance Gap | [✓ ] Ya / [ ] Tidak | *Contoh: Akurasi turun di bawah 80% untuk kelas minoritas* |
| Method Gap | [ ✓ ] Ya / [ ] Tidak | |
| Data Gap | [ ✓ ] Ya / [ ] Tidak | |
| Context Gap | [ ✓] Ya / [ ] Tidak | |

**Gap utama yang dipilih:** 
Method Gap + Context Gap
**Mengapa gap ini penting (bukan sekadar "belum ada yang meneliti")?**
> Karena sistem yang ada masih mahal dan sulit diterapkan secara luas. Penggunaan ESP32 dan multisensor dapat menjadi solusi murah, hemat energi, dan realistis untuk diterapkan pada lingkungan masyarakat Indonesia.

---

## Latihan 3 — Baseline Selection

Pilih 2 baseline dari literatur yang sudah dibaca.

| # | Baseline | Mengapa Relevan | Mengapa Representatif | Apakah SOTA? | Sumber |
|---|----------|----------------|----------------------|-------------|--------|
| 1 | *ESP32 + Ultrasonic Sensor* | *Sama-sama digunakan untuk monitoring dan pemilahan sampah berbasis IoT* | *Banyak dipakai pada penelitian smart bin berbasis ESP32* | *Bukan, tapi common practice* | *Putra et al., 2024* |
| 2 | CNN Waste Classification|Sama-sama melakukan klasifikasi sampah otomatis |Menjadi metode umum pada penelitian AI smart waste sorting |Ya | White et al., 2020|

**Apakah pemilihan baseline ini bisa dianggap straw man?** [ ✔] Ya / [ ] Tidak
> Justifikasi: Baseline dipilih dari dua pendekatan utama pada literatur, yaitu sistem IoT low-cost dan sistem AI state-of-the-art sehingga perbandingan tetap adil dan relevan.

---

## Refleksi

> Apa perbedaan antara "belum ada yang meneliti ini" (klaim tanpa bukti) dengan research gap yang valid? Bagaimana cara membuktikan bahwa sebuah gap benar-benar ada?

**Jawaban:**
> “Belum ada yang meneliti ini” hanyalah asumsi jika tidak didukung pencarian literatur yang jelas. Sedangkan research gap yang valid harus dibuktikan melalui analisis beberapa penelitian sebelumnya untuk menemukan kekurangan, limitasi, atau masalah yang belum terselesaikan.
> Gap dapat dibuktikan dengan melakukan pencarian sistematis pada database akademik, membandingkan metode dan hasil penelitian terdahulu, lalu menunjukkan pola kelemahan yang berulang, misalnya akurasi rendah, penggunaan metode yang terbatas, dataset kecil, atau belum diterapkan pada konteks tertentu.