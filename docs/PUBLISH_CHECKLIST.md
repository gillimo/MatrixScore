## Publish Checklist

GitHub
- Create repository and push code.
- Add topics: `scoring`, `risk`, `portfolio`, `coverage`.
- Create a release tag (e.g., v0.1.0).

PyPI
- Verify `pyproject.toml` metadata.
- Build: `python -m build`
- Upload: `python -m twine upload dist/*`
- Verify README renders correctly on PyPI.

conda-forge
- Create recipe or open feedstock request.
- Confirm PyPI release is live before submitting.

Libraries.io
- Check that GitHub + PyPI metadata are correct.
- Wait for indexing (usually automatic).

Hugging Face Hub (optional)
- Create repo card with description and install instructions.
- Upload README and link to PyPI.
