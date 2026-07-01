# WS-09: Implementation & Environment

> **Bab 9 — Implementasi Riset & Kontrol Lingkungan**

---

## Ringkasan Materi

### Implementasi Riset ≠ Coding Biasa

Tujuan implementasi riset bukan membuat software yang berfungsi, melainkan membangun **instrumen pengukuran yang konsisten**. Setiap modul harus di-mapping ke variabel (dari Bab 6), parameter harus config-driven, dan logging aktif dari hari pertama.

> **Mengapa reproducibility penting?** Sains dibangun di atas prinsip verifikasi — temuan harus bisa dikonfirmasi oleh peneliti lain. _Replicability crisis_ yang terjadi di banyak paper riset ML/AI disebabkan oleh environment tidak terdokumentasi: orang lain tidak bisa reproduksi, hasil diragukan, kepercayaan terhadap temuan hilang. Prinsip: **dokumentasi environment = snapshot kredibilitas riset Anda.**

### Reproducible Implementation Model

```
Design → Implementation → Environment Setup → Execution Consistency → Reproducibility → Trustworthy Result
```

Setiap transisi memiliki syarat:
- Design → Implementation: kode sesuai mapping variabel-ke-komponen
- Implementation → Environment: versi, dependency, seed, path, OS eksplisit
- Environment → Consistency: seed terkunci, urutan deterministik
- Consistency → Reproducibility: dokumentasi lengkap
- Reproducibility → Trust: siapa pun ikuti dokumentasi → hasil sama/serupa

### Repeatability vs Reproducibility

| Level | Peneliti | Environment | Hasil |
|-------|---------|-------------|-------|
| **Repeatability** | Sama | Sama | Sama persis |
| **Reproducibility** | Berbeda | Berbeda (ikuti docs) | Sama/serupa |

Capai **repeatability** dulu, baru **reproducibility**.

### Engineering vs Research Perspective

| Aspek | Engineering | Research |
|-------|-----------|---------|
| Tujuan | Sistem berfungsi untuk user | Instrumen pengukuran konsisten |
| Dependency | Update ke terbaru | Lock di versi spesifik |
| Testing | Unit, integration, E2E | Repeatability test (run ulang → sama?) |
| Dokumentasi | User guide, API docs | Environment spec, execution steps, expected output |
| Config | Default masuk akal | Setiap parameter eksplisit & adjustable |

### Jebakan Kognitif

1. Menunda environment setup → bug sulit dilacak
2. Tidak pakai version control → hasil tidak bisa direkonstruksi
3. Menolak Docker/container → "di laptop saya bisa" saat review
   - **Docker** = teknologi container yang "membungkus" aplikasi beserta seluruh dependency-nya dalam satu unit terisolasi. Hasilnya: kode berjalan identik di laptop, server, maupun reviewer lain. Intro singkat: `docker run -v $(pwd):/workspace environment-image python run_experiment.py`
4. 3× hasil sama ≠ repeatable (bisa cache/state tersimpan)

### Dependency Locking

Mengandalkan "install library terbaru" berbahaya: versi berbeda = perilaku berbeda = hasil tidak reproducible. Praktik:
- **Python**: buat `requirements.txt` dengan versi eksplisit: `scikit-learn==1.3.2`, lalu kunci dengan `pip freeze > requirements.txt`
- **Conda**: gunakan `conda env export > environment.yml` untuk snapshot lengkap
- **Node.js/R/Julia**: gunakan `package-lock.json` / `renv.lock` / `Project.toml` — semua fungsi serupa: lock versi + hash

### Istilah Penting

- **Environment Specification** — Deskripsi lengkap: hardware, OS, runtime, library + versi, config, seed
- **Dependency** — Komponen eksternal yang harus di-lock versinya
- **Config-driven** — Parameter dieksternalisasi ke file konfigurasi, bukan hardcode

---

## Template A.9 — Dokumentasi Setup Eksperimen

```
EXPERIMENT SETUP DOCUMENTATION

Hardware:
  CPU     : AMD Ryzen 5 7520U
  RAM     : 16gb
  GPU     :AMD Radeon Graphics 610M
  Storage : SSD 512 GB

Software:
  OS        : Windows 11
  Runtime   : PlatformIO
  Framework : Arduino Framework
  Simulator: wokwi

Dependencies:
| Library | Version | Sumber |Has/Checksum  |
|Arduino Core for
 ESP32|     3.x|Arduino Boards Manager|Default|
|  UniversalTelegramBot |   1.3.0      |  Arduino Library Manager      | Default |
|    ThingSpeak     |   2.1.1  |   Arduino Library Manager     |      Default |
|ESP32Servo|3.0.6|Arduino Library Manager|Default
|WiFi (ESP32)|Built-in|Arduino ESP32 Core|Built-in|
|WiFiClientSecure|Built-in|Arduino ESP32 Core|Built-in|

Konfigurasi:
  Config file     : Konfigurasi ditulis langsung pada source code (main.cpp), meliputi SSID WiFi, password, BOT Token Telegram, Chat ID, Channel ID, dan API Key ThingSpeak.
  Random seed     : Tidak digunakan (sistem tidak menggunakan algoritma acak atau machine learning)

  Hyperparameters : - Servo angle : 90°
- Interval pengiriman data : sesuai pembacaan sensor (real-time)
- Baud rate Serial Monitor : 115200
- WiFi timeout : default ESP32

Reproducibility Check:
  [ ☑ ] Dependency terdokumentasi (requirements.txt / lock file)
  [  ] Seed ditetapkan di semua level (Python, NumPy, framework)
  [ ☑ ] Config di version control
  [ ☑ ] README instruksi reproduksi lengkap
```

---

## Latihan 1 — Environment Specification

Dokumentasikan environment untuk eksperimen Anda (boleh environment saat ini atau yang direncanakan).

| Komponen | Spesifikasi |
|----------|------------|
| CPU | AMD Ryzen 5 7520U, 2.80 GHz|
| RAM | 16.0 GB (15.3 GB usable) |
| GPU | AMD Radeon Graphics|
| OS | Windows 11 (64-bit)|
| Runtime |Python Extension for VS Code v2026.4.0 |
| Framework |arduino  |
| Random Seed |42 |

**Dependencies (minimal 5):**

| Library | Version | Alasan Dibutuhkan |
|Arduino Core for ESP32|3.x|Menjalankan program pada board ESP32|
|  Wifi | Built-in | Menghubungkan ESP32 ke jaringan WiFi |
|WiFiClientSecure | Built-in|Komunikasi HTTPS dengan Telegram Bot |
|UniversalTelegramBot |1.3.0 | Mengirim notifikasi ke Telegram|
|ThingSpeak |2.1.1|Mengirim data monitoring ke ThingSpeak |
|ESP32Servo |3.0.6|Mengendalikan motor servo pembuka tutup sampah|

---

## Latihan 2 — Repeatability Test Plan

Rancang tes repeatability sederhana: jalankan kode yang sama 3× di environment yang sama.

| Run | Seed | Metrik Utama | Hasil Sama? |
|-----|------|-------------|-------------|
| 1 | Tidak digunakan| Sensor mendeteksi kondisi penuh, servo membuka 90°, notifikasi Telegram terkirim, data ThingSpeak berhasil dikirim | — |
| 2 |Tidak digunakan |Sensor mendeteksi kondisi penuh, servo membuka 90°, notifikasi Telegram terkirim, data ThingSpeak berhasil dikirim | [ ☑] Ya / [ ] Tidak |
| 3 |Tidak digunakan |Sensor mendeteksi kondisi penuh, servo membuka 90°, notifikasi Telegram terkirim, data ThingSpeak berhasil dikirim | [☑ ] Ya / [ ] Tidak |

**Jika hasil berbeda, kemungkinan penyebab:**

> Penyebab umum non-repeatability:
Perbedaan hasil dapat disebabkan oleh koneksi WiFi yang tidak stabil, keterlambatan respons server Telegram atau ThingSpeak, gangguan catu daya ESP32, atau kondisi sensor/switch yang tidak terbaca secara konsisten.
> - **Thermal throttling** Koneksi WiFi tidak stabil — ESP32 gagal terhubung ke internet sehingga notifikasi Telegram atau pengiriman data ke ThingSpeak mengalami keterlambatan atau gagal.
> - **Background process** — Gangguan dari jaringan, pembaruan sistem operasi, atau aplikasi lain pada komputer yang digunakan untuk pemrograman dapat memengaruhi proses upload program dan monitoring serial.
> - **Cache dari run sebelumnya** — hasil tersimpan di memori/disk sehingga run berikutnya tidak menjalankan komputasi penuh
> - **Random state tidak dikontrol di semua level** — Python seed di-set, tapi NumPy/PyTorch/TensorFlow punya seed independen

___________________________________________________

**Checklist kontrol yang sudah diterapkan:**
- [ ] Random seed di-set di semua level (tidak diterapkan karena sistem tidak menggunakan algoritma acak atau machine learning)
- [ ☑ ] Tidak ada background process yang mengganggu
- [ ☑ ] Cache dibersihkan antar-run
- [ ☑] Config file yang sama untuk semua run

---

## Latihan 3 — README Eksperimen

Tulis README minimum untuk eksperimen Anda (6 komponen wajib).

```
# Judul Eksperimen: “RANCANG BANGUN TEMPAT SAMPAH PINTAR BERBASIS INTERNET OF THINGS (IoT) UNTUK MEMILAH SAMPAH LOGAM DAN NON-LOGAM”

## 1. Environment
CPU : AMD Ryzen 5 7520U, 2.80 GHz
 RAM: 16.0 GB 15.3 GB usable
 OS : Windows 11 (64-bit)
Framework: Arduino Framework
Platform:PlatformIO
Simulator:Wokwi dan Thinkspeak
## 2. Installation
1. Install vs code
2. Instal Ekstensi PlatformIO
3. Install seluruh Library.

## 3. Data
-Kaleng= logam= Benar
-Plastik=Non-logam= Benar
-Kertas= Non-lLogam= Benar
-kaleng= Logam= Benar
## 4. Execution
Hubungkan ESP32 ke jaringan WiFi.
Jalankan program pada ESP32.
Ubah kondisi limit switch untuk mensimulasikan tempat sampah penuh atau kosong.
Amati:
Pergerakan servo.
Notifikasi Telegram.
Data yang masuk ke ThingSpeak.

## 5. Configuration
File konfigurasi:

main.cpp

Parameter utama:

SSID WiFi
Password WiFi
BOT Token Telegram
Chat ID Telegram
Channel ID ThingSpeak
Write API Key ThingSpeak
GPIO Servo = 18
GPIO Limit Switch = 14
Baud Rate = 115200
Delay pembacaan = 500 ms

## 6. Expected Output
Jika sensor mendeteksi kondisi penuh:

Servo membuka tutup tempat sampah hingga 90°.
Telegram mengirim pesan:
"Peringatan: Tempat Sampah sudah penuh!"
ThingSpeak menerima nilai 1.

Jika sensor mendeteksi kondisi kosong:

Servo kembali ke posisi 0°.
ThingSpeak menerima nilai 0.
Status ditampilkan pada Serial Monitor.

---

## Refleksi

> Apakah eksperimen Anda saat ini bisa direproduksi oleh orang lain tanpa bantuan Anda? Komponen apa yang masih hilang?

**Level saat ini:** [☑ ] Repeatability / [ ] Reproducibility / [ ] Belum keduanya
**Komponen yang belum terdokumentasi:**
> Belum tersedia README lengkap pada repositori proyek.
Belum menggunakan version control (Git) untuk mendokumentasikan perubahan kode.
Belum menyediakan file konfigurasi terpisah sehingga beberapa parameter masih ditulis langsung pada source code.
Belum dilakukan pengujian reproduksi oleh pengguna atau peneliti lain pada perangkat yang berbeda.