# VibeLink - Analisis Unsur IMK (Human-Computer Interaction)

> Dokumen fondasi IMK untuk VibeLink. Dipakai semua scene (`docs/scenes/*.md`) + jadi bab analisis di laporan.
> Modalitas: aplikasi mobile (Android-first), sensory substitution audio -> visual + haptik.
> Pengguna utama: tunarungu / hard of hearing + neurodivergent (ASD).
>
> Bagian Target User, Accessibility, dan Mobile-HCI diperkuat riset di `docs/research/ux-research.md`. Sistem warna dan bentuk diperbarui dari `docs/research/color-shape-research.md`.

## 1. Kerangka IMK yang dipakai

Analisis ini memetakan VibeLink ke kerangka HCI standar:

- 8 Golden Rules - Shneiderman
- 10 Usability Heuristics - Nielsen
- 6 Principles of Design - Don Norman
- Gestalt principles
- Visual hierarchy & layout
- Accessibility - kontras, ukuran target, redundant coding
- Inclusive Design + Sensory Substitution - substitusi audio ke modalitas visual & taktil

## 2. Target User (persona)

VibeLink melayani tiga profil pengguna dengan kebutuhan sensorik berbeda:

| Profil | Kebutuhan inti | Implikasi desain |
|---|---|---|
| Tunarungu (Deaf) | Substitusi sensorik penuh | Tidak boleh ada info audio-only; semua status punya visual + haptik |
| Hard of Hearing | Augmentasi sisa pendengaran | Penegas konteks emosi & arah suara, bukan pengganti total |
| Neurodivergent (ASD) | Interpretasi emosional eksplisit; rawan sensory overload | Label emosi gamblang + kontrol intensitas haptik/visual |

Persona ringkas:

1. Rina, 24 - tunarungu sejak lahir, desainer grafis. Butuh Conversation Mode + Sound Map.
2. Dimas, 19 - ASD, mahasiswa. Butuh Emotion Bar + Insight Harian; sensitif intensitas, sehingga butuh personalisasi.

## 3. Identitas Brand & Logo

Nama VibeLink menggabungkan vibe (suasana/getaran emosi) dan link (jembatan/koneksi). Logo tetap berupa gelombang suara yang bertransformasi menjadi pita visual, tetapi warna UI utama mengikuti sistem pastel-on-cream.

| Elemen | Makna |
|---|---|
| Gelombang suara | Input audio dunia nyata |
| Wordmark "VibeLink" | Jembatan antara suara, visual, dan haptik |
| Bentuk simpel & flat | Tenang, low-stimulation, ramah ASD |
| Titik/node "link" | Koneksi antara pengguna dan lingkungan akustik |

## 4. Sistem Warna

Palet baru memakai soft pastel-on-cream dengan black-ink sebagai satu-satunya warna teks utama. Rujukan: `docs/research/color-shape-research.md`.

### Token dasar

| Token | Hex | Peran |
|---|---|---|
| Cream | `#FFF8EE` | App background |
| Surface | `#FFFFFF` | Card / panel / control fill |
| Ink | `#161616` | Semua teks, ikon, angka besar, dan label di atas pastel |
| Line | `#222222` | Border pastel controls, focus outline, separator |
| Muted | `#5C5C5C` | Teks sekunder di atas cream |
| Accent pink | `#E96B95` | FAB, active nav, CTA utama |
| Accent soft | `#F7B7CF` | Soft pink fill |
| Track | `#EFE7D6` | Progress/slider track |

### Warna emosi (semantic fill - selalu + ikon + teks)

| Emosi | Hex | Makna |
|---|---|---|
| Positif/senang | `#B8E6C4` | Antusias, lega, ramah |
| Netral/info | `#F6E6A8` | Informasional, datar |
| Frustrasi/tegang | `#F7C59F` | Ragu, tegang |
| Marah/urgensi | `#F3A6A6` | Marah, urgensi tinggi |

### Warna kategori suara (fill - selalu + ikon + teks)

| Kategori | Hex | Contoh |
|---|---|---|
| Yellow | `#F7E7A3` | Kendaraan / status informasional |
| Pink | `#F7B7CF` | Musik / personal |
| Blue | `#B7D8F2` | Pintu / Conversation |
| Green | `#BDE8CA` | Orang / lingkungan aman |

### Kontras (WCAG 2.1)

| Kombinasi | Rasio approx | Verdict |
|---|---|---|
| Ink `#161616` di atas Cream `#FFF8EE` | ~16:1 | AAA - teks badan |
| Ink `#161616` di atas Positive `#B8E6C4` | ~12:1 | AAA - label emosi |
| Ink `#161616` di atas Neutral `#F6E6A8` | ~14:1 | AAA - label emosi |
| Ink `#161616` di atas Frustrated `#F7C59F` | ~11:1 | AAA - label emosi |
| Ink `#161616` di atas Angry `#F3A6A6` | ~10:1 | AAA - label bahaya |
| Pastel sebagai teks di atas Cream | ~1.2-2.8:1 | Gagal - jangan dipakai sebagai teks |
| Muted `#5C5C5C` di atas Cream `#FFF8EE` | ~6:1 | AA - teks sekunder |

**Aturan:** pastel hanya fill, bukan teks. Semua angka, label, body copy, ikon penting, dan teks pada CTA pink memakai ink `#161616`. Kontrol pastel wajib punya `1.5px solid #222222` untuk non-text contrast.

**Aturan kunci (WCAG 1.4.1 Use of Color):** warna emosi/status tidak pernah berdiri sendiri - selalu dipasangkan ikon + label teks (+ getaran).

## 5. Tipografi

Typeface: Inter / Roboto. Body minimum 14px, default 16px. Big number memakai `clamp(48px, 14vw, 64px)`, weight 800, tabular nums. Transkripsi dapat diskalakan via A-/A/A+.

## 6. Ikonografi dan Bentuk

- Ikon outline 24x24 dengan stroke tegas dan label teks untuk aksi penting.
- Ikon emosi dan kategori suara dipakai sebagai redundansi visual.
- Bentuk default rounded: card 24px, chip 16px, pill 999px, cat-chip circle 44px.
- Bentuk tajam hanya untuk danger/alarm agar salience tinggi tanpa mengandalkan warna saja.
- Rationale bentuk mengikuti `docs/research/color-shape-research.md`: bentuk rounded mengurangi kesan ancaman dan cocok untuk low-stimulation UI; danger memakai bentuk tajam terbatas sebagai pengecualian salience (Bar & Neta).

## 7. Peletakan & Layout

- Screen max-width 390px, padding 20px, tidak overflow horizontal.
- Satu fungsi utama per layar.
- Visualisasi sebagai fokus utama: Home hero ring dan Sound Map radar 260px.
- Conversation memakai emotion summary di atas dan transkrip di bawah.
- Bottom nav 5 slot konsisten, mic FAB center 60px.
- Touch target >=48dp; pill 52px; icon button 48px; FAB 60px.

## 8. 8 Golden Rules (Shneiderman) -> VibeLink

1. Konsistensi - bottom nav, palet emosi, token, dan komponen sama di semua layar.
2. Shortcut - quick access, filter, alert mode, A-/A/A+.
3. Feedback informatif - dB, status chip, emotion label, confidence, haptik.
4. Dialog dengan penutupan - rekam -> ringkasan -> riwayat.
5. Cegah error - label field, mode kalibrasi, danger action terpisah.
6. Pembalikan aksi - jeda/hapus/toggle mudah dibatalkan.
7. Locus of control - sensitivitas, haptik, visual, privasi bisa diatur.
8. Kurangi beban memori - label eksplisit, history thumbnail, insight naratif.

## 9. 10 Usability Heuristics (Nielsen) -> VibeLink

- Visibility of system status: listening, dB, status chip, confidence.
- Match real world: radar arah suara dan ikon kategori familiar.
- User control & freedom: Jeda, Hapus, Filter, Alert Mode, kembali ke Home.
- Consistency & standards: pola navigasi dan token konsisten.
- Error prevention: label form, kalibrasi noise floor, konfirmasi aksi destruktif.
- Recognition over recall: icon+label, history thumbnail, settings grouping.
- Flexibility: quick access dan pengaturan rinci.
- Aesthetic & minimalist: satu fokus per layar, visual noise rendah.
- Help recover errors: error form memakai warna + ikon + teks.
- Help & documentation: onboarding, label, dan insight.

## 10. Prinsip Norman -> VibeLink

- Affordance: FAB bulat besar, pill button, slider.
- Signifier: tab selected, status chip, emotion strip.
- Feedback: perubahan visual dan haptik per event.
- Mapping: arah ikon di radar sesuai arah suara estimasi.
- Constraint: register bertahap, Alert Mode membatasi suara bahaya.
- Conceptual model: penerjemah suara di saku pengguna.

## 11. Gestalt -> VibeLink

- Proximity: statistik dan setting dikelompokkan dalam card.
- Similarity: warna emosi konsisten.
- Common region: card membungkus konten terkait.
- Figure/ground: angka dan ikon ink di atas cream/pastel.
- Continuity: mood palette dan trend bar.

## 12. State & Feedback Interaksi

| State | Visual |
|---|---|
| Default | Surface card/control dengan border ink |
| Focus | Outline 3px solid line |
| Active/selected | Ink fill atau accent pink |
| Listening ON | FAB accent + label status |
| Bahaya | Fill angry, bentuk tajam, border ink, haptik SOS |
| Disabled | Opacity diturunkan, label tetap ada |

Timing: respon <100ms. Animasi pulse/radar/blink dinonaktifkan di `prefers-reduced-motion`.

## 13. Accessibility

- Kontras: patuhi tabel Section 4.
- Redundant coding: semua status = warna + ikon + teks (+ getaran).
- Touch target: semua interaktif >=48x48dp, FAB 60px.
- Teks: body >=14px, transkripsi skala A-/A/A+.
- Multimodal: informasi audio tidak pernah audio-only.
- Personalisasi sensorik: haptik, sensitivitas mic, mode buta warna, kontras tinggi, kurangi gerak, screen reader.
- Screen reader: semua aksi punya label.
- Motion: default konservatif dan bisa dikurangi.

## 14. Mobile / Sensory-Substitution-Specific HCI

- Latensi rendah agar visualisasi dan haptik sinkron dengan suara.
- Keterbatasan deteksi harus jujur: tampilkan confidence, jarak estimasi, dan disclaimer.
- Keselamatan kritis: alarm/klakson memakai label, ikon, shape, blink, dan haptik SOS; tidak mengandalkan satu kanal.
- Sensory overload (ASD): default rendah stimulasi, rounded shape, warna lembut, dan kontrol intensitas.
- Shape/rounded rationale mengikuti `docs/research/color-shape-research.md`: rounded shapes lebih ramah dan kurang mengancam; danger menggunakan sharp-corner terbatas untuk membangun salience tanpa bergantung warna.
- Privasi: sediakan toggle penyimpanan riwayat, auto-delete, dan ekspor terkontrol.

## 15. Peta IMK per Scene

| Scene | Sorotan IMK |
|---|---|
| Home | Visibility status (ring+dB+label), feedback real-time, FAB 60px |
| Conversation | Emotion Bar, redundant coding, transkrip dengan strip emosi |
| Sound Map | Mapping spasial, confidence, disclaimer, salience bahaya |
| Analytics | Proximity statistik, mood palette, insight naratif |
| Onboarding | Help & docs, signifier dot indicator, ilustrasi rounded |
| Auth | Error prevention, label di atas field, progressive disclosure |
| Settings | Locus of control, personalisasi sensorik |
| Profile | Statistik, kontak darurat, perangkat haptik |

## Status

- Brand/logo: gelombang suara -> visual/haptik.
- Warna, tipografi, prinsip: final pada pastel-on-cream + ink.
- Target User, Accessibility, Mobile-HCI: diperkuat riset di `docs/research/ux-research.md` dan `docs/research/color-shape-research.md`.
- Selaras SDG 3 (kesehatan & keselamatan) + SDG 10 (kurangi kesenjangan) via inklusi sensorik digital.
