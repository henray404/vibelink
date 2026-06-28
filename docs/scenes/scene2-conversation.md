# Scene 2 — Conversation Mode

> VibeLink · Mobile · Alat bantu percakapan tatap muka
> Source screen: `screen2-conversation.html`
> Mengikat ke `docs/imk-analysis.md` + `docs/research/ux-research.md`. Fitur inti = transkripsi + indikator emosi pembicara.

---

## 1. Purpose

Menutup "emotional gap": bukan hanya *apa* yang dikatakan (transkripsi), tapi *bagaimana* dikatakan (emosi/intonasi). Layar terbagi: Emotion Bar di atas (suasana emosi real-time), transkripsi chat bubble di bawah (kata + jejak emosi per kalimat).

**Primary goal:** pengguna tunarungu mengikuti percakapan lengkap dengan konteks emosional; pengguna ASD mendapat konfirmasi eksplisit emosi pembicara (mis. tulus vs sarkastis).

---

## 2. Actors

| Actor | Keterlibatan |
|---|---|
| **Pengguna** (tunarungu/HoH/ASD) | Membaca transkrip + Emotion Bar, mengelola sesi |
| **Pembicara** (lawan bicara) | Suaranya ditangkap, ditranskripsi, dianalisis emosinya |
| **SER Engine** (sistem) | Analisis intonasi/sentiment → warna Emotion Bar + confidence |
| **Haptic Engine** (sistem) | Getaran per-emosi (sine/sharp/repeat) |

---

## 3. Use cases covered

1. Transkripsi percakapan real-time (chat bubble)
2. Lihat emosi pembicara real-time (Emotion Bar)
3. Telusuri jejak emosi per kalimat (indikator per-bubble)
4. Rasakan emosi via haptik
5. Rekam / Jeda / Hapus sesi
6. Aktifkan Ringkasan AI
7. Skala ukuran teks (pinch / A±)

---

## 4. Layout (split-view 40:60)

```
┌──────────────────────────────────────┐
│ ‹ Conversation      [Ringkasan AI ⏷] │  header + toggle + A+/A-
│ ╔══════════════════════════════════╗ │
│ ║  EMOTION BAR (live)              ║ │  40% — strip warna
│ ║  🟢🟢🟡🟠🟠  "Tegang"  😟        ║ │  warna + label + emoji
│ ╚══════════════════════════════════╝ │
│ ┌──────────────────────────────────┐ │
│ │🟢│ "Oh bagus banget idemu!"       │ │  60% — transkrip
│ │  │                                │ │  bubble + indikator emosi kiri
│ │🟠│ "Ya... nggak papa sih."        │ │
│ │🟡│ "Kita lanjut besok ya."        │ │
│ │  │                          ▍live │ │
│ └──────────────────────────────────┘ │
│   [● Rekam]   [⏸ Jeda]   [🗑 Hapus]   │  kontrol
└──────────────────────────────────────┘
```

---

## 5. Component inventory (`screen2-conversation.html`)

### A. Header / Toolbar
- Back ‹; toggle **Ringkasan AI**; tombol **A+ / A-** (text scaling) + dukung pinch-to-zoom.

### B. Emotion Bar (40% atas)
- Strip horizontal yang berubah warna real-time sesuai intonasi/sentiment pembicara:
  | Warna | Emosi | Label | Emoji |
  |---|---|---|---|
  | Hijau `#4CAF50` | Positif/senang | "Senang" | 🙂 |
  | Kuning `#FFC107` | Netral/info | "Netral" | 😐 |
  | Oranye `#FF9800` | Frustrasi/tegang | "Frustrasi" | 😟 |
  | Merah `#F44336` | Marah/urgensi | "Marah" | 😠 |
- **Redundansi:** warna + label teks + ikon emoji (tidak warna saja).

### C. Transkripsi (60% bawah)
- Chat bubble per ucapan; tiap bubble punya **indikator warna kecil di sisi kiri** = emosi saat kalimat itu diucapkan → pengguna bisa menelusuri ulang alur emosi.
- Teks default 16sp, skala 16→24sp.
- Indikator "live" saat transkripsi berjalan.

### D. Kontrol
- **Rekam** (simpan sesi) · **Jeda** (hentikan sementara) · **Hapus** (bersihkan layar).

### E. Haptik (default ON)
- Getaran lembut = emosi positif; getaran tajam singkat = emosi negatif; getaran panjang berulang = urgensi tinggi. Dapat diatur di Settings.

---

## 6. Interaksi

| Target | Interaksi | Hasil |
|---|---|---|
| (pasif) suara pembicara | — | Transkrip + Emotion Bar update real-time + haptik |
| Toggle Ringkasan AI | Tap | Aktifkan ringkasan poin kunci |
| A+ / A- | Tap | Perbesar/perkecil teks transkrip |
| Transkrip | Pinch | Zoom ukuran teks |
| Rekam / Jeda / Hapus | Tap | Kelola sesi (Hapus = konfirmasi) |
| Bubble | (lihat) | Telusuri indikator emosi per kalimat |

**Feedback:** Emotion Bar + haptik sinkron <100ms dengan ucapan. Tiga kanal redundan: warna bar + label + emoji + getaran. Confidence rendah → emosi ditandai "tidak yakin" (jangan klaim pasti — keterbatasan SER, lihat `ux-research.md`).

---

## 7. Interaction flow (skenario emosional — Rina di rapat)

1. Rina buka Conversation Mode, tap Rekam.
2. PM bicara santai → Emotion Bar hijau "Santai", bubble transkrip muncul dengan strip hijau.
3. PM bahas keterlambatan → Emotion Bar bergeser ke oranye "Tegang" + getaran tajam; transkrip "kita perlu selesaikan ini sebelum Jumat" dengan strip oranye.
4. Rina paham urgensi nada walau teks netral.
5. Rekan beri solusi → Emotion Bar kembali hijau "Lega".
6. Rina tap toggle Ringkasan AI → poin kunci rapat terangkum.

### Skenario sosial — Dimas (ASD)
- Teman: "Oh bagus banget idemu" → Emotion Bar hijau "Antusias" + 🙂 → Dimas yakin itu pujian tulus.
- Teman lain: "Ya nggak papa sih" → kuning-oranye "Ragu" → Dimas sadar temannya kurang setuju.

---

## 8. Visual style tokens

| Token | Value |
|---|---|
| Surface | `#FFEBAF` |
| Bubble | `#FFF6E0`, radius 18px, strip emosi 4px kiri |
| Emotion Bar | strip gradient warna emosi, label + emoji |
| Hijau/Kuning/Oranye/Merah | `#4CAF50`/`#FFC107`/`#FF9800`/`#F44336` |
| Transkrip text | `#1E3A42`, 16sp (skala 16→24sp), Inter 500 |
| Kontrol | filled (Rekam) + outlined (Jeda/Hapus), ≥48dp |

---

## 9. Figma build instructions

### Frame — `Scene2 / Conversation` — 390 × 844
1. Background `#FFEBAF`. Header: back ‹ + "Conversation" + toggle "Ringkasan AI" + A+/A-.
2. **Emotion Bar (top 40%):** horizontal strip with gradient segments (green→yellow→orange), current state "Tegang"/orange highlighted, big label "Tegang" + emoji 😟. Add subtle confidence sub-label.
3. **Transcript (bottom 60%):** 3-4 chat bubbles `#FFF6E0`, each with a 4px colored left strip (emotion). Sample lines (ID): green "Oh bagus banget idemu!", orange "Ya... nggak papa sih.", yellow "Kita lanjut besok ya." + live cursor.
4. **Controls:** Rekam (filled Moonstone) · Jeda (outlined) · Hapus (outlined), ≥48dp, spacing ≥8dp.
5. **Annotation layer:** mark redundancy (color+label+emoji+haptic) and that emotion ≠ color-only.

### Komponen reusable
`EmotionBar`, `EmotionBadge` (varian Senang/Netral/Frustrasi/Marah), `ChatBubble` (dengan strip emosi), `TextScaleControl`, `SessionControl`. `EmotionBadge` dipakai juga di Analytics & Profile.

---

## 9b. Penerapan IMK pada scene ini

| Unsur IMK | Penerapan di Conversation |
|---|---|
| **Match real world** (Nielsen 2) | Emotion Bar = "nada bicara" yang hilang dari teks |
| **Redundant coding** (WCAG 1.4.1) | Emosi = warna + label + emoji + getaran |
| **Visibility of status** (Nielsen 1) | Emotion Bar live + confidence + indikator "live" |
| **Recognition over recall** (Nielsen 6) | Indikator emosi per-bubble → telusuri ulang, tak perlu ingat |
| **Feedback** (Norman) | Bar + haptik <100ms sinkron ucapan |
| **Continuity** (Gestalt) | Strip emosi sepanjang percakapan = alur emosional |
| **Dialog closure** (Shneiderman 4) | Rekam → Ringkasan AI → tersimpan |
| **User control** (Nielsen 3) | Jeda/Hapus, text scaling, toggle ringkasan |
| **Error/honesty** | Confidence rendah ditandai, tidak klaim emosi pasti |
| **Help & docs** (Nielsen 10) | Ringkasan AI = bantuan kontekstual |

---

## 10. Acceptance criteria

- [ ] Split-view 40:60 (Emotion Bar : transkrip).
- [ ] Emotion Bar = warna + label teks + emoji (bukan warna saja).
- [ ] Tiap bubble transkrip punya indikator emosi (strip kiri).
- [ ] Teks transkrip dapat diskalakan (A± / pinch), default 16sp.
- [ ] Kontrol Rekam/Jeda/Hapus ≥48dp; Hapus konfirmasi.
- [ ] Toggle Ringkasan AI tersedia.
- [ ] Confidence emosi ditampilkan / ketidakpastian ditandai.
- [ ] Haptik per-emosi dijelaskan (default ON, dapat diatur).

---

## 11. Codex + Figma MCP prompt (paste-ready)

```
Build Figma frame "Scene2 / Conversation" at 390x844 for dark-mode accessibility app "VibeLink". Purpose: live transcription PLUS speaker-emotion indicator for Deaf / autistic users.

Background #FFEBAF. Header: back chevron + "Conversation" + a "Ringkasan AI" toggle + A+/A- text-size buttons.

TOP 40% — "Emotion Bar": a horizontal strip segmented in emotion colors green #4CAF50 -> yellow #FFC107 -> orange #FF9800 -> red #F44336, currently showing a TENSE state (orange highlighted), with a big label "Tegang" + emoji 😟 + a small "confidence 82%" sub-label. Emotion must be color + LABEL + emoji, never color alone.

BOTTOM 60% — transcript as chat bubbles (#FFF6E0, radius 18, a 4px colored LEFT strip per bubble = the emotion when that line was said). Indonesian sample lines: [green] "Oh bagus banget idemu!"; [orange] "Ya... nggak papa sih."; [yellow] "Kita lanjut besok ya." + a live typing cursor. Body text #1E3A42 16sp Inter medium.

Controls row: "Rekam" (filled Moonstone), "Jeda" (outlined), "Hapus" (outlined), all >=48dp, spacing >=8dp.

Make EmotionBar, EmotionBadge (Senang/Netral/Frustrasi/Marah variants), ChatBubble (with emotion strip), SessionControl reusable. Note on an annotation layer: emotion uses color+label+emoji+haptic redundancy.
```
