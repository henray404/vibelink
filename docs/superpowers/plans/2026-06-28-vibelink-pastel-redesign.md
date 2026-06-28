# VibeLink Pastel Redesign Implementation Plan

> **For agentic workers:** Execute this plan task-by-task, in order. Steps use checkbox (`- [ ]`) syntax. After each task, OPEN the HTML in a browser (or validate structurally) before the next. This redesign reskins the EXISTING prototype in `vibelink/` (styles.css + 9 HTML screens) to a soft-pastel + cream + black-accent flat aesthetic matching `docs/image.png`, with all values fixed by `docs/research/color-shape-research.md`.

**Goal:** Reskin VibeLink's existing static HTML/CSS prototype to a calm pastel-on-cream flat UI (big numbers, rounded pill shapes, multi-pastel category coding, pink primary accent, black ink text), while strengthening accessibility for Deaf/HoH + ASD users.

**Architecture:** One shared `styles.css` holds the entire design system (CSS custom properties + components). Each `screen*.html` is standalone, links `styles.css`, and is reskinned region-by-region. No frameworks, no build tools, no CDNs. Tiny inline vanilla JS only for tab/segment/keyboard behavior already present.

**Tech Stack:** Static HTML5 + CSS3 (custom properties, flexbox/grid) + minimal vanilla JS. Existing SVG assets in `assets/icons/`.

## Global Constraints

Copy these EXACT values. Every task inherits this section.

**Palette (from research — pastels are FILL ONLY, never text):**
- `--cream: #FFF8EE` — app background
- `--surface: #FFFFFF` — light cards
- `--ink: #161616` — ALL text, icons, big numbers, labels on pastel
- `--line: #222222` — borders on pastel controls, focus outline, separators
- `--accent: #E96B95` — primary pink: FAB, active nav, primary CTA fill. **Text on pink = `#161616`, never white.**
- `--accent-soft: #F7B7CF` — soft pink fill
- Emotion fills (label/icon on them = `--ink`): `--emo-pos: #B8E6C4` · `--emo-neu: #F6E6A8` · `--emo-fru: #F7C59F` · `--emo-ang: #F3A6A6`
- Category fills: `--cat-yellow: #F7E7A3` · `--cat-pink: #F7B7CF` · `--cat-blue: #B7D8F2` · `--cat-green: #BDE8CA`
- Black accent block: bg `--ink`, text/icon `--cream`
- `--muted: #5C5C5C` — secondary text on cream (contrast ~6:1, OK for body, NOT for <14px critical)

**Contrast rules (WCAG):** text/number/critical-icon use `--ink` (≥9:1 on any pastel/cream). NEVER use a pastel as a text color on cream (fails, ~1.2–2.8:1). Any pastel-filled CONTROL gets a `1.5px solid var(--line)` border (non-text contrast 1.4.11). Focus = `outline:3px solid var(--line); outline-offset:2px`.

**Type scale (Inter; all resizable to 200%):**
- Display / big number: `clamp(48px, 14vw, 64px)` / 800, `letter-spacing:-1px`, tabular-nums
- Headline (screen title): 24px / 700
- Title (card title): 18px / 700
- Body: 16px / 500 (minimum 14px anywhere)
- Label/meta: 14px / 500
- Caption (non-essential only): 12px / 500

**Widget sizing (from research):**
- Min touch target 48×48px; primary actions 56px. No interactive element below 44px.
- FAB (center nav, mic): 60px circle, `--accent` fill, `--ink` icon.
- Bottom nav: height 72px, 5 slots, icon 24px inside 48px hit area, active slot icon `--accent`.
- Icon button: 48px circle, `--surface` fill, `1.5px solid var(--line)`.
- Card radius 24px; pill/capsule radius 999px; chip radius 16px.
- Screen padding 20px; card padding 18px; gap between cards 14px.
- Pill button height 52px, horizontal padding 24px.
- Category icon chip: 44px circle (pastel fill + `--ink` icon + `1.5px var(--line)` border).
- Progress bar: height 12px, radius 999px, track `#EFE7D6`, fill pastel/accent.
- Hero ring (Home score / Sound Map radar): 260px diameter.
- Emotion bar: height 56px, radius 16px.
- Phone canvas: max-width 390px, centered, `min-height:100vh`, no horizontal overflow.

**Accessibility (non-negotiable):**
- Redundant coding: every emotion/category/status = color + icon + TEXT label (+ shape). Never color alone (WCAG 1.4.1).
- `prefers-reduced-motion`: disable all aurora/radar/blink animations under the media query.
- Shapes rounded everywhere; sharp corners ONLY on the danger/alarm salience element.
- All clickable cards: `tabindex="0"`, role, keyboard Enter/Space (reuse existing shared script).
- Indonesian UI copy; keep real content from `docs/PRD.md` + `docs/scenes/*.md` (Rina/Dimas, 62 dB, 5 Percakapan, 2j 14m, confidence %, disclaimer).

---

## File Structure

- Rewrite: `vibelink/styles.css` (whole design system — keystone, Task 1)
- Reskin: `vibelink/screen0-onboarding.html`, `screen-auth.html`, `screen1-home.html`, `screen2-conversation.html`, `screen3-soundmap.html`, `screen4-analytics.html`, `screen5-settings.html`, `screen6-profile.html`, `index.html`
- Update: `vibelink/docs/DESIGN_SPEC.md` + `docs/imk-analysis.md` §4 (palette tokens → pastel set; note research)
- Assets unchanged (reuse `assets/icons/*.svg`; recolor via CSS filter or treat as `--ink`).

Each HTML keeps its existing structure/content; tasks change classes, tokens, and widget markup to the new system. Do screens one at a time; validate each.

---

## Task 1: Rewrite the design system (`styles.css`)

**Files:**
- Rewrite: `vibelink/styles.css`

**Produces:** CSS classes every screen consumes: `.app` (phone canvas), `.topbar`, `.icon-btn`, `.h-title`, `.card`, `.card--dark`, `.pill-btn`, `.pill-btn--dark`, `.segmented`, `.chip`, `.cat-chip`, `.bignum`, `.progress`/`.progress__fill`, `.hero-ring`, `.emotion-bar`, `.emotion-seg`, `.bubble`, `.bubble--strip`, `.stat-card`, `.mood-palette`, `.badge-tile`, `.timeline`, `.bottom-nav`, `.nav-item`, `.fab`, `.list-row`, `.toggle`, `.slider`, `.disclaimer`, plus tokens `:root{...}`.

- [ ] **Step 1: Replace `:root` tokens + base reset**

```css
:root{
  --cream:#FFF8EE; --surface:#FFFFFF; --ink:#161616; --line:#222222;
  --muted:#5C5C5C; --accent:#E96B95; --accent-soft:#F7B7CF;
  --emo-pos:#B8E6C4; --emo-neu:#F6E6A8; --emo-fru:#F7C59F; --emo-ang:#F3A6A6;
  --cat-yellow:#F7E7A3; --cat-pink:#F7B7CF; --cat-blue:#B7D8F2; --cat-green:#BDE8CA;
  --track:#EFE7D6;
  --r-card:24px; --r-chip:16px; --pad:18px; --screen-pad:20px; --gap:14px;
  --font:'Inter',system-ui,-apple-system,'Segoe UI',Roboto,sans-serif;
}
*{box-sizing:border-box;margin:0;padding:0}
html{-webkit-text-size-adjust:100%}
body{background:#E9E0CE;font-family:var(--font);color:var(--ink);
  display:flex;justify-content:center;min-height:100vh}
.app{width:100%;max-width:390px;background:var(--cream);min-height:100vh;
  position:relative;padding:0 var(--screen-pad) 96px;overflow-x:hidden}
img{display:block}
a{color:inherit;text-decoration:none}
```

- [ ] **Step 2: Topbar, titles, icon buttons**

```css
.topbar{display:flex;align-items:center;justify-content:space-between;
  padding:16px 0 8px;min-height:56px}
.h-title{font-size:24px;font-weight:700;letter-spacing:-.3px}
.icon-btn{width:48px;height:48px;border-radius:50%;background:var(--surface);
  border:1.5px solid var(--line);display:flex;align-items:center;justify-content:center}
.icon-btn img{width:22px;height:22px}
.back-btn{width:44px;height:44px;border-radius:50%;border:1.5px dashed var(--line);
  background:transparent;display:flex;align-items:center;justify-content:center;font-size:20px}
```

- [ ] **Step 3: Cards, pills, segmented, chips**

```css
.card{background:var(--surface);border-radius:var(--r-card);padding:var(--pad);
  margin-bottom:var(--gap)}
.card--dark{background:var(--ink);color:var(--cream)}
.card--accent{background:var(--accent)} /* text inside must be --ink */
.pill-btn{height:52px;border-radius:999px;padding:0 24px;border:1.5px solid var(--line);
  background:var(--surface);font:600 16px/1 var(--font);color:var(--ink);
  display:inline-flex;align-items:center;justify-content:center;gap:8px;cursor:pointer}
.pill-btn--dark{background:var(--ink);color:var(--cream);border-color:var(--ink)}
.pill-btn--accent{background:var(--accent);border-color:var(--accent);color:var(--ink)}
.segmented{display:inline-flex;background:var(--surface);border:1.5px solid var(--line);
  border-radius:999px;padding:4px}
.segmented button{border:0;background:transparent;border-radius:999px;height:40px;
  padding:0 16px;font:600 14px var(--font);color:var(--ink);cursor:pointer}
.segmented button[aria-selected="true"]{background:var(--ink);color:var(--cream)}
.chip{display:inline-flex;align-items:center;gap:6px;height:32px;padding:0 12px;
  border-radius:var(--r-chip);border:1.5px solid var(--line);font:600 13px var(--font)}
.cat-chip{width:44px;height:44px;border-radius:50%;border:1.5px solid var(--line);
  display:flex;align-items:center;justify-content:center}
.cat-chip img{width:22px;height:22px}
```

- [ ] **Step 4: Big number, progress, hero ring, list rows**

```css
.bignum{font-weight:800;font-size:clamp(48px,14vw,64px);letter-spacing:-1px;
  line-height:1;font-variant-numeric:tabular-nums}
.bignum--sm{font-size:28px}
.progress{height:12px;border-radius:999px;background:var(--track);overflow:hidden}
.progress__fill{height:100%;border-radius:999px;background:var(--accent)}
.hero-ring{width:260px;height:260px;margin:8px auto;position:relative;
  display:flex;align-items:center;justify-content:center}
.list-row{display:flex;align-items:center;gap:12px;padding:12px 0;min-height:56px}
.list-row .label{flex:1;font-weight:600;font-size:16px}
.list-row .meta{color:var(--muted);font-size:14px}
.disclaimer{font-size:12px;color:var(--muted);text-align:center;margin-top:10px;line-height:1.4}
```

- [ ] **Step 5: Emotion bar, chat bubble, mood palette (semantic pastels)**

```css
.emotion-bar{height:56px;border-radius:16px;border:1.5px solid var(--line);
  overflow:hidden;display:flex}
.emotion-seg{flex:1}
.emotion-seg.pos{background:var(--emo-pos)} .emotion-seg.neu{background:var(--emo-neu)}
.emotion-seg.fru{background:var(--emo-fru)} .emotion-seg.ang{background:var(--emo-ang)}
.emotion-label{display:flex;align-items:center;gap:8px;font-weight:700;font-size:18px;margin:10px 0}
.bubble{background:var(--surface);border:1.5px solid var(--line);border-radius:18px;
  padding:12px 14px;margin-bottom:10px;position:relative;font-size:16px;line-height:1.4}
.bubble .strip{position:absolute;left:0;top:10px;bottom:10px;width:5px;border-radius:5px}
.bubble small{display:block;color:var(--muted);font-size:13px;margin-top:4px}
.mood-palette{height:32px;border-radius:12px;border:1.5px solid var(--line);
  overflow:hidden;display:flex}
.mood-palette i{flex:1}
```

- [ ] **Step 6: Stat cards, badge tiles, timeline, toggle, slider**

```css
.grid2{display:grid;grid-template-columns:1fr 1fr;gap:var(--gap)}
.stat-card{background:var(--surface);border-radius:var(--r-card);padding:16px}
.stat-card .k{color:var(--muted);font-size:14px;margin-top:4px}
.badge-tile{background:var(--surface);border:1.5px solid var(--line);border-radius:20px;
  padding:14px;text-align:center;font-size:13px;font-weight:600}
.timeline{position:relative;padding-left:22px}
.timeline::before{content:"";position:absolute;left:6px;top:6px;bottom:6px;width:2px;background:var(--line)}
.timeline .dot{position:absolute;left:0;width:14px;height:14px;border-radius:50%;
  background:var(--cream);border:2px solid var(--ink)}
.toggle{width:52px;height:32px;border-radius:999px;background:var(--track);
  border:1.5px solid var(--line);position:relative}
.toggle[aria-checked="true"]{background:var(--accent)}
.toggle .knob{position:absolute;top:3px;left:3px;width:24px;height:24px;border-radius:50%;background:var(--ink)}
.toggle[aria-checked="true"] .knob{left:25px}
.slider{width:100%;height:12px;border-radius:999px;background:var(--track);border:1.5px solid var(--line)}
```

- [ ] **Step 7: Bottom nav + FAB + reduced motion**

```css
.bottom-nav{position:fixed;bottom:0;left:50%;transform:translateX(-50%);
  width:100%;max-width:390px;height:72px;background:var(--surface);
  border-top:1.5px solid var(--line);display:flex;align-items:center;justify-content:space-around;padding:0 8px}
.nav-item{width:48px;height:48px;display:flex;flex-direction:column;align-items:center;
  justify-content:center;gap:2px;font-size:11px;color:var(--ink)}
.nav-item img{width:24px;height:24px}
.nav-item.active{color:var(--accent)}
.fab{width:60px;height:60px;border-radius:50%;background:var(--accent);
  border:1.5px solid var(--line);display:flex;align-items:center;justify-content:center;
  margin-top:-24px;box-shadow:0 6px 16px rgba(233,107,149,.4)}
.fab img{width:26px;height:26px}
:focus-visible{outline:3px solid var(--line);outline-offset:2px}
@media (prefers-reduced-motion: reduce){*{animation:none!important;transition:none!important}}
```

- [ ] **Step 8: Validate**

Run: open `vibelink/index.html` in a browser; or check structurally:
```bash
grep -c "FFF8EE\|E96B95\|--ink" vibelink/styles.css
```
Expected: tokens present; file has no `#121212`/`#4C9DB0` leftovers (`grep -ci "121212\|4C9DB0" vibelink/styles.css` → 0).

---

## Task 2: Home — `screen1-home.html` (hero number + soundscape ring + quick access + mic FAB)

**Files:** Modify `vibelink/screen1-home.html`

Reskin to match `docs/image.png` hero pattern. Regions top→bottom:

- [ ] **Step 1: Topbar** — left `.back-btn` (or logo `assets/vibelink-logo.svg` height 28px), right two `.icon-btn` (notification.svg, profile via avatar). 

- [ ] **Step 2: Hero ring (replaces dark aurora canvas)** — `.hero-ring` 260px. Center: `.bignum` showing current loudness e.g. `62` with a `dB` label under it (14px) + status chip `.chip` "Normal" (icon + text, fill `--emo-neu`, border `--line`). Around the ring place 4–6 small `.cat-chip` (pastel category fills + `--ink` sound icons from `assets/icons/sound-*.svg`) at arc positions, like the reference's icon arc. Ring arc segments use category pastels. Animation (slow pulse) MUST be under `prefers-reduced-motion` guard.

- [ ] **Step 3: Primary action row** — a `.pill-btn--dark` "Mulai Mendengarkan" (mic icon) + two `.icon-btn` (filter.svg, export.svg), mirroring reference's "Plan check-up" + icon buttons.

- [ ] **Step 4: Assistant/insight card** — `.card--accent` (pink) with `--ink` text: "VibeLink: suasana sekitar tenang 12 menit terakhir." + a `.pill-btn--dark` "Lihat detail". (Mirrors reference's pink "Intelly assistant" card; text is `--ink` not white.)

- [ ] **Step 5: "Suara terdeteksi" list** — section title `.h-title` (18px) + 2–3 `.list-row`: `.cat-chip` (category color+icon) + label (e.g. "Percakapan", "Kendaraan") + `.progress` + `.bignum--sm` level. Mirrors reference "Health systems" list.

- [ ] **Step 6: Bottom nav + FAB** — `.bottom-nav` 5 slots: Home(active) · Conversation · [FAB mic, center, pink] · Sound Map · Profile. Use `assets/icons/nav-*.svg` + `mic.svg` in FAB. Each `.nav-item` links its screen.

- [ ] **Step 7: Validate** — open in browser; confirm: big number readable, no pastel-as-text, every category chip has icon+label, FAB ≥56px, nav links work. `grep -c "cat-chip\|bignum\|bottom-nav" screen1-home.html` ≥ 3.

---

## Task 3: Conversation — `screen2-conversation.html`

**Files:** Modify `vibelink/screen2-conversation.html`

- [ ] **Step 1: Topbar** — `.back-btn` + `.h-title` "Conversation" + `.segmented` A-/A/A+ (text scaling).
- [ ] **Step 2: Emotion bar (40%)** — `.emotion-bar` with `.emotion-seg` pos/neu/fru/ang. Below it `.emotion-label`: emoji icon (`assets/icons/emotion-*.svg`) + bold label "Tegang" + a `.chip` "confidence 82%". Color + icon + label redundancy.
- [ ] **Step 3: Transcript (60%)** — 3 `.bubble` each with `.strip` colored by emotion (pos/neu/fru/ang) + Indonesian sample lines from scene2 doc ("Oh bagus banget idemu!", "Kita perlu selesaikan ini sebelum Jumat.", "Ya... nggak papa sih.") + `small` emotion label per bubble.
- [ ] **Step 4: Controls** — row of `.pill-btn--accent` "Rekam" + `.pill-btn` "Jeda" + `.pill-btn` "Hapus", each ≥52px.
- [ ] **Step 5: Bottom nav** — Conversation active.
- [ ] **Step 6: Validate** — open; emotion shown as color+icon+label; bubbles have strips; controls ≥52px.

---

## Task 4: Sound Map — `screen3-soundmap.html`

**Files:** Modify `vibelink/screen3-soundmap.html`

- [ ] **Step 1: Topbar** — `.back-btn` + "Sound Map" + `.segmented` Filter/Alert.
- [ ] **Step 2: Radar ring** — reuse `.hero-ring` (260px) as the radar: concentric rounded rings (border `--line`), center dot "Anda". Place category blips as `.cat-chip` at directions (alarm top, car lower-left bigger, person right). The DANGER blip (alarm) is the ONLY sharp-cornered element + red `--emo-ang` fill + `--line` border + (motion-guarded) blink. Icon size ∝ intensity.
- [ ] **Step 3: Detection list** — 3 `.list-row`: `.cat-chip` + label ("Alarm — depan", "Kendaraan — kiri", "Orang — kanan") + `.meta` confidence/jarak/waktu ("92% · ~5m · now"). 
- [ ] **Step 4: Disclaimer** — `.disclaimer`: "Arah & deteksi bersifat estimasi — bukan alat keselamatan tunggal."
- [ ] **Step 5: Bottom nav** — Sound Map active.
- [ ] **Step 6: Validate** — open; categories differ by color+shape+label; disclaimer present; danger blip distinct.

---

## Task 5: Analytics — `screen4-analytics.html`

**Files:** Modify `vibelink/screen4-analytics.html`

- [ ] **Step 1: Topbar** — `.back-btn` + "Analytics" + `.segmented` Harian/Mingguan/Bulanan.
- [ ] **Step 2: Mood Palette** — section title + `.mood-palette` strip of ~10 `i` segments using emotion pastels (mostly pos, some neu/fru, one ang), caption "Hari ini".
- [ ] **Step 3: Stat cards** — `.grid2` of 4 `.stat-card`: `.bignum--sm` "5" / k "Percakapan"; "2j 14m" / "Listening"; "2" / "Peringatan"; a CSS donut (conic-gradient of emotion pastels) + label "Distribusi emosi" with a small legend (color+label+%).
- [ ] **Step 4: Insight card** — `.card--accent` (pink) `--ink` text: "Hari ini Anda melakukan 5 percakapan. Mayoritas bernada positif. Ada 2 peringatan klakson di sore hari."
- [ ] **Step 5: Riwayat + tren** — 2 `.list-row` session rows each with a mini `.mood-palette` thumbnail; a weekly trend bar row (pastel bars on `--track`).
- [ ] **Step 6: Export** — `.pill-btn--dark` "Ekspor PDF" (export.svg).
- [ ] **Step 7: Bottom nav** — (Analytics reached via Home/Profile; keep nav consistent). Validate: big numbers, donut has legend+%, mood palette present.

---

## Task 6: Settings — `screen5-settings.html`

**Files:** Modify `vibelink/screen5-settings.html`

- [ ] **Step 1: Topbar** — `.back-btn` + "Pengaturan".
- [ ] **Step 2: Sections as `.card`** with `.h-title` headers + `.list-row` + `.toggle`/`.slider`:
  - Profil Aksesibilitas (Tunarungu/HoH · Neurodivergent · Lainnya — choose)
  - Pengaturan Visual (5 preset palet via chips; **Mode Buta Warna** toggle; **Kurangi Gerak / reduced motion** toggle)
  - Pengaturan Haptik (intensitas `.slider` + per-kategori `.toggle`)
  - Pengaturan Suara (sensitivitas `.slider` + kalibrasi noise floor)
  - Aksesibilitas Tambahan (Ukuran Teks `.segmented` Kecil/Normal/Besar/XL; Kontras Tinggi `.toggle`; Screen reader `.toggle`)
  - Data & Privasi (simpan riwayat, auto-delete, ekspor)
- [ ] **Step 3: Validate** — every toggle/slider ≥48px target; reduced-motion + color-blind + text-size controls present (these implement the research must-do checklist).

---

## Task 7: Profile — `screen6-profile.html`

**Files:** Modify `vibelink/screen6-profile.html`

- [ ] **Step 1: Header card** — avatar (64px circle) with a pastel "mood signature" ring + name + email + badge `.chip` "Profil: Tunarungu".
- [ ] **Step 2: Statistik Saya** — `.grid2` `.stat-card` with `.bignum--sm` (total listening, percakapan, peringatan, emosi tersering).
- [ ] **Step 3: Kontak Darurat** — `.card` listing ≤3 `.list-row` + "Tambah kontak" `.pill-btn`; note auto SMS+GPS >10s.
- [ ] **Step 4: Hubungkan Perangkat** — `.list-row` smartwatch.
- [ ] **Step 5: Footer** — `.pill-btn` "Keluar" + `.pill-btn` "Hapus Akun" (danger styling: text `--ink`, border `--emo-ang`), spaced apart.
- [ ] **Step 6: Bottom nav** — Profile active. Validate: targets ≥48px, danger button distinct but not pastel-text.

---

## Task 8: Onboarding + Auth + index

**Files:** Modify `vibelink/screen0-onboarding.html`, `screen-auth.html`, `index.html`

- [ ] **Step 1: Onboarding** — Splash: `assets/vibelink-icon.svg` + wordmark on cream; playful rounded organic pastel shapes (NOT sharp). 3 slides (Canvas/Conversation/Sound Map) each with big rounded illustration block (`.card` pastel) + ≤2-line text (18px) + `.segmented`-style dot indicator + `.pill-btn--dark` "Lanjut" + "Lewati" text link top-right (≥44px).
- [ ] **Step 2: Auth** — Login: labelled fields (label ABOVE input, 14px), `.pill-btn--accent` "Masuk" full-width, Google/Apple `.pill-btn`. Register step 2: 3 big `.card` profile choices (Tunarungu/HoH · ASD · Lainnya) as selectable tiles (`tabindex`, `aria-pressed`). Inputs: 52px height, `1.5px var(--line)` border, radius 16px.
- [ ] **Step 3: index.html** — launcher: cream bg, title "VibeLink — Prototype", grid of `.card` thumbnails linking each screen with its name.
- [ ] **Step 4: Validate** — open each; onboarding shapes rounded; auth labels above fields; index links all 9 screens.

---

## Task 9: Update design docs to the pastel system

**Files:** Modify `vibelink/docs/DESIGN_SPEC.md`, `vibelink/docs/imk-analysis.md`

- [ ] **Step 1: DESIGN_SPEC `## Visual Direction`** — replace Vanilla/Moonstone brand palette block with the pastel set: cream `#FFF8EE` bg, ink `#161616` text, pink `#E96B95` accent, emotion pastels `#B8E6C4`/`#F6E6A8`/`#F7C59F`/`#F3A6A6`, category pastels `#F7E7A3`/`#F7B7CF`/`#B7D8F2`/`#BDE8CA`. Note: pastels = fill only, text always ink.
- [ ] **Step 2: imk-analysis.md `## 4. Sistem Warna`** — replace token table + contrast table with the pastel set + the research contrast ratios (ink on each pastel 9–14:1 ✅; pastel-as-text fails). Add one line linking `docs/research/color-shape-research.md` and the shape/rounded rationale (Bar & Neta) under §6/§14.
- [ ] **Step 3: Validate** — `grep -ci "4C9DB0\|FFEBAF\|Moonstone\|Vanilla" docs/DESIGN_SPEC.md docs/imk-analysis.md` → 0 (brand palette fully migrated; emotion/category hexes remain).

---

## Self-Review (run before handoff)

1. **Spec coverage:** image.png patterns mapped — hero big-number ring (Home T2 / Sound Map T4), pink assistant card (T2 Home / T5 Analytics), pastel-icon list w/ progress + big number (T2/T5), bottom nav + center pink FAB (all screens), pill/segmented/big-number (T1). ✓
2. **Research must-do covered:** contrast (ink text only, T1), redundant coding (icon+label everywhere), reduced-motion (T1 Step 7 + Settings T6), adjustable text (Settings text-size + 200% resize), adjustable haptics (Settings), color-blind mode (Settings), touch ≥48px (T1 sizing), rounded shapes + sharp only for danger (T1/T4). ✓
3. **Placeholder scan:** every CSS block is concrete; per-screen specs name exact classes, sizes, content. ✓
4. **Token consistency:** class names in screens (`.hero-ring`, `.cat-chip`, `.bignum`, `.emotion-bar`, `.bottom-nav`, `.fab`) all defined in Task 1. ✓

---

## Execution note

Tasks 1→9 in order. Task 1 (styles.css) is the keystone — all screens depend on it; do it first and validate before reskinning screens. Keep existing HTML content/copy; change classes + widget markup + tokens only. Reuse `assets/icons/*.svg`. Open each screen in a browser after its task.
