# PPG — modality-specific candidate principles

**Status:** Draft v0.2  
**Extends:** shared core ([task prioritisation](./candidate-principles-task-prioritisation.md) · [benchmark design](./candidate-principles-benchmarking.md))  
**Who rates:** PPG / wearable / pulse-oximetry clinicians and engineers, optical sensing researchers

These items do **not** replace the shared core. PPG experts rate core + this file.

---

## A · Task prioritisation (PPG)

### TP-PPG-1 · Wearable vs clinical PPG are different task families

Priority items must separate optical wearable ambulatory use from clinical fingertip / bedside PPG — including motion and wear-time assumptions.

*Why:* Corpus convenience often collapses these regimes; clinical decisions do not.

---

### TP-PPG-2 · Prefer tasks where perfusion and skin-tone strata matter to the claim

If the intended decision could fail systematically by perfusion or skin pigmentation, that risk must be named at prioritisation time.

*Why:* Equity for PPG is not optional post-hoc reporting; it decides whether the task is fit to prioritise.

*Example:* SpO₂ or pulse-rate support with pre-specified stratum evaluation — not pooled accuracy alone.

---

### TP-PPG-3 · Prefer tasks bound to an actionable threshold or workflow

PPG tasks should state the clinical or consumer-care action they inform (screening referral, alarm, titration support), not only continuous metric estimation.

*Why:* Beat-level or window-level error without an action is easy to score and hard to use.

---

## B · Benchmark design (PPG)

### BM-PPG-1 · Disclose optical hardware, site, and motion / wear-time gates

Benchmarks must report sensor type, wear location, sampling, motion filtering, and wear-time / quality thresholds — and whether they apply at inference.

*Why:* PPG “quality” gates often define the task more than the model does.

---

### BM-PPG-2 · Require stratum reporting for skin tone and perfusion when material

For use claims affected by optical sensing biases, pre-specify skin-tone and/or perfusion strata and make stratum metrics part of the headline report.

*Why:* Pooled SpO₂ or heart-rate error can hide unsafe subgroup failure.

---

### BM-PPG-3 · Test motion and ambulatory shift as first-class conditions

Ambulatory or wearable claims must include motion-rich evaluation as primary evidence, not a footnote.

*Why:* Resting fingertip PPG is a different measurement problem from daily-wear optical sensing.

---

### BM-PPG-4 · Tie metrics to the decision threshold of the use claim

Report performance at the operating point implied by the clinical or screening action — not only continuous estimation error.

*Why:* RMSE without an action threshold does not validate a workflow claim.

---

## Rating IDs (site)

| ID | Family |
|----|--------|
| TP-PPG-1 … TP-PPG-3 | Task prioritisation |
| BM-PPG-1 … BM-PPG-4 | Benchmark design |
