# V-model operating spine

## Contents

1. Purpose and boundary
2. The paired model
3. Traceability contract
4. Continuous, iterative use
5. Route overlays
6. Verification design
7. Evidence invalidation
8. Review rules and failure patterns
9. Compact example

## 1. Purpose and boundary

The V-model is the organizing spine for completeness: every need, requirement, architecture boundary, and component design decision on the definition side receives a matching verification or validation activity on the evidence side.

It does not require a single sequential waterfall. Use it recursively for a system, feature, migration, bug fix, or vertical slice. Definition and proof can evolve together. The non-negotiable property is traceability: no blocking left-side claim is complete without a right-side proof designed for the same boundary.

Use the task route to decide which lifecycle steps are necessary and the assurance level to decide their depth. The V-model answers a different question: whether the selected work is both specified and proven at every relevant level.

## 2. The paired model

| Left-side definition | Required content | Right-side proof | Boundary proved |
|---|---|---|---|
| Need / intended outcome | User, problem, value, prohibited outcome, success signal | Real-world acceptance | The delivered system solves the intended problem under actual use |
| System requirements | Observable behavior, quality attributes, constraints, failure semantics | System or end-to-end verification | The system meets its requirements in the target topology |
| Architecture and contracts | Components, trust boundaries, APIs, data ownership, compatibility, recovery | Integration, contract, migration, and recovery verification | Boundaries compose correctly and fail safely |
| Component design | Owning component, internal contract, dependency behavior, invariants | Component verification | The component satisfies its contract with realistic dependency behavior |
| Implementation | Logic, types, local state transitions, defensive checks | Unit, static, type, and focused invariant checks | The code is internally consistent with the component design |

Keep verification and validation distinct:

- **Verification:** Does this artifact satisfy the contract specified for it?
- **Validation:** Does the resulting system satisfy the actual user or operational need?

A correct implementation of the wrong requirement may be verified and still fail validation.

## 3. Traceability contract

Create one row per blocking requirement, risk control, or operational invariant:

| Field | Requirement |
|---|---|
| ID | Stable identifier, not row position |
| Need / rationale | Why the requirement exists and whom it protects |
| Requirement | Observable behavior or constraint, free of premature implementation detail |
| Risk / prohibited outcome | Failure the row exists to prevent |
| Design owner | Component or boundary responsible for the invariant |
| Implementation slice | Exact files, symbols, schema, config, or operational change |
| Verification level | Unit, component, contract, integration, system, or acceptance |
| Criterion | Falsifiable expected behavior and boundary conditions |
| Oracle | Source of truth plus independence and shared-assumption limits |
| Scope / expected count | Enumerated surfaces and expected discovered cases, or `N/A` with reason |
| Environment identity | Runtime, services, data, configuration, and topology |
| Evidence | Exact artifact/result identity, raw output location, UTC time |
| Invalidation dependencies | Changes that require this evidence to be refreshed |
| Delta evidence state | `INVALIDATED`, `PARTIALLY_INVALIDATED`, `REUSABLE`, `NEWLY_REQUIRED`, `N/A`, or `UNKNOWN`, with rationale |
| Lifecycle activation | `NEXT-STEP BLOCKER` with basis `REACHABLE_RISK` or `GOVERNING_POLICY`, or later hardening boundary where the row becomes required |
| Owner | Person/system responsible for closure |
| State | One exact lifecycle state from [operating-model.md](operating-model.md) |

Trace in both directions:

- **Forward:** every requirement reaches an implementation slice and proof;
- **Backward:** every implementation slice and test points to a requirement, risk control, or justified enabling work.

An orphan requirement means missing implementation or evidence. An orphan implementation means scope creep, hidden infrastructure, speculative abstraction, or an undocumented requirement.

## 4. Continuous, iterative use

For each safe vertical slice:

1. Select one user-visible behavior, boundary contract, or risk reduction.
2. Write or refine its left-side trace rows.
3. For A2+ work, establish the exact baseline-to-target delta, trace direct and transitive impact, and record the [Delta Evidence Plan](delta-first.md).
4. Define the [next safe step](next-safe-step.md): exact transition, reachable residual risks, exposure cap, checkpoint, rollback, blockers, and later hardening.
5. Design right-side criteria before changing implementation.
6. Confirm the criteria observe the real boundary and name a falsifying defect; execute a safe negative control when required by assurance.
7. Implement the minimum complete slice.
8. Run the earliest matching checks immediately: local, component, contract, then higher-level when justified by impact, reachable risk, or policy.
9. Preserve exact evidence and update lifecycle state.
10. Reconcile new evidence into requirements, design, residual risk, the Delta Evidence Plan, the Next-Safe-Step Record, and the next slice.

Clarification is allowed at any point. When evidence contradicts a requirement or design, return to the affected left-side row, change it explicitly, and invalidate only dependent proof. Do not patch the implementation while leaving the governing contract stale.

## 5. Route overlays

### Idea

The left side is intentionally shallow: need, beneficiaries, constraints, outcome, alternatives, and decision risks. The right side is decision evidence such as user research, feasibility probes, cost/reversibility analysis, or explicit unknowns. The terminal result is `GO`, `CLARIFY`, or `STOP`, not working code.

### Feature

Use the full V. Start with WHAT/WHY, clarify uncertainty, then architecture and vertical tasks. Define acceptance and system evidence before implementation. Converge code, tests, documentation, configuration, release controls, and operational ownership before calling the feature complete.

### Bug

Map the observed symptom and expected behavior to a failing reproduction or explicit reason reproduction is unavailable. Map the owning cause to component proof, affected contracts to integration proof, and user impact to regression/acceptance proof. A test that never reproduced the original defect is not sufficient closure by itself.

### Refactor or migration

Treat existing behavior, consumers, data, and compatibility as left-side requirements. Establish behavior and data baselines before change. Pair contracts with mixed-version, migration, reconciliation, rollback, and cutover proof. Retire the old path only after consumer inventory and recovery obligations close.

### Incident

The first need is safe service restoration. Pair stabilization and containment actions with immediate service, data-integrity, and automation checks. After recovery, create durable requirement/control rows for each corrective action. A postmortem is not closure until owned controls have evidence.

### Release

Bind the left side to the exact source, build, dependency lock, configuration, schema, feature flags, topology, rollout policy, and rollback target. Pair it with live required checks, staged exposure, user-facing signals, abort thresholds, deployment identity, and real-world acceptance.

### Review or audit

Reconstruct the V from the artifact rather than trusting the author's summary. Inventory requirements, implementation surfaces, tests, release state, and risk controls. Orphan rows, boundary mismatches, and evidence from another identity are findings.

## 6. Verification design

A right-side activity is credible only when it answers all of these:

1. **Claim:** What exact statement is being proved?
2. **Boundary:** At what V level does the claim live?
3. **Target:** Which production symbol, route, contract, build, config, or runtime is exercised?
4. **Oracle:** What decides correctness, and which assumptions are or are not independent of the code under test?
5. **Falsifiability:** Which target defect makes the check fail, is an executed demonstration required, and what limitation remains if it is unsafe or unavailable?
6. **Inventory:** What surfaces exist, and what count should discovery produce, or why is an executable count `N/A`?
7. **Environment:** Which topology, services, data, and configuration are part of the claim?
8. **Result:** What raw values, counts, checksums, statuses, or observations were collected?
9. **Freshness:** When was evidence observed, and what changes invalidate it?
10. **Authority:** Which next action does this proof permit, and which actions remain forbidden?

Prefer an independent oracle. If implementation and test repeat the same assumption, they can agree while both are wrong. Use contracts, known fixtures, reference implementations, invariant-based checks, externally observed outcomes, or reconciled production facts as appropriate.

## 7. Evidence invalidation

Bind evidence to the narrowest proved unit: criterion ID, exact production symbol or path, artifact identity, environment/config identity, oracle version, and time.

Apply [delta-first evidence selection](delta-first.md) before rereading artifacts or choosing tests. Map each source, schema, configuration, workflow, dependency, environment, generated-artifact, and external-interface change to every affected trace row, including rows owned by unchanged direct or transitive consumers. Classify each row's evidence as `INVALIDATED`, `PARTIALLY_INVALIDATED`, `REUSABLE`, `NEWLY_REQUIRED`, `N/A`, or `UNKNOWN`; artifact identity alone does not establish relevance.

- A local logic change invalidates dependent unit/component evidence.
- A contract change invalidates provider, consumer, compatibility, and integration evidence.
- A config, schema, flag, or dependency change invalidates tests whose environment identity no longer matches.
- A new consumer invalidates a previously complete inventory and its coverage claim.
- A deployment change invalidates real-world acceptance for the prior deployed identity.
- A requirement change invalidates every downstream row that depends on it.

Run the smallest test set that proves all invalidated and newly required rows **material to the exact next transition** at their matching V-model boundaries. Keep other affected rows traced to their later activation boundary. Broaden to a full suite or system convergence gate only when a named dependency uncertainty or reachable claim cannot be bounded more narrowly, or when applicable policy requires it. Do not rerun unrelated expensive gates solely because a file changed elsewhere. Conversely, do not reuse a green report because its timestamp looks recent or its artifact hash is unchanged.

## 8. Review rules and failure patterns

| Failure pattern | Why it fails | Required correction |
|---|---|---|
| Tests are designed after implementation with no trace | They may prove the code's assumptions rather than the requirement | Define paired criteria with the left-side artifact |
| Many unit tests, no system acceptance | Lower-level correctness cannot establish user outcome or routing | Add the missing higher-level proof |
| End-to-end happy path only | Broad execution can miss local invariants and failure semantics | Add boundary-appropriate component/contract checks |
| Test cannot turn red | Its existence is not evidence that it detects the defect | Name the logical counterexample; add a safe negative control when required or label the limitation and alternative evidence |
| Applicable test gate discovers zero tests with exit 0 | The harness ran, but the intended scope did not | Assert nonzero expected count and target identity; use justified `N/A` only when no executable test applies |
| Brownfield spec generated from prose | It may contradict live behavior and consumers | Validate executable criteria against the actual system |
| Same author declares independent success | Correlated assumptions remain unchallenged | Use separate context/reviewer or label self-review |
| CI result belongs to another SHA | Evidence and artifact identities do not match | Read live forge state for the exact head and required checks |
| Only tests near changed files are selected | File proximity misses shared contracts, schemas, configuration, generated artifacts, and transitive consumers | Build the impact graph; test every invalidated row required now and trace later affected rows to their activation boundary |
| Every available test is run without rationale | PASS volume spends time and context without proving that affected claims were selected | Use the Delta Evidence Plan; reserve broad convergence for explicit triggers or policy |
| Desired unattended controls block a bounded supervised transition | It confuses later reachable risk with the next checkpoint's residual risk | Separate next-step blockers from hardening and apply the blocker-admission test |
| Summed worst cases create a fixed idle gate | An upper bound does not establish likely consumption or harm before the next checkpoint | Trace the counterfactual and use a dynamic guard or STOP trigger when it contains the risk |
| Tests, reviews, corrections, and reruns are counted as milestones | Proof activity inflates perceived lifecycle progress and destabilizes the denominator | Count only durable externally meaningful transitions |
| Worktree treated as environment isolation | Shared ports, services, data, quotas, and schedulers can interfere | Inventory and isolate or serialize shared resources |
| V-model treated as a one-way stage gate | Learning is suppressed and verification arrives too late | Use recursive vertical slices and explicit backtracking |

## 9. Compact example

Requirement: a payment retry must never create a second charge for the same caller intent.

| V level | Definition | Paired proof |
|---|---|---|
| Need | User pays once despite transient failure | Acceptance scenario observes one settled charge and a clear terminal outcome |
| System | Repeated same-intent requests are safe across timeout/restart | System test injects ambiguous timeout and restart, then reconciles provider and ledger |
| Architecture | Intent key owns idempotency across API, durable attempt, and provider | Contract/integration test checks same-key/same-intent, same-key/different-intent, and late response |
| Component | Attempt state machine forbids a second active charge | Component test covers typed transitions and concurrent requests |
| Implementation | Atomic transition and uniqueness rule are correct | Unit/static/database constraint checks |

The local uniqueness test is necessary but cannot establish provider reconciliation or real user outcome. The acceptance test is necessary but cannot replace component proof of every state transition. Together, traced to one invariant, they close the V.
