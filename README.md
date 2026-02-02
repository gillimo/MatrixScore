# MatrixScore

Mission Learning Statement
- Mission: Build a reusable scoring and rating engine for structured data.
- Learning focus: metrics design, scoring calibration, and evaluation workflows.
- Project start date: 2026-01-20 (inferred from earliest git commit)

Domain-agnostic rating engine for matrix-driven coverage, gaps, and overlap risk.

## Features

- Deterministic scoring from interaction matrices and weighted issues
- Portfolio evaluation with exposure maps and deltas
- CLI for quick summaries and comparisons
- Documented scoring formulas in `METRICS.md`

## Installation

### Requirements

- Python 3.8+

### Setup

```bash
pip install -e .
```

## Quick Start

```bash
python matrixscore_cli.py path/to/config.json
```

## Usage

- Provide a JSON config that defines items, interactions, weights, and optional portfolio.
- The CLI prints overall score, component scores, and an exposure map.

## Architecture

```
Config JSON
   |
   v
Schema Loader (matrixscore.core.schema)
   |
   v
Scoring Engine (matrixscore.core.scoring)
   |
   +--> Coverage Map
   +--> Component Scores
   v
CLI Summary Output
```

## Project Structure

```
matrixscore_cli.py     # CLI entry point
matrixscore/           # Core library
METRICS.md             # Scoring formulas
tests/                 # Test coverage
```

## Building

No build step required. Run directly with Python.

## Contributing

See `CONTRIBUTING.md` for guidelines and `CODE_OF_CONDUCT.md` for expected behavior.

## License

MIT License - see [LICENSE](LICENSE) for details.
