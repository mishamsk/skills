---
name: uv
description: "Use uv for Python projects, dependencies, and scripts instead of pip, direct python environment management, or hand-built virtualenvs."
---

## Quick Reference

```bash
uv run script.py                   # Run a script
uv run --with requests script.py   # Run with ad-hoc dependency
uv add requests                    # Add dependency to project
uv init --script foo.py            # Create script with inline metadata
```

## Inline Script Dependencies

```python
# /// script
# requires-python = ">=3.12"
# dependencies = ["requests"]
# ///
```

See [scripts.md](scripts.md) for full details on running scripts, locking, and reproducibility.

## Bootstrap Projects

Bootstrap new command-line applications with `uv init`; do not hand-write the initial `pyproject.toml`. A CLI is a packaged application, so use `--app --package` to create its `src/` layout and command entry point:

```bash
uv init --app --package my-cli
uv init --app --package .
mise x python@3.11 -- uv init --app --package --python python my-cli
```

Keep the generated `src/` layout, command entry point, and build-system constraint rather than replacing them with hand-written scaffolding or a copied `uv_build` version.
