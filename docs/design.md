# BioSIGNAL-AI website — Phase 1 design

**Status:** Active  
**Audience:** consortium organisers + site maintainers  
**Live site:** https://bosonhwang.github.io/BioSIGNAL-A-website/  
**Repo:** https://github.com/BosonHwang/BioSIGNAL-A-website

This note concentrates the product decisions for the current site. It is the source of truth for what Phase 1 is — and is not.

---

## 1. Problem the site must solve

The position paper argues that biosignal AI is benchmarked on corpus-available labels, not on clinical decisions, and proposes a consortium to agree:

1. **Which** clinical problems should be prioritised as benchmarking tasks  
2. **How** those tasks should become clinically grounded benchmarks  

A clinically grounded evaluation standard is a public good. The paper’s near-term instrument is a **Delphi** on candidate principles, then a prioritised task portfolio, specification template, worked exemplar, and pilot — not a finished leaderboard.

**Implication for the website:** Phase 1 must support *forming consensus*, not pretend the platform already exists. Fake “Live” panels, fictional datasets, and leaderboards undermine credibility with the clinicians and regulators we need to recruit.

---

## 2. Product principle

> Decide the rules before building the leaderboard.

| Do now | Do later |
|--------|----------|
| Publish candidate principles | Consensus checklist / PDF |
| Let participants rate them | Invited expert login |
| Collect structured ratings | Formal Delphi rounds + preregistered protocol |
| Interest / identity on submit | Full benchmark platform, panels, submit pipeline |

Expert authentication belongs to **Delphi Round 1+** (magic link / invite token). Phase 1 has **no login**.

---

## 3. Information architecture

### 3.1 Two orthogonal axes

Principles are addressed in a **2 × 4** matrix. Filters are independent: pick one family **and** one scope.

```
                    Scope (Axis 2)
                 Core   ECG   EEG   PPG
Family       ┌─────────────────────────
(Axis 1)  A  │  A×Core  A×ECG … 
          B  │  B×Core  B×ECG …
```

**Axis 1 — Family** (what kind of principle)

| Code | Label | Question |
|------|--------|----------|
| `tp` | A · Task prioritisation | Which clinical problems should become benchmarks? |
| `bm` | B · Benchmark design | How does a prioritised task become a clinical benchmark? |

**Axis 2 — Scope** (where it applies)

| Code | Label | Who rates |
|------|--------|-----------|
| `core` | Shared core | Everyone |
| `ecg` | ECG · Electrocardiography | Modality experts (+ everyone may view) |
| `eeg` | EEG · Electroencephalography | Modality experts |
| `ppg` | PPG · Photoplethysmography | Modality experts |

Modality blocks **extend** the core; they do not replace it. Phase 1 modalities are **ECG, EEG, PPG only**.

UI must make orthogonality obvious (separate axis rows + “Now rating: Family × Scope” readout). Tags carry a short title and a subtitle explaining the axis choice.

### 3.3 Brand assets (`asset/`)

| File | Use |
|------|-----|
| `asset/logo.png` | Nav brand mark (icon + wordmark) |
| `asset/back1.png` | Full-page background art (signal bundle pinched at a waist → teal/coral/blue waveforms), fixed layer behind all content |
| `asset/web-background.svg` | Vector trace of `back1.png` (generated, kept as a scalable fallback/source) |
| `asset/web-background.png` | Legacy raster background (superseded) |

Site stays light so these assets read cleanly.

### 3.4 Colour system

The five brand colours. All site colours derive from these tokens (`:root` CSS variables in `index.html`); do not introduce ad-hoc hex values.

| Name | Hex | Token | Use |
|------|-----|-------|-----|
| 深海蓝 Deep-sea navy | `#103A6F` | `--brand-navy`, `--ink` | Brand primary: headings, body ink, outer bundle strands in background art |
| 科技蓝 Tech blue | `#2878D0` | `--accent` | Primary buttons, links, selected chips, kicker/IDs, curves |
| 生物青 Bio teal | `#16B4B8` | `--teal` | Physiological-signal accents (background art signal lines, decorative) |
| 活力珊瑚 Vital coral | `#F04E45` | `--coral` | Emphasis: live/pulse dots, ECG hero line in background art |
| 冷调白 Cool white | `#F8FBFC` | `--plane` | Page background (with faint navy ECG-paper grid on top) |

Supporting derived tones: `--accent-soft #D8E8F9` (tints), `--critical #D33A2F` (error text — darkened coral for contrast on white), `--good #1b8a1b` (completion green, functional only). Typography pairs with the palette: Space Grotesk for display, JetBrains Mono for data accents.

### 3.5 Visual & layout system (keep)

Principles behind the current `index.html` implementation. Follow these when extending the site.

**Typography — three-tier**

| Tier | Face | Used for |
|------|------|----------|
| Display | Space Grotesk (Google Fonts) | h1–h3, hero |
| Data / instrument | JetBrains Mono | kicker, axis numbers, principle IDs, progress counter, Likert digits, monitor labels |
| Body | system-ui stack | everything else |

The mono tier is what gives the site its "instrument" character — any new data-like element (counts, IDs, statuses) uses it.

**Fluid, zoom-resistant layout**

1. Container: full-width fluid — `width:calc(100% - 2*var(--pad))`, centred. No max-width cap: cards and the filter bar always fill the viewport. `--pad` (clamp 16–40px) provides the only side breathing room.
2. Proportional grids (`fr`) inside the container; `clamp()` for gaps and section padding.
3. Display type uses `clamp(min-rem, N vw, max-rem)`. The vw midpoint makes headings physically stable under browser zoom (1vw is a fixed physical width), matching the "can't shrink it" feel of reference sites. Do not size headings in fixed px/rem alone.
4. Few breakpoints, structural only: 900px (hero → single column), 720px (Likert row → vertical). Continuous scaling handles everything between.
5. Likert rows stretch with the card (5 equal `fr` columns); only the submit form keeps a width cap (720px) for readability.

**Background layering (bottom → top)**

1. `html` — cool white `#F8FBFC` with faint navy ECG-paper grid (CSS gradients, 7px minor / 35px major).
2. `body::before` — fixed full-viewport art layer: `asset/back1.png`, `cover / center`, opacity .55, `position:fixed` (not `background-attachment`, which breaks on iOS). Body itself must stay `background:transparent` — an opaque body paints over negative-z children.
3. Content — translucent surfaces so the art reads through: sticky bar `rgba(255,255,255,.92)` + blur, cards `.94`, submit band `.85`, footer `.75`.

**Motion rules**

- Entrance: one-shot `rise` (fade + translateY, ~.6–.8s, staggered ≤.25s) on hero elements; cards reveal on first scroll into view (IntersectionObserver adds `.in`).
- Ambient loops: 1.6–4s ease-in-out infinite, animating only `transform` / `opacity` / `box-shadow` (pulse dots, ECG sweep via `stroke-dashoffset`, monitor bars with negative `animation-delay` stagger).
- Feedback: Likert select pop (.22s), completed-card green flash, card hover lift.
- All motion is decorative: `prefers-reduced-motion: reduce` disables everything, and no information is conveyed by animation alone.

---

### 3.6 Content sources (`docs/`)

| File | Role |
|------|------|
| [paper.md](./paper.md) | Position / call-to-action draft |
| [principles-core.md](./principles-core.md) | Shared-core index |
| [principles-ecg.md](./principles-ecg.md) | ECG TP + BM extensions |
| [principles-eeg.md](./principles-eeg.md) | EEG TP + BM extensions |
| [principles-ppg.md](./principles-ppg.md) | PPG TP + BM extensions |
| [candidate-principles-task-prioritisation.md](./candidate-principles-task-prioritisation.md) | Full Principles A |
| [candidate-principles-benchmarking.md](./candidate-principles-benchmarking.md) | Full Principles B |
| [ratings-schema.md](./ratings-schema.md) | Export JSON schema |

The public `index.html` embeds the same principle IDs and short statements for rating. Long *why* / *example* prose stays in markdown.

---

## 4. Rating interaction (Phase 1)

### 4.1 Dimensions (3)

Each principle is scored on:

1. **Importance**  
2. **Clarity**  
3. **Feasibility**  

(Applicability was dropped to reduce load.)

### 4.2 Scale (5 points, labelled)

Integers **1–5**. Labels are dimension-specific and visible on each control (not numbers alone).

| | 1 | 2 | 3 | 4 | 5 |
|---|---|---|---|---|---|
| Importance | Not important | Slightly important | Moderately important | Important | Essential |
| Clarity | Unclear | Mostly unclear | Adequate | Clear | Very clear |
| Feasibility | Not feasible | Difficult | Feasible with effort | Feasible | Readily feasible |

Optional free-text note per principle (revision suggestion).

### 4.3 Layout & presentation

- Single-column vertical stack of principle cards (not a multi-column matrix of cards)  
- Fluid full-width layout; forced **light / white** theme (no dark-mode follow)  
- Progress: `completed / expected` for principles in the participant’s in-scope set  
- Local persistence in `localStorage` while rating  

### 4.4 In-scope set for completion

- **Shared core** is always required  
- Selecting a modality scope (ECG / EEG / PPG) adds that modality’s principles to the expected set (and marks the modality on the submit form)  
- Submit requires all expected principles fully rated on all three dimensions  

---

## 5. Collection model (no backend yet)

Phase 1 is a static GitHub Pages site.

1. Participant rates principles in-browser  
2. Fills name, email, affiliation, role, modalities  
3. **Download JSON** (`biosignal-ai-principle-ratings/v3`)  
4. Optionally open a mailto draft to `hello@biosignal-ai.org` and attach the file  

Organisers aggregate offline (e.g. median / IQR per principle × dimension). Schema: [ratings-schema.md](./ratings-schema.md).

**Later:** replace download+email with REDCap / Qualtrics / Formspree / custom API without changing the conceptual rating model.

---

## 6. What we deliberately removed

Earlier demos over-claimed. Phase 1 does **not** include:

- Multi-page “Delphi platform” with fake rounds / consensus results  
- Benchmark page with Live panels, fictional datasets, leaderboards, submit-to-rank  
- Open registration as authenticated experts  
- Demo badges that imply a finished product  

Those belong after consensus (pilot benchmark) or with a real Delphi backend.

---

## 7. Roadmap

| Phase | Goal | Site capability |
|-------|------|-----------------|
| **1 · now** | Candidate principles + structured feedback | Public rating UI, JSON export, white single-page app |
| **2 · Delphi** | Preregistered rounds | Invite / magic-link login; anonymous-within-panel rating; attrition tracking |
| **3 · Synthesis** | Publish agreement + disagreements | Consensus view; principle status badges |
| **4 · Pilot** | Worked exemplar → pilot benchmark | Spec template; one modality pilot; federate existing panels (e.g. SzCORE) where appropriate |

---

## 8. Design constraints (keep)

1. **Honesty over completeness** — never show infrastructure we have not built.  
2. **Orthogonal filters** — Family × Scope; never flatten into one chip strip of peers.  
3. **Docs are canonical** — site statements stay short; depth lives in `docs/`.  
4. **Low friction collect** — rating must produce analysable artefacts without requiring a server on day one.  
5. **Modality discipline** — Phase 1 only ECG / EEG / PPG extensions.  

---

## 9. Open decisions

- Intake endpoint (REDCap vs Formspree vs custom) for Phase 1.5  
- Consensus thresholds and preregistration venue for Phase 2  
- Which modality hosts the first worked exemplar after Round 1  
- Whether patients / advocates rate the same core items or a shortened set  

---

**Document version:** 0.1 · 2026-08-20 · aligns with site schema `biosignal-ai-principle-ratings/v3`
