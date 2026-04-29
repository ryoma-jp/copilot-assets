---
name: design-review
description: 'Baseline software design review skill. Use for architecture, module boundaries, data flow, API contracts, security/performance/scalability trade-offs, and operational readiness.'
argument-hint: 'Provide design scope, constraints, target quality attributes, and artifacts (docs/diagrams/interfaces)'
user-invocable: true
---

# Design Review Skill

## When to Use
- A new feature or subsystem design is proposed.
- Existing architecture is being changed significantly.
- You need risk-focused review before implementation starts.
- You need a structured go/no-go quality gate for design.

## Review Procedure
1. Clarify scope, assumptions, and non-goals.
2. Identify architecture context:
   - upstream/downstream dependencies
   - domain boundaries and ownership
3. Evaluate quality attributes:
   - correctness and consistency
   - reliability and failure handling
   - security and privacy
   - performance and scalability
   - operability and observability
4. Check interface and data design:
   - API contracts and versioning strategy
   - schema evolution and migration compatibility
   - idempotency and concurrency behavior
5. Assess delivery readiness:
   - rollout/rollback strategy
   - test strategy and acceptance criteria
   - documentation and runbook requirements
6. Classify findings by severity and required action.

## Baseline Review Criteria
- Clear problem statement and measurable success criteria
- Explicit trade-off decisions with alternatives considered
- Defined failure modes and mitigation paths
- Backward compatibility plan where needed
- Security controls mapped to threat surface
- Capacity/performance assumptions validated or testable
- Operational ownership and alerts/logging defined

## Guardrails
- Focus on design-level concerns, not coding style details.
- Do not block on low-impact preferences when risk is low.
- Distinguish confirmed issues from assumptions clearly.
- Mark unknowns that require experiments or spikes.

## Output Contract
Return a concise report with:
- design summary reviewed
- findings by severity (`high`, `medium`, `low`)
- open questions and assumptions
- decision recommendation (`approve`, `approve with changes`, `rework`)
