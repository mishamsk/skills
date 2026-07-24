# Agent skills

A small collection of agent skills for Codex, Claude Code, and Pi.

## Install

Install every skill globally for Codex, Claude Code, and Pi:

```sh
npx skills add mishamsk/skills --skill '*' --agent codex --agent claude-code --agent pi --global --yes
```

Omit `--skill '*'`, `--global`, or `--yes` for interactive selection or project-local installation.

## Claude Code plugin

Alternatively, install the whole repository as one Claude Code plugin:

```sh
claude plugin marketplace add mishamsk/skills
claude plugin install skills@mishamsk-skills
```
