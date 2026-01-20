## Metrics (Agnostic Refactor)

This document reframes the scoring formulas into a domain-agnostic model for
evaluating items against issues/capabilities. It will be kept aligned with the
refactored library.

Key terms
- **Issue**: any dimension where items can be weak or strong (risk types, gaps, failure modes).
- **Item**: a candidate in the set (vendor, control, model, feature, person).
- **Coverage map**: per-issue totals of weak/resist/immune/neutral counts.
- **Exposure**: `weak > (resist + immune)`.

Resilience score
- Inputs: coverage map (per issue: weak/resist/immune/neutral).
- Exposure gap total: `sum(max(0, weak - (resist + immune)))`.
- Overlap: `sum(max(0, weak - 1))` for exposed issues only.
- Formula: `resilience = 100 - 8*exposure_gap_total - 8*overlap` (clamped 0..100).

Resilience delta
- Base delta: `resilience(sim) - resilience(base)`.
- Optional bonus for issue closure:
  - `immune_gain*6 + resist_gain*3` for gains against currently exposed issues.
- Use raw delta for headroom calculations; bonus only for candidate ranking.

Concentration risk score
- `overlap = max(0, max_weak - 1)`
- `exposed = count(weak > resist+immune)`
- Score: `100 - 10*overlap - 5*exposed` (clamped 0..100).

Coverage effectiveness score
- Build a capability set from items (capability types, controls, mitigations).
- For each exposed issue:
  - If any capability directly closes it: no penalty.
  - Else if partial/neutral coverage exists: `+6` penalty.
  - Else (cannot cover): `+14` penalty.
- Breadth penalty: `max(0, 2 - len(capabilities)) * 3`.
- Base score: `100 - penalties - breadth_penalty`, clamped 0..100.
- If all exposures are covered, add a capped breadth bonus:
  - `neutral_ratio = neutral_or_better / total_issues`
  - `strong_ratio = strong_coverage / total_issues`
  - `breadth_bonus = min(10, 5*neutral_ratio + 6*strong_ratio)`

Best improvement headroom
- Base gain: `sim_coverage_score - base_coverage_score`.
- Gain factor: `(1 + 1.0*closed_exposure) * (1 + 0.25*len(new_capabilities))`
- Optional item strength factor: `strength_factor = clamp(0.8, 1.3, 0.7 + item_strength/450)`
- Strong-coverage factor: `1.0 + 0.05*min(6, strong_coverage_count)`
- Coverage penalty: `0.85` when neutral reach is near-complete but strong coverage is thin; else `1.0`.
- Ranked gain: `gain * gain_factor * strength_factor * strong_factor * coverage_penalty` (cap 100).

Overall health score
- `delta_penalty = 0.10 * (best_resilience_delta + best_coverage_headroom)`
- `shared_penalty = max(0, 100 - concentration_score) * 0.03`
- `overall = 100 - delta_penalty - shared_penalty` (clamped 0..100)
- Resilience floor: if `resilience < 85`, subtract `(85 - resilience) * 0.4`.
- Optional balance penalty: subtract `0.25*(count-2)` for any category with 3+ items.

Candidate safety list
- Strong coverage: `resist + immune - weak >= 2` from current exposure map.
- Score: `100 - 12*missing_strong - added_exposure_penalty + 15 bonus if no new exposures` (clamped 0..100).
  - `added_exposure_penalty`: per newly added weak issue, based on net margin after adding:
    - `margin >= 2`: `+0`
    - `margin >= 1`: `+3`
    - `margin >= 0`: `+6`
    - `margin < 0`: `+12`
- Coverage bonus: for each newly added weak issue that remains covered (`margin >= 0`), add `immune*6 + resist*3`.
- Inclusion: show candidates that keep all new weaknesses covered or produce a positive resilience delta.
