---
name: rebase
description: "Rebase the current branch onto the latest trunk ref, resolve conflicts deliberately, and run repository verification."
---

# Rebase

## Goal

Rebase the current feature branch onto the latest available trunk ref and leave a verified local branch with any pre-existing work restored.

Success means:

- The repository's trunk branch is identified from repository guidance or remote configuration; it may be `main`, `master`, `trunk`, or another name.
- The base is the later of the local and remote-tracking trunk refs when one contains the other. Divergence is reported instead of guessed through.
- New trunk behavior remains intact and the feature branch's still-applicable intent is replayed on top.
- Verification required by repository-local guidance passes for the combined scope of trunk's incoming changes and the feature branch.
- Rebase-caused fixes are committed separately, any temporary stash is restored, pre-existing work is preserved, and nothing is pushed.

## Constraints

- Read `AGENTS.md` when present; otherwise read `CLAUDE.md`. Also read required project docs.
- Preserve uncommitted user work. If the worktree is dirty, record its state and stash tracked and untracked changes with a descriptive message before rebasing, then restore them after the rebase and verification.
- Do not rebase while on the trunk branch.
- During conflicts, remember that `--ours` is trunk/upstream and `--theirs` is the branch commit being replayed.
- Resolve each conflict from current trunk behavior plus the branch's applicable intent. Do not use blanket side selection.
- Do not use `git reset --hard`, skip or delete commits, abort the rebase, or force-push unless the user explicitly authorizes it or the repository is otherwise unrecoverable.

## Workflow

1. Inspect the worktree, current branch, remotes, remote default branch, repository guidance, and available trunk refs.
2. If the worktree is dirty, record `git status` and create a descriptive stash including untracked files.
3. Fetch current remote refs. Compare the local and remote-tracking trunk refs with ancestry checks and choose the later ref. Stop if they have diverged or no trunk can be identified.
4. Run `git rebase <trunk-ref>`.
5. If conflicts occur, inspect both sides and relevant history, preserve compatible changes, stage only resolved files, and continue the rebase.
6. Find and follow repository-local verification guidance in `AGENTS.md` or, when it is absent, `CLAUDE.md`, plus contributing docs and standard repository scripts. Select checks for the combined change scope from trunk and the feature branch. Fix failures caused by the rebase and commit those fixes as follow-up commits; do not silently fold them into replayed commits unless the user asks.
7. Restore any temporary stash. If restoration conflicts, preserve the stash and report the exact state rather than dropping or overwriting work.
8. Report the trunk name and chosen base, new branch tip, verification results, conflicts resolved, restored worktree state, and follow-up commits.

## Stop Rules

- Stop when pre-existing work, a conflict's intended result, or a verification failure cannot be resolved from repository evidence without changing scope.
- Report the concrete blocker and current rebase state instead of guessing or discarding work.
