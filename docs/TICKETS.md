# Release Tickets (Rating Engine v0)

Scope: complete agnostic refactor and open-source packaging for the first release.

Core refactor
- T1 Remove domain-specific data dependencies; replace with generic data loader interface.
- T2 Replace domain constants with config inputs; default to empty arrays or config values.
- T3 Refactor scoring core to use agnostic schema (issues/capabilities) and remove domain terminology.
- T4 Fix broken imports by removing or replacing non-agnostic dependencies.
- T5 Preserve caching system but generalize keys/fields ("item" cache, lazy enrichment).
- T6 Preserve rating tools (coverage map, resilience, concentration, overall) with agnostic names.

CLI rework
- T7 Rewrite CLI to load JSON config + dataset and output scores with agnostic descriptors.
- T8 Remove GUI launch and payload code.
- T9 Replace domain-specific coverage flow with generic capability coverage flow.

Schema and config
- T10 Define formal schema: interaction_matrix, items, portfolio, weights, categories (optional).
- T11 Parameterize all weights/penalties in config with defaults.

Open-source readiness
- T12 Add pyproject metadata (name, version, description, classifiers).
- T13 Add LICENSE, CONTRIBUTING, CODE_OF_CONDUCT.
- T14 Add minimal tests for coverage map, resilience, concentration, overall.
- T15 Add example datasets (risk controls, capability matrix) and CLI demo.
- T16 Update README + METRICS to match final API names and schema.
- T17 Publish GitHub repo with release tags and basic project metadata.
- T18 Publish to PyPI (build, twine upload, verified README).
- T19 Add conda-forge recipe (or file request) after PyPI release.
- T20 Verify Libraries.io indexing (ensure repo + PyPI metadata are correct).
- T21 Optional: publish to Hugging Face Hub (library card + pip install info).
- T22 Create a publish checklist doc (GitHub, PyPI, conda-forge, Libraries.io, HF Hub).
- T23 Create release documentation (release notes template + versioning policy).
- T24 Create function map doc (index of public APIs, inputs/outputs, and examples).
