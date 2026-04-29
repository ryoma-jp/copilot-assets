---
name: code-review
description: 'Baseline pull request/code change review skill. Use for correctness, regression risk, security, maintainability, tests, and release safety.'
argument-hint: 'Provide changed files/PR scope, expected behavior, and critical risk areas to prioritize'
user-invocable: true
---

# Code Review Skill

## When to Use
- You need a structured review of code changes before merge.
- You need risk-based findings prioritized by severity.
- You need to validate tests and release safety for a patch.

## Review Procedure
1. Understand intent and expected behavior from change context.
2. Inspect diffs for logic and regression risks.
3. Verify core quality areas:
   - functional correctness
   - error handling and edge cases
   - security and data safety
   - performance impact
   - readability and maintainability
4. Validate test coverage:
   - unit/integration/e2e relevance
   - missing tests for critical paths
5. Check operational and release impact:
   - migrations/config/env assumptions
   - backward compatibility concerns
6. Produce findings ordered by severity with concrete evidence.

## Baseline Review Criteria
- Behavior matches stated requirements and contracts.
- No obvious race conditions or state inconsistency risks.
- Input validation and auth/authz boundaries are preserved.
- Sensitive data is not exposed in logs/errors.
- Complexity remains understandable; abstractions are justified.
- Tests cover positive, negative, and boundary scenarios.
- Changes are scoped; unrelated modifications are minimized.

## Severity Model
- `high`: likely production incident, security flaw, or data corruption risk
- `medium`: significant bug/regression risk or maintainability hazard
- `low`: minor issue, clarity improvement, or non-blocking suggestion

## Guardrails
- Prioritize actionable defects over style-only comments.
- Avoid speculative rewrites unless risk justifies them.
- If no findings exist, state that explicitly and mention residual risks.

## Output Contract
Return a concise report with:
- findings (ordered by severity) with file/line evidence
- test and validation gaps
- overall merge readiness (`ready`, `ready with fixes`, `not ready`)
