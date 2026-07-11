# WS-13: Data Preprocessing

> **Bab 13 — Preprocessing & Persiapan Data untuk Analisis**

---

## Ringkasan Materi

### Data Refinement Pipeline

```
Raw Data → Cleaning → Transformation → Normalization → Processed Data → Analysis Ready
```

Setiap tahap memiliki tujuan berbeda. **Preprocessing bukan langkah teknis biasa** — setiap keputusan preprocessing adalah keputusan riset yang bisa mengubah kesimpulan.

### Empat Prinsip Preprocessing

| Prinsip | Deskripsi |
|---------|----------|
| **Consistency** | Metode sama untuk data yang sama |
| **Transparency** | Setiap langkah terdokumentasi |
| **Reproducibility** | Orang lain bisa mengulang dengan hasil sama |
| **Minimal Distortion** | Ubah sesedikit mungkin; jika normalisasi tidak perlu, jangan lakukan |

### Cleaning Triad

| Masalah | Strategi | Risiko |
|---------|---------|--------|
| **Missing values** | | |
| — Listwise deletion | Missing < 5%, random | Data loss |
| — Mean/median imputation | Sedikit missing, dist. normal | Mengurangi variabilitas |
| — Model-based imputation | Banyak missing, pola sistematis | Introduces dependency |
| — Flag & separate | Missing karena alasan substantif | Kompleksitas analisis |
| **Duplikat** | Identifikasi → verifikasi → hapus | False positive (data mirip ≠ duplikat) |
| **Error format** | Standardisasi tipe, encoding | Kehilangan informasi saat konversi |

### Normalisasi — Kapan & Metode Mana

| Metode | Formula | Output | Sensitif Outlier? |
|--------|---------|--------|-------------------|
| Min-max | (x-min)/(max-min) | [0, 1] | Ya |
| Z-score | (x-mean)/std | Unbounded | Lebih robust |
| Robust scaling | (x-median)/IQR | Unbounded | Paling robust |

**Kunci:** Parameter normalisasi harus dihitung dari **training set saja** — bukan seluruh data. Pelanggaran = **data leakage**.

### Data Leakage Prevention

Data leakage terjadi ketika informasi dari test set "bocor" ke preprocessing:
- Normalisasi parameter dari seluruh dataset ← **SALAH**
- Cross-validation dilakukan sebelum split ← **SALAH**
- Feature selection menggunakan label test set ← **SALAH**

### Jebakan Kognitif

1. "Preprocessing cuma teknis — tidak perlu detail" → bisa ubah kesimpulan
2. "Lebih banyak preprocessing = lebih bersih = lebih baik" → over-processing distorsi data
3. "Normalisasi selalu diperlukan" → belum tentu, tergantung metode analisis
4. "Imputation sama untuk semua situasi" → strategi harus sesuai konteks

---

## Template A.13 — Preprocessing Documentation Log

```
PREPROCESSING LOG

Dataset           : Log pengujian Smart Trash Bin (ESP32)
Jumlah data awal  : 25 data hasil pengujian

Cleaning:
| Masalah | Jumlah Kasus | Penanganan | Justifikasi |
|---------|-------------|------------|-------------|
| Missing | 0             |  Tidak ada tindakan          |   Semua data berhasil direkam           |
| Duplikat|  1            |  Menghapus data duplikat     |   Terjadi akibat pembacaan sensor berulang tanpa perubahan kondisi          |
| Error   |  0            |   Tidak ada tindakan                   |    Format data konsisten         |

Transformation:
| Transformasi | Variabel | Detail | Alasan |
|-------------|----------|--------|--------|
|             |          |        |        |

Normalization:
  Metode    : Tidak dilakukan
  Alasan    : Data berupa status biner (0 dan 1), sehingga tidak memerlukan normalisasi.
  Parameter : Tidak berlaku

Leakage Check:
  [ ] Parameter normalisasi dari training set saja
  [ ] Tidak ada informasi test set dalam preprocessing
  [ ] Cross-validation dilakukan setelah split

Jumlah data akhir : 24 data
Script tersedia   : [x] Ya → path:src/main.cpp | [ ] Belum
```

---

## Latihan 1 — Cleaning Plan

Periksa dataset Anda (atau dataset contoh) dan dokumentasikan masalah yang ditemukan.

| Masalah | Jumlah Kasus | Penanganan | Justifikasi |
|---------|-------------|------------|-------------|
| *Contoh: Missing di kolom "label"* | *12 dari 500 (2.4%)* | *Listwise deletion* | *< 5%, distribusi random (MCAR)* |
|Data duplikat status sensor | 1 |Menghapus data duplikat |Disebabkan sensor membaca kondisi yang sama secara berulang |
|Missing data|0|Tidak ada tindakan | Seluruh data berhasil diterima|
|Error format|0|Tidak ada tindakan | Format data konsisten         |

**Jumlah data sebelum cleaning:** 25
**Jumlah data setelah cleaning:** 24
**Persentase data yang hilang/berubah:** 4%

---

## Latihan 2 — Normalisasi Decision

Tentukan apakah data Anda perlu normalisasi, dan jika ya, metode apa yang tepat.

| Variabel | Range Asli | Distribusi | Outlier? | Metode Normalisasi | Alasan |
|---------- |-----------|-----------|----------|-------------------|--------|
| Status Sensor |0–1    | Biner   | Tidak | Tidak perlu | Data sudah berupa nilai logika |
| Sudut Servo   |0°–90° | Diskrit | Tidak | Tidak perlu | Nilai tetap sesuai desain sisteme berbasis distance tidak digunakan |
| Status ThingSpeak|0–1|Biner      |Tidak |Tidak perlu |Sudah dalam bentuk numerik sederhana |
| Status Telegram  | Berhasil/Gagal|Kategori| Tidak|Tidak perlu |Data bersifat kategorikal |

**Apakah normalisasi diperlukan?** [ ] Ya / [x] Tidak
**Justifikasi:**
> Data yang digunakan berupa status biner dan kategori sehingga tidak memerlukan normalisasi. Seluruh data sudah berada pada rentang yang sesuai dengan kebutuhan analisis sistem IoT.

**Leakage check:**
- [ ✔️] Parameter dihitung dari training set saja
- [ ✔️] Normalisasi diterapkan setelah train-test split

---

## Latihan 3 — Preprocessing Report

Buat ringkasan preprocessing lengkap — dokumentasi yang cukup bagi orang lain untuk mereplikasi.

```
PREPROCESSING SUMMARY

1. Dataset:log hasil pengujian Smart Trash Bin berbasis ESP32.

2. Data awal: 25 records, 4 features
3. Cleaning:
   - Missing values: 0 kasus, metode:tidak ada tindakan.
   - Duplikat:1 kasus,  tindakan:data duplikat dihapus.
   - Error:  0 kasus, tindakan: format data valid
4. Transformation: 
- Status sensor dikonversi menjadi:
     LOW = Penuh
     HIGH = Kosong
- Timestamp diseragamkan ke format YYYY-MM-DD HH:MM:SS.
5. Normalisasi:  Tidak dilakukan karena seluruh variabel berupa status biner atau kategorikal.(metode: Tidak ada), parameter dari:Tidak berlaku
6. Data akhir: 24 records,4 features
7. Leakage check: [x] Lulus / [ ] Ada masalah
```

---

## Refleksi

> Apakah Anda pernah melakukan normalisasi "karena biasa dilakukan" tanpa mempertimbangkan apakah benar-benar diperlukan? Apa risiko over-preprocessing?

>Pada proyek ini normalisasi tidak dilakukan karena data yang digunakan berupa status biner dan kategorikal. Melakukan normalisasi tanpa kebutuhan dapat mengubah representasi data yang sebenarnya dan menambah kompleksitas proses analisis tanpa memberikan manfaat. Oleh karena itu, preprocessing hanya dilakukan pada tahap yang memang diperlukan, seperti menghapus data duplikat dan menyeragamkan format data agar hasil analisis tetap akurat dan mudah direproduksi.

