# Operating model

## Contents

1. Precedence
2. Truth hierarchy
3. Project-agnostic wisdom
4. Status model
5. Role and authority boundaries
6. State, handoffs, and phase boundaries
7. Concurrency and shared systems
8. Configuration, automation, and incidents
9. Canonical knowledge and process quality

## 1. Precedence

Apply controls in this order:

1. governing system/project instructions, law, regulation, contracts, and actor authority; accountable user or operator decisions apply within those bounds;
2. safety, security, privacy, data integrity, accessibility, accounting, and trust-boundary controls;
3. V-model completeness and reliability: traceability, bounded risk, observability, recovery, rollout, rollback, and decision-capable evidence;
4. Baseline, Experiment, and Complexity-Promotion evidence when the AI/ML trigger applies;
5. KISS, YAGNI, reuse, native capabilities, and minimum new code after completeness is defined;
6. optional frameworks and templates as sources of selected practices.

Safety wins over minimalism when they conflict. Minimalism wins over ceremony that adds no assurance. Never import an entire framework merely because one control is useful.

## 2. Truth hierarchy

Prefer evidence in this order:

1. live read-only facts and immutable identifiers;
2. exact current tool or executor output;
3. repository, CI, release, and runtime evidence bound to identifiers;
4. current canonical project artifacts;
5. continuity notes and summaries;
6. conversation reconstruction and model memory.

A lower level cannot silently override a higher level. Record conflicts. For mutable facts, include the source, target identity, and observation time.

## 3. Project-agnostic wisdom

| # | Principle | Operational consequence |
|---:|---|---|
| 1 | State cannot be recovered from eloquence | Maintain a compact, inspectable State Capsule. |
| 2 | There is no universal PASS | Name the gate, scope, artifact, environment, and lifecycle state. |
| 3 | Exit 0 is a transport signal | Inspect what ran and what evidence it produced. |
| 4 | A negative control is stronger than another happy path | Name the counterexample; demonstrate failure detection when assurance requires it and doing so is safe. |
| 5 | Inventory precedes coverage | Enumerate routes, consumers, surfaces, or records before claiming completeness. |
| 6 | A phase boundary is an API | Define inputs, outputs, owner, preconditions, evidence, and handoff state. |
| 7 | File isolation is not world isolation | Worktrees do not isolate ports, databases, networks, schedulers, budgets, or release lanes. |
| 8 | Configuration is part of the release artifact | Bind code, build, config, schema, and runtime identity. |
| 9 | Retry is a business operation | Model intent, idempotency, durable attempts, cost, and ambiguous outcomes. |
| 10 | A red test can expose a bad test contract | Classify implementation defect, fixture drift, oracle defect, and environment mismatch separately. |
| 11 | Production acceptance cannot be simulated locally | Keep local, integration, deployment, and real-world acceptance gates distinct. |
| 12 | Automation is an actor | Give schedulers, watchdogs, and bots an owner, observable state, inhibit, and recovery protocol. |
| 13 | Evidence has TTL and dependencies | Reuse it only if the artifact and every relevant dependency are unchanged. |
| 14 | A corrective slice closes one invariant | Make each repair independently understandable, testable, and reversible. |
| 15 | Discovery can be parallel; shared integration must be serialized | Assign leases for shared integration, migration, release, and production lanes. |
| 16 | User decisions are scarce | Ask for product choices and risk acceptance, not facts that tools can establish. |
| 17 | Safety completeness precedes minimization | Define the full contract, then remove everything not required to satisfy it. |
| 18 | Different work needs different workflows | Route ideas, features, bugs, incidents, releases, and audits separately. |
| 19 | Process beats prose | Prefer steps, checkpoints, exit criteria, and red flags over a large passive document. |
| 20 | Acceptance criteria must be falsifiable | A blocking check names the target defect or counterexample; execution depth follows assurance and safety. |
| 21 | Invalidate evidence at the proved boundary | Tie evidence to criterion, production symbol/path, data boundary, and environment. |
| 22 | Mutable repository state needs authenticated evidence | Public web failure is not proof that current state is unknowable. Use an authenticated source or say "I don't know." |
| 23 | Risk scores prioritize; they do not measure truth | Keep assumptions visible and require accountable residual-risk acceptance. |
| 24 | Review the artifact and contract, not the author's confidence | Give an independent reviewer claims and evidence; reconcile findings instead of rubber-stamping conclusions. |
| 25 | Telemetry without a decision threshold is observation, not acceptance | Define an SLI/SLO, error budget, or explicit domain threshold before rollout. |
| 26 | A diagnostic probe is an operation | Inventory its reads, writes, cost, load, notifications, and cleanup before execution. |
| 27 | Configuration preservation must be testable | Require byte-identical output or an allowlisted semantic diff when a tool rewrites configuration. |
| 28 | A document can remain dangerous after replacement | Maintain canonical, superseded, successor, owner, and effective-date metadata. |
| 29 | Governance quality is observable | Track context-recovery time, redundant reruns, contradictions, user corrections, and escaped defects. |
| 30 | A benchmark must isolate its treatment | Detect hooks, plugins, caches, or shared state that contaminate a control arm. |
| 31 | Extensions are executable supply-chain actors | Inspect permissions, context injection, secrets, network, state, lifecycle, and rollback before adoption. |
| 32 | Definition without paired proof is incomplete | Design the matching V-model verification while defining the requirement or boundary. |
| 33 | Traceability runs in both directions | Every requirement needs implementation and evidence; every implementation and test needs a requirement, risk control, or justified enabling purpose. |
| 34 | Verification is not validation | Proving conformance to a contract cannot prove that the contract solves the real need. |
| 35 | Derived status cannot overrule source artifacts | Reconcile dashboards and indexes from exact files, live forge state, and runtime evidence. |
| 36 | Partial review leaves candidates unjudged | Record budgeted scope and carry forward uninspected surfaces instead of treating silence as approval. |
| 37 | Reviewer feedback is evidence, not an instruction | Test each finding against the contract and stronger evidence; correct, decline with reason, or mark unknown. |
| 38 | Brownfield requirements need executable validation | Run generated or recovered acceptance criteria against the live implementation before treating them as canonical. |
| 39 | A control must be capable of detecting its target failure | Demonstrate a safe negative control when required; otherwise disclose the limitation, alternative evidence, and verdict impact. |
| 40 | Risk acceptance is not delegated by analysis | Tools and reviewers surface residual risk; the accountable owner decides whether to accept it. |

## 4. Status model

Use lifecycle states instead of overloaded words:

| State | Meaning |
|---|---|
| `DISCOVERED` | Candidate issue or need identified; not yet assessed. |
| `PROPOSED` | A possible solution exists; requirements or tradeoffs may remain open. |
| `PLANNED` | Scope, owner, acceptance, and safety contract are defined. |
| `IMPLEMENTED_UNVERIFIED` | Code or configuration exists; required verification is incomplete. |
| `VERIFIED_LOCAL` | Named local gates passed on an exact artifact. |
| `VERIFIED_INTEGRATION` | Integration gates passed in the named environment. |
| `READY_FOR_MERGE` | Review and required pre-merge checks passed for exact head/base identities. |
| `MERGED_UNRELEASED` | Change is in the target branch but not proven released. |
| `RELEASED_UNACCEPTED` | Release/deployment identity is known; real-world acceptance is incomplete. |
| `ACCEPTED` | Required real-world or production acceptance passed for the deployed identity. |
| `BLOCKED` | A known unmet condition prevents progress. |
| `UNKNOWN` | Evidence is unavailable, ambiguous, stale, or contradictory. |

Keep four typed namespaces distinct:

| Namespace | Allowed examples | Meaning |
|---|---|---|
| Gate verdict | `PASS`, `FAIL`, `BLOCKED`, `UNKNOWN` | Result of one named gate only |
| Lifecycle state | one exact state in the table above | Progress of the artifact through implementation, verification, merge, release, and acceptance |
| Route/decision state | `GO`, `CLARIFY`, `STOP`, or the AI decisions defined in [ai-complexity-strategy.md](ai-complexity-strategy.md) | A scoped next-step or adoption decision |
| Review verdict | `CERTIFIED`, `NOT CERTIFIED`, `UNKNOWN` | Independent or self-review judgment for named claims and identity |

Never emit unqualified `READY`; use the exact scoped state such as `READY_FOR_MERGE`, `READY_FOR_EXPERIMENT`, or `READY_FOR_PROMOTION_REVIEW`. `BLOCKED` and `UNKNOWN` may appear in more than one namespace, so always label the namespace. Never infer a later lifecycle state from a gate or decision state.

## 5. Role and authority boundaries

Separate four authorities:

- **Architect:** frame objective, constraints, design, failure modes, verification, and tradeoffs.
- **Executor:** change the authorized target and collect raw evidence.
- **Reviewer:** challenge claims and evidence; report findings and a bounded verdict.
- **Risk owner:** accept residual business or operational risk.

One person or agent may occupy several roles for low-risk work, but label the transitions. For A3/A4, keep author and independent reviewer distinct. A reviewer recommends; the accountable human or policy grants merge, release, production, or risk-acceptance authority.

## 6. State, handoffs, and phase boundaries

Keep the State Capsule short enough to read before acting. Store:

- objective and current lifecycle state;
- scoped route, AI, and review decisions where applicable;
- exact artifact/repository/branch/commit/build/runtime identity;
- completed gates and their freshness;
- current executor/process state;
- open unknowns, decisions, and STOP conditions;
- authority granted and authority still required;
- next single action.

At every phase boundary, pass a structured contract:

- inputs and immutable identities;
- assumptions and preconditions;
- outputs and acceptance criteria;
- evidence locations;
- errors/corrections;
- owner and next authority.

Do not replay an expensive or mutating action merely to reconstruct state. Recover from durable evidence first.

## 7. Concurrency and shared systems

Use parallel work only when outputs and resources are independent. Inventory shared resources:

- repository branch and merge lane;
- ports and service names;
- databases, schemas, queues, caches, volumes, and networks;
- schedulers, watchdogs, cron jobs, and deployment controllers;
- credentials, quotas, paid-provider budgets, and rate limits;
- production change windows and rollback ownership.

Assign one owner or lease per shared mutation lane. A worktree isolates checked-out files, not these resources. When isolation is unproven, serialize.

## 8. Configuration, automation, and incidents

Treat configuration as versioned behavior. For a release, connect source SHA, build/image digest, config identity, schema/migration head, rollout record, and acceptance evidence. A test against a different combination is not release evidence.

When a formatter, generator, migration tool, or installer can rewrite configuration, choose the preservation contract before running it: byte-identical output when no change is intended, or an allowlisted semantic diff when normalization is expected. Preserve comments, ordering, permissions, secrets boundaries, and unknown fields unless the contract explicitly permits a change.

Treat automation as an actor with:

- explicit owner and purpose;
- observable current state;
- enable/disable or inhibit mechanism;
- safe restart and reconciliation semantics;
- conflict policy during manual changes;
- audit trail and failure alerting.

For incidents, stabilize before diagnosing deeply. Preserve a blameless record of impact, timeline, contributing system conditions, recovery, evidence, and preventive controls. Convert repeated manual recovery into a guardrail or automation only after its safety contract and failure modes are understood.

## 9. Canonical knowledge and process quality

Keep a small registry for durable operational documents. Record document ID, scope, owner, status (`ACTIVE`, `SUPERSEDED`, or `RETIRED`), effective date, successor, and last verification time. A newer-looking file does not silently supersede an active contract. Resolve conflicts before acting.

Measure whether the control system helps rather than merely grows. Useful signals include time to recover context, repeated fact-finding or test reruns, conflicting instructions discovered late, user corrections, review findings that escape to later phases, stale evidence reused, and time spent on controls by assurance level. Use the signals to remove ceremony that adds no assurance while preserving controls that catch material defects.
