# Candidate Principles A — Task Prioritisation

**Status:** Draft for Round 1 · v0.2  
**Purpose:** Decide *which* clinical problems should become biosignal AI benchmarking tasks.  
**Structure:** **Shared core** (all experts) + **modality-specific** extensions for **ECG, EEG, PPG** only in this phase. Other modalities later.

These drafts are starting material for the BioSIGNAL-AI Delphi. They are **not** consensus. All participants rate the shared core; ECG / EEG / PPG experts also rate their modality block.

---

# Shared core

## TP-1 · Begin from a documented care gap

A candidate task must start from a stated clinical need or care-delivery constraint — not from the availability of a public label set.

*Why:* Public corpora supply tasks by default. That selection is convenient, not clinical.

*Example:* Prioritise a named care gap over “classify every label the corpus happens to carry.”

---

## TP-2 · Bind the task to a defined clinical decision

Every task states *who* acts, *what* decision is informed, and *in which setting* (acuity, device class, time pressure).

*Why:* Without a decision, scores measure label agreement, not clinical utility.

---

## TP-3 · Prefer tasks where failure cost is clinically describable

False negatives, false positives, and inappropriate abstention must have stated consequences for patients or workflows.

*Why:* Aggregate discrimination hides asymmetric harm.

---

## TP-4 · Do not let label availability alone justify priority

Accessible, statistically convenient labels are insufficient grounds for inclusion in the priority portfolio.

*Why:* The field already over-indexes on what corpora contain.

---

## TP-5 · Require a path to multi-site / multi-device evaluation

A prioritised task must be evaluable beyond a single acquisition regime (site, device, population).

*Why:* Generality claims collapse when development and evaluation share one regime while deployment spans others.

---

## TP-6 · Make equity measurable by design

Tasks must specify which subgroups or settings are clinically material, and how underperformance would be detected rather than averaged away.

*Why:* Non-representative corpora make disparities unmeasurable.

---

## TP-7 · Prefer tasks that change what models are rewarded for

Among otherwise similar candidates, prefer those that redirect optimisation toward clinically grounded endpoints.

*Why:* Shared infrastructure should alter incentives, not reproduce corpus-default leaderboards.

---

# Modality-specific — ECG

*Rate if you have ECG clinical or modelling expertise. These extend the core; they do not replace it.*

## TP-ECG-1 · Lead set and device class are part of the task claim

Priority tasks must state whether the decision assumes standard 12-lead, reduced-lead, patch, or wearable single-lead acquisition — and refuse silent transfer across those classes.

*Why:* Rhythm labels on clinical 12-lead corpora do not define wearable or single-lead care gaps.

*Example:* “Wearable single-lead AF screening in ambulatory adults” is a different priority item from “12-lead ED triage for ischaemia-related decisions.”

---

## TP-ECG-2 · Prefer tasks where morphology (not only rhythm) binds care

Where the clinical decision depends on localised waveform morphology (ST/T, QRS morphology, intervals with spatial meaning), that dependence must be explicit in the task brief.

*Why:* Rhythm-only corpora dominate ECG ML; morphology-critical decisions are under-represented relative to their clinical weight.

*Example:* Prefer ischaemia / infarction support or reconstruction-adequacy for a named diagnostic use over another rhythm-only leaderboard.

---

## TP-ECG-3 · Acuity and recording condition must match the claimed gap

Tasks aimed at acute care must not be prioritised solely on elective, motion-light outpatient corpora.

*Why:* Signal quality and lead completeness matter most where public ECG data are scarcest.

---

# Modality-specific — EEG

*Rate if you have EEG / epilepsy / neurophysiology expertise.*

## TP-EEG-1 · Montage, reference, and channel set define the decision context

A priority task must state the montage / reference / channel assumptions of the clinical workflow it supports.

*Why:* The same “seizure detection” label does not transfer across montages and recording setups.

*Example:* Continuous ICU scalp EEG triage ≠ high-density research montage event labelling.

---

## TP-EEG-2 · Prefer tasks that name the review / escalation decision

Priority EEG tasks should specify who reviews alerts, under what workload, and what escalation the model is meant to support.

*Why:* Event labels without a review-cost model reward sensitivity that clinics cannot absorb.

*Example:* “Reduce missed electrographic seizures without flooding the on-call review queue.”

---

## TP-EEG-3 · Artefact and noise regimes are part of prioritisation, not afterthoughts

Tasks must declare which artefact / noise conditions are in-scope for the care setting (motion, impedance, ICU interference).

*Why:* Clean annotated segments overstate readiness for continuous monitoring.

---

# Modality-specific — PPG

*Rate if you have PPG / wearable / photoplethysmography expertise.*

## TP-PPG-1 · Wearable vs clinical PPG are different task families

Priority items must separate optical wearable ambulatory use from clinical fingertip / bedside PPG — including motion and wear-time assumptions.

*Why:* Corpus convenience often collapses these regimes; clinical decisions do not.

---

## TP-PPG-2 · Prefer tasks where perfusion and skin-tone strata matter to the claim

If the intended decision could fail systematically by perfusion or skin pigmentation, that risk must be named at prioritisation time.

*Why:* Equity for PPG is not optional post-hoc reporting; it decides whether the task is fit to prioritise.

*Example:* SpO₂ or pulse-rate support with pre-specified stratum evaluation — not pooled accuracy alone.

---

## TP-PPG-3 · Prefer tasks bound to an actionable threshold or workflow

PPG tasks should state the clinical or consumer-care action they inform (screening referral, alarm, titration support), not only continuous metric estimation.

*Why:* Beat-level or window-level error without an action is easy to score and hard to use.

---

# How these will be used

1. All experts rate **shared core** TP-1…TP-7.  
2. Modality experts also rate **TP-ECG-*** / **TP-EEG-*** / **TP-PPG-***.  
3. Nominated clinical tasks are scored against core + relevant modality extensions.  
4. Output: a **prioritised task portfolio** for ECG, EEG, and PPG first.

**Version:** 0.2 · Draft · BioSIGNAL-AI consortium  
**Phase-1 modalities:** ECG · EEG · PPG
