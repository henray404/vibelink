# Scene 3 — Sound Map

> VibeLink · Mobile · Kesadaran spasial suara lingkungan
> Source screen: `screen3-soundmap.html`
> Mengikat ke `docs/imk-analysis.md` + `docs/research/ux-research.md`. Fitur inti = radar arah suara + peringatan keselamatan.

---

## 1. Purpose

Menampilkan **dari mana** suara penting datang. Radar circular dengan pengguna di tengah; ikon kategori suara muncul di arah datangnya. Memberi kesadaran situasional — terutama suara berbahaya (klakson, alarm, sirene) — yang luput dari transkripsi teks.

**Primary goal:** kesadaran spasial + keselamatan. Pengguna tahu ada apa di sekelilingnya tanpa mendengar.

> **Catatan keterbatasan (riset):** lokalisasi arah dari mikrofon ponsel tunggal terbatas (umumnya butuh microphone array). Sound Map menampilkan arah **estimasi + confidence**, bukan presisi. Deteksi suara **bukan fitur keselamatan terjamin** — Apple sendiri menyatakan Sound Recognition tidak boleh diandalkan untuk situasi berbahaya/darurat. VibeLink mencantumkan disclaimer & fallback. Lihat `ux-research.md` §5 & §Supervisor notes 6–7.

---

## 2. Actors

| Actor | Keterlibatan |
|---|---|
| **Pengguna** (tunarungu/HoH/ASD) | Memantau radar, merespons peringatan, atur filter/sensitivitas |
| **Sound Classifier** (sistem) | Klasifikasi kategori suara + confidence + estimasi arah/jarak |
| **Haptic Engine** (sistem) | Getaran peringatan untuk suara bahaya (pola SOS) |

---

## 3. Use cases covered

1. Lihat arah datang suara (radar spasial)
2. Bedakan kategori suara (ikon + warna + bentuk)
3. Terima peringatan suara berbahaya (visual berkedip + haptik)
4. Baca detail deteksi (confidence, jarak estimasi, timestamp)
5. Filter & atur sensitivitas
6. Aktifkan Alert Mode (hanya suara bahaya)

---

## 4. Layout

```
┌──────────────────────────────────────┐
│ ‹ Sound Map        [Filter] [Alert ⏷]│  header
│                                        │
│            🔔(alarm, kedip)            │  radar circular
│         ╱───────────────╲             │  pengguna di center
│        │      🚗          │            │  ikon di arah suara
│        │        ( • You )  │           │  ukuran ikon ∝ intensitas
│        │   🐾        🧑    │           │
│         ╲───────────────╱             │
│                                        │
│  Terdeteksi:                           │  panel daftar
│  🔔 Alarm — depan · 92% · ~5m · now    │  kategori·arah·conf·jarak·waktu
│  🚗 Kendaraan — kiri · 78% · ~12m · 2s │
│  🧑 Orang — kanan · 84% · ~2m · 4s     │
└──────────────────────────────────────┘
```

---

## 5. Component inventory (`screen3-soundmap.html`)

### A. Header
- Back ‹; tombol **Filter**; toggle **Alert Mode**.

### B. Radar circular (fokus)
- Pengguna di center; ikon suara di sekeliling sesuai arah estimasi.
- Kategori (ikon + warna + **bentuk berbeda**):
  | Kategori | Ikon | Warna |
  |---|---|---|
  | Kendaraan | mobil | oranye |
  | Alarm/Sirene | lonceng | merah (berkedip) |
  | Ketukan Pintu | pintu | biru |
  | Orang Berbicara | orang | hijau |
  | Hewan | jejak kaki | coklat |
  | Musik | not balok | ungu |
- **Ukuran ikon ∝ intensitas** suara.
- Suara **bahaya** (alarm/klakson): animasi berkedip + border merah + getaran peringatan (pola SOS).

### C. Panel daftar
- Daftar suara terdeteksi: kategori · arah · **confidence %** · jarak estimasi · timestamp.

### D. Kontrol
- **Filter** (pilih kategori prioritas); **slider sensitivitas**; **Alert Mode** (hanya tampilkan suara bahaya).

### E. Disclaimer (kecil, persisten)
- "Arah & deteksi bersifat estimasi. Jangan andalkan sebagai satu-satunya alat keselamatan."

---

## 6. Interaksi

| Target | Interaksi | Hasil |
|---|---|---|
| (pasif) suara lingkungan | — | Ikon muncul di radar + (jika bahaya) kedip + haptik SOS |
| Ikon radar | Tap | Detail suara (confidence/jarak/waktu) |
| Filter | Tap | Pilih kategori prioritas |
| Slider sensitivitas | Geser | Atur ambang deteksi |
| Alert Mode | Toggle | Hanya tampilkan suara bahaya |

**Feedback:** suara bahaya = 3 kanal redundan: ikon berkedip + label + haptik SOS. Confidence rendah ditandai eksplisit (jangan klaim pasti). Kalibrasi noise floor (Settings) kurangi false positive.

---

## 7. Interaction flow (skenario keselamatan — Rina jalan kaki)

1. Rina berjalan di trotoar, buka VibeLink, aktifkan Sound Map.
2. Klakson truk dari belakang-kiri → ikon kendaraan oranye besar muncul di posisi belakang-kiri radar + getaran peringatan kuat.
3. Rina waspada, menjauh dari tepi trotoar.
4. Sampai kantor, seseorang menyapa dari kanan → ikon orang hijau muncul → Rina menoleh membalas.

---

## 8. Visual style tokens

| Token | Value |
|---|---|
| Surface | `#FFEBAF` |
| Radar | lingkaran konsentris, garis `#2A2A2A`, center "You" aksen |
| Ikon kategori | warna sesuai tabel + bentuk unik, ukuran ∝ intensitas |
| Bahaya | border merah `#F44336` + animasi kedip |
| Panel daftar | card `#FFF6E0`, confidence bar kecil |
| Disclaimer | `#4C6B73` 12sp, persisten |

---

## 9. Figma build instructions

### Frame — `Scene3 / SoundMap` — 390 × 844
1. Background `#FFEBAF`. Header: back ‹ + "Sound Map" + Filter + Alert Mode toggle.
2. **Radar:** concentric circles, center dot "You" (accent). Place category icons around at directions: alarm (bell, red, BLINKING + red border, top), car (orange, larger, lower-left), person (green, right), paw (brown, lower-left small), music (purple). Icon size ∝ intensity.
3. **Detail list:** rows — "🔔 Alarm — depan · 92% · ~5m · now"; "🚗 Kendaraan — kiri · 78% · ~12m · 2s"; "🧑 Orang — kanan · 84% · ~2m · 4s". Each with a small confidence bar.
4. **Disclaimer chip** (bottom, muted `#4C6B73`): "Arah & deteksi estimasi — bukan alat keselamatan tunggal."
5. **Annotation:** danger = blink + label + SOS haptic; categories differ by color AND shape AND label.

### Komponen reusable
`SoundRadar`, `SoundIcon` (varian Kendaraan/Alarm/Pintu/Orang/Hewan/Musik), `DetectionRow`, `ConfidenceBar`, `Disclaimer`.

---

## 9b. Penerapan IMK pada scene ini

| Unsur IMK | Penerapan di Sound Map |
|---|---|
| **Mapping** (Norman) | Arah ikon di radar = arah suara nyata (spasial 1:1) |
| **Match real world** (Nielsen 2) | Radar familiar; ikon kategori familiar |
| **Redundant coding** (WCAG 1.4.1) | Kategori = warna + bentuk + label; bahaya = kedip + label + haptik |
| **Visibility of status** (Nielsen 1) | Confidence %, jarak, timestamp eksplisit |
| **Error prevention** (Nielsen 5) | Slider sensitivitas + kalibrasi noise floor kurangi false positive |
| **Help recognize errors** (Nielsen 9) | Confidence rendah ditandai; disclaimer keterbatasan |
| **Flexibility** (Nielsen 7) | Filter + Alert Mode = jalur cepat keselamatan |
| **Keselamatan (SDG 3)** | Peringatan multimodal suara bahaya |
| **Fitts's Law** | Ikon radar & kontrol ≥48dp |

---

## 10. Acceptance criteria

- [ ] Radar circular, pengguna di center, ikon di arah estimasi.
- [ ] Kategori dibedakan warna + bentuk + label (bukan warna saja).
- [ ] Ukuran ikon mencerminkan intensitas.
- [ ] Suara bahaya = kedip + border merah + haptik SOS.
- [ ] Panel daftar tampilkan confidence + jarak + timestamp.
- [ ] Filter + slider sensitivitas + Alert Mode tersedia.
- [ ] Disclaimer keterbatasan deteksi/arah ditampilkan.
- [ ] Target ≥48dp, kontras ≥4.5:1.

---

## 11. Codex + Figma MCP prompt (paste-ready)

```
Build Figma frame "Scene3 / SoundMap" at 390x844 for dark-mode accessibility app "VibeLink". Purpose: spatial radar of environmental sounds with safety alerts for Deaf / hard-of-hearing users.

Background #FFEBAF. Header: back chevron + "Sound Map" + "Filter" button + "Alert Mode" toggle.

CENTER: a circular RADAR with concentric rings, a center dot labelled "You" (accent). Around it, category icons at their directions, size proportional to loudness: an ALARM bell (red, BLINKING, red border, top — the danger), a CAR (orange, larger, lower-left), a PERSON (green, right), a PAW (brown, small lower-left), MUSIC notes (purple). Each category differs by color AND shape AND label (never color alone).

Below: a detection list — "🔔 Alarm — depan · 92% · ~5m · now", "🚗 Kendaraan — kiri · 78% · ~12m · 2s", "🧑 Orang — kanan · 84% · ~2m · 4s", each with a small confidence bar.

A muted disclaimer chip near the bottom (#4C6B73, 12sp): "Arah & deteksi bersifat estimasi — bukan alat keselamatan tunggal."

Font Inter, text #1E3A42/#4C6B73, targets >=48dp. Make SoundRadar, SoundIcon (Kendaraan/Alarm/Pintu/Orang/Hewan/Musik variants), DetectionRow, ConfidenceBar reusable. Annotation: danger = blink + label + SOS haptic.
```
