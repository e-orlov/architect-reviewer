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
14. Delta Evidence Plan
15. Next-Safe-Step Record

Use only fields justified by the task. Preserve exact identities and raw evidence references. Delete instructional placeholders before delivery.

## 1. State Capsule

```markdown
# State Capsule

- Objective:
- Original requested decision/claim:
- Accepted scope change, if any: <authority/evidence>
- Task type / assurance: <type> / A0–A4
- Lifecycle state: <exact state from operating-model.md>
- Scoped route/AI decision state(s):
- Review verdict, if any: CERTIFIED | NOT CERTIFIED | UNKNOWN
- Canonical instructions/decision:
- Target identity: <repo/branch/SHA/build/config/schema/runtime as applicable>
- Evidence window: <last independently accepted immutable baseline or NO_PRIOR_ACCEPTED_BASELINE → exact target>
- Delta Evidence Plan: <identity, revision, COMPLETE | BLOCKED | UNKNOWN | NOT_REQUIRED>
- Next transition: <exact durable lifecycle transition, exposure cap, checkpoint, stop/rollback boundary>
- Next-Safe-Step Record: <identity, revision, COMPLETE | BLOCKED | UNKNOWN | NOT_REQUIRED>
- NEXT-STEP BLOCKERS:
- END-STATE HARDENING: <item, activation boundary/trigger, owner, target, review date>
- Milestones: <frozen denominator, completed durable transitions>
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

## Delta Evidence Plan or reference

## Next-Safe-Step Record or reference

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
- Next transition / checkpoint / exposure cap / rollback boundary:
- Critical-path class: NEXT_STEP_BLOCKER | END_STATE_HARDENING
- Blocker basis: REACHABLE_RISK | GOVERNING_POLICY | N/A
- Reachable risk / five-condition admission rationale:
- Governing policy and applicable boundary, if used:
- Expected time / execution / context cost:
- Evidence that retires the uncertainty:
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
- Original requested decision/claim:
- Reviewed decision/claim:
- Scope change from original request: NONE | PROPOSED | ACCEPTED
- Scope-change authority / acceptance evidence:
- Scope and exact artifact identity:
- Task type / assurance:
- Last independently accepted immutable baseline, or `NO_PRIOR_ACCEPTED_BASELINE` plus justified start boundary:
- Evidence window and exact final target:
- Delta Evidence Plan identity/revision and status:
- Reviewed next transition and Next-Safe-Step Record:
- NEXT-STEP BLOCKERS reviewed:
- END-STATE HARDENING and activation boundaries reviewed:
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

## Non-blocking end-state hardening

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
- Next bounded transition / exposure cap / checkpoint:
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
- Original requested decision/claim and any accepted scope change:
- Lifecycle state: <exact state from operating-model.md>
- Scoped route/AI decision state(s):
- Review verdict, if any: CERTIFIED | NOT CERTIFIED | UNKNOWN
- Exact target and artifact identities:
- Evidence window and last accepted immutable baseline:
- Delta Evidence Plan identity/revision, reuse decisions, and expansion triggers:
- Next-Safe-Step Record, blockers, deferred hardening, milestone denominator, and next checkpoint:
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

| ID | Need / rationale | Requirement or control | Risk / prohibited outcome | Design owner | Implementation slice | Verification level | Falsifiable criterion / oracle | Scope / expected count | Environment identity | Evidence / UTC | Invalidation dependencies | Lifecycle activation | Owner | State |
|---|---|---|---|---|---|---|---|---|---|---|---|---|---|---|
| REQ-001 |  |  |  |  |  | UNIT / COMPONENT / CONTRACT / INTEGRATION / SYSTEM / ACCEPTANCE |  |  |  |  |  | NEXT_STEP_BLOCKER:REACHABLE_RISK / NEXT_STEP_BLOCKER:GOVERNING_POLICY / END_STATE_HARDENING:<boundary> |  | DISCOVERED / PROPOSED / PLANNED / IMPLEMENTED_UNVERIFIED / VERIFIED_LOCAL / VERIFIED_INTEGRATION / READY_FOR_MERGE / MERGED_UNRELEASED / RELEASED_UNACCEPTED / ACCEPTED / BLOCKED / UNKNOWN |

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
- Original requested decision/claim:
- Reviewed transition and owner-accepted scope change, if any:
- Architect/reviewer:
- Independence status: INDEPENDENT | SELF_REVIEW_ONLY
- Last independently accepted immutable baseline, or `NO_PRIOR_ACCEPTED_BASELINE` plus justified start boundary:
- Exact final target identity:
- Exact next transition / checkpoint / exposure cap / rollback boundary:
- Next-Safe-Step Record identity / final revision:
- Required gate scope: <NEXT-STEP BLOCKERS, including applicable GOVERNING_POLICY blockers>
- Deferred END-STATE HARDENING and activation boundaries:
- Evidence window: <baseline → target>
- Delta Evidence Plan identity / final revision:
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

- All NEXT-STEP BLOCKERS, including applicable governing-policy gates, ran:
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

## 14. Delta Evidence Plan

```markdown
# Delta Evidence Plan

- Task / decision:
- Assurance: A0 | A1 | A2 | A3 | A4
- Architect/reviewer and UTC:
- Plan identity / revision:
- Plan status: COMPLETE | BLOCKED | UNKNOWN
- Last accepted immutable baseline, or `NO_PRIOR_ACCEPTED_BASELINE` plus justified start boundary:
- Exact target identity:
- Decision boundary: IMPLEMENTATION | REVIEW | MERGE | RELEASE | DEPLOYMENT | ACCEPTANCE
- Exact next transition / exposure cap / checkpoint / rollback boundary:
- Reachable residual risks after current controls:

## Exact delta

| Category | Baseline identity | Target identity | Exact change | Primary evidence |
|---|---|---|---|---|
| Source / schema / configuration / workflow / dependency / environment / generated artifact / external interface |  |  |  |  |

## Direct and transitive impact

| Changed artifact | Owned contract/invariant | Direct consumers | Transitive consumers | Data/migration | Build/CI/release | User/operator behavior | Rollback/recovery | Unknowns |
|---|---|---|---|---|---|---|---|---|
|  |  |  |  |  |  |  |  |  |

## Evidence classification

| Claim/gate | State | Dependency rationale | Existing evidence/identity | Required proof | V-model level | Invalidation/TTL |
|---|---|---|---|---|---|---|
|  | INVALIDATED / PARTIALLY_INVALIDATED / REUSABLE / NEWLY_REQUIRED / N/A / UNKNOWN |  |  |  | UNIT / COMPONENT / CONTRACT / INTEGRATION / SYSTEM / ACCEPTANCE |  |

## Targeted execution plan

| Order | Claim/gate | Test/read/probe | Oracle and expected count/result | Prerequisite | Estimated cost/context | Stop condition |
|---|---|---|---|---|---|---|
|  |  |  |  |  |  |  |

## Broad convergence gates

| Gate | Exact final target | Justification: dependency / uncertainty / risk / boundary / policy | Expected cost | Invalidation trigger |
|---|---|---|---|---|
|  |  |  |  |  |

## Expansion triggers

- Unknown dependency boundary:
- Unexpected coupling or failure:
- New/unplanned change:
- Evidence contradiction or stale oracle:
- Budget threshold requiring checkpoint:

## Evidence and context budget

- Expensive artifact reads:
- Targeted executions:
- Broad executions:
- Raw-log retention location:
- Initial context to load:
- Expansion authority/checkpoint:

## Completeness decision

- Every changed artifact has an impact path or explicit uncertainty: YES | NO
- Every relevant claim has exactly one evidence state: YES | NO
- Every invalidated/new claim required for the exact next transition or applicable governing policy has matching proof: YES | NO
- Every deferred invalidated/new claim has END-STATE HARDENING classification, activation boundary/trigger, owner, target, and review date: YES | NO
- Every reuse claim has dependency/identity/TTL/oracle rationale: YES | NO
- Every broad gate has a stated justification: YES | NO
- A2+ implementation/review/downstream authority allowed by this plan: YES | NO
- Remaining unknowns:
```

## 15. Next-Safe-Step Record

```markdown
# Next-Safe-Step Record

- Task / decision:
- Original requested decision/claim:
- Proposed narrower transition and scope-change acceptance, if any:
- Architect/reviewer and UTC:
- Record identity / revision:
- Exact accepted artifact/build/config/environment:
- Current lifecycle state:
- Exact next durable lifecycle transition:
- Exposure cap: <time, population, calls, cost, data volume, or N/A>
- Observation checkpoint and accountable operator:
- Stop condition / proven rollback boundary:
- Frozen milestone denominator / completed durable transitions:
- Rebaseline, if any: <old denominator, new denominator, lifecycle-topology evidence, owner approval, UTC date>

## Residual-risk recomputation

| Material control accepted | Failure modes prevented, detected, contained, or made recoverable | Evidence | Residual risk before next transition | Controls demoted/promoted |
|---|---|---|---|---|
|  |  |  |  |  |

## Reachable-risk inventory

| Failure mode | Reachable before checkpoint? | Existing preventive/detective/containment/recovery controls | Residual consequence | Evidence / unknowns |
|---|---|---|---|---|
|  | YES / NO / UNKNOWN |  |  |  |

## NEXT-STEP BLOCKERS

| Control/gate | Basis | Named reachable risk or governing policy/boundary | Why existing controls are insufficient | Why no bounded substitute is safe | Harm before checkpoint | Proportionate proof / V level | Cost | Owner / state |
|---|---|---|---|---|---|---|---|---|
|  | REACHABLE_RISK / GOVERNING_POLICY |  |  |  |  |  |  | OPEN / PASS / RECLASSIFIED_WITH_RATIONALE / BLOCKED / UNKNOWN |

## END-STATE HARDENING

| Control | Later risk reduced | Earliest activation boundary / trigger | Target outcome | Owner | Review date | Why non-blocking now |
|---|---|---|---|---|---|---|
|  |  |  |  |  |  |  |

## Bounded-supervision exception, if used

- Exposure cap:
- Accountable operator:
- Observable signals and threshold:
- Stop/rollback proof:
- Security/privacy/data-loss/irreversibility/paid-effect/side-effect check:
- Expiry and next decision point:

## Minimum-sufficient evidence plan

- Delta and transitive impact reference:
- Invalidated claims material to this transition:
- Required targeted proof:
- Governing-policy blockers:
- Convergence gate, only if a named trigger or policy justifies one:
- Post-transition telemetry not treated as blocking proof:
- Evidence budget / expansion trigger:

## Critical-path and milestone decision

- Activities combined because they share artifact/environment/authority/observation/rollback:
- Activities split because independently useful/releasable or materially risk-isolating:
- Next authorized transition: GO | BLOCKED | UNKNOWN
- Authority still required:
- Hardening activation reminders/checkpoints:
- Rationale:
```
