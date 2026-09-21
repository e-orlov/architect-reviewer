# Evidence and gate contracts

## Contents

1. Gate record
2. V-model pairing
3. Falsifiability and negative controls
4. Coverage and real-path proof
5. Evidence freshness and invalidation
6. Repository and CI evidence
7. Environment and production acceptance
8. Retries and external effects
9. Independent review
10. Risk assessment
11. STOP conditions
12. Review lenses
13. Extensions, hooks, and diagnostic actions

## 1. Gate record

Every blocking gate must answer:

| Field | Requirement |
|---|---|
| Claim | One precise statement being proved |
| Invariant | Property that must remain true |
| Artifact | Exact file/symbol/commit/build/config/schema/runtime identity |
| Scope | Enumerated targets and expected count |
| Oracle | Source that decides truth independently of the implementation where possible |
| Falsifiability | How the check is known to fail for the target defect |
| Environment | Relevant OS/runtime/services/data/configuration |
| Action | Exact test, query, probe, or inspection |
| Result | Raw counts, values, checksums, status, and relevant output |
| Time | UTC observation time and TTL if mutable |
| Dependencies | Changes that invalidate this evidence |
| Owner | Person/system responsible for the gate |
| Verdict | `PASS`, `FAIL`, `BLOCKED`, or `UNKNOWN` for this gate only |
| Next authority | Action now allowed, still forbidden, or requiring approval |

An exit code without the artifact, count, and asserted values is incomplete evidence.

## 2. V-model pairing

Pair definition with proof at the corresponding boundary:

| Definition side | Verification side | Typical proof |
|---|---|---|
| User/business need | Real-world acceptance | User-visible behavior and outcome |
| System requirements | System/production test | End-to-end behavior in target topology |
| Architecture and interfaces | Integration/contract test | Boundaries, compatibility, failure semantics |
| Component design | Component test | Module behavior and dependency interactions |
| Implementation | Unit/static checks | Local logic, types, invariants |

Lower-level proof cannot automatically satisfy a higher-level claim. A unit test cannot establish production routing; a production HTTP 200 cannot prove semantic correctness.

Use [v-model.md](v-model.md) to build the bidirectional requirement-to-evidence trace. A gate without a trace row may still be useful, but it cannot close a blocking requirement until its owning definition and verification level are explicit.

## 3. Falsifiability and negative controls

For each blocking criterion:

1. Name the defect it should detect.
2. Show that the check observes the affected boundary.
3. Safely inject or identify a known-bad condition when practical.
4. Confirm the check fails for the expected reason.
5. Restore the target and confirm it passes.

Use mutation testing, a deliberately invalid fixture, a known-bad request, a missing dependency, or a controlled configuration mismatch. Never mutate production merely to prove a check can fail. If a surface cannot be safely falsified, label the limitation.

Before accepting a generated, recovered, or brownfield criterion, run it against the current implementation where safe. If it passes both known-good and known-bad behavior, or cannot distinguish the behavior it describes, the criterion itself is defective. Classify that separately from an implementation failure.

## 4. Coverage and real-path proof

Before claiming complete coverage:

- enumerate all routes, entry points, consumers, schemas, jobs, configuration writers, UI surfaces, and release paths in scope;
- bind every inventory item to a check or an explicit exclusion;
- verify expected discovered count is nonzero and matches the inventory;
- import or invoke the exact production symbol when drift from a structural copy is possible;
- exercise the real call path when mocks could hide wiring, serialization, auth, routing, or persistence defects.

Treat inventory drift as a failing control, not a documentation inconvenience.

## 5. Evidence freshness and invalidation

Store evidence against the narrowest proved boundary:

- criterion ID;
- production symbol/path;
- artifact identity;
- data/config/environment identity;
- oracle version;
- timestamp and TTL.

Invalidate evidence when any dependency changes. A change elsewhere in the same file need not invalidate symbol-bound evidence, but policy may still require a full suite. Record why a rerun was or was not necessary. Never reuse evidence merely because a report looks recent.

## 6. Repository and CI evidence

For a live repository or pull-request claim, use an authenticated source and capture:

- host and exact repository;
- active authenticated account state without exposing credentials;
- default/target branch;
- head and base SHA;
- PR state, draft state, mergeability, review decision, and required checks;
- check name, status, conclusion, and the SHA it evaluated;
- UTC observation time.

Do not infer private or mutable state from public search, cached pages, screenshots, or an earlier report. If authenticated access is unavailable, state `UNKNOWN` and do not recommend merge or release.

Treat repository-local status files and generated indexes as derived views. Reconcile them against exact artifacts and the live forge. A locally recorded green status cannot establish that required remote checks ran on the current head SHA.

## 7. Environment and production acceptance

Name the environment and topology. Verify:

- source/build/config/schema identity matches the intended release;
- dependencies, routes, credentials, feature flags, and schedulers match the acceptance claim;
- user-visible semantics, not only health endpoints;
- latency, traffic, errors, and saturation where operationally relevant;
- explicit operating thresholds: an SLI/SLO, error budget, business guardrail, or documented equivalent; do not import percentages from another system;
- data integrity and side effects;
- restart, timeout, partial failure, and rollback behavior;
- automation does not undo or race the change.

Keep `VERIFIED_INTEGRATION`, `RELEASED_UNACCEPTED`, and `ACCEPTED` distinct.

For staged rollout, define the cohort, observation window, abort condition, rollback trigger, and accountable operator before exposure. A dashboard without a threshold and response is not an acceptance gate.

## 8. Retries and external effects

Treat paid, mutating, or externally visible calls as business operations. Require:

- a stable caller-intent or idempotency key;
- atomic or reconciled relationship between durable attempt state and side effects;
- typed outcomes: success, validation failure, retryable failure, terminal failure, refusal, timeout, ambiguous result;
- budget, attempt, time, and concurrency caps;
- policy for late responses and same key with different intent;
- recovery after process restart;
- audit trail linking intent, provider/request identity, cost, and terminal outcome.

Never blindly retry an ambiguous mutation. Reconcile first or park it for explicit resolution.

## 9. Independent review

For A3/A4, require:

- reviewer identity distinct from author;
- fresh or deliberately bounded context;
- exact artifact and evidence packet;
- explicit review scope and severity model;
- findings with evidence and consequence;
- one of `CERTIFIED`, `NOT CERTIFIED`, or `UNKNOWN`, scoped to the reviewed claims;
- residual risks and evidence gaps;
- dialogue/re-review after corrections when findings invalidate the original evidence.

Use a bounded doubt cycle:

1. **Claim:** enumerate the blocking claims and the contract each must satisfy.
2. **Extract:** inspect the exact artifact and raw evidence without relying on the author's summary.
3. **Doubt:** attack the highest-severity assumptions, including oracle independence and missing surfaces.
4. **Reconcile:** classify findings, repair or reject invalid evidence, and rerun only invalidated gates.
5. **Stop:** end at the defined exit condition or return `UNKNOWN/BLOCKED`; do not loop until fatigue produces agreement.

Pass the artifact against its contract, not the author's reasoning. Reviewer findings are evidence to reconcile, not an automatic verdict; technically challenge them when contradicted by stronger evidence.

A different model is useful for reducing correlated blind spots but is still an advisory reviewer. The accountable human or organization retains risk acceptance.

For a budgeted or interrupted review, record the inspected inventory and mark every remaining candidate `UNJUDGED`. Absence of a finding on an uninspected surface is not evidence. Persist each material finding in the review artifact or explicitly decline it with a technical reason.

## 10. Risk assessment

Use a compact living risk record:

- risk scenario and trigger;
- affected asset/user/process;
- inherent likelihood and impact with rationale;
- preventive, detective, and corrective controls;
- control evidence and effectiveness uncertainty;
- residual likelihood and impact;
- early-warning indicators;
- mitigation, contingency, owner, review date, and status;
- treatment: avoid, mitigate, transfer, or accept;
- accountable acceptance for residual risk.

Maintain a review log. Reassess on the scheduled date and when material changes occur: architecture or dependency change, new threat or incident evidence, control failure, scope expansion, data-classification change, or production exposure. Control existence is not control effectiveness; bind effectiveness to evidence and uncertainty.

A 5×5 score can prioritize discussion, but it is not a measured probability. Define scales for the actual context; do not copy monetary or regulatory thresholds from another organization.

## 11. STOP conditions

Stop or return `UNKNOWN/BLOCKED` when:

- current target, branch, commit, build, environment, or executor state is ambiguous;
- destructive, paid, external, merge, migration, release, or production authority is absent;
- expected test count is zero or unknown;
- the oracle shares the same unverified assumption as the implementation;
- the criterion cannot observe the claimed boundary;
- evidence belongs to a different artifact or has expired;
- rollback/recovery is required but absent or untested;
- retry can duplicate an irreversible or paid effect;
- automation has no owner or inhibit during a change window;
- an integration/release/production lane is already owned;
- A3/A4 lacks required independent review or residual-risk owner;
- authenticated live repository evidence is unavailable for a live verdict;
- canonical and superseded instructions cannot be distinguished.

## 12. Review lenses

Review in this order:

1. **Requirements:** Does the change solve the stated problem without silently changing scope?
2. **Correctness:** Are normal, boundary, concurrent, retry, and partial-failure paths sound?
3. **Security/privacy:** Are trust boundaries, authorization, secrets, input/output, and dependencies safe?
4. **Data/recovery:** Can data be lost, duplicated, corrupted, or made irreconcilable? Is recovery proven?
5. **Compatibility:** Are APIs, schemas, clients, mixed versions, and migrations handled?
6. **Operability:** Are identity, logs, metrics, alerts, rollout, rollback, and automation behavior adequate?
7. **Test adequacy:** Do tests exercise the real path, have a trustworthy oracle, and prove they can fail?
8. **Simplicity:** Is every abstraction, dependency, layer, and line needed now?

Report defects separately from optional improvements. Avoid drowning a blocking finding in style commentary.

## 13. Extensions, hooks, and diagnostic actions

Before installing or invoking an extension, plugin, hook, generator, benchmark harness, or third-party skill, inspect:

- source/provenance, version identity, update channel, and integrity mechanism;
- invocation points and lifecycle hooks;
- prompt/context injection and precedence over project instructions;
- filesystem, process, credential, secret, network, and shared-service access;
- persistent state, caches, telemetry, and data retention;
- enable, inhibit, uninstall, rollback, and recovery behavior;
- whether it can contaminate a benchmark, baseline, review, or supposedly independent run.

Do not persistently install or enable it without user authorization. Prefer a read-only or isolated evaluation when the control value is still unproven.

For every diagnostic action that can affect the target, keep a side-effect ledger: target, expected reads/writes, load/cost budget, notifications or audit events, temporary artifacts, cleanup/reconciliation step, and observed residue. A probe is complete only when its residue is accepted or removed and that result is verified.
