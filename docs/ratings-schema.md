# Principle ratings — collection format

Participants rate principles on the public site and download a JSON file (`biosignal-ai-ratings-*.json`). Collect those files by email (`hello@biosignal-ai.org`) until a server intake (REDCap / Formspree / API) is wired.

## Schema `biosignal-ai-principle-ratings/v3`

Dimensions: **importance**, **clarity**, **feasibility** (1–5, labelled).

```json
{
  "schema": "biosignal-ai-principle-ratings/v3",
  "scale": {
    "min": 1,
    "max": 5,
    "dimensions": ["importance", "clarity", "feasibility"],
    "labels": {
      "importance": {
        "1": "Not important",
        "2": "Slightly important",
        "3": "Moderately important",
        "4": "Important",
        "5": "Essential"
      },
      "clarity": {
        "1": "Unclear",
        "2": "Mostly unclear",
        "3": "Adequate",
        "4": "Clear",
        "5": "Very clear"
      },
      "feasibility": {
        "1": "Not feasible",
        "2": "Difficult",
        "3": "Feasible with effort",
        "4": "Feasible",
        "5": "Readily feasible"
      }
    }
  },
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
      "importance": 5,
      "clarity": 4,
      "feasibility": 3,
      "note": ""
    }
  }
}
```

- Core principles are always in scope; modality blocks only if listed in `participant.modalities`.
- Aggregate offline (e.g. median / IQR per dimension) for Round 1 feedback.
