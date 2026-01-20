# MatrixScore

Why this exists
This engine provides a consistent, auditable way to rate a portfolio against
issue coverage and capability gaps. It is designed to be fast, configurable, and
domain-agnostic, so teams can reuse the same scoring logic across different
problem spaces without rewriting the core.

Goal
Build a domain-agnostic scoring engine that rates a set of items against a set of
issues/capabilities, and highlights exposure gaps, overlap risk, and coverage
strength. This project preserves and refactors a proven scoring core into a
reusable Python library.

What the final library will look like
- A small Python package with a stable API for scoring a collection of items.
- Config-driven weights/penalties (no hardcoded domain assumptions).
- A generic schema for:
  - interaction_matrix (how capabilities mitigate issues)
  - items (their issues/capabilities + optional stats)
  - portfolio (the set to score)
- Core outputs:
  - exposure map (per-issue weak/resist/immune/neutral totals)
  - resilience score (exposure gaps + overlap penalties)
  - overlap/concentration risk score
  - coverage effectiveness score
  - overall health score + headroom (best possible improvement)
- Optional adapters for domain data (kept out of core).

Planned deliverables
- `matrixscore/core/scoring.py` refactored to use the generic schema
- `matrixscore/matrixscore_cli.py` updated to load a JSON config + dataset
- Example dataset(s): risk controls, capability matrix
- Minimal tests and usage examples

Status
Core refactor complete; packaging, tests, and release docs in progress.

How to use
- Install: `pip install matrixscore`
- CLI: `matrixscore path/to/config.json`
- Python: `from matrixscore import predict_overall`

Quickstart (minimal config)
```json
{
  "interaction_matrix": {
    "availability": {"availability": 2.0, "integrity": 1.0},
    "integrity": {"availability": 1.0, "integrity": 2.0}
  },
  "items": [
    {"name": "control_a", "issues": ["availability"], "capabilities": ["availability"]},
    {"name": "control_b", "issues": ["integrity"], "capabilities": ["integrity"]}
  ],
  "portfolio": ["control_a", "control_b"]
}
```

Examples
- `data/examples/risk_controls.json`
- `data/examples/capability_matrix.json`
