# VibeLink Product Requirements Document

## Problem Statement

Teknologi aksesibilitas audio yang ada saat ini (Live Caption, Google Live Transcribe, aplikasi Speech-to-Text) hanya mengonversi suara menjadi teks verbatim. Dimensi paralinguistik percakapan — intonasi, emosi, sarkasme, urgensi — hilang sepenuhnya dalam proses transkripsi. Suara lingkungan non-verbal yang kritis untuk keselamatan (klakson, alarm, sirene, ketukan pintu) juga luput. Akibatnya muncul "emotional gap": pengguna bisa membaca *apa* yang dikatakan, tapi tidak bisa merasakan *bagaimana* hal itu dikatakan, dan tidak sadar terhadap suasana akustik di sekitarnya.

Dua kelompok pengguna paling terdampak: penyandang disabilitas pendengaran (tunarungu & hard of hearing) yang butuh substitusi/augmentasi sensorik penuh, dan individu neurodivergent (ASD) yang pendengarannya normal tapi kesulitan memproses prosodi emosional percakapan.

Dokumen ini mendefinisikan VibeLink sebagai purwarupa antarmuka mobile yang menerjemahkan **seluruh spektrum informasi audio** (konten verbal, emosi, suara lingkungan) menjadi representasi **visual dinamis** dan **umpan balik haptik** yang dipersonalisasi.

## Solution

VibeLink adalah prototype aplikasi mobile (purwarupa High-Fidelity) yang mengadopsi pendekatan *sensory substitution* multimodal. Aplikasi memanfaatkan mikrofon dan haptic engine smartphone untuk mendeteksi, mengklasifikasi, dan menerjemahkan sinyal audio real-time.

Empat fitur inti:

- **Live Atmosphere Canvas** — visualisasi suasana audio lingkungan real-time sebagai aurora dinamis (warna + gerak = karakter suara).
- **Conversation Mode** — transkripsi real-time + Emotion Bar yang menunjukkan emosi pembicara, plus haptik per-emosi.
- **Sound Map** — radar spasial yang menampilkan arah datang suara penting, dengan peringatan haptik untuk suara berbahaya.
- **Interaction Analytics** — ringkasan pola emosi harian dalam bentuk Mood Palette + statistik interaksi.

Prinsip perancangan utama:

- Multimodal & *redundant coding*: setiap informasi disampaikan lewat ≥2 modalitas (warna + ikon + teks + getaran) agar tidak bergantung pada satu indra.
- Light theme Vanilla+Moonstone default (calm, low-stimulation, ramah ASD); dark theme opsional.
- Aksesibilitas WCAG 2.1 + Material Design (touch target ≥48dp, kontras ≥4.5:1).
- Personalisasi sensorik (intensitas haptik, palet warna, sensitivitas) untuk mengakomodasi perbedaan sensorik antar profil pengguna.

## Target Users

- **Tunarungu (Deaf):** butuh substitusi sensorik penuh — semua informasi audio harus tersedia secara visual + haptik.
- **Hard of Hearing:** butuh augmentasi — pelengkap sisa pendengaran, penegas konteks emosional & arah suara.
- **Neurodivergent (ASD):** pendengaran normal, butuh interpretasi emosional eksplisit untuk prosodi yang sulit mereka tangkap; sensitif terhadap sensory overload sehingga butuh kontrol intensitas.
- **Evaluator IMK:** reviewer yang menilai kelengkapan flow, visual hierarchy, prinsip inclusive design, dan usability prototype.

## User Stories

1. Sebagai pengguna baru, saya ingin onboarding singkat 3 slide, agar paham konsep visual+haptik sebelum mulai.
2. Sebagai pengguna baru, saya ingin memilih profil aksesibilitas saat register, agar default sensitivitas & mode sesuai kebutuhan saya.
3. Sebagai tunarungu, saya ingin melihat suasana akustik ruangan sebagai aurora, agar tahu lingkungan tenang/bising/bahaya tanpa mendengar.
4. Sebagai tunarungu, saya ingin label deskriptif + dB meter di Home, agar tingkat kebisingan jelas, tidak hanya warna.
5. Sebagai pengguna, saya ingin toggle mikrofon besar di Home, agar mudah mengaktifkan/menonaktifkan listening mode.
6. Sebagai tunarungu, saya ingin transkripsi percakapan real-time, agar bisa mengikuti pembicaraan tatap muka.
7. Sebagai tunarungu, saya ingin Emotion Bar menunjukkan emosi pembicara (warna+ikon+label), agar tahu nada bicara di balik kata.
8. Sebagai pengguna, saya ingin tiap bubble transkripsi punya indikator emosi, agar bisa menelusuri alur emosional percakapan.
9. Sebagai pengguna, saya ingin getaran berbeda per emosi, agar merasakan konteks tanpa selalu menatap layar.
10. Sebagai pengguna, saya ingin mengubah ukuran teks transkripsi (pinch / A+ A-), agar nyaman dibaca.
11. Sebagai individu ASD, saya ingin konfirmasi apakah komentar tulus atau sarkastis, agar tidak salah membaca situasi sosial.
12. Sebagai pengguna, saya ingin merekam / menjeda / menghapus sesi percakapan, agar bisa mengelola transkrip.
13. Sebagai pengguna, saya ingin opsi Ringkasan AI, agar poin kunci percakapan terangkum.
14. Sebagai tunarungu, saya ingin radar Sound Map menampilkan arah suara, agar sadar sumber suara di sekitar.
15. Sebagai tunarungu, saya ingin ikon kategori suara berbeda warna+bentuk, agar bisa membedakan klakson, alarm, orang, dll.
16. Sebagai pengguna, saya ingin suara berbahaya berkedip + bergetar kuat, agar segera waspada.
17. Sebagai pengguna, saya ingin daftar suara terdeteksi dengan confidence, jarak, timestamp, agar konteks deteksi jelas.
18. Sebagai pengguna, saya ingin Filter & sensitivitas di Sound Map, agar bisa memprioritaskan suara tertentu.
19. Sebagai pengguna, saya ingin Alert Mode hanya menampilkan suara berbahaya, agar fokus pada keselamatan.
20. Sebagai pengguna, saya ingin Mood Palette harian, agar tahu mood keseluruhan hari saya.
21. Sebagai pengguna, saya ingin statistik (jumlah percakapan, durasi listening, peringatan, distribusi emosi), agar memahami pola interaksi.
22. Sebagai individu ASD, saya ingin Insight Harian naratif, agar pola sosial saya mudah dimengerti.
23. Sebagai pengguna, saya ingin ekspor data PDF, agar bisa dibawa ke terapis/pendamping.
24. Sebagai pengguna, saya ingin mengubah profil aksesibilitas, palet aurora, intensitas haptik di Settings, agar pengalaman sesuai preferensi.
25. Sebagai pengguna ASD, saya ingin mengatur intensitas getaran per-kategori, agar terhindar dari sensory overload.
26. Sebagai pengguna, saya ingin kalibrasi noise floor mikrofon, agar deteksi akurat di lingkungan saya.
27. Sebagai pengguna, saya ingin opsi ukuran teks global, kontras tinggi, integrasi screen reader, agar aksesibilitas menyeluruh.
28. Sebagai pengguna, saya ingin menyimpan ≤3 kontak darurat, agar SMS+GPS terkirim otomatis saat suara darurat terdeteksi >10 detik.
29. Sebagai pengguna, saya ingin menghubungkan smartwatch, agar alert getaran terasa di pergelangan tangan.
30. Sebagai pengguna, saya ingin navigasi tetap berupa bottom nav 4 tab dengan ikon+label, agar tidak ada gesture tersembunyi.

## Functional Requirements

- **Splash & Onboarding:** animasi gelombang→aurora; 3 slide (Canvas, Conversation, Sound Map); tombol Lanjut ≥48dp + dot indicator + opsi Lewati.
- **Auth:** Login (email/password + Google/Apple); Register progressive disclosure 2 langkah (data akun → pilih profil aksesibilitas); label di atas field, error merah + ikon.
- **Home (Live Atmosphere Canvas):** canvas aurora ~60% layar atas; dB meter + label ("Tenang/Normal/Bising/Bahaya"); Quick Access Cards horizontal; FAB mikrofon center-bottom; bottom nav 4 tab.
- **Conversation Mode:** Emotion Bar (40%) warna+label+emoji; transkripsi chat bubble (60%) dengan indikator emosi per-bubble; tombol Rekam/Jeda/Hapus; toggle Ringkasan AI; text scaling; haptik per-emosi default on.
- **Sound Map:** radar circular, pengguna di center; ikon kategori (kendaraan/alarm/pintu/orang/hewan/musik) warna+bentuk; ukuran ikon ∝ intensitas; suara bahaya berkedip+border merah+haptik; panel daftar (confidence/jarak/timestamp); Filter + slider sensitivitas; Alert Mode.
- **Interaction Analytics:** Mood Palette harian/mingguan/bulanan; card statistik; donut chart distribusi emosi; Riwayat Percakapan dengan thumbnail Emotion Bar; Insight Harian naratif; area chart tren mingguan; ekspor PDF.
- **Settings:** section Profil Aksesibilitas, Visual (5 preset aurora), Haptik (intensitas + toggle kategori), Suara (sensitivitas + kalibrasi noise floor), Aksesibilitas Tambahan (text size, kontras, screen reader), Data & Privasi (riwayat, auto-delete, ekspor).
- **Profile:** avatar + lingkaran aurora "mood signature"; badge profil; Statistik Saya kumulatif; Kontak Darurat (≤3) + SMS/GPS otomatis; Hubungkan Perangkat (smartwatch); Keluar / Hapus Akun terpisah jauh.
- Semua elemen interaktif: touch target ≥48dp, kontras ≥4.5:1 (3:1 teks besar), informasi tidak bergantung warna saja.

## Implementation Decisions

- Purwarupa High-Fidelity, fidelitas visual + interaksi; backend & ML inference disimulasikan (mock/static) untuk scope tugas.
- Stack untuk demo web: HTML/CSS statis per layar (selaras pola medilens), tanpa build tool baru — agar mudah dipindahkan ke Figma frame.
- Light theme: Vanilla `#FFEBAF` latar, Cream `#FFF6E0` card, Moonstone `#4C9DB0` aksen, deep teal `#1E3A42` teks.
- Font Inter/Roboto; body ≥14sp, heading ≥18sp, transkripsi 16sp (skala s/d 24sp).
- Palet emosi terkalibrasi: hijau `#4CAF50` positif, kuning `#FFC107` netral, oranye `#FF9800` frustrasi, merah `#F44336` marah/urgensi.
- Redundant coding wajib untuk semua status (warna + ikon + teks/getaran).
- Personalisasi haptik via "temporal envelope processing": amplitudo audio → pola getaran (sine halus=positif, sharp pulse=negatif, repeat intens=urgensi, SOS=bahaya).

## Testing Decisions

- Testing manual: buka tiap layar di browser, verifikasi flow & responsive.
- Yang diuji (perilaku eksternal):
  - Tidak ada informasi yang hanya bergantung warna (matikan warna → masih terbaca via ikon/teks).
  - Touch target ≥48dp dapat disentuh di lebar mobile.
  - Kontras teks ≥4.5:1 di light theme.
  - Navigasi bottom nav konsisten antar layar.
  - Skenario uji: percakapan emosional, lingkungan bising dengan suara kritis (alarm/klakson), interaksi sosial sehari-hari.
- Tidak perlu unit test untuk purwarupa statis tanpa business logic kompleks.

## Out of Scope

- Inference ML real (speech emotion recognition, sound classification, sound localization) — disimulasikan.
- Backend, database, autentikasi nyata, sinkronisasi cloud.
- Akurasi klinis / diagnosis; VibeLink bukan alat medis.
- Integrasi smartwatch & SMS/GPS darurat nyata (UI stub).
- Ekspor PDF nyata (UI stub).
- Dukungan bahasa isyarat (BISINDO) recognition.

## Further Notes

Dokumen ini menjadi sumber fitur untuk `DESIGN_SPEC.md`, `imk-analysis.md`, dan scene specs (`docs/scenes/*.md`). Riset bersitasi yang memperkuat keputusan desain ada di `docs/research/ux-research.md`. Selaras tema "Perancangan Pengalaman Pengguna untuk Pembangunan Indonesia Maju dan Berkelanjutan", mendukung SDG 3 & SDG 10.
