---
name: mise
description: "Use mise to install, pin, and run project development tools, including Go, Node and its ecosystem, Python, uv, Rust, and Ruby."
---

# mise Tool Management

Use `mise` as the source of truth for project development-tool versions. Read existing `mise.toml`, `.mise.toml`, and `.tool-versions` files before changing tool configuration.

## Rules

- Add or update project tools with `mise use <tool>@<version>` so the version is recorded in repository configuration.
- Install versions already declared by the project with `mise install`.
- Run one-off commands under a selected version with `mise x <tool>@<version> -- <command>`.
- Manage Go, Node, npm, pnpm, Yarn, Bun, Node-based CLIs, Python, Rust, and Ruby through mise.
- Never use Corepack. Manage pnpm and Yarn versions directly with mise.
- Do not use `npm install --global` for Node-based CLIs; declare them with `mise use npm:<package>@<version>`.
- Use an already configured global `uv` when it satisfies the project. Otherwise declare a project-local version with `mise use uv@<version>`.
- Keep package dependencies in their native project manifests; mise manages the package-manager and runtime versions, not application dependencies.

## Examples

```bash
mise use go@1.25 node@24 pnpm@10 python@3.13 rust@stable ruby@3.4
mise use npm:prettier@3
mise use uv@latest
mise install

mise x node@22 -- node --version
mise x python@3.11 -- uv run --python python script.py
```
