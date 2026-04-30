---
name: task-management
description: 'Manage sequential engineering tasks in .github/tasks/current.yaml with completed history in .github/tasks/archive/. Use for decomposition, assignment, status transitions, and handoff control in this project.'
argument-hint: 'Describe the request, current queue state, and desired next owner'
user-invocable: true
---

# Task Management Skill

## When to Use
- A new user request must be broken into executable tasks.
- A new requirement needs a new `.github/tasks/current.yaml` file.
- A task status needs to move across `todo`, `in_progress`, `blocked`, `done`.
- Ownership must be transferred between customer, project manager, and specialists.
- The project manager needs to enforce single-thread sequential execution.

## Procedure
1. Create `.github/tasks/current.yaml` for each new requirement using `skills/task-management/current.template.yaml` as the baseline structure.
2. Populate root keys: `request_id`, `requirement_summary`, `created_at`, `updated_at`, `completion_condition_for_requirement`, and `tasks`.
3. Convert the incoming request into small tasks with clear task-level `done_criteria`.
4. For each task, set: `task_id`, `title`, `owner`, `status`, `handoff_to`, `branch_name`, `inputs`, `done_criteria`, and `blockers`.
5. Ensure only one task is `in_progress`.
6. Before moving any task to `in_progress`, create or switch to the task branch from `branch_name` using:
   - `git switch <branch_name> || git switch -c <branch_name>`
   - `git branch --show-current` and verify it matches `branch_name`
7. If branch bootstrap fails or active branch does not match `branch_name`, keep the task out of `in_progress` and set `status: blocked` with concrete blocker details.
8. Assign each task to one owner from:
   - `customer`
   - `project-manager`
   - `design-reviewer`
   - `backend-developer`
   - `frontend-developer`
   - `ml-engineer`
   - `infra-qa`
   - `code-reviewer`
   - `documentation`
   - `performance`
9. Set `handoff_to` for the next owner after completion.
10. Write concise blocker notes when status is `blocked`.
11. Keep tasks in strict sequence and avoid parallel execution unless explicitly requested.
12. Do not define a root-level `done_criteria`; use `completion_condition_for_requirement` for requirement completion.
13. Before marking a task `done`, merge the task branch into `main`:
    - `git switch main && git pull`
    - `git merge --no-ff <branch_name> -m "merge: <task_id> <title>"`
    - If merge conflicts occur, set `status: blocked` and record conflict details in `blockers`.
14. When all tasks are `done` and requirement completion condition is met, move `current.yaml` to `.github/tasks/archive/`.
15. For a new requirement, create a new `current.yaml`.

## Template
- Use `skills/task-management/current.template.yaml` as the canonical starter template.

## Output Contract
Return a concise report with:
- queue changes
- active task id
- active branch
- next owner
- blockers (if any)

## Guardrails
- Do not edit files outside `.github/tasks/` while using this skill.
- Do not mark a task `done` without matching `done_criteria`.
- Do not keep multiple `in_progress` tasks.
- Do not omit `branch_name` for task entries.
- Do not move a task to `in_progress` until active branch matches the task `branch_name`.
- Do not mark a task `done` until the task branch has been merged into `main`.
