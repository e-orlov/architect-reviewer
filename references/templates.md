# Reusable templates

## Contents

1. State Capsule
2. Architecture/Task Packet
3. Gate Record
4. Review Verdict
5. Risk Record
6. Release Identity Manifest
7. Errors encountered and corrections
8. Canonical Document Registry
9. Diagnostic Side-Effect Ledger
10. Handoff
11. V-model Trace Matrix
12. AI Complexity Decision Record

Use only fields justified by the task. Preserve exact identities and raw evidence references. Delete instructional placeholders before delivery.

## 1. State Capsule

```markdown
# State Capsule

- Objective:
- Task type / assurance: <type> / A0–A4
- Current typed state:
- Canonical instructions/decision:
- Target identity: <repo/branch/SHA/build/config/schema/runtime as applicable>
- Current executor/process state:
- Completed gates: <gate, artifact, UTC, verdict>
- Freshness/invalidation notes:
- Facts:
- Inferences:
- Decisions:
- Unknowns:
- Active risks / STOP conditions:
- Authority granted:
- Authority still required:
- Next single action:
```

## 2. Architecture/Task Packet

```markdown
# Architecture / Task Packet

## Objective

## Non-goals

## Current state and evidence

## Actors, data, trust boundaries, and real execution path

## Invariants and prohibited outcomes

## Proposed owning boundary and minimal design

## Alternatives and tradeoffs

## Failure modes, containment, recovery, and rollback

## Observability and acceptance criteria

| ID | Requirement | Falsifiable criterion | Verification level | Evidence |
|---|---|---|---|---|

## Task slices

| Slice | Primary invariant | Scope | Required gates | Dependencies |
|---|---|---|---|---|

## Risks and decisions reserved for owner

## Explicitly forbidden actions
```

## 3. Gate Record

```markdown
# Gate <ID>: <name>

- Claim:
- Invariant:
- Artifact identity:
- Production symbol/path:
- Scope/inventory:
- Expected count:
- Oracle:
- Falsifiability/negative control:
- Environment/config identity:
- Command/probe:
- Collected result:
- UTC timestamp / TTL:
- Evidence dependencies:
- Owner:
- Verdict: PASS | FAIL | BLOCKED | UNKNOWN
- Impact on lifecycle state:
- Next authorized action:
```

## 4. Review Verdict

```markdown
# Review Verdict

- Review type: SELF-REVIEW | INDEPENDENT REVIEW
- Scope and exact artifact identity:
- Task type / assurance:
- Evidence reviewed:
- Untested or unavailable surfaces:

## Findings

### <Severity>: <finding title>

- Location/scope:
- Violated invariant:
- Evidence:
- Consequence:
- Required correction:
- Evidence invalidated:

## Assumptions and unknowns

## Residual risk

## Verdict

<TYPED STATE or CERTIFIED | NOT CERTIFIED | UNKNOWN>

## Next authority/action

## Errors encountered and corrections

None
```

If findings are absent, write `No findings within the reviewed scope` and still preserve unknowns and residual risk.

## 5. Risk Record

```markdown
# Risk <ID>: <scenario>

- Trigger:
- Affected asset/users/process:
- Inherent likelihood / rationale:
- Inherent impact / rationale:
- Preventive controls:
- Detective controls:
- Corrective controls:
- Control evidence / uncertainty:
- Residual likelihood / rationale:
- Residual impact / rationale:
- Early-warning indicators:
- Mitigation:
- Contingency:
- Treatment: AVOID | MITIGATE | TRANSFER | ACCEPT
- Owner:
- Review date/status:
- Residual-risk acceptance authority:
```

## 6. Release Identity Manifest

```markdown
# Release Identity

- Repository / target branch:
- Source commit:
- Build/artifact/image digest:
- Dependency/lock identity:
- Configuration identity/hash:
- Schema/migration head:
- Feature-flag state:
- Target environment/topology:
- Rollout/canary cohort:
- Required checks and evaluated SHA:
- Monitoring window/signals:
- Rollback target and procedure:
- Deployment record and UTC:
- Real-world acceptance record and UTC:
- Terminal state:
```

## 7. Errors encountered and corrections

```markdown
## Errors encountered and corrections

### <error title>

- Command/step:
- Symptom:
- Classified cause:
- Correction:
- Rerun/result:
- Impact on earlier evidence:
- Residual risk:
```

If no errors occurred, use:

```markdown
## Errors encountered and corrections

None
```

## 8. Canonical Document Registry

```text
Document ID:
Scope:
Owner:
Status: ACTIVE | SUPERSEDED | RETIRED
Effective date:
Supersedes:
Successor:
Last verified (UTC):
Conflicts/unknowns:
```

## 9. Diagnostic Side-Effect Ledger

```text
Action/probe:
Target identity:
Expected reads:
Expected writes/effects:
Load/cost/notification budget:
Temporary artifacts:
Cleanup or reconciliation:
Observed residue:
Residue verdict: ACCEPTED | REMOVED | UNKNOWN
Evidence and UTC time:
```

## 10. Handoff

```markdown
# Handoff

- Objective and current typed state:
- Exact target and artifact identities:
- What changed / what did not change:
- Completed gates with evidence locations and UTC:
- Known failures and corrections:
- Open findings, unknowns, and residual risks:
- Shared resources and current owners/leases:
- Current executor/process status:
- Required next action:
- Required authority before that action:
- Actions that must not be repeated:
- Actions that remain forbidden:
```

## 11. V-model Trace Matrix

```markdown
# V-model Trace Matrix

| ID | Need / rationale | Requirement or control | Risk / prohibited outcome | Design owner | Implementation slice | Verification level | Falsifiable criterion / oracle | Scope / expected count | Environment identity | Evidence / UTC | Invalidation dependencies | Owner | State |
|---|---|---|---|---|---|---|---|---|---|---|---|---|---|
| REQ-001 |  |  |  |  |  | UNIT / COMPONENT / CONTRACT / INTEGRATION / SYSTEM / ACCEPTANCE |  |  |  |  |  |  | PROPOSED / IMPLEMENTED_UNVERIFIED / VERIFIED_* / BLOCKED / UNKNOWN |

## Orphan check

- Requirements without implementation:
- Requirements without matching proof:
- Implementation without requirement, risk control, or enabling-work justification:
- Tests without a traced claim:
- Evidence at the wrong V level:
- Stale or identity-mismatched evidence:
```

## 12. AI Complexity Decision Record

```markdown
# AI Complexity Decision Record

- Decision scope / assurance:
- User or business need:
- Non-goals and prohibited outcomes:
- Accountable decision/risk owner:

## Baseline Gate

- Simplest credible comparator:
- Why this comparator is credible:
- Baseline artifact/config/environment identity:
- Evaluation-set identity, provenance, scope, and limitations:
- Primary metric and project-defined acceptance threshold:
- Safety/quality/cost/latency/operational guardrails:
- Raw result and uncertainty:
- Named unmet gap:
- Gate verdict: PASS | FAIL | BLOCKED | UNKNOWN
- Decision: STOP | READY_FOR_EXPERIMENT

## Experiment Gate

- Predeclared hypothesis:
- Baseline arm identity:
- Candidate arm identity:
- Primary changed mechanism:
- Controlled factors:
- Disclosed additional differences:
- Model/prompt/tool/retrieval/data/evaluator/runtime identities:
- Split, deduplication, leakage, and contamination controls:
- Practical-equivalence margin or qualitative decision boundary, and decision rule:
- Repetition/uncertainty treatment:
- Falsifiability / known-bad control:
- Raw result, slices, regressions, and guardrails:
- Attribution limits:
- Gate verdict: PASS | FAIL | BLOCKED | UNKNOWN

## Complexity-Promotion Gate

- Proposed added complexity:
- Lower-complexity alternatives considered:
- Measured benefit and practical significance:
- Lifecycle complexity/cost inventory:
- New failure, security, privacy, data, vendor, and compliance risks:
- Observability and owner:
- Fallback / rollback / decommission path:
- Target-topology and staged-release evidence:
- Residual risk and acceptance authority:
- Gate verdict: PASS | FAIL | BLOCKED | UNKNOWN
- Decision: STOP | EXPERIMENT_ONLY | APPROVED_LIMITED | PROMOTED | BLOCKED | UNKNOWN
- Scope and expiry/invalidation dependencies:
```
