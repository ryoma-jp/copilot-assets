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
6. Assign each task to one owner from:
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
7. Set `handoff_to` for the next owner after completion.
8. Write concise blocker notes when status is `blocked`.
9. Keep tasks in strict sequence and avoid parallel execution unless explicitly requested.
10. Do not define a root-level `done_criteria`; use `completion_condition_for_requirement` for requirement completion.
11. When all tasks are `done` and requirement completion condition is met, move `current.yaml` to `.github/tasks/archive/`.
12. For a new requirement, create a new `current.yaml`.

## Template
- Use `skills/task-management/current.template.yaml` as the canonical starter template.

## Output Contract
Return a concise report with:
- queue changes
- active task id
- next owner
- blockers (if any)

## Guardrails
- Do not edit files outside `.github/tasks/` while using this skill.
- Do not mark a task `done` without matching `done_criteria`.
- Do not keep multiple `in_progress` tasks.
- Do not omit `branch_name` for task entries.
