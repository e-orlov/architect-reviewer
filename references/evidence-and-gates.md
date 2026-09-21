# Evidence and gate contracts

## Contents

1. Gate record
2. V-model pairing
3. Falsifiability and negative controls
4. Coverage and real-path proof
5. Evidence freshness and invalidation
6. Repository, CI, and mandatory forge connection
7. Evidence lineage and failure reconciliation
8. Environment and production acceptance
9. Retries and external effects
10. Independent review
11. Risk assessment
12. STOP conditions
13. Review lenses
14. Extensions, hooks, and diagnostic actions
15. AI/ML complexity evidence

## 1. Gate record

Every blocking gate must answer:

| Field | Requirement |
|---|---|
| Claim | One precise statement being proved |
| Invariant | Property that must remain true |
| Artifact | Exact file/symbol/commit/build/config/schema/runtime identity |
| Scope | Enumerated targets and expected count, or `N/A` with reason when no executable count applies |
| Oracle | Source that decides truth, including independence and shared-assumption limits |
| Falsifiability | Target defect or counterexample, negative-control status, and alternative evidence if execution is unsafe or unavailable |
| Environment | Relevant OS/runtime/services/data/configuration |
| Action | Exact test, query, probe, or inspection |
| Result | Raw counts, values, checksums, status, and relevant output |
| Time | UTC observation time and TTL if mutable |
| Dependencies | Changes that invalidate this evidence |
| Delta selection | Delta Evidence Plan identity, evidence state, impact rationale, and why this gate is run, reused, or `N/A` |
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
3. Decide whether an executed negative control is required by project policy, assurance, or materiality.
4. When required and safe, inject or identify a known-bad condition, confirm failure for the expected reason, restore the target, and confirm the good case passes.
5. When execution is unsafe or unavailable, record why, the strongest alternative failure-detection evidence, and the limitation on the verdict.

Use mutation testing, a deliberately invalid fixture, a known-bad request, a missing dependency, or a controlled configuration mismatch. Never mutate production merely to prove a check can fail. A0/A1 may rely on logical falsifiability or proportionate review. For A2+ blocking test criteria, demonstrate failure detection when safe; A3/A4 use the strongest practical independent challenge.

An unexecuted negative control does not automatically block every low-risk decision. It does prevent that gate from being the sole basis for `CERTIFIED` when failure-detection capability is material to the reviewed claim. Return a gate-level `BLOCKED` or `UNKNOWN` when the missing demonstration is required by assurance or project policy, or when alternative evidence cannot establish the claim.

Before accepting a generated, recovered, or brownfield criterion, run it against the current implementation where safe. If it passes both known-good and known-bad behavior, or cannot distinguish the behavior it describes, the criterion itself is defective. Classify that separately from an implementation failure.

## 4. Coverage and real-path proof

Before claiming complete coverage:

- enumerate all routes, entry points, consumers, schemas, jobs, configuration writers, UI surfaces, and release paths in scope;
- bind every inventory item to a check or an explicit exclusion;
- for each applicable executable test gate, verify the expected discovered count is nonzero and matches the inventory; otherwise record `N/A` and why no test count applies;
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

Use the dependency graph and evidence states in [delta-first.md](delta-first.md) before reusing or rerunning evidence. Hash equality proves identity, not continued relevance. Missing impact analysis makes a reuse claim `UNKNOWN`; an invalidated gate that was not rerun remains `IMPLEMENTED_UNVERIFIED`.

## 6. Repository, CI, and mandatory forge connection

For any GitHub-backed target or GitHub-hosted material evidence, establish an authenticated GitHub connector before making or accepting a live repository, pull-request, CI, merge, release, deployment, or certification claim. This is a mandatory evidence dependency, not an optional convenience. The connector must expose, as applicable:

- host, exact repository, and authenticated account state without exposing credentials;
- default/target branch and exact head/base commits;
- PR state, draft state, mergeability, review decision, and required checks;
- source, configuration, schema, workflow, and relevant environment revisions in the bounded evidence window;
- GitHub Actions workflow runs and every relevant run attempt, including unsuccessful, cancelled, skipped, timed-out, retried, rerun, superseded, and expected-negative executions;
- jobs, steps, conclusions, discovered test counts, logs, and artifacts for those attempts;
- check name, status, conclusion, evaluated SHA, run/attempt identity, and UTC observation time.

Confirm the connector can read every material surface needed by the claim. Access to a PR summary without Actions logs and artifacts is not sufficient when those logs or artifacts are material. Public search, cached pages, screenshots, local status files, generated indexes, the current check summary, or an executor's narrative cannot replace primary authenticated evidence. If the connector is unavailable, points at the wrong account/repository, or cannot expose a material surface, the affected claim is `UNKNOWN`; do not issue a downstream implementation mandate, merge/release/deployment `GO`, or `CERTIFIED` from that evidence.

For a non-GitHub forge, require the equivalent authenticated native connector or API and the same evidence capabilities. A mandatory connection is read-only by default: it does not imply authority to rerun workflows, edit the repository, merge, release, deploy, or accept risk. Obtain those permissions separately.

The GitHub connector is mandatory but not sufficient for material state held outside GitHub. Inspect external CI, deployment, cloud, runtime, data, or configuration evidence through its authenticated authoritative source and reconcile it into the same evidence window.

Treat repository-local status files and generated indexes as derived views. Reconcile them against exact artifacts and the live forge. A locally recorded green status cannot establish that required remote checks ran on the current head SHA.

GitHub's primary platform documentation defines the relevant evidence surfaces: [workflow runs and attempts](https://docs.github.com/en/rest/actions/workflow-runs), [jobs and all executions](https://docs.github.com/en/rest/actions/workflow-jobs), [run logs and failed steps](https://docs.github.com/en/actions/how-tos/monitor-workflows/use-workflow-run-logs), [artifacts and expiry](https://docs.github.com/en/rest/actions/artifacts), [`continue-on-error` behavior](https://docs.github.com/en/actions/reference/workflows-and-actions/workflow-syntax#jobsjob_idcontinue-on-error), and [required status checks](https://docs.github.com/en/repositories/configuring-branches-and-merges-in-your-repository/managing-protected-branches/about-protected-branches). Recheck current behavior before relying on mutable platform semantics.

## 7. Evidence-Lineage and Failure-Reconciliation Rule

A latest green result is a current-state fact, not sufficient review evidence.

Before accepting an executor's result, issuing the next mandate or `GO`, or declaring an artifact ready, the architect or reviewer must independently reconcile the complete bounded evidence lineage from the last accepted immutable baseline to the exact target under review.

This obligation belongs to the architect or reviewer. It cannot be delegated to, or satisfied solely by, the executor's summary.

### Required procedure

1. **Define the evidence window.** Bind the review to:
   - the last independently accepted immutable baseline;
   - the exact final target identity;
   - every relevant source, configuration, schema, workflow, and environment revision between them.

   If no independently accepted baseline exists, record `NO_PRIOR_ACCEPTED_BASELINE`, choose the earliest immutable boundary justified by the decision—such as the merge base, last release, or initial commit—and mark earlier or unavailable history `UNJUDGED`. If that unjudged history is material to the claim, the affected claim is `UNKNOWN`.

2. **Inventory every attempt.** Inspect primary artifacts for all relevant executions in that window, including:
   - passed;
   - failed;
   - cancelled;
   - timed out;
   - skipped;
   - retried;
   - rerun;
   - superseded;
   - expected RED or mutation runs.

   For CI, inspect workflow runs, jobs, steps, logs, discovered test counts, and artifacts—not only the current check summary.

3. **Preserve failure history.** A later `PASS` may supersede the gate result for an exact newer target, but it never deletes an earlier failure from the review record.

   Every non-successful or anomalous attempt remains an open evidence item until it is explicitly reconciled.

4. **Reconcile every open evidence item.** Record:
   - exact artifact and target identity;
   - UTC time and environment;
   - failing step and observable symptom;
   - expected versus actual scope and counts;
   - classification: product, test, fixture, harness, configuration, environment, infrastructure, expected negative control, or unknown;
   - proven or provisional cause;
   - correction taken, or justified reason no correction was needed;
   - evidence invalidated by the correction;
   - falsifiable proof that the correction addresses the cause;
   - final result on the exact corrected target;
   - remaining uncertainty and residual risk.

   `Flaky`, `transient`, `green after rerun`, and `works now` are not root-cause classifications.

5. **Prove causal closure.** When safe and proportionate, demonstrate that:
   - the original target or a controlled mutation reproduces the failure;
   - the corrected target passes the same oracle;
   - removing the correction makes the relevant gate fail again;
   - unrelated assertions, counts, and safety boundaries were not weakened.

   A rerun on the same SHA can provide evidence about nondeterminism or environment, but it cannot prove that a source correction fixed the defect. A pass on a new SHA requires inspection of the intervening diff and rerunning every invalidated gate.

6. **Verify final-head completeness.** Before acceptance, prove on the exact target:
   - the final Delta Evidence Plan matches the actual delta and includes every unplanned change or discovered coupling;
   - every invalidated, partially invalidated, or newly required claim received its matching proof, and every reused or `N/A` claim retains a valid rationale;
   - all required gates ran;
   - expected discovery counts are nonzero and exact where known;
   - no required step was skipped or silently tolerated;
   - logs and artifacts belong to that target;
   - retry, caching, `continue-on-error`, conditional execution, or workflow ordering did not hide a failure;
   - the working tree, generated artifacts, and external state match the claimed identity.

7. **Run the Result-Acceptance Gate.** The architect or reviewer must complete this reconciliation before producing any downstream implementation task, merge `GO`, release `GO`, deployment `GO`, or certification.

   Executor feedback is an input to this gate, never its verdict.

### Verdict consequences

- A historical failure that is fully explained, causally corrected, and re-proven on the exact target does not block acceptance, but must remain visible under `Errors encountered and corrections`.
- An expected RED or mutation failure is acceptable only when its expected oracle and cleanup are proven.
- Any unexplained failure, missing run, skipped required step, inaccessible material log, unexplained rerun, or mismatch between reported and primary evidence makes the affected claim `UNKNOWN`.
- Any failure still reproducible on the exact target makes the affected gate `FAIL` and the lifecycle state `BLOCKED`.
- The architect or reviewer must not reconstruct missing evidence optimistically or defer reconciliation to a later task.

Gate completion and a `PASS` verdict are distinct. A completed `FAIL` or `BLOCKED` gate may authorize only a bounded diagnostic or corrective task that names and directly addresses the reconciled evidence item; it cannot authorize normal progression or acceptance. `UNKNOWN` permits evidence recovery or an access request, not implementation based on the unknown claim. An incomplete gate authorizes neither.

The Delta Evidence Plan is prospective and the Result-Acceptance Gate is retrospective. The plan selects the necessary reads and proof; Result Acceptance reconciles the complete actual attempt history. Neither substitutes for the other. A broad passing suite cannot compensate for an omitted affected gate, and targeted execution cannot waive an explicitly justified convergence or policy gate.

### Anti-rationalization rule

Never say `all checks are green` as a complete assurance claim when the bounded evidence window contains a failure or correction.

Say instead:

> The exact final target is green after the following reconciled failures and corrections: …

If that sentence cannot yet be completed from primary evidence, the result is not ready for downstream authority.

Use the Result-Acceptance / Evidence-Lineage Record in [templates.md](templates.md). Its gate verdict is `PASS`, `FAIL`, `BLOCKED`, or `UNKNOWN`; it is separate from lifecycle, route, and review verdict namespaces.

## 8. Environment and production acceptance

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

## 9. Retries and external effects

Treat paid, mutating, or externally visible calls as business operations. Require:

- a stable caller-intent or idempotency key;
- atomic or reconciled relationship between durable attempt state and side effects;
- typed outcomes: success, validation failure, retryable failure, terminal failure, refusal, timeout, ambiguous result;
- budget, attempt, time, and concurrency caps;
- policy for late responses and same key with different intent;
- recovery after process restart;
- audit trail linking intent, provider/request identity, cost, and terminal outcome.

Never blindly retry an ambiguous mutation. Reconcile first or park it for explicit resolution.

## 10. Independent review

For A3/A4, require:

- reviewer identity distinct from author;
- fresh or deliberately bounded context;
- exact artifact and evidence packet;
- explicit review scope and severity model;
- findings with evidence and consequence;
- one of `CERTIFIED`, `NOT CERTIFIED`, or `UNKNOWN`, scoped to the reviewed claims;
- a separate exact lifecycle state for the reviewed artifact;
- residual risks and evidence gaps;
- dialogue/re-review after corrections when findings invalidate the original evidence.

Use a bounded doubt cycle:

1. **Claim:** enumerate the blocking claims and the contract each must satisfy.
2. **Extract:** inspect the exact artifact and raw evidence without relying on the author's summary.
3. **Doubt:** attack the highest-severity assumptions, including oracle independence and missing surfaces.
4. **Reconcile:** classify findings, repair or reject invalid evidence, and rerun only invalidated gates.
5. **Stop:** end at the defined exit condition or return `UNKNOWN/BLOCKED`; do not loop until fatigue produces agreement.

Pass the artifact against its contract, not the author's reasoning. Reviewer findings are evidence to reconcile, not an automatic verdict; technically challenge them when contradicted by stronger evidence. Do not issue `CERTIFIED` when a failure-detection limitation is material to a blocking claim and no decision-capable alternative evidence exists.

Before issuing `CERTIFIED` or accepting corrected work, complete the Result-Acceptance Gate in Section 7 against the exact reviewed target. Independent review does not waive evidence-lineage reconciliation; it owns that reconciliation for the reviewed claim.

A different model is useful for reducing correlated blind spots but is still an advisory reviewer. The accountable human or organization retains risk acceptance.

For a budgeted or interrupted review, record the inspected inventory and mark every remaining candidate `UNJUDGED`. Absence of a finding on an uninspected surface is not evidence. Persist each material finding in the review artifact or explicitly decline it with a technical reason.

## 11. Risk assessment

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

## 12. STOP conditions

Stop or return `UNKNOWN/BLOCKED` when:

- current target, branch, commit, build, environment, or executor state is ambiguous;
- destructive, paid, external, merge, migration, release, or production authority is absent;
- an applicable required test gate has an expected count of zero or unknown;
- the oracle shares the same unverified assumption as the implementation;
- the criterion cannot observe the claimed boundary;
- evidence belongs to a different artifact or has expired;
- rollback/recovery is required but absent or untested;
- retry can duplicate an irreversible or paid effect;
- automation has no owner or inhibit during a change window;
- an integration/release/production lane is already owned;
- A3/A4 lacks required independent review or residual-risk owner;
- the required GitHub or native-forge connector is unauthenticated, points to the wrong identity, or cannot expose material repository/CI evidence for a live verdict;
- the bounded evidence window is undefined, a relevant attempt is missing, or a historical failure, cancellation, skip, timeout, rerun, or anomaly remains unreconciled;
- a material log or artifact is inaccessible or expired and no independent primary evidence can establish the affected claim;
- A2+ implementation or review lacks a complete Delta Evidence Plan, or the plan does not cover the actual final delta;
- transitive impact is unknown but inspection/testing was not broadened, or an invalidated/newly required claim has no matching proof;
- the Result-Acceptance Gate is incomplete for a requested downstream implementation mandate, merge/release/deployment `GO`, or certification;
- canonical and superseded instructions cannot be distinguished.

## 13. Review lenses

Review in this order:

1. **Requirements:** Does the change solve the stated problem without silently changing scope?
2. **Correctness:** Are normal, boundary, concurrent, retry, and partial-failure paths sound?
3. **Security/privacy:** Are trust boundaries, authorization, secrets, input/output, and dependencies safe?
4. **Data/recovery:** Can data be lost, duplicated, corrupted, or made irreconcilable? Is recovery proven?
5. **Compatibility:** Are APIs, schemas, clients, mixed versions, and migrations handled?
6. **Operability:** Are identity, logs, metrics, alerts, rollout, rollback, and automation behavior adequate?
7. **Delta and impact:** Is the exact delta complete, are direct and transitive consumers traced, are evidence reuse/invalidation states justified, and are convergence triggers explicit?
8. **Evidence lineage:** Is every relevant attempt from the last accepted baseline to the exact target present, independently reconciled, and causally closed where proportionate?
9. **Test adequacy:** Do tests exercise every invalidated/new claim at the matching boundary, avoid unrelated execution without reason, have a trustworthy oracle, and prove they can fail?
10. **AI/ML complexity:** When applicable, is there a credible baseline, attributable experiment, and justified promotion after lifecycle cost and risk?
11. **Simplicity:** Is every abstraction, dependency, layer, and line needed now?

Report defects separately from optional improvements. Avoid drowning a blocking finding in style commentary.

## 14. Extensions, hooks, and diagnostic actions

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

## 15. AI/ML complexity evidence

For AI/ML introduction or material lifecycle-complexity growth, the generic Gate Record is necessary but not sufficient. Add the Baseline, Experiment, and Complexity-Promotion contracts from [ai-complexity-strategy.md](ai-complexity-strategy.md). For other AI changes, use that reference's trigger matrix rather than forcing an inapplicable promotion gate.

Treat the following as first-class artifact and dependency identities when applicable: model/provider/version/settings, prompt and schema, tool and routing policy, training/fine-tuning/retrieval/evaluation data, labels and split logic, embedding/index/knowledge snapshot, evaluator or human-review rubric, randomness treatment, runtime configuration, and observation time.

Block promotion when there is no credible baseline, no named gap, no decision-capable evaluation, material undisclosed differences between experiment arms, evidence contamination, a breached guardrail, improvement that does not cross the practical-equivalence margin or qualitative decision boundary, uncertainty that prevents the claimed conclusion, or missing lifecycle ownership/fallback/rollback. Use the AI Complexity Decision Record in [templates.md](templates.md) to preserve the decision and invalidation dependencies.
