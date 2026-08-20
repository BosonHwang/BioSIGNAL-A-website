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
| `asset/web-background.png` | Hero art (signal arcs → ECG/EEG-like waveforms), right of copy |

Site stays light/white so these assets read cleanly. Accent colour tracks brand navy/blue.

---

### 3.4 Content sources (`docs/`)

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
