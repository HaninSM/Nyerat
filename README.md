# Nyerat.AI — Sentuhan Udara Aksara Jawa (Air-Writing Interactive Learning)

> **Kategori 4: Pembelajaran dan Edukasi Digital Berbasis Budaya (Kompetisi BudayaGO)**  
> Platform Web Air-Writing Interaktif Aksara Jawa berbasis Computer Vision MediaPipe Hands 60 FPS (Client-Side).

---

## 🌟 Fitur Utama

- **Real-Time Air-Writing (60 FPS Native WebAssembly):**
  - Menggunakan Google MediaPipe Hands klasik (`camera_utils` + `hands.js`) yang berkinerja tinggi langsung di sisi peramban web (*client-side*) tanpa jeda (*zero latency*).
  - Interpolasi koordinat mulus (*Physics Lerp*) pada ujung jari telunjuk (*Landmark 8*) untuk mengeliminasi getaran tangan (*jitter-free*).
- **Penanganan Khusus Seretan Berkelanjutan (*Smooth Cursive Bézier*):**
  - Aksara Jawa memiliki karakteristik goresan meliuk (*cursive continuous curves*). Tinta dirender menggunakan *Quadratic Bézier Curves* dengan *Dual-Pass Halo Contrast* (tebal gelap luar + neon terang dalam) agar terbaca tajam di ruangan terang.
- **State Mesin Gestur Tangan Kanan:**
  - ☝️ **1 Jari (Telunjuk Tunggal):** Mode **Menulis / Draw** — Menggoreskan tinta kaligrafi neon di dalam area latihan.
  - ✌️ **2 Jari (Telunjuk + Tengah):** Mode **Angkat Pena / Hover** — Memindahkan tangan bebas ke goresan berikutnya tanpa meninggalkan coretan seretan liar (*anti-stray drag lines*).
  - 🖐️ **5 Jari Terbuka:** Mode **Bersih / Clear** — Menghapus kanvas seketika.
  - 👍 **Ibu Jari (Thumbs Up):** Mode **Kunci & Lanjut** — Mengunci huruf dan melangkah ke aksara berikutnya.
- **Demo Animasi Pensil Virtual (On-Demand):**
  - Menampilkan demonstrasi langkah demi langkah urutan tarikan garis (*stroke order guidance*) sebelum atau saat pengguna berlatih.
  - Dapat diinterupsi kapan saja hanya dengan mengacungkan jari telunjuk ☝️ ke dalam kotak.
- **20 Aksara Nglegena & Filosofi Budaya:**
  - Pembelajaran lengkap *Ha-Na-Ca-Ra-Ka* hingga *Ma-Ga-Ba-Tha-Nga* dilengkapi makna filosofi Aji Saka.
- **Sintesis Audio Mandiri (*Web Audio API*):**
  - Efek suara kaligrafi, sapuan *whoosh*, dan lonceng/gong apresiasi evaluasi tanpa ketergantungan berkas MP3 eksternal.

---

## 🚀 Menjalankan Secara Lokal

Aplikasi ini 100% statis berbasis HTML5, Tailwind CSS, dan JavaScript murni.

1. **Clone repositori:**
   ```bash
   git clone https://github.com/HaninSM/Nyerat.git
   cd Nyerat
   ```

2. **Jalankan server HTTP lokal:**
   ```bash
   # Menggunakan Python 3:
   python -m http.server 8000
   ```

3. **Buka di Browser:**
   Buka `http://localhost:8000/` pada peramban Chrome, Edge, atau Firefox. Izinkan akses kamera web untuk mulai menulis.

---

## 📁 Struktur Direktori

```text
├── index.html                           # Halaman utama Air-Writing Studio (Fullscreen Stage)
├── DESIGN.md                            # Panduan Desain Cyber-Cultural Neo-Javanese
├── PRD-02-Edukasi-Aksara-Jawa.md        # Dokumen Kebutuhan Produk (PRD) Lomba BudayaGO
├── README.md                            # Dokumentasi Proyek
└── stitch_screens/                      # Layar Prototipe Desain
    ├── 01_studio_belajar_air_writing.html
    ├── 02_katalog_hanacaraka_filosofi.html
    ├── 03_statistik_ujian_kompetensi.html
    └── 04_hadiah_font_ebooklet.html
```

---

## 📜 Lisensi & Pengembang

Dikembangkan oleh **Tim Karya Guru** untuk pelestarian literasi Aksara Jawa modern di era kecerdasan artifisial.
