# CV Evaluator

Aplikasi evaluasi CV berbasis AI yang berjalan offline dan lokal di komputer Anda.

## Tentang Aplikasi

CV Evaluator adalah aplikasi desktop yang menggunakan kecerdasan buatan untuk mengevaluasi kecocokan antara Curriculum Vitae (CV) Anda dengan Job Description yang dilamar. Aplikasi ini berjalan sepenuhnya offline, sehingga data pribadi Anda tetap aman dan tidak pernah dikirim ke server manapun.

## Fitur Utama

- Offline - Tidak memerlukan koneksi internet setelah model diunduh
- Privasi Terjaga - Data CV dan JD tidak pernah dikirim ke server
- Dua Mode - Terminal dan Web Server
- Multi Format - Mendukung PDF, DOCX, DOC, ODT, dan TXT
- Multi Model - Mendukung berbagai model GGUF
- Evaluasi Otomatis - Memberikan skor, verdict, kekuatan, kelemahan, dan rekomendasi perbaikan
- Template CV - Template sederhana untuk membantu membuat CV yang optimal
- Stop Proses - Tombol untuk menghentikan evaluasi yang sedang berjalan
- Penyimpanan Hasil - Hasil evaluasi disimpan otomatis di folder results
- Loading Animation - Indikator progres untuk setiap tahap evaluasi
- Konfigurasi Fleksibel - Argumen CLI untuk mengatur model dan parameter token

## Persyaratan Sistem

| Komponen | Minimum | Direkomendasikan |
|----------|---------|------------------|
| RAM | 4 GB | 8 GB atau lebih |
| Storage | 2 GB | 5 GB atau lebih |
| OS | Windows 10, Linux | Windows 11, Linux |
| Prosesor | Intel Core i3 | Intel Core i5/i7 |

## Instalasi

### 1. Unduh Aplikasi

Unduh file executable sesuai sistem operasi Anda:
- Windows: `cv-evaluator.exe`
- Linux: `cv-evaluator`

### 2. Unduh Model

Aplikasi membutuhkan file model AI untuk berfungsi. Unduh salah satu model berikut dari Hugging Face:

**Pilihan Model:**

| Model | Ukuran File | RAM Minimal | Kualitas |
|-------|-------------|-------------|----------|
| [LFM2.5-1.2B-MOAT.i1-IQ2_M.gguf](https://huggingface.co/mradermacher/LFM2.5-1.2B-MOAT-i1-GGUF/resolve/main/LFM2.5-1.2B-MOAT.i1-IQ2_M.gguf) | ~500 MB | 4 GB | Rendah |
| [LFM2.5-1.2B-MOAT.i1-Q6_K.gguf](https://huggingface.co/mradermacher/LFM2.5-1.2B-MOAT-i1-GGUF/resolve/main/LFM2.5-1.2B-MOAT.i1-Q6_K.gguf) | ~1.8 GB | 8 GB | Sedang |
| [Llama-3.1-Storm-8B-Q3_K_XL.gguf](https://huggingface.co/bartowski/Llama-3.1-Storm-8B-GGUF/blob/main/Llama-3.1-Storm-8B-Q3_K_XL.gguf) | ~4.3 GB | 12 GB | Tinggi |

**Cara Unduh:**
1. Kunjungi halaman model di Hugging Face
2. Cari file dengan ekstensi `.gguf`
3. Unduh file yang sesuai dengan spesifikasi komputer Anda

**model default** : [LFM2.5-1.2B-MOAT.i1-Q6_K.gguf](https://huggingface.co/mradermacher/LFM2.5-1.2B-MOAT-i1-GGUF/resolve/main/LFM2.5-1.2B-MOAT.i1-Q6_K.gguf)
download model ini untuk dapat menjalankan app.

### 3. Struktur Folder

Buat folder dengan struktur berikut:

```
app/
├── cv-evaluator              # Executable (Linux) atau cv-evaluator.exe (Windows)
├── models/                   # Folder untuk file model
│   └── [model].gguf          # File model yang sudah diunduh
└── cv_template.txt           # File template CV (akan dibuat otomatis)
```

### 4. Jalankan Aplikasi

**Windows:**
```cmd
cv-evaluator.exe --as-host --port 8080
```

**Linux:**
```bash
chmod +x cv-evaluator
./cv-evaluator --as-host --port 8080
```

Buka browser dan akses: `http://localhost:8080`

## Cara Penggunaan

### Mode Web Server (Direkomendasikan)

1. Jalankan aplikasi dengan perintah:
   ```bash
   ./cv-evaluator --as-host --port 8080
   ```

2. Buka browser di `http://localhost:8080`

3. Upload file CV (PDF, DOCX, DOC, ODT, TXT)

4. Upload file Job Description atau isi teks JD

5. Klik tombol Evaluasi CV

6. Tunggu proses selesai, hasil akan ditampilkan

### Mode Terminal

```bash
# Evaluasi dengan file CV dan file JD
./cv-evaluator --cv=/path/to/cv.pdf --file-jobesk=/path/to/jobdesc.pdf

# Evaluasi dengan file CV dan teks JD
./cv-evaluator --cv=/path/to/cv.docx --text-jobesk="Deskripsi pekerjaan..."

# Generate template CV berdasarkan JD
./cv-evaluator --generate-template-cv --file-jobesk=/path/to/jobdesc.pdf
```

## Argumen Command Line

| Argumen | Default | Deskripsi |
|---------|---------|-----------|
| `--cv` | - | Path ke file CV |
| `--file-jobesk` | - | Path ke file Job Description |
| `--text-jobesk` | - | Job Description dalam teks |
| `--as-host` | `False` | Jalankan sebagai web server |
| `--port` | `8000` | Port untuk web server |
| `--host` | `0.0.0.0` | Host untuk web server |
| `--generate-template-cv` | `False` | Generate template CV berdasarkan JD |
| `--model` | `./models/Llama-3.1-Storm-8B-Q3_K_XL.gguf` | Path ke file model GGUF |
| `--context` | `32768` | Max context tokens |
| `--chunk` | `6000` | Max chunk characters untuk ringkasan |
| `--output` | `4096` | Max output tokens dari model |
| `--version` | - | Tampilkan versi aplikasi |

## Penggunaan dengan Custom Model dan Konfigurasi Token

### Mengganti Model

Secara default, aplikasi menggunakan model `Llama-3.1-Storm-8B-Q3_K_XL.gguf`. Anda dapat mengganti model dengan argumen `--model`:

```bash
# Menggunakan model LFM2.5
./cv-evaluator --cv=cv.pdf --file-jobesk=jobdesc.pdf --model ./models/LFM2.5-1.2B-MOAT.i1-Q6_K.gguf

# Menggunakan model lain
./cv-evaluator --cv=cv.pdf --file-jobesk=jobdesc.pdf --model ./models/model_lain.gguf
```

### Mengatur Parameter Token

Anda dapat mengatur tiga parameter token sesuai kebutuhan:

1. **`--context`** - Max context tokens (seberapa banyak teks yang dapat diproses model)
2. **`--chunk`** - Max chunk characters (seberapa besar potongan teks per bagian)
3. **`--output`** - Max output tokens (seberapa panjang respons yang dihasilkan model)

```bash
# Konfigurasi untuk model besar (Llama 8B)
./cv-evaluator --cv=cv.pdf --file-jobesk=jobdesc.pdf --context 32768 --chunk 6000 --output 4096

# Konfigurasi untuk model kecil (LFM2.5 1.2B)
./cv-evaluator --cv=cv.pdf --file-jobesk=jobdesc.pdf --context 2048 --chunk 1500 --output 1800

# Konfigurasi untuk CV yang sangat panjang
./cv-evaluator --cv=cv.pdf --file-jobesk=jobdesc.pdf --context 16384 --chunk 4000 --output 2048
```

### Rekomendasi Konfigurasi Berdasarkan Model

| Model | `--context` | `--chunk` | `--output` |
|-------|-------------|-----------|------------|
| LFM2.5-1.2B-MOAT.i1-IQ2_M | 2048 | 1500 | 1800 |
| LFM2.5-1.2B-MOAT.i1-Q6_K | 2048 | 1500 | 1800 |
| Llama-3.1-Storm-8B-Q3_K_XL | 32768 | 6000 | 4096 |
| Gemma 3n 8B | 32768 | 6000 | 4096 |
| Mistral 7B | 32768 | 5000 | 3072 |

### Contoh Penggunaan Lengkap

```bash
# Menggunakan model LFM2.5 dengan konfigurasi optimal
./cv-evaluator --cv=cv.pdf --file-jobesk=jobdesc.pdf --model ./models/LFM2.5-1.2B-MOAT.i1-Q6_K.gguf --context 2048 --chunk 1500 --output 1800

# Menggunakan model Llama dengan konfigurasi optimal
./cv-evaluator --cv=cv.pdf --file-jobesk=jobdesc.pdf --model ./models/Llama-3.1-Storm-8B-Q3_K_XL.gguf --context 32768 --chunk 6000 --output 4096

# Mode web server dengan model dan konfigurasi kustom
./cv-evaluator --as-host --port 8080 --model ./models/model.gguf --context 32768 --chunk 6000 --output 4096

# Menampilkan versi dan konfigurasi yang digunakan
./cv-evaluator --version
```

## Format CV yang Direkomendasikan

Untuk hasil evaluasi terbaik, gunakan format CV yang sederhana dan terstruktur:

```
RINGKASAN PROFESIONAL
[2-3 kalimat tentang diri Anda]

PENGALAMAN KERJA
1. [Perusahaan] | [Posisi] | [Tahun]
   - [Tanggung jawab 1]
   - [Tanggung jawab 2]
   - [Pencapaian]

PENDIDIKAN
- [Gelar] | [Institusi] | [Tahun]

KEAHLIAN TEKNIS
- [Skill 1]
- [Skill 2]
- [Skill 3]

BAHASA
- [Bahasa]: [Tingkat]
```

### Tips Membuat CV

- Hilangkan informasi pribadi (nama, alamat, telepon) karena tidak mempengaruhi penilaian
- Fokus pada pengalaman dan keahlian yang relevan dengan posisi yang dilamar
- Maksimum 3000 karakter untuk hasil optimal
- Gunakan format yang jelas dan konsisten
- Gunakan template yang disediakan aplikasi sebagai panduan

## Hasil Evaluasi

Hasil evaluasi disimpan di folder `results/` dengan format JSON:

```json
{
  "timestamp": "20260906_031122",
  "cv_file": "cv_saya.pdf",
  "jd_file": "jobdesc.pdf",
  "result": {
    "score": 67,
    "verdict": "Sangat Cocok",
    "strengths": ["...", "..."],
    "weaknesses": ["...", "..."],
    "improvement_suggestions": ["...", "..."]
  },
  "raw_output": "..."
}
```

### Skor dan Verdict

| Skor | Verdict | Keterangan |
|------|---------|------------|
| 80-100 | Sangat Cocok | CV sangat sesuai dengan posisi yang dilamar |
| 60-79 | Cocok | CV sesuai dengan posisi yang dilamar |
| 40-59 | Cukup Cocok | CV cukup sesuai, masih ada beberapa kekurangan |
| 0-39 | Kurang Cocok | CV kurang sesuai dengan posisi yang dilamar |

## Troubleshooting

### Error: File model tidak ditemukan

**Penyebab:** File model tidak ada di folder models/

**Solusi:**
1. Pastikan file model sudah diunduh
2. Pastikan file model berada di folder models/
3. Periksa path model dengan argumen `--model`

### Error: Requested tokens exceed context window

**Penyebab:** CV atau JD terlalu panjang untuk konteks model

**Solusi:**
1. Kurangi panjang teks CV atau JD
2. Gunakan template CV yang disediakan
3. Tingkatkan parameter `--context` jika model mendukung
4. Gunakan model dengan konteks lebih besar (Llama 8B)

### Error JSON saat evaluasi

**Penyebab:** Output model terpotong karena batas token

**Solusi:**
1. Aplikasi akan otomatis mencoba memperbaiki JSON yang terpotong
2. Jika masih error, cek file debug di folder `results/`
3. Tingkatkan parameter `--output` untuk memberi ruang lebih pada output

### File .doc tidak terbaca

**Penyebab:** Aplikasi memerlukan antiword untuk membaca file .doc

**Solusi:**
- Linux: `sudo apt-get install antiword`
- Windows: Download dari http://www.winfield.demon.nl/

### Aplikasi lambat atau macet

**Penyebab:** Model terlalu berat untuk spesifikasi komputer

**Solusi:**
1. Gunakan model yang lebih ringan (IQ2_M)
2. Tutup aplikasi lain yang menggunakan banyak RAM
3. Gunakan model dengan kuantisasi lebih rendah
4. Kurangi parameter `--context` dan `--output`

## File dan Folder

| File/Folder | Deskripsi |
|-------------|-----------|
| `cv-evaluator` / `cv-evaluator.exe` | File executable aplikasi |
| `models/` | Folder untuk menyimpan file model |
| `results/` | Folder hasil evaluasi (otomatis dibuat) |
| `cv_template.txt` | Template CV (otomatis dibuat) |
| `evaluation_*.json` | File hasil evaluasi |
| `debug_*.json` | File debug jika terjadi error |

## Dukungan Model

Aplikasi ini mendukung semua model dalam format GGUF. Beberapa model yang direkomendasikan:

| Model | Kelebihan | Kekurangan | Konteks Maks |
|-------|-----------|------------|--------------|
| LFM2.5-1.2B-MOAT | Ringan, cepat | Kualitas evaluasi sedang | 2048 |
| Llama-3.1-Storm-8B | Kualitas tinggi | Membutuhkan RAM besar | 32768 |
| Gemma 3n 8B | Kualitas tinggi | Membutuhkan RAM besar | 32768 |
| Mistral 7B | Kualitas baik | Membutuhkan RAM besar | 32768 |

## Keamanan dan Privasi

- Aplikasi berjalan 100% offline
- Data CV dan JD tidak pernah dikirim ke server manapun
- Semua proses berjalan di komputer lokal
- Hasil evaluasi disimpan secara lokal

## Lisensi

Aplikasi ini menggunakan lisensi MIT.

---

Dibuat untuk membantu Anda mengevaluasi CV secara cepat dan akurat.