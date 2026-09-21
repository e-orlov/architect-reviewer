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
13. Result-Acceptance / Evidence-Lineage Record

Use only fields justified by the task. Preserve exact identities and raw evidence references. Delete instructional placeholders before delivery.

## 1. State Capsule

```markdown
# State Capsule

- Objective:
- Task type / assurance: <type> / A0–A4
- Lifecycle state: <exact state from operating-model.md>
- Scoped route/AI decision state(s):
- Review verdict, if any: CERTIFIED | NOT CERTIFIED | UNKNOWN
- Canonical instructions/decision:
- Target identity: <repo/branch/SHA/build/config/schema/runtime as applicable>
- Evidence window: <last independently accepted immutable baseline or NO_PRIOR_ACCEPTED_BASELINE → exact target>
- Forge connector: GITHUB_AUTHENTICATED | NATIVE_AUTHENTICATED | NOT_APPLICABLE | UNAVAILABLE
- Open attempt/anomaly IDs:
- Result-Acceptance Gate: PASS | FAIL | BLOCKED | UNKNOWN | NOT_YET_REQUIRED
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
- Expected count / `N/A` reason:
- Oracle and independence/shared-assumption limits:
- Logical counterexample / target defect:
- Negative-control status: NOT_REQUIRED | REQUIRED | EXECUTED | UNSAFE | UNAVAILABLE
- Negative-control or alternative evidence / limitation:
- Environment/config identity:
- Command/probe:
- Collected result:
- UTC timestamp / TTL:
- Evidence dependencies:
- Owner:
- Gate verdict: PASS | FAIL | BLOCKED | UNKNOWN
- Lifecycle-state impact: <exact lifecycle state or no change>
- Scoped decision impact, if applicable:
- Next authorized action:
```

## 4. Review Verdict

```markdown
# Review Verdict

- Review type: SELF-REVIEW | INDEPENDENT REVIEW
- Scope and exact artifact identity:
- Task type / assurance:
- Last independently accepted immutable baseline, or `NO_PRIOR_ACCEPTED_BASELINE` plus justified start boundary:
- Evidence window and exact final target:
- Forge connector and observed repository/account identity:
- Result-Acceptance Record / gate verdict:
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

- Lifecycle state: DISCOVERED | PROPOSED | PLANNED | IMPLEMENTED_UNVERIFIED | VERIFIED_LOCAL | VERIFIED_INTEGRATION | READY_FOR_MERGE | MERGED_UNRELEASED | RELEASED_UNACCEPTED | ACCEPTED | BLOCKED | UNKNOWN
- Review verdict: CERTIFIED | NOT CERTIFIED | UNKNOWN

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

## Review history

| UTC date | Trigger / scope | Evidence or control change | Reviewer / owner | Residual-risk decision | Next review |
|---|---|---|---|---|---|
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
- Forge connector / observed account and UTC:
- Result-Acceptance Record / gate verdict:
- Monitoring window/signals:
- Rollback target and procedure:
- Deployment record and UTC:
- Real-world acceptance record and UTC:
- Terminal lifecycle state: DISCOVERED | PROPOSED | PLANNED | IMPLEMENTED_UNVERIFIED | VERIFIED_LOCAL | VERIFIED_INTEGRATION | READY_FOR_MERGE | MERGED_UNRELEASED | RELEASED_UNACCEPTED | ACCEPTED | BLOCKED | UNKNOWN
```

## 7. Errors encountered and corrections

```markdown
## Errors encountered and corrections

### <error title>

- Exact target / run / attempt / job / step identity:
- UTC time / environment:
- Observable symptom:
- Expected versus actual scope/count:
- Classification: PRODUCT | TEST | FIXTURE | HARNESS | CONFIGURATION | ENVIRONMENT | INFRASTRUCTURE | EXPECTED_NEGATIVE_CONTROL | UNKNOWN
- Cause / confidence: PROVEN | PROVISIONAL | UNKNOWN
- Correction, or justified reason none was needed:
- Evidence invalidated by the correction:
- Falsifiable causal proof:
- Final result on the exact corrected target:
- Remaining uncertainty / residual risk:
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

- Objective:
- Lifecycle state: <exact state from operating-model.md>
- Scoped route/AI decision state(s):
- Review verdict, if any: CERTIFIED | NOT CERTIFIED | UNKNOWN
- Exact target and artifact identities:
- Evidence window and last accepted immutable baseline:
- Forge connector state and observed identity:
- Result-Acceptance Record / gate verdict:
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
| REQ-001 |  |  |  |  |  | UNIT / COMPONENT / CONTRACT / INTEGRATION / SYSTEM / ACCEPTANCE |  |  |  |  |  |  | DISCOVERED / PROPOSED / PLANNED / IMPLEMENTED_UNVERIFIED / VERIFIED_LOCAL / VERIFIED_INTEGRATION / READY_FOR_MERGE / MERGED_UNRELEASED / RELEASED_UNACCEPTED / ACCEPTED / BLOCKED / UNKNOWN |

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
- Decision: STOP | READY_FOR_EXPERIMENT | BLOCKED | UNKNOWN

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
- Decision: STOP | EXPERIMENT_ONLY | VALIDATED_NO_PROMOTION | READY_FOR_PROMOTION_REVIEW | BLOCKED | UNKNOWN

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

## Incident break-glass exception, if used

- Incident / accountable owner:
- Exact artifact/configuration identity:
- Narrow scope and prohibited expansion:
- Start / expiry UTC:
- Monitoring / abort thresholds:
- Fallback / rollback:
- Post-stabilization gate owner and due action:
```

## 13. Result-Acceptance / Evidence-Lineage Record

```markdown
# Result-Acceptance Gate

- Decision being authorized: NEXT_IMPLEMENTATION_MANDATE | MERGE_GO | RELEASE_GO | DEPLOYMENT_GO | CERTIFICATION | OTHER
- Architect/reviewer:
- Independence status: INDEPENDENT | SELF_REVIEW_ONLY
- Last independently accepted immutable baseline, or `NO_PRIOR_ACCEPTED_BASELINE` plus justified start boundary:
- Exact final target identity:
- Evidence window: <baseline → target>
- Relevant source/configuration/schema/workflow/environment revisions:
- Forge connector: GITHUB_AUTHENTICATED | NATIVE_AUTHENTICATED | NOT_APPLICABLE | UNAVAILABLE
- Observed host/repository/account state without credentials:
- GitHub PR/base/head and required-check identities, if applicable:
- Material evidence surfaces available:
- Missing, inaccessible, or expired evidence surfaces:

## Attempt inventory

| ID | Artifact/target | Run/attempt/job/step | UTC/environment | Status | Expected/actual scope or count | Primary evidence | Reconciliation state |
|---|---|---|---|---|---|---|---|
| ATT-001 |  |  |  | PASSED / FAILED / CANCELLED / TIMED_OUT / SKIPPED / RETRIED / RERUN / SUPERSEDED / EXPECTED_RED / MUTATION |  |  | OPEN / RECONCILED |

## Open evidence-item reconciliation

### <attempt or anomaly ID>

- Exact artifact and target identity:
- UTC time and environment:
- Failing step and observable symptom:
- Expected versus actual scope/count:
- Classification: PRODUCT | TEST | FIXTURE | HARNESS | CONFIGURATION | ENVIRONMENT | INFRASTRUCTURE | EXPECTED_NEGATIVE_CONTROL | UNKNOWN
- Cause / confidence: PROVEN | PROVISIONAL | UNKNOWN
- Correction, or justified reason none was needed:
- Evidence invalidated by the correction:
- Falsifiable proof that the correction addresses the cause:
- Final result on the exact corrected target:
- Remaining uncertainty and residual risk:
- Reconciliation state: OPEN | RECONCILED

## Causal closure

- Original target or controlled mutation reproduces failure:
- Corrected target passes the same oracle:
- Removal/reversal of correction fails the relevant gate, or reason unsafe/disproportionate:
- Unrelated assertions, discovery counts, and safety boundaries preserved:
- Intervening diff inspected:
- Invalidated gates rerun:

## Final-head completeness

- All required gates ran:
- Discovery counts nonzero and exact where known:
- No required step skipped or silently tolerated:
- Logs and artifacts match the exact target:
- Retry/cache/continue-on-error/condition/order reviewed:
- Working tree/generated artifacts/external state match claimed identity:

## Gate outcome

- Open evidence items:
- Result-Acceptance Gate verdict: PASS | FAIL | BLOCKED | UNKNOWN
- Lifecycle-state impact:
- Downstream authority now allowed: PROGRESSION | BOUNDED_DIAGNOSIS | BOUNDED_CORRECTION | EVIDENCE_RECOVERY | ACCESS_REQUEST | NONE
- Evidence item the bounded response directly addresses, if applicable:
- Downstream authority still forbidden:
- Errors encountered and corrections section updated: YES | NO
```
