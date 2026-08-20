# EEG — modality-specific candidate principles

**Status:** Draft v0.2  
**Extends:** shared core ([task prioritisation](./candidate-principles-task-prioritisation.md) · [benchmark design](./candidate-principles-benchmarking.md))  
**Who rates:** EEG / epilepsy / neurophysiology clinicians, EEG engineers, seizure-detection researchers

These items do **not** replace the shared core. EEG experts rate core + this file.

---

## A · Task prioritisation (EEG)

### TP-EEG-1 · Montage, reference, and channel set define the decision context

A priority task must state the montage / reference / channel assumptions of the clinical workflow it supports.

*Why:* The same “seizure detection” label does not transfer across montages and recording setups.

*Example:* Continuous ICU scalp EEG triage ≠ high-density research montage event labelling.

---

### TP-EEG-2 · Prefer tasks that name the review / escalation decision

Priority EEG tasks should specify who reviews alerts, under what workload, and what escalation the model is meant to support.

*Why:* Event labels without a review-cost model reward sensitivity that clinics cannot absorb.

*Example:* “Reduce missed electrographic seizures without flooding the on-call review queue.”

---

### TP-EEG-3 · Artefact and noise regimes are part of prioritisation, not afterthoughts

Tasks must declare which artefact / noise conditions are in-scope for the care setting (motion, impedance, ICU interference).

*Why:* Clean annotated segments overstate readiness for continuous monitoring.

---

## B · Benchmark design (EEG)

### BM-EEG-1 · Fix and report montage, reference, and preprocessing

Benchmarks must lock montage/reference assumptions and disclose filtering, resampling, and channel selection used for scoring.

*Why:* Montage and reference dependence can dominate apparent model differences.

---

### BM-EEG-2 · Evaluate under clinically realistic artefact regimes

Primary EEG evaluation must include artefact / noise conditions representative of the intended monitoring setting — not only clean annotated clips.

*Why:* Clean segments overstate continuous-monitoring performance.

*Example:* Motion, electrode pop, ICU interference held out or stratified in the headline split.

---

### BM-EEG-3 · Report operating points that respect review workload

Beyond event-level detection metrics, report alert burden / positive predictive behaviour at thresholds relevant to human review.

*Why:* Clinical EEG AI fails in practice when sensitivity is bought with unreadable false-alarm rates.

---

### BM-EEG-4 · Align with federated panel norms where they exist

When federating existing EEG frameworks (e.g. SzCORE / epilepsybenchmarks.com), map BioSIGNAL-AI core requirements onto their task definitions without erasing modality-specific governance.

*Why:* Shared core should compose with specialised communities, not overwrite them.

---

## Rating IDs (site)

| ID | Family |
|----|--------|
| TP-EEG-1 … TP-EEG-3 | Task prioritisation |
| BM-EEG-1 … BM-EEG-4 | Benchmark design |
