## Function Map

Public API (from `matrixscore`)
- `compute_coverage(items, interaction_matrix, issues=None)`
  - Returns per-issue exposure totals: weak/resist/immune/neutral/size.
- `resilience_score(coverage, weights=None)`
  - Returns a 0..100 resilience score from exposure gaps and overlap.
- `resilience_delta(base_coverage, sim_coverage, weights=None, bonus_weights=None)`
  - Returns (delta_with_bonus, sim_score, base_score).
- `concentration_score(coverage, weights=None)`
  - Returns a 0..100 concentration/overlap score.
- `coverage_effectiveness(items, coverage, interaction_matrix, issues=None, weights=None)`
  - Returns a 0..100 coverage effectiveness score for exposed issues.
- `overall_score(best_resilience_delta, best_coverage_headroom, concentration, weights=None, resilience=None)`
  - Returns a 0..100 overall health score.
- `predict_overall(portfolio, interaction_matrix, issues=None, candidates=None, weights=None)`
  - Returns (overall, components) including coverage map and headroom.

Core modules
- `matrixscore/core/schema.py`
  - `load_config(data)` validates schema input and returns a `RatingConfig`.
- `matrixscore/core/cache.py`
  - `cache_item(name, context=None, loader=None)`
  - `portfolio_infos_from_cache(portfolio, context=None, loader=None)`
- `matrixscore/core/api.py`
  - `register_item_loader(fn)` / `register_context_loader(fn)`
  - `load_item(name)` / `load_context(key)`

CLI
- `python -m matrixscore.matrixscore_cli path/to/config.json`
  - Loads config, prints scores, prints exposure map.
