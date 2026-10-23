# Product Requirements Document (PRD)
## Ide 2: "Nyerat.AI" — Edukasi & Pengenalan Aksara Jawa Berbasis Computer Vision Hand Gesture (Air-Writing)

---

### 1. Informasi Proyek & Identitas Lomba
- **Nama Produk:** *Nyerat.AI: Sentuhan Udara Aksara Jawa (Air-Writing Interactive Learning)*
- **Kategori Lomba BudayaGO:** **Kategori 4 — Pembelajaran dan Edukasi Digital Berbasis Budaya**
- **Target Pengguna:** Pelajar Sekolah (SD, SMP, SMA/SMK), Guru Muatan Lokal Bahasa Jawa, Komunitas Pegiat Aksara Nusantara, dan Masyarakat Umum pecinta kaligrafi etnik.
- **Platform Distribusi:** Web Application (Webcam-enabled Chrome/Edge/Firefox di Laptop/PC/Tablet) via WebGL/Canvas tanpa instalasi aplikasi luar.

---

### 2. Latar Belakang & Akar Budaya (Bobot Penilaian 25%)
- **Problem Statement:** Aksara Jawa (*Hanacaraka*) sering dianggap rumit, kuno, dan membingungkan oleh siswa modern karena kurva lekukan yang mirip dan tidak adanya bimbingan urutan goresan (*stroke order*) yang interaktif. Selain itu, materi pelajaran di sekolah sering berhenti di hafalan teoritis tanpa memberikan dampak praktis bagi siswa untuk menggunakannya di dunia digital mereka (misal mengetik di komputer/laptop).
- **Solusi Inovasi:** Menghadirkan pengalaman belajar menulis aksara Jawa secara kinestetik melalui **AI Air-Writing**. Pengguna melukis aksara di udara menggunakan jari telunjuk tangan kanan yang dipindai langsung oleh kamera, menerima tutorial animasi seretan, dinilai kemiripan goresannya secara matematis oleh AI, dan di akhir perjalanan dihadiahi paket Font Aksara Jawa siap pakai untuk Microsoft Word yang dikirimkan langsung ke email mereka.
- **Akar Budaya Otentik:**
  - Silabus berpatokan pada pakem standar penulisan Aksara Jawa (Keputusan Kongres Bahasa & Aksara Jawa).
  - Mengajarkan filosofi filosofis 20 Aksara Nglegena (kisah kesetiaan dan pengorbanan abdi setia Aji Saka: Dora dan Sembada).

---

### 3. Arsitektur Interaksi Gestur Tangan Kanan (Kinesthetic Air-Writing)
Sistem memanfaatkan **MediaPipe Hand Landmarker** (21 3D hand keypoints) yang berjalan 60 FPS secara real-time di sisi peramban web (*client-side*).

#### 3.1. Spesifikasi State Mesin Gestur (Hand Pose Commands)
| Gestur / Pose Tangan Kanan | Simbol | Fungsi Aksi Sistem | Perilaku UI / Layar |
|---|:---:|---|---|
| **Ujung Telunjuk Tunggal (Single Index Finger)** | ☝️ | **Pena Virtual (*Drawing Ink*)** | Menggoreskan tinta kaligrafi emas di atas kanvas udara sesuai pergerakan ujung jari (*landmark 8*). |
| **Dua Jari: Telunjuk & Jari Tengah (Peace / Cheers Pose)** | ✌️ | **Pause / Siap Menulis Sesi Baru** | Menghentikan tinta. Layar memicu *countdown* melingkar: **3, 2, 1**, memberi waktu pemain menata posisi jari sebelum goresan berikutnya. |
| **Ibu Jari Mengacung (Thumbs Up)** | 👍 | **Navigasi: Lanjut ke Huruf Berikutnya** | Mengunci hasil tulisan huruf saat ini. Layar memicu *countdown*: **3, 2, 1**, lalu beralih menampilkan huruf baru dan tutorial animasinya. |
| **Lima Jari Terbuka Penuh (Open Palm)** | 🖐️ | **Clear Canvas (Hapus Layar)** | Menghapus seluruh goresan di kanvas saat ini jika terjadi kesalahan goresan, kanvas kembali bersih seketika. |

---

### 4. User Journey & Alur Pengalaman Belajar
1. **Langkah 1 — Inisiasi & Kalibrasi Kamera (Onboarding):**
   - Pengguna mengizinkan akses webcam.
   - Kotak panduan hijau memastikan tangan kanan berada di zona optimal deteksi.
   - Uji coba cepat 4 gesture (Pena, Cheers, Thumbs Up, Open Palm).
2. **Langkah 2 — Tutorial Animasi Berpanduan (*Ghost Stroke Guidance*):**
   - Huruf target ditampilkan di layar dengan animasi garis transparan (*ghost path*).
   - Panah penunjuk arah memperlihatkan kapan harus menarik garis melengkung, menyeret ke bawah, atau memutar loop aksara.
3. **Langkah 3 — Praktek Mandiri & Penilaian Kemiripan AI:**
   - Pengguna meniru goresan di udara.
   - Algoritma mencocokkan koordinat path goresan terhadap kurva ground-truth aksara asli (*Dynamic Time Warping & Fréchet Distance*).
   - Di akhir penulisan, muncul kartu nilai: **Skor Kemiripan (0 - 100%)**, umpan balik detail (misal: *"Lekukan kedua kurang melengkung 15%"*), serta bintang apresiasi.
4. **Langkah 4 — Lingkup Pembelajaran Terfokus (Tingkat 1 & Tingkat 2):**
   - **Tingkat 1:** 20 Aksara Nglegena (Ha-Na-Ca-Ra-Ka s/d Ma-Ga-Ba-Tha-Nga).
   - **Tingkat 2:** Sandhangan Swara (Wulu, Suku, Taling, Pepet, Taling Tarung) & Sandhangan Panyigeg (Layar, Cecak, Wignyan, Pangkon).
   - Tantangan Mini: Menulis 1-2 kata bermakna (misal: *"Tata Krama"*, *"Sinau"*).
5. **Langkah 5 — Hadiah Kelulusan Otomatis (Email Fulfillment):**
   - Pengguna memasukkan Nama & Alamat Email di form akhir.
   - Sistem backend mentrigger email apresiasi instan yang melampirkan:
     1. Ucapan selamat dan apresiasi dedikasi pelestarian aksara Nusantara.
     2. File **Font Aksara Jawa Resmi (.ttf / .otf)** Unicode compliant.
     3. E-Booklet panduan instalasi font di Windows/MacOS dan tutorial cara mengetik aksara Jawa di Microsoft Word.

---

### 5. Arsitektur Teknis & Kelayakan Implementasi (Bobot Penilaian 25%)
- **Computer Vision Frontend:** Google MediaPipe Hand Landmarker via JavaScript SDK.
- **Rendering & Drawing Canvas:** HTML5 2D Canvas / WebGL dengan efek partikel kaligrafi tinta emas bercahaya (*glow trail shader*).
- **Evaluasi Kemiripan Aksara:** Normalisasi ukuran & bounding box goresan, dilanjutkan dengan perbandingan vektor kurva (*Shape Context Matching* & *Hausdorff Distance*) secara komputasi ringan di browser tanpa membebani server.
- **Backend Email Service:** FastAPI (Python) terhubung ke SMTP Mail Service (Resend / AWS SES / SendGrid) dengan proteksi anti-spam rate limiting.

---

### 6. Keberlanjutan & Model Pengembangan (Bobot Penilaian 20%)
- **Fase MVP V1 (Kompetisi BudayaGO):**
  - Validasi teknologi deteksi gerak udara, akurasi skoring kemiripan, dan viralitas kepuasan pengguna menerima font aksara gratis di email.
- **Rencana Pasca MVP (Evaluasi Berkelanjutan):**
  - Setelah data interaksi dan respons pengguna terkumpul di versi 1, modul dapat diekspansi menjadi *School Muatan Lokal Assessment Toolkit* (lisensi instansi sekolah untuk ujian praktik menulis aksara digital) dan integrasi sertifikasi kompetensi aksara.

---

### 7. Rencana Kerja & Deliverables Proposal BudayaGO (Bobot Penilaian 30%)
- **Pekan 1:** Pemrograman Web Hand Tracking MediaPipe (integrasi gestur ☝️, ✌️, 👍, 🖐️) dan kalibrasi countdown 3 detik.
- **Pekan 2:** Pembuatan aset kurva vektor 20 Aksara Nglegena & Sandhangan serta algoritma penilaian kemiripan goresan.
- **Pekan 3:** Integrasi alur UI/UX, animasi tutorial seret goresan, dan modul otomatisasi pengiriman email font .ttf + PDF instalasi MS Word.
- **Pekan 4:** Uji coba performa di ragam spesifikasi webcam/laptop, penyusunan proposal terstruktur, dan video demo interaktif.
