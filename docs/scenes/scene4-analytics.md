# Scene 4 — Interaction Analytics

> VibeLink · Mobile · Ringkasan pola emosi & interaksi
> Source screen: `screen4-analytics.html`
> Mengikat ke `docs/imk-analysis.md` + `docs/research/ux-research.md`. Fitur inti = Mood Palette + statistik interaksi.

---

## 1. Purpose

Merangkum data interaksi audio pengguna (harian/mingguan/bulanan) jadi refleksi yang mudah dibaca. Mood Palette = "heatmap emosional" hari; statistik + Insight Harian naratif membantu pengguna (dan terapis/pendamping) melacak pola sosial.

**Primary goal:** beri refleksi pola emosi & interaksi; turunkan beban memori; dukung kepercayaan diri sosial (mis. Dimas melihat harinya didominasi hijau = interaksi positif).

---

## 2. Actors

| Actor | Keterlibatan |
|---|---|
| **Pengguna** (tunarungu/HoH/ASD) | Melihat ringkasan, ekspor data |
| **Terapis / Pendamping** (sekunder) | Menerima PDF ekspor untuk konsultasi |
| **Analytics Engine** (sistem) | Agregasi sesi → Mood Palette, statistik, Insight |

---

## 3. Use cases covered

1. Lihat Mood Palette (distribusi emosi harian)
2. Lihat statistik (jumlah percakapan, durasi listening, peringatan, distribusi emosi)
3. Telusuri Riwayat Percakapan (thumbnail Emotion Bar)
4. Baca Insight Harian naratif
5. Lihat tren mingguan (area chart)
6. Ekspor PDF untuk terapis/pendamping

---

## 4. Layout

```
┌──────────────────────────────────────┐
│ ‹ Analytics      [Harian|Mingguan|⏷] │  header + periode
│  MOOD PALETTE                          │
│  🟩🟩🟨🟧🟩🟩🟥🟩🟩🟨  (hari ini)     │  strip warna emosi
│                                        │
│  ╭───────────╮ ╭───────────╮          │  statistik card
│  │ 5 percakap│ │ 2j 14m    │          │
│  │ -an       │ │ listening │          │
│  ╰───────────╯ ╰───────────╯          │
│  ╭───────────╮ ╭───────────╮          │
│  │ 2 peringat│ │  ◔ donut  │          │
│  │ -an suara │ │  emosi    │          │
│  ╰───────────╯ ╰───────────╯          │
│                                        │
│  💡 Insight: "Hari ini 5 percakapan,  │  insight naratif
│     mayoritas positif. 2 peringatan    │
│     klakson sore hari."                │
│                                        │
│  Riwayat:  [▮▮▯▮ sesi 1] [▮▯▮▮ sesi 2]│  thumbnail Emotion Bar
│  Tren mingguan: ╱╲___╱ (area chart)    │
│            [ Ekspor PDF ]              │
└──────────────────────────────────────┘
```

---

## 5. Component inventory (`screen4-analytics.html`)

### A. Header + selector periode
- Back ‹; toggle **Harian / Mingguan / Bulanan**.

### B. Mood Palette
- Strip warna horizontal = distribusi emosi sepanjang hari (heatmap emosional). Warna dominan = mood hari. Selalu dapat di-tap untuk detail + label (bukan warna saja).

### C. Statistik card
- Jumlah percakapan ditranskripsi · Total durasi listening · Jumlah peringatan suara lingkungan · **Donut chart** distribusi emosi (dengan label + %).

### D. Insight Harian (naratif)
- Ringkasan teks: mis. "Hari ini Anda melakukan 5 percakapan. Mayoritas bernada positif. Ada 2 peringatan suara klakson di sore hari."

### E. Riwayat Percakapan
- List sesi tersimpan dengan **thumbnail Emotion Bar** masing-masing → identifikasi cepat sesi berdasarkan pola emosi.

### F. Tren mingguan
- Area chart berwarna pola emosi dari waktu ke waktu.

### G. Ekspor
- Tombol **Ekspor PDF** untuk konsultasi profesional.

---

## 6. Interaksi

| Target | Interaksi | Hasil |
|---|---|---|
| Selector periode | Tap | Ganti Harian/Mingguan/Bulanan |
| Mood Palette segmen | Tap | Detail emosi + waktu |
| Statistik card | Tap | Rincian metrik |
| Sesi (Riwayat) | Tap | Buka sesi (transkrip + Emotion Bar) |
| Ekspor PDF | Tap | Hasilkan PDF ringkasan |

**Feedback:** semua data emosi pakai warna + label + angka (redundan). Donut/area chart selalu berlabel teks + %.

---

## 7. Interaction flow (Dimas setelah tugas kelompok)

1. Dimas selesai sesi kelompok, buka Analytics.
2. Mood Palette hari ini didominasi hijau → ia melihat interaksinya berjalan positif.
3. Insight Harian: "5 percakapan, mayoritas positif."
4. Dimas merasa lebih percaya diri secara sosial.

---

## 8. Visual style tokens

| Token | Value |
|---|---|
| Surface | `#FFEBAF` |
| Card | `#FFF6E0`, radius 18px |
| Mood Palette | strip warna emosi (`#4CAF50`/`#FFC107`/`#FF9800`/`#F44336`) |
| Donut/area chart | warna emosi + label + % |
| Insight | card aksen lembut + ikon 💡 |
| Ekspor | tombol filled aksen, ≥48dp |

---

## 9. Figma build instructions

### Frame — `Scene4 / Analytics` — 390 × 844
1. Background `#FFEBAF`. Header: back ‹ + "Analytics" + segmented control Harian/Mingguan/Bulanan.
2. **Mood Palette:** horizontal strip ~10 segmen warna emosi (mostly green, some yellow/orange, one red), label "Hari ini".
3. **Stat cards (2×2):** "5 Percakapan", "2j 14m Listening", "2 Peringatan", donut chart "Distribusi Emosi" with legend + %.
4. **Insight card:** 💡 + teks naratif ID.
5. **Riwayat:** 2-3 session rows each with a mini Emotion Bar thumbnail.
6. **Tren mingguan:** colored area chart.
7. **Ekspor PDF** button (filled Moonstone, ≥48dp).
8. Annotation: all emotion data = color + label + number.

### Komponen reusable
`MoodPalette`, `StatCard`, `DonutChart`, `InsightCard`, `SessionRow` (dengan `EmotionBar` thumbnail), `AreaChart`, `ExportButton`. `EmotionBadge`/`EmotionBar` reuse dari Scene 2.

---

## 9b. Penerapan IMK pada scene ini

| Unsur IMK | Penerapan di Analytics |
|---|---|
| **Proximity / Common region** (Gestalt) | Statistik dikelompok dalam card |
| **Recognition over recall** (Nielsen 6) | Thumbnail Emotion Bar → kenali sesi tanpa mengingat |
| **Reduce memory load** (Shneiderman 8) | Insight Harian merangkum; tak perlu hafal |
| **Continuity** (Gestalt) | Area chart tren = alur emosi dari waktu |
| **Redundant coding** (WCAG 1.4.1) | Chart = warna + label + % |
| **Match real world** (Nielsen 2) | Mood Palette = metafora "warna hari" |
| **Visibility** (Nielsen 1) | Metrik jelas (jumlah, durasi, peringatan) |
| **Help & docs** (Nielsen 10) | Insight naratif = penjelasan kontekstual |
| **Flexibility** (Nielsen 7) | Ekspor PDF untuk pihak ketiga (terapis) |

---

## 10. Acceptance criteria

- [ ] Mood Palette = strip warna + dapat ditelusuri + label.
- [ ] Statistik card: percakapan, durasi, peringatan, donut emosi (dengan label/%).
- [ ] Riwayat Percakapan dengan thumbnail Emotion Bar.
- [ ] Insight Harian naratif hadir.
- [ ] Tren mingguan area chart.
- [ ] Ekspor PDF tersedia (stub).
- [ ] Selector periode Harian/Mingguan/Bulanan.
- [ ] Semua data emosi tidak hanya warna (ada label + angka).

---

## 11. Codex + Figma MCP prompt (paste-ready)

```
Build Figma frame "Scene4 / Analytics" at 390x844 for dark-mode accessibility app "VibeLink". Purpose: daily emotion + interaction summary for Deaf / autistic users and their therapists.

Background #FFEBAF. Header: back chevron + "Analytics" + segmented control "Harian | Mingguan | Bulanan".

TOP: a "Mood Palette" — a horizontal strip of ~10 emotion-color segments (mostly green #4CAF50, a few yellow #FFC107 / orange #FF9800, one red #F44336), labelled "Hari ini" (heatmap of the day's emotions).

Stat cards (2x2, #FFF6E0 radius 18): "5 Percakapan", "2j 14m Listening", "2 Peringatan Suara", and a Donut chart "Distribusi Emosi" with a labelled legend + percentages.

Insight card: 💡 + Indonesian narrative "Hari ini Anda melakukan 5 percakapan. Mayoritas bernada positif. Ada 2 peringatan suara klakson di sore hari."

"Riwayat Percakapan": 2-3 session rows, each with a mini Emotion Bar thumbnail. A weekly trend AREA CHART (emotion colors). An "Ekspor PDF" button (filled Moonstone, >=48dp).

Font Inter, text #1E3A42/#4C6B73. All emotion data shown as color + LABEL + number (never color alone). Make MoodPalette, StatCard, DonutChart, InsightCard, SessionRow, AreaChart, ExportButton reusable.
```
