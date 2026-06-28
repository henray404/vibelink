# Scene 1 — Home (Live Atmosphere Canvas)

> VibeLink · Mobile (Android-first) · Layar utama / home
> Source screen: `screen1-home.html`
> Mengikat ke `docs/imk-analysis.md` + `docs/research/ux-research.md`. Fitur inti = visualisasi suasana audio real-time.

---

## 1. Purpose

Titik masuk aplikasi. Saat dibuka, pengguna langsung melihat **Live Atmosphere Canvas** — area aurora dinamis yang menerjemahkan suasana akustik ruangan secara real-time. Dalam sekali pandang pengguna tahu apakah lingkungan tenang, normal, bising, atau berbahaya — tanpa mendengar.

**Primary goal:** beri kesadaran suasana audio instan + akses cepat ke fitur lain (Conversation, Sound Map, Analytics) + toggle listening.

---

## 2. Actors

| Actor | Keterlibatan |
|---|---|
| **Pengguna** (tunarungu/HoH/ASD) | Membaca aurora + status, menyalakan/mematikan listening, masuk fitur lain |
| **Audio Engine** (sistem) | Tangkap mikrofon, analisis amplitudo/frekuensi/tempo → render aurora + dB |
| **Haptic Engine** (sistem) | Getaran lembut konfirmasi listening aktif |

---

## 3. Use cases covered

1. Lihat suasana audio lingkungan real-time (aurora)
2. Baca tingkat kebisingan (dB meter + label deskriptif)
3. Aktif/nonaktifkan listening mode (FAB mikrofon)
4. Akses cepat Conversation Mode → Scene 2
5. Akses cepat Sound Map → Scene 3
6. Akses cepat Analytics → Scene 4
7. Navigasi ke tab lain (bottom nav)

---

## 4. Layout

```
┌──────────────────────────────────────┐
│  VibeLink            🔔   👤          │  header (logo + notif + profil)
│                                        │
│      ╭──────────────────────────╮     │
│      │                          │     │
│      │   LIVE ATMOSPHERE        │     │  ~60% layar
│      │   CANVAS (aurora live)   │     │  fokus visual utama
│      │                          │     │  figure/ground: aurora vs #FFEBAF
│      ╰──────────────────────────╯     │
│                                        │
│  ▮▮▮▮▮▯▯▯  62 dB · "Normal"           │  status bar (dB meter + label)
│                                        │
│  ╭────────╮ ╭────────╮ ╭────────╮     │  Quick Access Cards
│  │ 💬 Conv │ │ 📡 Map │ │ 📊 Stats│ →  │  (horizontal scroll)
│  ╰────────╯ ╰────────╯ ╰────────╯     │
│                                        │
│                ( 🎤 )                  │  FAB mic 56dp (center-bottom)
│  ┌──────┬──────────┬─────────┬──────┐ │
│  │ Home │ Convers. │ SoundMap│ Prof │ │  bottom nav 4 tab
│  └──────┴──────────┴─────────┴──────┘ │
└──────────────────────────────────────┘
```

### Hierarki
Aurora (fokus, ~60%) → status bar (dB + label) → quick access → FAB → bottom nav. Satu fungsi utama per layar (kesadaran suasana).

---

## 5. Component inventory (`screen1-home.html`)

### A. Header
- Logo VibeLink (kiri); ikon notifikasi 🔔 + avatar profil 👤 (kanan), touch target ≥48dp.

### B. Live Atmosphere Canvas (fokus)
- Area aurora ~60% atas, render real-time dari analisis audio:
  | Kondisi audio | Aurora |
  |---|---|
  | Tenang | Gradasi Moonstone–teal, gerak lambat |
  | Suara keras / percakapan intens | Gradasi merah-oranye, gerak cepat/dinamis |
  | Musik | Pola mengikuti ritme & tempo |
- Animasi continuous; figure/ground tegas terhadap Vanilla `#FFEBAF`.

### C. Status Bar
- dB meter visual (bar tersegmentasi) + angka dB + **label deskriptif**: "Tenang" / "Normal" / "Bising" / "Bahaya".
- Status **selalu** warna + label teks (tidak warna saja — WCAG 1.4.1).

### D. Quick Access Cards (horizontal scroll)
- Card besar ikon + label: **Conversation Mode** (→ Scene 2) · **Sound Map** (→ Scene 3) · **Analytics** (→ Scene 4).

### E. FAB Mikrofon
- Lingkaran 56dp center-bottom; toggle listening on/off. Aktif → aurora hidup + getaran lembut konfirmasi + label status berubah.

### F. Bottom Navigation
- 4 tab ikon + label: **Home** (aktif) · Conversation (→ Scene 2) · Sound Map (→ Scene 3) · Profile (→ Profile). Tab aktif ditandai aksen + dot.

---

## 6. Interaksi

| Target | Interaksi | Hasil |
|---|---|---|
| FAB mikrofon | Tap | Toggle listening; aurora hidup/diam + getaran konfirmasi |
| Quick Access Card | Tap | Buka fitur terkait (Scene 2/3/4) |
| Canvas | (pasif) | Aurora update real-time mengikuti audio |
| Bottom nav tab | Tap | Pindah tab |
| Notif / avatar | Tap | Notifikasi / Profile |

**Feedback:** semua tap respon <100ms + ripple Material. Listening aktif punya 3 sinyal redundan: aurora bergerak + label "Mendengarkan" + getaran. Touch target ≥48dp (FAB 56dp), spacing ≥8dp.

---

## 7. Interaction flow (primary path)

1. Pengguna buka app → Home muncul, aurora fade-in (0.4s).
2. Tap FAB mikrofon → listening aktif: aurora mulai bergerak sesuai audio, getaran lembut, label status update.
3. Aurora Moonstone–teal + "Tenang/Normal" → pengguna tahu lingkungan aman.
4. Pengguna tap Quick Access "Conversation" → Scene 2. *(atau)*
5. Pengguna tap tab Sound Map → Scene 3.

---

## 8. Visual style tokens

| Token | Value |
|---|---|
| Surface | `#FFEBAF` |
| Card | `#FFF6E0`, radius 18px |
| Primary | Moonstone `#4C9DB0` |
| Aurora — tenang | Moonstone–teal (`#4C9DB0`/cyan), gerak lambat |
| Aurora — intens | merah-oranye (`#FF9800`/`#F44336`), gerak cepat |
| Status label | warna sesuai level + teks ("Tenang/Normal/Bising/Bahaya") |
| Text | `#1E3A42` primary, `#4C6B73` secondary |
| Type | Inter, heading 22–24sp/700, body 14–16sp |
| FAB | 56dp, aksen Moonstone |
| Touch target | ≥48dp, spacing ≥8dp |

---

## 9. Figma build instructions (execution-ready)

### Frame — `Scene1 / Home` — 390 × 844 (mobile)
1. **Background:** full `#FFEBAF`.
2. **Header:** logo VibeLink kiri; notif + avatar kanan (44px icon, 48dp target).
3. **Live Atmosphere Canvas:** rounded rect ~60% tinggi, isi aurora mesh (Moonstone–teal di atas Vanilla), efek blur/glow; tampilkan state "Normal" (Moonstone–teal bergerak). Beri kesan animasi via streak gradient.
4. **Status Bar:** segmented dB bar (mis. 6/8 segmen aktif) + "62 dB" + chip label "Normal" (warna + ikon + teks).
5. **Quick Access Cards:** 3 card horizontal (Conversation/Sound Map/Analytics), ikon besar + label, card `#FFF6E0` radius 18.
6. **FAB:** lingkaran 56dp aksen Moonstone, ikon mikrofon, center-bottom, shadow.
7. **Bottom nav:** 4 tab ikon+label, Home aktif (aksen + dot).
8. **Redundancy note (annotation layer):** tandai bahwa status = warna+label, listening = aurora+label+haptik.

### Komponen reusable
`AuroraCanvas`, `DbMeter`, `StatusChip` (varian Tenang/Normal/Bising/Bahaya), `QuickAccessCard`, `FAB`, `BottomNav`, `Header`. Dipakai lintas scene — buat di sini.

---

## 9b. Penerapan IMK pada scene ini

> Mengikat ke `docs/imk-analysis.md`.

| Unsur IMK | Penerapan di Home |
|---|---|
| **Visibility of status** (Nielsen 1) | Aurora live + dB meter + label + state listening |
| **Match real world** (Nielsen 2) | Aurora = metafora "suasana"; intensitas warna = intensitas suara |
| **Feedback** (Norman) | Aurora <100ms ikut audio; getaran saat toggle listening |
| **Figure/ground** (Gestalt) | Aurora (figure) menonjol dari Vanilla bg (ground) |
| **Konsistensi** (Shneiderman 1) | Bottom nav + token sama dengan scene lain |
| **Aesthetic & minimalist** (Nielsen 8) | Satu fokus (suasana), noise rendah — aman untuk ASD |
| **Redundant coding** (WCAG 1.4.1) | Status = warna + label; listening = aurora + label + haptik |
| **Fitts's Law** | FAB 56dp center-bottom (zona jempol), target ≥48dp |
| **Affordance** (Norman) | FAB bulat besar jelas bisa ditekan |
| **Recognition over recall** (Nielsen 6) | Quick Access Cards berikon+label |

---

## 10. Acceptance criteria

- [ ] Aurora memenuhi ~60% atas, jelas terhadap Vanilla bg.
- [ ] Status kebisingan = dB meter + angka + label teks (bukan warna saja).
- [ ] FAB mikrofon 56dp center-bottom; toggle memberi aurora + label + getaran.
- [ ] Quick Access Cards (Conversation/Sound Map/Analytics) berikon + label.
- [ ] Bottom nav 4 tab konsisten, Home aktif ditandai.
- [ ] Semua target ≥48dp, kontras teks ≥4.5:1.
- [ ] Identitas VibeLink (dark + aurora + gradient) terjaga.

---

## 11. Codex + Figma MCP prompt (paste-ready)

```
Build Figma frame "Scene1 / Home" at 390x844 for a dark-mode accessibility mobile app "VibeLink" (translates ambient sound into visuals + haptics for Deaf / hard-of-hearing / autistic users).

Background: solid #FFEBAF. Header: VibeLink logo left, notification bell + profile avatar right (48dp targets).

MAIN (top ~60%): a "Live Atmosphere Canvas" — large rounded rectangle filled with a flowing AURORA mesh (Moonstone teal #4C9DB0 -> soft cyan) over the Vanilla canvas with soft glow/blur, conveying a calm "Normal" ambient state. This is the visual focus.

Below it a Status Bar: segmented dB meter (6 of 8 segments lit) + "62 dB" + a chip "Normal" (color + icon + TEXT label, never color alone).

Quick Access row (horizontal): 3 cards #FFF6E0 radius 18 — "Conversation" (chat icon), "Sound Map" (radar icon), "Analytics" (chart icon), each icon + label.

A circular 56dp FAB with a microphone icon, accent Moonstone #4C9DB0 solid, centered above the bottom nav (thumb zone).

Bottom navigation: 4 tabs icon+label — Home (active, accent + dot), Conversation, Sound Map, Profile.

Font Inter, heading 22-24sp bold, body 14-16sp, text #1E3A42 / #4C6B73. All touch targets >=48dp, spacing >=8dp. Make AuroraCanvas, DbMeter, StatusChip, QuickAccessCard, FAB, BottomNav reusable components.
```
