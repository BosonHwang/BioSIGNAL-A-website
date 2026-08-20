# ECG — modality-specific candidate principles

**Status:** Draft v0.2  
**Extends:** shared core ([task prioritisation](./candidate-principles-task-prioritisation.md) · [benchmark design](./candidate-principles-benchmarking.md))  
**Who rates:** ECG clinicians, cardiology informatics, ECG ML / device researchers

These items do **not** replace the shared core. ECG experts rate core + this file.

---

## A · Task prioritisation (ECG)

### TP-ECG-1 · Lead set and device class are part of the task claim

Priority tasks must state whether the decision assumes standard 12-lead, reduced-lead, patch, or wearable single-lead acquisition — and refuse silent transfer across those classes.

*Why:* Rhythm labels on clinical 12-lead corpora do not define wearable or single-lead care gaps.

*Example:* “Wearable single-lead AF screening in ambulatory adults” ≠ “12-lead ED triage for ischaemia-related decisions.”

---

### TP-ECG-2 · Prefer tasks where morphology (not only rhythm) binds care

Where the clinical decision depends on localised waveform morphology (ST/T, QRS morphology, intervals with spatial meaning), that dependence must be explicit in the task brief.

*Why:* Rhythm-only corpora dominate ECG ML; morphology-critical decisions are under-represented relative to their clinical weight.

*Example:* Prefer ischaemia / infarction support or reconstruction-adequacy for a named diagnostic use over another rhythm-only leaderboard.

---

### TP-ECG-3 · Acuity and recording condition must match the claimed gap

Tasks aimed at acute care must not be prioritised solely on elective, motion-light outpatient corpora.

*Why:* Signal quality and lead completeness matter most where public ECG data are scarcest.

---

## B · Benchmark design (ECG)

### BM-ECG-1 · Declare lead set, placement, and lead availability

Benchmarks must state required leads, electrode placement assumptions, and how missing / noisy leads are handled at train and at test.

*Why:* Lead relationships and availability change what “same task” means across devices.

*Example:* Reduced-lead input with mandatory reporting when a claimed diagnostic feature lives primarily in absent leads.

---

### BM-ECG-2 · Preserve diagnostically important morphology in adequacy criteria

Where the use claim depends on morphology, benchmarks must include morphology- or feature-level adequacy — not waveform MAE / correlation alone.

*Why:* Temporal features (e.g. QT) can look solved while precordial amplitudes collapse; infarct patterns can be hallucinated as normal (Presacan et al.).

*Example:* Critical-feature checklist (ST segments, R-wave progression, intervals) + reader-adequacy for the named use.

---

### BM-ECG-3 · Separate rhythm claims from morphology / reconstruction claims

Do not let a downstream rhythm check substitute for morphology-critical use evaluation.

*Why:* Rhythm classification can pass while spatially meaningful information is lost.

---

### BM-ECG-4 · Score device- and acuity-shifted ECG explicitly

Headline ECG claims that extend beyond the development device or acuity class must include those shifts in the primary evaluation table.

*Why:* Clinical-grade 12-lead elective sets are an acquisition regime, not a proxy for patches or ED motion.

---

## Rating IDs (site)

| ID | Family |
|----|--------|
| TP-ECG-1 … TP-ECG-3 | Task prioritisation |
| BM-ECG-1 … BM-ECG-4 | Benchmark design |
