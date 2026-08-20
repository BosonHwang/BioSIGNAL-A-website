# Principle ratings — collection format

Participants rate principles on the public site and download a JSON file (`biosignal-ai-ratings-*.json`). Collect those files by email (`hello@biosignal-ai.org`) until a server intake (REDCap / Formspree / API) is wired.

## Schema `biosignal-ai-principle-ratings/v1`

```json
{
  "schema": "biosignal-ai-principle-ratings/v1",
  "exported_at": "ISO-8601",
  "version": "0.2",
  "participant": {
    "name": "",
    "email": "",
    "affiliation": "",
    "role": "",
    "modalities": ["ecg", "eeg"]
  },
  "expected_principle_ids": ["TP-1", "…"],
  "completed_count": 0,
  "ratings": {
    "TP-1": {
      "importance": 8,
      "clarity": 7,
      "feasibility": 6,
      "applicability": 8,
      "note": ""
    }
  }
}
```

- Scales are integers **1–9** (Delphi-style).
- Core principles are always in scope; modality blocks only if listed in `participant.modalities`.
- Aggregate offline (e.g. median / IQR per dimension) for Round 1 feedback.
