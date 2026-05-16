# WS-06: System-Experiment Mapping

> **Bab 6 — System Design sebagai Experimental Artifact**

---

## Ringkasan Materi

### Sistem = Instrumen Pengujian, Bukan Produk

Seorang engineer bertanya "apakah sistem bekerja?" — seorang peneliti bertanya "apa yang bisa dibuktikan sistem ini?" Sistem dalam riset adalah **artifact** — objek yang sengaja dibuat untuk menguji klaim spesifik.

### System as Experiment Model

```
RQ → Variable → System Component → Experimental Setup → Output
```

Setiap komponen sistem harus bisa ditelusuri ke variabel riset (top-down), dan setiap pengukuran harus menjawab RQ (bottom-up).

### Mapping Variabel ke Komponen

| Tipe Variabel | Peran di Sistem | Contoh |
|---------------|----------------|--------|
| **IV** (Independent) | Modul yang bisa di-toggle/swap | Algoritma A vs B |
| **DV** (Dependent) | Modul pengukuran | Logger, metrics collector |
| **CV** (Control) | Config yang dikunci | Dataset, parameter tetap |

Jika variabel tidak bisa di-map ke komponen apapun → arsitektur perlu didesain ulang.

### 4 Prinsip Desain Eksperimental

| Prinsip | Pertanyaan Kunci |
|---------|-----------------|
| **Traceability** | Komponen ini melayani variabel yang mana? |
| **Modularity** | Bisakah IV diubah tanpa memengaruhi yang lain? |
| **Controllability** | Apakah CV dieksternalisasi ke config file? |
| **Measurability** | Apakah sistem otomatis menghasilkan data yang dibutuhkan? |

### Variable Isolation melalui Arsitektur

- **Modular architecture** — Pisahkan berdasarkan variabel
- **Configuration-driven** — Ubah config (YAML/JSON), bukan code
- **Feature toggles** — On/off flag untuk ablation study

  Contoh config YAML dengan feature toggles:
  ```yaml
  model:
    type: cnn          # IV: ganti "rf" untuk kondisi baseline
  features:
    use_temporal: true  # toggle komponen temporal
    use_normalization: true  # toggle preprocessing
  experiment:
    seed: 42
    runs: 5
  ```
  Dengan pendekatan ini, berbeda kondisi eksperimen = berbeda satu baris config, **tanpa mengubah kode**.

### Research vs Engineering

| Aspek | Engineering | Research |
|-------|------------|----------|
| Tujuan sistem | Memenuhi kebutuhan user | Menguji hipotesis, menghasilkan bukti |
| Arsitektur | Optimasi performa & skalabilitas | Optimasi isolasi variabel & reprodusibilitas |
| Konfigurasi | Sering hardcoded | Dieksternalisasi ke config file |
| Fitur tambahan | Menambah nilai user | Menambah noise jika tidak terkait RQ |

### Istilah Penting

- **Artifact** — Objek yang sengaja dibuat untuk memecahkan masalah atau menguji proposisi
- **Traceability** — Kemampuan menelusuri hubungan RQ → variabel → komponen → output
- **Variable Isolation** — Mengubah hanya satu variabel sambil menahan yang lain konstan
- **Ablation Study** — Menguji kontribusi tiap komponen dengan melepasnya satu per satu
- **Configuration-driven Execution** — Semua parameter di config file, bukan hardcoded

---

## Template A.6 — Mapping RQ ke Arsitektur Sistem

```
SYSTEM-EXPERIMENT MAPPING

Research Question:Apakah sistem pemilahan sampah anorganik berbasis ESP32 menggunakan sensor multivariable menghasilkan akurasi klasifikasi dan delay notifikasi yang lebih baik dibanding sistem sensor tunggal?

Variable → Component Mapping:
| Variabel | Tipe | Komponen Sistem | Cara Manipulasi/Pengukuran |
|----------|------|-----------------|---------------------------|
|   Jenis sensor       | IV   |Modul sensor ESP32                 |   Mengganti mode sensor tunggal  multisensor melalui konfigurasi                        |
|    Delay notifikasi      | DV   |  Modul Telegram Bot               |   Mengukur waktu dari deteksi hingga notifikasi diterima                        |
|     Jenis sampah     | CV   |  Objek pengujian               |    Menggunakan jenis sampah yang sama pada setiap eksperimen                       |

4 Prinsip Desain:
  [ ☑ ] Traceability — Setiap komponen bisa ditelusuri ke variabel
  [ ☑ ] Variable Isolation — IV bisa diubah tanpa mengubah CV
  [ ☑ ] Measurement Integration — Pengukuran DV built-in
  [ ☑ ] Reproducibility — Setup bisa direkonstruksi

Experimental Setup:
  Input data     :Sampah anorganik (plastik, kaleng, kaca)
  Parameter      :-Mode sensor (single/multisensor)
                  -Jumlah pengujian
                  -Koneksi internet tetap
                  -ESP32 configuration
  Output format  :Delay notification (detik)

---

## Latihan 1 — Variable-to-Component Mapping

Gunakan RQ dan variabel dari WS-05. Petakan ke komponen sistem.

**RQ:** Apakah sistem multisensor berbasis ESP32 meningkatkan accuracy klasifikasi sampah dan mengurangi delay notifikasi dibanding sensor tunggal

| Variabel | Tipe | Komponen Sistem | Cara Manipulasi / Pengukuran |
|----------|------|-----------------|---------------------------|
| Jenis sensor| IV | Modul sensor ESP32 (single sensor ↔ multisensor)| Mengubah konfigurasi sensor pada sistem|
| Akurasi klasifikasi| DV | Modul klasifikasi sampah|Menghitung jumlah klasifikasi benar dari total pengujian |
|Kondisi jaringan | CV | Modul WiFi ESP32| Menggunakan koneksi internet yang sama selama pengujian|

**Apakah semua variabel bisa di-map?** [☑ ] Ya / [ ] Tidak
> Jika tidak, komponen apa yang perlu ditambahkan? Tidak perlu tambahan karena semua variabel sudah memiliki komponen sistem yang sesuai.
---

## Latihan 2 — 4 Prinsip Desain

Evaluasi desain sistem terhadap 4 prinsip.

| Prinsip | Status | Bukti / Penjelasan |
|---------|--------|-------------------|
| Traceability |  ✅ — Setiap modul terhubung langsung dengan variabel penelitian |
| Modularity |✅ |Sensor dapat diganti tanpa mengubah modul lain |
| Controllability | ✅|Parameter eksperimen dapat diatur melalui konfigurasi |
| Measurability |✅ |Sistem otomatis mencatat accuracy dan delay |

**Prinsip mana yang paling sulit dipenuhi?** Measurability
**Strategi untuk mengatasinya:**
>Menambahkan sistem logging otomatis pada ESP32 dan Telegram untuk mencatat waktu deteksi dan hasil klasifikasi secara real-time.
---

## Latihan 3 — Ablation Study Planning

Jika sistem memiliki 3 komponen utama, rencanakan ablation study.

> **Panduan jumlah kondisi:** Untuk 3 komponen (A, B, C), kondisi minimal yang direkomendasikan:
> Full + (-A) + (-B) + (-C) = **4 kondisi dasar**. Jika waktu memungkinkan, tambahkan kombinasi ganda: (-A,-B), (-A,-C), (-B,-C) = **7 kondisi**. Sesuaikan dengan *computational cost* dan tenggat waktu penelitian.

| Kondisi | Komponen A | Komponen B | Komponen C | Hasil yang Diharapkan |
|---------|-----------|-----------|-----------|----------------------|
| Full | ✅ Multisensor| ✅ Telegram Notification | ✅ Data Logging| Accuracy dan monitoring optimal |
| – A | ❌ Single sensor | ✅ | ✅ |Accuracy menurun |
| – B | ✅ | ❌ Tanpa Telegram | ✅ |Tidak ada monitoring real-time |
| – C | ✅ | ✅ | ❌ Tanpa logging |Data eksperimen tidak lengkap |

**Komponen mana yang diprediksi paling berkontribusi?** Komponen multisensor
**Mengapa?**
> Karena multisensor secara langsung memengaruhi kemampuan sistem dalam membedakan jenis sampah sehingga berpengaruh besar terhadap accuracy klasifikasi.

---

## Refleksi

> Apa risiko jika sistem dibangun seperti produk (monolitik, fitur lengkap) lalu baru dilakukan eksperimen? Mengapa arsitektur modular penting untuk riset?

**Jawaban:**
>Jika sistem dibangun seperti produk monolitik dengan banyak fitur tambahan, maka eksperimen menjadi sulit dikontrol karena banyak variabel saling memengaruhi. Hal ini dapat menyebabkan hasil penelitian tidak valid dan sulit direproduksi.
> Arsitektur modular penting dalam riset karena memungkinkan setiap variabel diuji secara terpisah, mempermudah eksperimen, serta meningkatkan traceability dan reproducibility penelitian.