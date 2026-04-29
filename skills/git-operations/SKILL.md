---
name: git-operations
description: 'Standard Git workflow support for day-to-day software development. Use for status checks, branch workflow, commits, sync with remote, conflict handling, rollback options, and release-safe history practices.'
argument-hint: 'Describe current branch/status, desired git outcome, and any safety constraints (no-force-push, no-history-rewrite, etc.)'
user-invocable: true
---

# Git Operations Skill

## When to Use
- You need safe, routine Git actions in active development.
- You need to prepare clean commits from local changes.
- You need to sync local work with remote branches.
- You need to resolve merge/rebase conflicts with minimal risk.
- You need rollback guidance without destructive operations.

## Baseline Workflow
1. Inspect state with `git status`, current branch, and diff summary.
2. Verify branch strategy:
   - feature work on task branch tracked by `branch_name` in `.github/tasks/current.yaml`
   - avoid direct commit to protected branches
3. Stage intentionally:
   - include only relevant hunks/files
   - avoid accidental generated/secrets files
4. Create atomic commits:
   - one logical change per commit
   - clear message (what + why)
5. Synchronize:
   - fetch latest remote state
   - rebase or merge according to repository policy
6. Validate after history operations:
   - rerun status and key tests
   - ensure branch is push-ready
7. Push safely:
   - avoid force push unless explicitly approved and policy-compliant
   - push each task branch after creation and after meaningful updates

## Task-Driven Branch Policy
1. Read active task `branch_name` from `.github/tasks/current.yaml` before starting implementation.
2. Create or switch to the task branch and keep commits scoped to that task.
3. Complete the task, merge to `main` according to repository policy, and update task status.
4. After all requirement tasks are merged, perform final `main` sync check and push.

## Common Operations Coverage
- Status triage: staged/unstaged/untracked review
- Branch lifecycle: create/switch/rename/delete local branches
- Commit hygiene: split, amend (only when explicitly requested), and message quality checks
- Integration: fetch/pull/rebase/merge with conflict notes
- Recovery: `git restore`, `git revert`, reflog-based recovery guidance
- Release prep: tag creation checks and changelog alignment

## Guardrails
- Do not run destructive history commands without explicit user approval.
- Do not rewrite shared branch history by default.
- Do not include unrelated files in commits.
- Prefer non-interactive commands for reproducibility.
- Preserve existing uncommitted user work unless asked otherwise.

## Output Contract
Return a concise report with:
- current git state summary
- operations performed (or recommended command sequence)
- branch/commit outcomes
- risks and follow-up checks
