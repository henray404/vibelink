# VibeLink — Dokumentasi Desain UI/UX

Antarmuka penerjemah emosi & suasana lingkungan berbasis visualisasi audio-haptik untuk penyandang disabilitas pendengaran & neurodiversitas (ASD). Tugas IMK / Final Project.

## Struktur dokumen

| File | Isi |
|---|---|
| [`PRD.md`](PRD.md) | Product Requirements — problem, solusi, target user, 30 user story, functional req, scope. |
| [`DESIGN_SPEC.md`](DESIGN_SPEC.md) | Spesifikasi desain — visual direction, layout rules, 8 layar, Figma frame plan, acceptance criteria. |
| [`imk-analysis.md`](imk-analysis.md) | **Bab analisis IMK** — Shneiderman, Nielsen, Norman, Gestalt, WCAG, sensory substitution, per-scene map. |
| [`research/ux-research.md`](research/ux-research.md) | Riset UX bersitasi (WHO, NIDCD, CDC, NIMH, WCAG, arXiv, Apple, Android) — supervised, Codex web search. |
| [`scenes/scene1-home-canvas.md`](scenes/scene1-home-canvas.md) | Home — Live Atmosphere Canvas. |
| [`scenes/scene2-conversation.md`](scenes/scene2-conversation.md) | Conversation Mode (transkrip + Emotion Bar). |
| [`scenes/scene3-soundmap.md`](scenes/scene3-soundmap.md) | Sound Map (radar arah suara + keselamatan). |
| [`scenes/scene4-analytics.md`](scenes/scene4-analytics.md) | Interaction Analytics (Mood Palette). |

Layar pendukung (Onboarding, Login/Register, Settings, Profile) dispesifikasi di `PRD.md` + `DESIGN_SPEC.md` (tidak punya scene file terpisah karena bukan fitur visualisasi inti).

## Tiap scene file berisi

Purpose · Actors · Use cases · Layout (ASCII) · Component inventory · Interaksi · Interaction flow · Visual tokens · **Figma build instructions** · **Penerapan IMK** (§9b) · Acceptance criteria · **Codex + Figma MCP prompt** (paste-ready).

## Prinsip desain inti

- **Sensory substitution multimodal:** audio → visual (aurora/emotion bar/radar) + haptik.
- **Redundant coding (WCAG 1.4.1):** status = warna + ikon + teks (+ getaran), tidak pernah warna saja.
- **Palet Vanilla `#FFEBAF` + Moonstone `#4C9DB0`** (light, calm) + palet emosi terkalibrasi (`#4CAF50`/`#FFC107`/`#FF9800`/`#F44336`).
- **Aksesibilitas:** touch target ≥48dp, kontras ≥4.5:1, personalisasi sensorik (kritis untuk ASD).
- **Kejujuran sistem:** SER & sound detection probabilistik → tampilkan confidence, bukan klaim pasti; disclaimer keselamatan.

Selaras tema "Perancangan Pengalaman Pengguna untuk Pembangunan Indonesia Maju dan Berkelanjutan" · SDG 3 & SDG 10.
