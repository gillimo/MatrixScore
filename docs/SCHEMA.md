## Rating Engine Schema (Draft)

Top-level JSON structure
```
{
  "interaction_matrix": {
    "capability_a": { "issue_1": 2.0, "issue_2": 1.0 },
    "capability_b": { "issue_1": 0.5, "issue_2": 0.0 }
  },
  "items": [
    {
      "name": "item_1",
      "issues": ["issue_1"],
      "capabilities": ["capability_a"],
      "strength": 0.9,
      "category": "group_a",
      "metadata": { "notes": "optional" }
    }
  ],
  "portfolio": ["item_1", "item_2"],
  "weights": {
    "exposure_gap": 8.0,
    "overlap": 8.0,
    "concentration_overlap": 10.0
  },
  "categories": {
    "group_a": ["item_1", "item_3"]
  }
}
```

Field notes
- `interaction_matrix`: a square matrix of type-to-issue multipliers.
  - Use the same type names for issue tags and capability tags.
  - `> 1.0` means it amplifies/targets the issue.
  - `< 1.0` means it mitigates the issue.
  - `0.0` means it neutralizes the issue.
- `items`: the candidates being evaluated.
- `portfolio`: the selected set to score (by name).
- `weights`: optional overrides for scoring penalties/bonuses.
- `categories`: optional grouping metadata for balance penalties.
