# WS-10: Experiment Execution & Data Collection

> **Bab 10 — Eksekusi Eksperimen & Pengumpulan Data**

---

## Ringkasan Materi

### Experiment Execution Pipeline

```
Design → Execution Plan → Controlled Execution → Data Collection → Data Logging → Dataset for Analysis
```

### Multiple Run = Non-Negotiable

Single run **tidak pernah cukup** untuk klaim ilmiah. Minimum 5-10 run per skenario dengan seed berbeda. Multiple run menghasilkan:
- Mean, std, confidence interval
- Distribusi hasil → uji statistik
- Variabilitas → error bar di grafik

### Execution Plan

Setiap eksperimen harus memiliki plan sebelum eksekusi:
- Daftar skenario
- Jumlah run per skenario
- Random seed per run (pre-determined!)
- Urutan eksekusi (randomisasi/counterbalancing)
- Pre-execution checklist

### Data Logging Komprehensif

Setiap run menghasilkan log terstruktur:
1. **Identitas** — Run ID, timestamp, skenario
2. **Konfigurasi** — Semua parameter, seed, code version
3. **Hasil** — Semua metrik, output detail
4. **Metadata** — Waktu eksekusi, resource usage, warning/error

Format: CSV/JSON/database — **bukan stdout yang di-copy-paste**.

### Engineering vs Research Execution

| Aspek | Engineering | Research |
|-------|-----------|---------|
| Run | Sekali (deploy) | Multiple (min 5-10, seed berbeda) |
| Logging | Error log, access log | Semua parameter, metrik, metadata |
| Anomali | Bug → fix → redeploy | Investigasi → dokumentasi → analisis |
| Urutan | Tidak penting | Bisa bias — perlu randomisasi |

### Anomali = Dokumentasi, Bukan Hapus

Run gagal/anomali tidak boleh dihapus tanpa dokumentasi. Bisa jadi:
- **Bug** → fix & re-run (dokumentasikan!)
- **Batas kemampuan metode** → DNF = temuan
- **Data yang bias** jika hanya simpan run "berhasil"

### Jebakan Kognitif

1. "Satu angka cukup" → tanpa distribusi, tidak bisa diuji
2. "Seed tidak penting" → bahkan algoritma deterministik bisa dipengaruhi library stokastik
3. "Run gagal langsung hapus" → kehilangan temuan potensial
4. "Semua run harus hari ini" → thermal throttling, fatigue

---

## Template A.10 — Execution Plan & Data Log

```
EXECUTION PLAN

| Run # |      Skenario               | Seed |         | Parameter |         |Status | Waktu | Output File |
|-------|----------|------|-----------|--------|-------|-------------|
| 1     |Tempat sampah kosong|        |Tidak digunakan |Switch = OFF, WiFi aktif|Planned|             |
| 2     |Tempat sampah penuh |        |Tidak digunakan |           |        |       |             |
| 3     |Tempat sampah kosong|        | Tidak digunakan        |           |        |       |             |
| ...   |          |      |           |        |       |             |

Jumlah runs per skenario : 3 kali
Total runs               : 6 kali (atau dapat disesuaikan menjadi 10 kali untuk hasil yang lebih konsisten).
DATA LOG (per run):
  Run ID    : run-001
  Timestamp : 2025-06-20 14:30:00
  Skenario  : Tempat Sampah Penuh
  Input     : ____________________
  Output    : ____________________
  Anomali   : ____________________
  Catatan   : ____________________
```

---

## Latihan 1 — Execution Plan

Susun execution plan untuk eksperimen Anda. Tentukan skenario, jumlah run, dan seed sebelum eksekusi.

| Run # | Skenario                               | Seed | Parameter Kunci                      | Status  |
|-------|----------------------------------------|------|--------------------------------------|---------|
| 1 | Pengujian sistem normal                  | 42   | Sensor aktif, WiFi ON, Telegram ON   | Planned |
| 2 | Pengujian sistem normal (pengulangan)    | 123  | Sensor aktif, WiFi ON, Telegram ON   | Planned |
| 3 | Pengujian perubahan kondisi sampah       | 456  | Servo 0°–90°, ThingSpeak ON          | Planned |
| 4 | Pengujian notifikasi Telegram            | 789  | Bot aktif, API ThingSpeak valid      | Planned |
| 5 | Pengujian sistem terintegrasi            | 999  | Semua modul aktif                    | Planned |
| 5 | | | | |

**Total skenario:**4
**Run per skenario:** 5 kali (direncanakan untuk memperoleh hasil yang konsisten)
**Total run keseluruhan:**20 run

---

## Latihan 2 — Data Log Terstruktur

Desain format data log untuk eksperimen Anda. Tentukan field apa saja yang akan dicatat.

**Identitas:**
| Field | Contoh |
|-------|--------|
| Run ID | *run-001* |
| Timestamp | *2025-03-15T10:30:00* |
| Skenario| |

**Konfigurasi:**
| Field | Contoh |
|-------|--------|
| Seed | 42 |
| Code version | v1.0 (main.cpp) |
| WiFi Status|Connected |

**Hasil:**
| Metrik | Tipe Data | Range Valid |
|--------|----------|-------------|
|Status Sensor |Boolean | 0–1 |
|Sudut Servo| | |
|Status Telegram | | |
|Status ThingSpeak

**Format output:** [✔] CSV / [ ] JSON / [ ] Database / [ ] Lainnya: ____

---

## Latihan 3 — Anomaly Protocol

Rencanakan bagaimana menangani anomali. Untuk setiap jenis, tentukan langkah yang diambil.

| Jenis Anomali | Contoh | Tindakan |
|---------------|--------|----------|
| Run gagal(crash) | ESP32 restart karena listrik terputus| Catat penyebab, nyalakan kembali sistem, ulangi pengujian|
| Hasil ekstrem |Servo tidak bergerak saat sensor aktif | Periksa koneksi kabel dan program, kemudian ulangi pengujian|
| Waktu eksekusi anomali |Notifikasi Telegram terlambat (>10 detik) |Periksa kualitas koneksi WiFi dan lakukan pengujian ulang |
| Inkonsistensi dengan run lain | Sensor membaca penuh padahal tempat sampah kosong|Kalibrasi sensor, dokumentasikan hasil, lalu lakukan run ulang |

**Prinsip:** Detect → Investigate → Document → Decide
Detect : Mengidentifikasi adanya anomali selama eksperimen.
Investigate : Menelusuri penyebab anomali (hardware, software, atau jaringan).
Document : Mencatat seluruh informasi mengenai anomali pada data log.
Decide : Menentukan apakah hasil tetap digunakan atau dilakukan pengujian ulang.
---

## Refleksi

> Pernahkah Anda melaporkan hasil riset/tugas dari single run? Apa risikonya? Bagaimana multiple run mengubah kepercayaan terhadap hasil?

**Pengalaman sebelumnya:**
> Pada tugas atau proyek sebelumnya saya sering hanya melakukan satu kali pengujian (single run) untuk memastikan sistem berjalan. Cara tersebut memiliki risiko karena hasil yang diperoleh belum tentu konsisten dan dapat dipengaruhi oleh kondisi tertentu, seperti gangguan jaringan, kesalahan pembacaan sensor, atau faktor lingkungan lainnya.
**Yang akan dilakukan berbeda:**
> Pada penelitian ini saya akan melakukan beberapa kali pengujian (multiple run) pada setiap skenario dengan konfigurasi yang sama. Setiap hasil akan didokumentasikan dalam data log sehingga dapat dibandingkan untuk mengetahui konsistensi sistem. Dengan demikian, hasil penelitian menjadi lebih valid, dapat dipercaya, dan lebih mudah direproduksi oleh peneliti lain.
