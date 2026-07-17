# WS-15: Scientific Writing

> **Bab 15 — Penulisan Ilmiah**

---

## Ringkasan Materi

### Scientific Argument Flow

```
Problem → Gap → RQ → Method → Result → Analysis → Conclusion → Contribution
```

Paper ilmiah adalah **satu argumen utuh** dari masalah ke kontribusi. Setiap node harus terhubung logis ke node sebelum dan sesudahnya.

### Struktur IMRAD

| Section | Peran | Pertanyaan Kunci |
|---------|-------|-----------------|
| **Introduction** | Motivasi + frame | Why is this needed? |
| **Method** | Deskripsi (reproducible) | How was it done? |
| **Results** | Laporan objektif | What was found? |
| **Discussion** | Interpretasi + refleksi | What does it mean? |
| **Conclusion** | Ringkasan + kontribusi | So what? |

### Logical Flow — "Red Thread"

Setiap paragraf menjawab satu pertanyaan dan memicu pertanyaan berikutnya. Alur logis ini harus terasa di tiga level:
1. **Antar-kalimat** dalam paragraf
2. **Antar-paragraf** dalam section
3. **Antar-section** dalam paper

### Internal Consistency

Setiap elemen yang dijanjikan di Introduction harus hadir di Discussion/Conclusion.

**Consistency Matrix:**
```
           Intro  Method  Result  Discuss  Conclude
RQ1          ✓      ✓       ✓       ✓        ✓
RQ2          ✓      ✓       ✓       ✗ ←      ✓
Metrik-X     ✗      ✗       ✓ ←     ✗        ✗
```
**Masalah:** RQ2 dibahas di semua bagian kecuali Discussion. Metrik-X muncul di Result tapi tidak diperkenalkan di Method.

### Writing Quality Triad

| Kualitas | Deskripsi | Contoh Buruk → Baik |
|----------|----------|---------------------|
| **Clarity** | Dipahami sekali baca | "Performa meningkat" → "Accuracy meningkat dari 85.3% ke 89.7%" |
| **Precision** | Istilah eksak, tanpa ambiguitas | "signifikan" → "signifikan secara statistik (p=0.003, d=1.2)" |
| **Conciseness** | Setiap kata menambah informasi | Hapus kalimat redundan, filler words |

### Urutan Penulisan yang Disarankan

1. **Method & Results** — paling stabil, tulis pertama
2. **Discussion** — interpretasi berdasarkan hasil
3. **Introduction** — frame sesuai temuan aktual
4. **Abstract & Conclusion** — terakhir

### Target Jumlah Kata

| Section | Target |
|---------|--------|
| Introduction | 500–700 |
| Related Work | 700–1000 |
| Method | 800–1200 |
| Results | 500–800 |
| Discussion | 600–900 |
| Conclusion | 200–400 |

### Jebakan Kognitif

1. "Lebih panjang = lebih lengkap" → conciseness lebih berharga
2. "Introduction harus ditulis pertama" → justru ditulis terakhir
3. "Jargon teknis = lebih ilmiah" → clarity lebih penting
4. "Discussion = ringkasan Results" → Discussion = interpretasi + konteks

---

## Template A.15 — Paper Structure Checklist

```
PAPER STRUCTURE CHECKLIST

Title   : Sistem Monitoring Tempat Sampah Pintar Berbasis IoT Menggunakan ESP32, Telegram Bot, dan ThingSpeak  
Target  : [ ] Jurnal  [ ] Konferensi  [✓] Laporan

Section Check:
  [✓] Abstract — masalah, metode, hasil utama, kontribusi (max 250 kata)
  [✓] Introduction — konteks → gap → RQ → kontribusi → struktur paper
  [✓] Related Work — concept-centric, gap positioning
  [✓] Method — reproducible: desain, variabel, metrik, setup, prosedur
  [✓] Results — tabel + grafik + observasi (tanpa interpretasi)
  [✓] Discussion — interpretasi, perbandingan, implikasi, limitation
  [✓] Conclusion — jawaban RQ, kontribusi, future work

Consistency Matrix:
  [✓] RQ di Introduction = RQ di Method = RQ di Conclusion
  [✓] Variabel di Method = variabel di Results
  [✓] Klaim di Discussion didukung data di Results
  [✓] Limitasi di Discussion di-address di Conclusion/Future Work

Writing Quality:
  [✓] Clarity — mudah dipahami tanpa re-read
  [✓] Precision — tidak ada istilah ambigu
  [✓] Conciseness — tidak ada kalimat redundan
```

---

## Latihan 1 — Paper Outline

Buat outline paper untuk riset Anda menggunakan struktur IMRAD.

| Section | Konten Utama (2-3 kalimat) | Target Kata |
|---------|---------------------------|------------|
| Abstract | Penelitian ini mengembangkan sistem monitoring tempat sampah pintar berbasis ESP32 menggunakan limit switch sebagai pendeteksi kondisi penuh. Sistem mengirimkan notifikasi melalui Telegram dan menyimpan data ke ThingSpeak sehingga monitoring dapat dilakukan secara real-time. | 200-250 |
| Introduction | Pengelolaan tempat sampah masih banyak dilakukan secara manual sehingga petugas sering terlambat mengetahui kondisi tempat sampah. Penelitian ini menawarkan sistem monitoring berbasis IoT untuk mendeteksi kondisi tempat sampah dan mengirimkan informasi secara otomatis. | 500-700 |
| Related Work | Membahas penelitian sebelumnya mengenai smart trash bin, penggunaan ESP32, Telegram Bot, ThingSpeak, serta keterbatasan sistem monitoring yang ada sehingga diperoleh research gap penelitian. | 700-1000 |
| Method | Menjelaskan perancangan perangkat keras dan perangkat lunak, konfigurasi ESP32, limit switch, servo, Telegram Bot, ThingSpeak, serta prosedur pengujian setiap skenario. | 800-1200 |
| Results | Menyajikan hasil pengujian berupa keberhasilan deteksi sensor, respon servo, pengiriman notifikasi Telegram, serta pencatatan data pada ThingSpeak dalam bentuk tabel dan grafik. | 500-800 |
| Discussion | Menjelaskan makna hasil pengujian, kelebihan dan keterbatasan sistem, serta membandingkan hasil penelitian dengan penelitian terdahulu. | 600-900 |
| Conclusion | Menyimpulkan bahwa sistem berhasil melakukan monitoring kondisi tempat sampah secara otomatis menggunakan ESP32 serta memberikan rekomendasi pengembangan pada penelitian selanjutnya. | 200-400 |

---

## Latihan 2 — Consistency Matrix

Buat consistency matrix untuk memverifikasi internal consistency paper Anda.

|  | Intro | Method | Result | Discussion | Conclusion |
|--|-------|--------|--------|-----------|-----------|
| *Contoh: RQ1* | ✓ | ✓ | ✓ | ✓ | ✓ |
| *Contoh: Metrik-X* | ✓ | ✓ | ✓ | ✓ | ✓ |
| RQ1 | ✓ | ✓ | ✓ | ✓ | ✓ |
| RQ2 | ✓ | ✓ | ✓ | ✓ | ✓ |
| Metrik utama | ✓ | ✓ | ✓ | ✓ | ✓ |
| Variabel IV  | ✓ | ✓ | ✓ | ✓ | ✓ |
| Variabel DV   | ✓| ✓ | ✓ | ✓ | ✓ |
| Klaim/kontribusi | ✓ | ✓ | ✓ | ✓ | ✓ |

**Isi setiap sel:** ✓ (ada & konsisten), ✗ (missing), ~ (ada tapi inkonsisten)

**Inkonsistensi yang ditemukan**:
> Tidak ditemukan inkonsistensi. Seluruh research question, variabel, metode, hasil, dan kontribusi telah konsisten pada setiap bagian paper.

**Tindakan perbaikan**:
> Memastikan seluruh hasil pengujian yang ditampilkan pada bagian Results dibahas kembali pada bagian Discussion dan diringkas pada bagian Conclusion sehingga alur penulisan tetap konsisten.

---

## Latihan 3 — Writing Quality Check

Ambil satu paragraf dari tulisan Anda (atau tulis paragraf baru) dan evaluasi kualitasnya.

**Paragraf asli:**
> (Sistem monitoring tempat sampah pintar menggunakan ESP32 dibuat untuk membantu pengguna mengetahui kondisi tempat sampah. Sistem menggunakan limit switch sebagai sensor, servo sebagai aktuator, Telegram sebagai media notifikasi, dan ThingSpeak sebagai media monitoring data.)

| Kriteria | Evaluasi | Perbaikan |
|----------|---------|-----------|
| Clarity | Alur kerja sistem belum dijelaskan secara runtut.| Menjelaskan urutan proses mulai dari deteksi sensor hingga pengiriman notifikasi.|
| Precision |Istilah "membantu pengguna" masih terlalu umum.|Diganti menjadi "memantau kondisi tempat sampah secara otomatis dan real-time". |
| Conciseness |Masih terdapat kalimat yang dapat dipadatkan. |Menggabungkan informasi yang memiliki makna serupa agar lebih ringkas. |

**Paragraf setelah perbaikan:**
> (Sistem monitoring tempat sampah pintar berbasis ESP32 menggunakan limit switch untuk mendeteksi kondisi tempat sampah. Ketika sensor mendeteksi kondisi penuh, ESP32 menggerakkan servo, mengirimkan notifikasi melalui Telegram, dan menyimpan status ke ThingSpeak sehingga kondisi tempat sampah dapat dipantau secara otomatis dan real-time.)

---

## Refleksi

> Apa perbedaan antara menulis "tentang" riset dan menulis sebagai "argumen" riset? Bagaimana urutan penulisan (Method → Discussion → Introduction) mengubah kualitas tulisan?

> Menulis tentang riset hanya menjelaskan proses yang dilakukan selama penelitian, sedangkan menulis sebagai argumen riset menyusun hubungan logis antara masalah, metode, hasil, dan kontribusi penelitian sehingga pembaca memahami alasan mengapa penelitian dilakukan dan apa manfaat temuannya.
> Menulis dimulai dari Method, kemudian Results dan Discussion, lalu Introduction, membuat isi paper lebih konsisten karena latar belakang dan tujuan penelitian disusun berdasarkan hasil eksperimen yang telah diperoleh. Dengan demikian, setiap bagian saling mendukung dan menjawab research question secara utuh.