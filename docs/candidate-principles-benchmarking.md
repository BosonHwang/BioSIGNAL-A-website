# Candidate Principles B — Benchmark Design

**Status:** Draft for Round 1 · v0.2  
**Purpose:** Decide *how* a prioritised clinical task should be turned into a clinically grounded benchmark.  
**Structure:** **Shared core** (all experts) + **modality-specific** extensions for **ECG, EEG, PPG** only in this phase. Other modalities later.

These drafts are starting material for the BioSIGNAL-AI Delphi. They are **not** consensus. All participants rate the shared core; ECG / EEG / PPG experts also rate their modality block.

---

# Shared core

## BM-1 · Specify intended use, population, and setting

Every benchmark states the intended use claim, target population, clinical setting, and device / acquisition class in scope — and what is out of scope.

*Why:* Generality without scope is an unbounded claim.

---

## BM-2 · Define endpoints by the decision, not only by the label

Primary endpoints must map to the clinical decision the task informs. Labels inherited from corpora are starting points, not automatic endpoints.

*Why:* Models can satisfy corpus metrics and still lack clinical utility.

---

## BM-3 · Disclose the acquisition and processing chain

Benchmarks require documentation of sensor/device, placement, filtering, segmentation, and quality gating — and whether the same gates apply at inference.

*Why:* Hidden filters create silent train–serve mismatch.

---

## BM-4 · Test clinically grounded distribution shift

Headline claims require evaluation under declared shifts that matter for the intended use (site, device, acuity, population), not only i.i.d. splits of one corpus.

*Why:* Within-corpus tests are not generality.

---

## BM-5 · Report subgroup performance and calibration

Beyond aggregate discrimination, report pre-specified subgroups and calibration / threshold behaviour appropriate to the use claim.

*Why:* Pooled AUROC alone cannot support accountability or equity.

---

## BM-6 · Score clinical adequacy alongside error metrics

Pair conventional metrics with at least one clinical-adequacy or harm-aware measure (including abstention where appropriate).

*Why:* Aggregate error can reward regression-to-the-mean and miss decision-changing local failures.

---

## BM-7 · Require external validation for headline claims

Claims of fitness for the stated intended use require external validation (independent site and/or device regime), with protocol deviations reported.

*Why:* Internal tests from the same filtered pool cannot detect the selection effect the consortium exists to fix.

---

## BM-8 · Name the comparator and the analysis pipeline

Specify the reference standard / comparator and freeze a transparent scoring pipeline as shared infrastructure.

*Why:* Comparability needs an owned reference point, not whichever dataset was handy.

---

# Modality-specific — ECG

*Rate if you have ECG clinical or modelling expertise.*

## BM-ECG-1 · Declare lead set, placement, and lead availability

Benchmarks must state required leads, electrode placement assumptions, and how missing / noisy leads are handled at train and at test.

*Why:* Lead relationships and availability change what “same task” means across devices.

*Example:* Reduced-lead input with mandatory reporting when a claimed diagnostic feature lives primarily in absent leads.

---

## BM-ECG-2 · Preserve diagnostically important morphology in adequacy criteria

Where the use claim depends on morphology, benchmarks must include morphology- or feature-level adequacy — not waveform MAE / correlation alone.

*Why:* Temporal features (e.g. QT) can look solved while precordial amplitudes collapse; infarct patterns can be hallucinated as normal.

*Example:* Critical-feature checklist (ST segments, R-wave progression, intervals) + reader-adequacy for the named use.

---

## BM-ECG-3 · Separate rhythm claims from morphology / reconstruction claims

Do not let a downstream rhythm check substitute for morphology-critical use evaluation.

*Why:* Rhythm classification can pass while spatially meaningful information is lost.

---

## BM-ECG-4 · Score device- and acuity-shifted ECG explicitly

Headline ECG claims that extend beyond the development device or acuity class must include those shifts in the primary evaluation table.

*Why:* Clinical-grade 12-lead elective sets are an acquisition regime, not a proxy for patches or ED motion.

---

# Modality-specific — EEG

*Rate if you have EEG / epilepsy / neurophysiology expertise.*

## BM-EEG-1 · Fix and report montage, reference, and preprocessing

Benchmarks must lock montage/reference assumptions and disclose filtering, resampling, and channel selection used for scoring.

*Why:* Montage and reference dependence can dominate apparent model differences.

---

## BM-EEG-2 · Evaluate under clinically realistic artefact regimes

Primary EEG evaluation must include artefact / noise conditions representative of the intended monitoring setting — not only clean annotated clips.

*Why:* Clean segments overstate continuous-monitoring performance.

*Example:* Motion, electrode pop, ICU interference held out or stratified in the headline split.

---

## BM-EEG-3 · Report operating points that respect review workload

Beyond event-level detection metrics, report alert burden / positive predictive behaviour at thresholds relevant to human review.

*Why:* Clinical EEG AI fails in practice when sensitivity is bought with unreadable false-alarm rates.

---

## BM-EEG-4 · Align with federated panel norms where they exist

When federating existing EEG frameworks (e.g. seizure-benchmark ecosystems), map BioSIGNAL-AI core requirements onto their task definitions without erasing modality-specific governance.

*Why:* Shared core should compose with specialised communities, not overwrite them.

---

# Modality-specific — PPG

*Rate if you have PPG / wearable / photoplethysmography expertise.*

## BM-PPG-1 · Disclose optical hardware, site, and motion / wear-time gates

Benchmarks must report sensor type, wear location, sampling, motion filtering, and wear-time / quality thresholds — and whether they apply at inference.

*Why:* PPG “quality” gates often define the task more than the model does.

---

## BM-PPG-2 · Require stratum reporting for skin tone and perfusion when material

For use claims affected by optical sensing biases, pre-specify skin-tone and/or perfusion strata and make stratum metrics part of the headline report.

*Why:* Pooled SpO₂ or heart-rate error can hide unsafe subgroup failure.

---

## BM-PPG-3 · Test motion and ambulatory shift as first-class conditions

Ambulatory or wearable claims must include motion-rich evaluation as primary evidence, not a footnote.

*Why:* Resting fingertip PPG is a different measurement problem from daily-wear optical sensing.

---

## BM-PPG-4 · Tie metrics to the decision threshold of the use claim

Report performance at the operating point implied by the clinical or screening action — not only continuous estimation error.

*Why:* RMSE without an action threshold does not validate a workflow claim.

---

# How these will be used

1. All experts rate **shared core** BM-1…BM-8.  
2. Modality experts also rate **BM-ECG-*** / **BM-EEG-*** / **BM-PPG-***.  
3. Agreed items become a **benchmark specification template**: shared core + ECG/EEG/PPG extensions.  
4. A **worked exemplar** (one modality first) is revised after Delphi, then advanced to a pilot.

**Version:** 0.2 · Draft · BioSIGNAL-AI consortium  
**Phase-1 modalities:** ECG · EEG · PPG
