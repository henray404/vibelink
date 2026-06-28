# VibeLink Agent Notes

## Purpose

VibeLink is a static high-fidelity mobile prototype for an IMK final project. The product translates audio information into visual and haptic feedback for Deaf, hard-of-hearing, and neurodivergent (ASD) users.

The core product promise from the docs is: users should be able to understand conversation emotion, environmental sound context, sound direction, and daily interaction patterns without depending on hearing alone.

## Source Of Truth

Read these before changing copy, layout, or visual direction:

- `docs/README.md` - project overview and document map.
- `docs/PRD.md` - problem statement, solution, target users, user stories, functional requirements, implementation decisions, and scope.
- `docs/DESIGN_SPEC.md` - visual direction, tokens, layout rules, screen requirements, reusable components, and acceptance criteria.
- `docs/imk-analysis.md` - IMK theory mapping and accessibility rationale.
- `docs/research/ux-research.md` - cited UX and accessibility research.
- `docs/scenes/*.md` - detailed specs for Home, Conversation, Sound Map, and Analytics.

Do not invent product names, taglines, features, user types, metrics, or labels when they are absent from these files. Use the Indonesian terminology already present in the docs and screens.

## Critical Files

- `index.html` - prototype launcher for all screens.
- `screen0-onboarding.html` - splash and onboarding slides.
- `screen-auth.html` - login/register and accessibility profile selection.
- `screen1-home.html` - Home / Live Atmosphere Canvas.
- `screen2-conversation.html` - Conversation Mode with Emotion Bar and transcript bubbles.
- `screen3-soundmap.html` - Sound Map radar, detected sounds, confidence, distance, and safety disclaimer.
- `screen4-analytics.html` - Interaction Analytics, Mood Palette, stats, insight, history, and export entry point.
- `screen5-settings.html` - sensory personalization, accessibility, sound, haptic, and privacy settings.
- `screen6-profile.html` - user profile, cumulative stats, emergency contacts, smartwatch entry, and account actions.
- `styles.css` - shared tokens, layout primitives, cards, nav, controls, radar, charts, and accessibility behavior.
- `assets/` - VibeLink logo, icon, and UI SVG icons.

## Product Shape

Let the product's native structure organize work:

- Home is a live atmosphere/status view centered on dB level and detected sound categories.
- Conversation is a transcript plus explicit emotion interpretation.
- Sound Map is a spatial radar for sound direction and safety alerts.
- Analytics is a reflective summary of emotion and interaction patterns.
- Settings and Profile support personalization, accessibility, privacy, and emergency workflows.

The feature that should dominate the page is the one the README/PRD leads with: sensory substitution from audio into visual and haptic feedback. The four core features are Live Atmosphere Canvas, Conversation Mode, Sound Map, and Interaction Analytics.

## Visual Identity

Inherit the existing design language instead of introducing a new one:

- Static HTML/CSS, no build tool.
- Mobile frame target around 390px wide.
- Light, calm, low-stimulation interface for accessibility and ASD comfort.
- Background cream `#FFF8EE`, surface `#FFFFFF`, ink `#161616`, line `#222222`.
- Primary accent pink `#E96B95`, soft pink `#F7B7CF`.
- Emotion fills: positive `#B8E6C4`, neutral `#F6E6A8`, frustrated `#F7C59F`, angry/urgent `#F3A6A6`.
- Category fills: yellow `#F7E7A3`, pink `#F7B7CF`, blue `#B7D8F2`, green `#BDE8CA`.
- Typography uses Inter/Roboto/system sans. Text and important icons stay ink-colored over pastel fills.
- Shared spacing and radii live in `styles.css`: screen padding 20px, card padding 18px, card gap 14px, card radius 24px, chip radius 16px.

## Design And Content Rules

- Start from real repo content: docs, HTML labels, CSS tokens, SVG assets, scene specs, and PRD terminology.
- Preserve redundant coding: status must use color plus icon/text and, where relevant, haptic language.
- Never rely on color alone for emotion, alerts, categories, or navigation state.
- Keep touch targets at least 48px and avoid hidden gestures.
- Keep bottom navigation consistent across primary screens.
- Keep safety language honest: detection, direction, confidence, and distance are estimates; VibeLink is not a sole safety or medical tool.
- Keep backend, ML inference, smartwatch integration, emergency SMS/GPS, and PDF export as simulated UI only unless the project scope changes.
- Prefer focused edits to the existing static files over adding framework dependencies.

## Verification

For UI changes, manually open `index.html` and navigate every changed screen. Check mobile width, no horizontal overflow, readable contrast, keyboard focus, bottom nav consistency, and that the design still matches `docs/DESIGN_SPEC.md`.
