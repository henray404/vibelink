# VibeLink Design Spec

## Design Goal

Rancang antarmuka mobile yang menerjemahkan suara - emosi percakapan dan suasana lingkungan - menjadi visual dan haptik yang intuitif bagi pengguna tunarungu, hard of hearing, dan neurodivergent (ASD). Fokus desain: sensory substitution multimodal dengan redundant coding, satu fungsi utama per layar, dan aksesibilitas WCAG 2.1.

## Screens

- `screen0-onboarding.html`: Splash + 3 slide onboarding.
- `screen-auth.html`: Login & Register (progressive disclosure + pilih profil).
- `screen1-home.html`: Home - hero dB ring, assistant card, dan suara terdeteksi.
- `screen2-conversation.html`: Conversation Mode.
- `screen3-soundmap.html`: Sound Map.
- `screen4-analytics.html`: Interaction Analytics.
- `screen5-settings.html`: Settings.
- `screen6-profile.html`: Profile.

## Visual Direction

- Tone: tenang, hangat, calm, low-stimulation (ramah ASD), readable.
- Style: soft pastel-on-cream flat UI dengan aksen black-ink; surface putih untuk card.
- **Pastel palette:**
  - Cream `#FFF8EE` - background utama yang hangat dan low-stimulation.
  - Surface `#FFFFFF` - card / panel / control fill.
  - Ink `#161616` - semua teks, ikon, angka besar, dan label di atas pastel.
  - Line `#222222` - border pastel controls, separator, dan focus outline.
  - Pink accent `#E96B95` - FAB, active nav, CTA utama; teks di atasnya selalu ink.
  - Soft pink `#F7B7CF` - fill lembut untuk card/choice.
- **Emotion fills** (fill only, never text): positive `#B8E6C4`, neutral `#F6E6A8`, frustrated `#F7C59F`, angry/urgent `#F3A6A6`.
- **Category fills** (fill only, icon/text always ink): yellow `#F7E7A3`, pink `#F7B7CF`, blue `#B7D8F2`, green `#BDE8CA`.
- Pastels are fills only. Text, numbers, labels, and critical icons use ink `#161616`.
- Tipografi: Inter / Roboto. Hierarki via ukuran + weight, bukan warna saja.
- Card: radius 24px, pill radius 999px, chip radius 16px.

## Core Design Principles

| Prinsip | Penerapan |
|---|---|
| Redundant coding (WCAG 1.4.1) | Setiap status = warna + ikon + teks (+ getaran). Tidak pernah warna saja. |
| Sensory substitution multimodal | Audio -> visual (ring/emotion bar/radar) + haptik. |
| One primary function per screen | Home=suasana, Conversation=percakapan, Sound Map=spasial, Analytics=ringkasan. |
| Minimal cognitive load | Ilustrasi besar, teks minimal, progressive disclosure pada form. |
| Personalisasi sensorik | Profil aksesibilitas + Settings menyesuaikan sensitivitas, haptik, visual. |
| No hidden gesture | Semua fitur lewat elemen visual terlihat; bottom nav ikon+label. |

## Layout Rules

- Light theme default: cream `#FFF8EE` latar, surface `#FFFFFF` card, ink `#161616` untuk semua teks.
- Screen padding 20px; card padding 18px; gap antar card 14px.
- Touch target >=48x48dp; FAB dan aksi utama 56-60dp.
- Jarak antar tombol >=8dp.
- Kontras teks >=4.5:1; ink di atas cream/pastel jauh di atas AA.
- Bottom navigation tetap 5 slot: Home, Conversation, mic FAB, Sound Map, Profile.
- Focus visible: outline 3px solid ink/line dengan offset 2px.
- Reduced motion: semua animasi pulse/radar/blink mati di `prefers-reduced-motion`.

## Typography Scale

| Peran | Size | Weight |
|---|---|---|
| Display / big number | `clamp(48px, 14vw, 64px)` | 800 |
| Judul layar | 24px | 700 |
| Judul card | 18px | 700 |
| Body | 16px | 500 |
| Label/meta | 14px | 500 |
| Caption non-esensial | 12px | 500 |

## Screen Design

### Onboarding

Purpose: perkenalkan konsep visual+haptik. Splash memakai `assets/vibelink-icon.svg` + wordmark di atas cream. Tiga slide memakai blok ilustrasi rounded pastel untuk Canvas, Conversation, dan Sound Map. Teks maksimal ringkas, tombol "Lanjut" >=48dp, "Lewati" di topbar.

### Auth

Login memakai label di atas field, input 52px, CTA pink accent full-width, serta Google/Apple pill. Register memakai 3 card profil besar: Tunarungu/HoH, ASD, dan Lainnya, masing-masing selectable tile dengan target besar.

### Home

Purpose: kesadaran suasana akustik real-time. Fokus atas adalah hero ring 260px dengan angka besar `62 dB`, chip status "Normal", dan cat-chip pastel di arc. Aksi utama: pill gelap "Mulai Mendengarkan", icon button filter/export, pink assistant card, daftar suara terdeteksi dengan progress dan angka.

### Conversation Mode

Purpose: percakapan tatap muka dengan konteks emosi. Emotion bar tampil sebagai strip pastel 56px, diikuti ikon emosi, label "Tegang", chip confidence, bubble transkrip dengan strip emosi, dan kontrol Rekam/Jeda/Hapus.

### Sound Map

Purpose: kesadaran spasial + keselamatan. Radar 260px memakai ring konsentris dan center "Anda". Danger/alarm adalah satu-satunya bentuk tajam, memakai fill `#F3A6A6`, border ink, blink yang tunduk pada reduced motion, serta daftar confidence/jarak/waktu. Disclaimer wajib tampil.

### Interaction Analytics

Purpose: refleksi pola emosi & interaksi. Mood Palette, stat cards, donut chart dengan legend teks, pink insight card, riwayat percakapan dengan thumbnail palette, tren mingguan, dan ekspor PDF.

### Settings

Sections: Profil Aksesibilitas, Pengaturan Visual, Pengaturan Haptik, Pengaturan Suara, Aksesibilitas Tambahan, Data & Privasi. Wajib ada Mode Buta Warna, Kurangi Gerak, Ukuran Teks, Kontras Tinggi, Screen reader, slider haptik, slider sensitivitas, kalibrasi noise floor, simpan riwayat, auto-delete, dan ekspor.

### Profile

Header card menampilkan avatar 64px dalam pastel mood signature ring, nama, email, badge profil. Statistik Saya memakai grid 2 kolom. Kontak Darurat <=3 row dengan catatan auto SMS+GPS >10s, row smartwatch, dan footer Keluar/Hapus Akun.

## Design Element Analysis

- **Layout:** satu fungsi utama per layar, visualisasi sebagai fokus, spacing konsisten 20/18/14px.
- **Buttons:** target >=48dp, pill 52px, FAB 60px, filled dark/accent vs outlined surface.
- **Typography:** Inter/Roboto, body >=14px, big number tabular.
- **Color & Contrast:** cream `#FFF8EE`, surface `#FFFFFF`, ink `#161616`, accent `#E96B95`; pastel hanya fill, teks selalu ink.
- **Navigation:** bottom nav 5 slot ikon+label dengan center pink FAB.
- **Haptic:** sine halus / sharp pulse / repeat intens / pola SOS untuk bahaya; sepenuhnya dikustomisasi.

## Figma Frame Plan

Buat frame mobile 390x844 untuk tiap layar: Onboarding, Login/Register, Home, Conversation, Sound Map, Analytics, Settings, Profile. Tiap frame memakai cream `#FFF8EE` background, visualisasi sebagai fokus, status badge warna+ikon+teks, dan touch target >=48dp.

Komponen reusable: `HeroRing`, `EmotionBar`, `EmotionBadge`, `ChatBubble`, `SoundRadar`, `SoundIcon`, `StatCard`, `MoodPalette`, `BottomNav`, `FAB`, `ProfileCard`, `SettingsRow`, `HapticToggle`.

## Acceptance Criteria

- Semua layar render tanpa overflow horizontal di lebar mobile.
- Tidak ada informasi yang hanya bergantung warna.
- Touch target >=48dp untuk semua elemen interaktif.
- Kontras teks >=4.5:1 di light theme (ink `#161616` di atas cream/pastel).
- Bottom nav 5 slot konsisten & dapat diakses tanpa gesture tersembunyi.
- Palet emosi konsisten maknanya di semua layar.
- Identitas VibeLink (cream + pastel + black-ink gelombang flat + Inter) terjaga.
