# 🎬 LearnVid AI

> Platform web berbasis AI yang secara otomatis menghasilkan **video edukatif animasi** dari topik apa pun yang dimasukkan pengguna — dirender menggunakan Manim dan didukung oleh Google Gemini.

---

## 📌 Deskripsi Proyek

LearnVid AI memungkinkan pengguna mengetikkan topik sains atau matematika apa pun, lalu sistem AI secara otomatis: (1) membuat skrip edukatif terstruktur via Gemini Flash, (2) menghasilkan kode animasi Manim bergaya 3Blue1Brown via Gemini Pro, (3) merender video animasi 720p, dan (4) menyimpan & menyajikan video ke pengguna via chat.

Proyek ini merupakan Final Project kuliah **Pengembangan Aplikasi Berbasis Web**.

---

## ✨ Fitur Utama

- 🤖 **AI Script Generator** — Gemini 2.5 Flash menyusun rencana edukatif 6-langkah: analisis topik, tujuan pembelajaran, rencana visual, skrip narasi, hingga pertanyaan kuis
- 🎨 **Manim Code Generator** — Gemini 2.5 Pro mengubah rencana tersebut menjadi kode animasi Python (Manim) bergaya 3Blue1Brown
- 🎬 **Auto Rendering** — Video dirender otomatis di server dengan validasi & auto-fix error hingga 10 percobaan
- ☁️ **Cloudflare R2 Storage** — Video diunggah ke R2 dan tersedia via URL publik
- 💬 **Chat Interface** — Antarmuka berbasis chat dengan riwayat percakapan dan galeri video
- 📋 **Gallery** — Pengguna dapat melihat kembali semua video yang pernah dibuat
- 🔐 **Auth System** — Register, login, sesi pengguna berbasis cookie terenkripsi (itsdangerous + bcrypt)
- 📡 **SSE Streaming** — Progress pembuatan video di-stream real-time ke browser via Server-Sent Events

---

## 🛠️ Tech Stack

| Layer | Teknologi |
| --- | --- |
| Backend | Python, FastAPI |
| AI / LLM | Google Gemini 2.5 Flash & Pro (via LangChain) |
| Animasi | Manim v0.19 (Mathematical Animation Engine) |
| Database | PostgreSQL + SQLModel (SQLAlchemy) |
| Storage | Cloudflare R2 (boto3 / S3-compatible) |
| Frontend | HTML, CSS, JavaScript (Jinja2 templates) |
| Auth | Cookie sesi terenkripsi (itsdangerous), bcrypt |
| Server | Uvicorn (ASGI) |

---

## 📂 Struktur Direktori

```
LearnVidAI/
├── MAIN/
│   ├── AI/
│   │   ├── app.py                  # Orkestrasi: generate_educational_video()
│   │   ├── script_generator.py     # Stage 1: Gemini → rencana edukatif (JSON)
│   │   ├── manim_code_generator.py # Stage 2: Gemini → kode Manim (Python)
│   │   └── animation_creator.py   # Render, validasi & auto-fix kode Manim
│   ├── main.py                     # FastAPI app (routes, auth, DB, SSE)
│   ├── templates/                  # HTML pages (chat, gallery, login, dll)
│   └── static/                     # CSS, font, logo
├── requirements.txt
├── run.sh
├── before-install-manim.sh
└── deploy-config.sh
```

---

## ⚙️ Cara Menjalankan

### Prasyarat

- Python 3.10+
- LaTeX (MikTeX / TeX Live) — wajib untuk Manim
- FFmpeg
- PostgreSQL

### 1. Clone Repository

```bash
git clone https://github.com/NureSketsa/LearnVidAI.git
cd LearnVidAI
```

### 2. Install dependensi sistem (Linux)

```bash
bash before-install-manim.sh
```

### 3. Install Python packages

```bash
pip install -r requirements.txt
```

### 4. Konfigurasi Environment

Buat file `.env` di `MAIN/` atau root project:

```env
GOOGLE_API_KEY=your_google_api_key
DATABASE_URL=postgresql://user:password@host/dbname
SECRET_KEY=your_secret_key
R2_ENDPOINT=https://<account>.r2.cloudflarestorage.com
R2_ACCESS_KEY_ID=your_r2_access_key
R2_SECRET_ACCESS_KEY=your_r2_secret_key
R2_BUCKET_NAME=your_bucket_name
R2_BUCKET_PUBLIC_URL=https://your-public-domain.com
```

### 5. Jalankan Server

```bash
bash run.sh
# atau manual:
uvicorn MAIN.main:app --reload --host 0.0.0.0 --port 8000
```

Buka browser: `http://localhost:8000/learnvid-ai/`

---

## 🔄 Alur Kerja Sistem

**Input topik** → Stage 1: Gemini Flash buat rencana edukatif JSON → Stage 2: Gemini Pro buat kode Manim Python → **Render** Manim (auto-fix jika error, maks 10 percobaan) → **Upload** ke Cloudflare R2 → **Tampil** di chat via SSE streaming.

---

## 🎯 Cara Penggunaan

1. Buka aplikasi dan **daftar / login**
2. Mulai **chat baru**
3. Klik tombol video dan masukkan **topik** — contoh: `Teorema Pythagoras`, `Fotosintesis`, `Hukum Newton`
4. Tunggu proses AI — progress tampil real-time
5. **Tonton** video animasi langsung di browser
6. Lihat semua video lama di halaman **Gallery**

---

## 📦 Dependensi Utama

- `fastapi`, `uvicorn` — Web framework & server
- `sqlmodel`, `psycopg2-binary` — ORM & koneksi PostgreSQL
- `langchain-google-genai` — Integrasi LangChain + Gemini
- `manim==0.19.0` — Render animasi matematis
- `boto3` — Upload ke Cloudflare R2
- `itsdangerous`, `passlib[bcrypt]` — Autentikasi & keamanan sesi

---

## 👥 Tim Pengembang

Dikembangkan oleh kelompok **NureSketsa** sebagai Final Project.

> Tambahkan nama dan NRP anggota tim di sini.

---

## 📄 Lisensi

Proyek ini dibuat untuk keperluan akademik — **Final Project Pengembangan Aplikasi Berbasis Web**.
