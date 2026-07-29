---
name: uv
description: "Use uv for Python projects, dependencies, and scripts instead of pip, direct python environment management, or hand-built virtualenvs."
---

## Quick Reference

```bash
uv run script.py                   # Run a script
uv run --with requests script.py   # Run with ad-hoc dependency
uv run python -                    # Run Python from stdin
uv add requests                    # Add dependency to project
uv init --script foo.py            # Create script with inline metadata
```

## Inline Python

Use uv's Python discovery and project environment for inline Python instead of invoking `python3` directly:

```bash
uv run python - <<'PY'
print("Hello from inline Python")
PY
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

Assume uv 0.12 or newer. Bootstrap packaged applications with plain `uv init`; it already creates the `uv_build` build system, `src/` layout, and command entry point. Do not hand-write the initial `pyproject.toml`:

```bash
uv init my-cli
uv init
mise x python@3.11 -- uv init --python python my-cli
```

Use `uv init --lib` for a library. Use `uv init --no-package` only when you intentionally want a flat, non-importable application without a build system.

Keep the generated layout, entry point, and build-system constraint rather than replacing them with hand-written scaffolding or a copied `uv_build` version.
