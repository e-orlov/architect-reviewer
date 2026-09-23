# Testing strategy and execution pipeline

## Contents

1. Purpose and operating rule
2. Build the strategy from the V-model trace
3. Stage-by-stage pipeline
4. Test-level contracts
5. Select critical paths and failure paths
6. Structure test scenarios
7. Verify APIs and contracts
8. Use coverage as evidence, not a target substitute
9. Record environment differences
10. Select regression scope
11. Scale by assurance and close with evidence
12. Primary references

## 1. Purpose and operating rule

Use this reference whenever executable behavior changes or test adequacy is reviewed. Keep two dimensions distinct:

- a **test level** names the boundary being proved: static, unit, component, contract, integration, system/end-to-end, or acceptance;
- an **execution stage** names where and when evidence is produced: local, pull request/CI, shared integration, staging/preproduction, or progressive production acceptance.

Do not equate a stage with a level. A contract test may run locally and in CI; a system test may run in an isolated local stack and again against a release candidate. Run each check at the earliest environment where its claim is credible, then rerun it only when a changed boundary, environment, or policy invalidates the earlier evidence.

Apply [delta-first.md](delta-first.md) before selecting tests: establish the exact baseline-to-target delta, trace direct and transitive impact, classify prior evidence, then run the smallest sufficient proof at the matching boundary. A changed-file list is not an impact graph. A2+ work requires the Delta Evidence Plan from [templates.md](templates.md) before implementation or review.

Scope the required proof with [next-safe-step.md](next-safe-step.md): name the exact next transition and reachable residual risks, prove every `NEXT-STEP BLOCKER`—including applicable gates with basis `GOVERNING_POLICY`—and defer unrelated `END-STATE HARDENING` to its activation boundary. Bounded exposure does not excuse missing proof for a claim required now; other affected claims retain a named later activation boundary. A theoretical maximum does not make an otherwise unrelated test blocking; apply [the worst-case gate challenge](worst-case-gates.md).

Prefer the repository's existing test tools and conventions. Do not introduce Playwright, Cypress, Cucumber, a SAST product, or another framework merely because it appears in an example. Add or replace tooling only when the current stack cannot prove a required invariant and the lifecycle, permissions, cost, maintenance, and rollback are acceptable.

## 2. Build the strategy from the V-model trace

For every blocking requirement or risk-control row, define:

1. the V-model level and exact boundary to prove;
2. the defect or prohibited outcome the check must detect;
3. the earliest credible execution stage;
4. any higher-level stage needed to prove wiring, topology, deployment, or real use;
5. the production symbol, route, contract, build, configuration, or runtime exercised;
6. the oracle and expected values;
7. the expected discovered test count or enumerated scenarios, or `N/A` with reason when no executable test applies;
8. the logical counterexample and, when assurance requires and safety permits, a negative-control execution; otherwise the limitation and alternative evidence;
9. the environment identity and known differences from the target environment;
10. the evidence artifact, invalidation dependencies, owner, and next authority.
11. whether the claim is a `NEXT-STEP BLOCKER` based on `REACHABLE_RISK` or `GOVERNING_POLICY`, or belongs to later hardening.

For existing evidence, also assign exactly one delta state: `INVALIDATED`, `PARTIALLY_INVALIDATED`, `REUSABLE`, `NEWLY_REQUIRED`, `N/A`, or `UNKNOWN`. Cite dependency, identity, TTL, environment, and oracle rationale for reuse. Broaden inspection when impact is unknown.

Choose tests from requirements and risks, not from a desire to fill every layer. A lower-level check cannot close a higher-level claim. A browser E2E test cannot replace focused state-machine proof, and a unit test cannot establish deployed routing or user acceptance.

## 3. Stage-by-stage pipeline

Use this as a menu of execution stages, then select those needed by the affected claims, next transition, and policy. Record an omission when an otherwise applicable claim, risk, or policy makes that stage a reasonable candidate; do not create a waiver for every irrelevant row.

| Stage | Primary purpose | Typical checks | Exit evidence |
|---|---|---|---|
| Specification and planning | Define proof before implementation | Exact delta, transitive-impact graph, Delta Evidence Plan, Next-Safe-Step Record, executable acceptance criteria, V-model trace, risk and affected-surface inventory, oracle and negative-control design | Every relevant claim has one evidence state; every next-step blocker has matching proof; later hardening has an activation boundary |
| Local inner loop | Find narrow defects quickly | Formatting, linting, compilation/type checks, configured SAST and secret checks, focused unit tests, component tests, lightweight contract tests | Named commands, target identity, applicable nonzero expected counts or justified `N/A`, raw failures or passes |
| Pull request / CI | Reproduce the change in a clean, reviewable context | Deterministic local checks, affected and policy-required suites, component/API/contract/integration tests, migration checks, build/package checks, configured security and dependency scans | Authenticated forge evidence bound to exact repository/head SHA; all relevant run attempts, jobs, steps, expected counts, logs, results, and artifacts |
| Shared integration environment | Prove composition across real boundaries | Service/database/queue integration, provider-consumer compatibility, auth and serialization, jobs, failure injection, restart and recovery | Deployed identities, dependency/config identity, reconciled data and side effects |
| Staging / preproduction | Prove the release candidate in a target-like topology | Critical-path system/E2E, impacted regression, accessibility/performance/recovery checks when required, rollback rehearsal where safe | Release identity, environment-difference register, scenario results, residual gaps |
| Progressive rollout / production acceptance | Validate actual routing and user/operational outcome | Non-destructive smoke and real-life acceptance, canary/cohort observation, SLI and business guardrails, side-effect reconciliation, rollback trigger | Deployed identity, cohort/window, observed values, acceptance or rollback verdict |

Do not postpone cheap deterministic checks to CI when they can run locally. Do not make local execution a prerequisite when the developer environment cannot credibly reproduce the boundary. Keep merge, release, deployment, and acceptance as separate states.

## 4. Test-level contracts

| Level | Prove | Include | Do not claim |
|---|---|---|---|
| Static quality and security | Source or artifact satisfies mechanically inspectable rules | Formatter/linter, compiler/type checker, SAST, secret/IaC/dependency checks when applicable | Runtime behavior or absence of all vulnerabilities |
| Unit | One local unit of behavior satisfies its contract in isolation | Normal, boundary, invalid, and state-transition cases with controlled dependencies | Database, network, serialization, wiring, or user outcome |
| Component | An owning component satisfies its public contract | Real component entry point, realistic dependency behavior, persistence adapter or UI component boundary as appropriate | Cross-service composition unless exercised |
| API / contract | Provider and consumer agree on interface and failure semantics | Request/response or event schema, compatibility, auth, validation, errors, idempotency, timeout/retry semantics | Implementation correctness behind an unobserved contract |
| Integration | Multiple real components compose correctly | Database, queue, filesystem, service, provider, transaction, migration, restart, and partial-failure behavior as relevant | Full user journey or production routing unless present |
| System / E2E | The assembled system meets observable requirements | Critical user or machine journeys in the declared topology, including decisive failure paths | Exhaustive local invariants or every combinatorial edge case |
| Regression | Previously working or repaired behavior remains correct | Original defect, affected consumers, adjacent boundaries, and policy-required suite | Complete protection without an affected-surface inventory |
| Acceptance / operational | The delivered identity solves the real need safely | User-visible result, actual routing, data integrity, operational signals, rollout and rollback criteria | Future reliability outside the observation window |

Keep tests deterministic, isolated where the level permits, self-checking, and behavior-focused. Use doubles to control irrelevant dependencies, not to hide the boundary whose behavior is being claimed.

## 5. Select critical paths and failure paths

Use E2E and system tests for paths whose cross-boundary behavior materially affects users or operations. Prioritize:

- the principal user or machine journey that delivers the feature's value;
- authorization, payment, irreversible action, persistent-data, safety, privacy, and compliance boundaries;
- compatibility paths used by material consumers;
- timeout, retry, idempotency, concurrency, partial success, restart, and recovery where relevant;
- the original production symptom for a defect;
- rollback or safe-degradation behavior for A3/A4 changes.

Do not attempt to enumerate every input through E2E. Push combinatorial input coverage down to unit, component, or contract levels and retain only representative boundary-spanning scenarios at system level. For A2+ blocking critical journeys, cover at least one decisive negative or failure path when safe. If execution is unsafe or unavailable, preserve the logical counterexample, alternative evidence, and verdict limitation; a happy path alone is not sufficient for a material blocking claim.

## 6. Structure test scenarios

### AAA for unit, component, and integration tests

Use Arrange–Act–Assert when it makes the test's intent clearer:

- **Arrange:** create the minimum state, fixtures, dependencies, and inputs needed for the criterion;
- **Act:** perform one primary behavior or transition;
- **Assert:** compare observable output and required side effects with a trustworthy expected result; record any shared assumption that limits oracle independence.

Name the behavior, scenario, and expected result. Keep the Act singular where practical, avoid reproducing production logic in the expected-value calculation, and assert meaningful outcomes rather than incidental implementation details. Use another structure when property-based, state-machine, concurrency, or lifecycle testing communicates the contract more accurately; AAA is a clarity convention, not a reason to distort the test.

### BDD/Gherkin: Given–When–Then for acceptance and system behavior

Express business-facing criteria as:

- **Given:** a relevant, observable initial context;
- **When:** one user action, external event, or system trigger;
- **Then:** an observable outcome for the user, consumer, or operator.

Treat BDD as collaborative specification of observable behavior and Gherkin as one optional syntax for expressing it. Add `And` or `But` only when they preserve readability. Keep implementation details out of the scenario and make the Then clause falsifiable. Use Gherkin files only when executable specifications and stakeholder collaboration justify the tooling; otherwise use Given–When–Then directly in requirements, test names, or tables.

Example:

```gherkin
Given an authenticated customer has an eligible basket totaling 100 EUR
When the customer applies a valid 10 percent promotion
Then the displayed and persisted payable total is 90 EUR
And one promotion application is recorded
```

## 7. Verify APIs and contracts

For a changed REST, GraphQL, RPC, event, CLI, or file contract, select the applicable assertions:

- operation, route/topic, method, version, and content type;
- success HTTP status or equivalent outcome and JSON, GraphQL, RPC, or event schema;
- required, optional, nullable, defaulted, and unknown fields;
- authentication and authorization for allowed and forbidden actors;
- input validation, boundary values, error status, typed error body, and safe error detail;
- backward/forward compatibility and provider-consumer expectations;
- idempotency, duplicate delivery, ordering, timeout, cancellation, retry, and late response;
- persistence, emitted events, audit records, and absence of unintended side effects;
- pagination, filtering, sorting, rate/budget limits, and concurrency when in scope.

Assert semantic behavior, not irrelevant serialization details such as object-field order. Exercise the real production handler and serialization path whenever direct function calls or mocks could hide routing, middleware, authentication, schema, or persistence defects.

## 8. Use coverage as evidence, not a target substitute

Do not import a universal 70–80% or any other percentage. Let project policy and accountable owners define thresholds from business criticality, change frequency, expected lifetime, complexity, and testability.

Apply these controls:

1. Inventory changed and affected behaviors before reading a coverage number.
2. For each applicable test gate, confirm expected tests were discovered and the count is nonzero; record `N/A` with reason for a non-executable claim.
3. Inspect changed-code and critical-branch coverage where the project supports it.
4. Explain uncovered blocking behavior or add the missing criterion.
5. Document justified exclusions such as generated code or unreachable defensive branches.
6. Pair coverage with behavior assertions and, where assurance and safety require it, negative controls, mutation testing, or known-bad fixtures.
7. Reject percentage-only completion claims; execution without a trustworthy oracle is not proof.

A high percentage can coexist with incorrect expectations, mocked-away wiring, missing consumers, or untested failure semantics. A lower percentage can be adequate only when the omitted behavior is inventoried and justified against the actual risk.

## 9. Record environment differences

Never state that staging is identical to production without exact evidence. Describe staging or preproduction as **target-like**, then maintain an environment-difference register for every acceptance-relevant dimension:

| Dimension | Record |
|---|---|
| Source and artifacts | Commit, build/image/package, dependency lock, schema and migration level |
| Configuration | Environment variables, defaults, feature flags, limits, timeouts and retry policy |
| Data | Fixtures or anonymized data, volume, distribution, age, integrity and prohibited production data |
| Topology | Replicas, regions, network paths, proxies, caches, queues, schedulers and failover |
| Identity and access | Accounts, roles, credentials, certificates, secrets and trust boundaries |
| External dependencies | Real service, sandbox, emulator or double; version, quota, rate and cost behavior |
| Load and timing | Traffic, concurrency, latency, clock, background work and observation window |
| Operations | Logging, metrics, traces, alerts, automation, backup, rollback and operator ownership |

For each difference, state which criterion it can invalidate and how the residual gap will be closed: a lower-level proof, a production-safe probe, progressive exposure, monitoring, accountable risk acceptance, or `BLOCKED/UNKNOWN`. Treat an unknown material difference as an evidence gap, not as parity.

## 10. Select regression scope

Build regression scope from the affected-surface inventory:

1. preserve a test for the original defect or behavior;
2. enumerate callers, consumers, routes, schemas, jobs, UI surfaces, configuration writers, and release paths affected by the change;
3. add focused tests at the owning boundary and representative tests across changed contracts;
4. run the project's required baseline suite;
5. expand impact analysis when a shared contract, schema, foundational utility, cross-cutting configuration, security boundary, or broad refactor makes the affected boundary uncertain; run the necessary broad tests or full suite only if the uncertainty cannot be bounded more narrowly or policy requires it;
6. record exclusions and the evidence used to justify them.

Include direct and transitive consumers reached through contracts, schemas, adapters, configuration, migrations, workflows, generated artifacts, build/release machinery, and runtime dependencies even when their files are unchanged. Do not use directory proximity as a substitute for impact analysis.

Do not rerun every expensive test by reflex when dependency analysis proves it unaffected. Do not narrow the suite merely to save time when the impact inventory is incomplete.

These changes or discoveries trigger a broader impact review: shared foundations, frameworks, adapters, schemas, build systems, lockfiles, global configuration, incomplete dependency graphs, unexpected coupling, or multiple changed persistence boundaries. Escalate testing only to the breadth needed to close a named residual risk or uncertainty; use a full suite when no narrower boundary is defensible or when applicable policy requires it. A named release/migration/deployment claim or residual A3/A4 exposure can justify system proof without automatically justifying every test. Record the reason and run an expensive broad gate once on the exact final target unless a later change invalidates it.

## 11. Scale by assurance and close with evidence

| Assurance | Minimum testing posture |
|---|---|
| A0 | Validate factual/document claims; executable tests are optional unless the artifact itself runs |
| A1 | Focused local static/unit/component proof; CI or higher level when the changed boundary requires it |
| A2 | Affected local and CI suites plus contract/integration proof for material boundaries; target-like system proof when environment-sensitive |
| A3 | Required automated proof, failure/recovery paths, target-topology evidence, independent review, staged rollout, and real-world acceptance |
| A4 | A3 plus strongest available adversarial verification, rehearsed recovery or formal justification, explicit residual-risk acceptance, and retained evidence |

Close each blocking gate with the Gate Record from [templates.md](templates.md). Report the exact artifact and environment, applicable expected and actual counts or justified `N/A`, oracle and independence limits, logical counterexample, negative-control status, raw outcome, UTC time, invalidation dependencies, residual gaps, verdict, and next authority. A green local or CI suite leaves deployment and real-world acceptance open.

Before an architect or reviewer accepts an executor's test result as the basis for the next implementation mandate or any merge/release/deployment/certification decision, complete the Result-Acceptance Gate in [evidence-and-gates.md](evidence-and-gates.md) for the exact next transition. Inventory every relevant required attempt in the bounded baseline-to-target window and preserve failed, cancelled, timed-out, skipped, retried, rerun, superseded, expected RED, and mutation evidence until explicitly reconciled. For GitHub-backed evidence, use the mandatory authenticated GitHub connector; the latest check summary is insufficient.

Order new execution by information value: static/structural, focused unit/regression, contract/integration, migration/recovery, system/E2E, then staged production or real-world acceptance. Stop after a blocking prerequisite failure unless a downstream action is specifically required for diagnosis. Preserve raw logs outside the active context; load summaries, counts, and relevant failure intervals first. Estimate expensive reads and runs in the Delta Evidence Plan and checkpoint before material budget expansion.

Treat automatically triggered post-transition checks as telemetry unless a named blocker or governing policy maps to them. Do not wait for, poll, or inspect them merely because they exist. Run a convergence gate on the exact final artifact only when a named trigger or governing policy justifies one; repeat it only when a later change invalidates its evidence or an explicit independence claim requires another execution.

## 12. Primary references

This strategy adopts concepts, not vendor mandates:

- [Microsoft: Unit testing best practices](https://learn.microsoft.com/en-us/dotnet/core/testing/unit-testing-best-practices) — fast, isolated, repeatable, self-checking unit tests; Arrange–Act–Assert; and the warning that coverage percentage alone does not establish quality.
- [Cucumber: Gherkin reference](https://cucumber.io/docs/gherkin/reference/) — Given–When–Then as initial context, event, and observable expected outcome in executable specifications.
- [OWASP: Source Code Analysis Tools](https://owasp.org/www-community/Source_Code_Analysis_Tools) — source-code analysis and SAST as static security checks, not runtime proof.
- [Google Testing Blog: Code Coverage Best Practices](https://testing.googleblog.com/2020/08/code-coverage-best-practices.html) — no universal ideal coverage number; targets depend on product criticality and context.
- [Playwright: Best Practices](https://playwright.dev/docs/best-practices) — test user-visible behavior and isolate browser tests; Playwright itself remains optional.
- [Microsoft: Test Impact Analysis](https://learn.microsoft.com/en-us/azure/devops/pipelines/test/test-impact-analysis?view=azure-devops) — dependency-based relevant-test selection, inclusion of new and previously failing tests, manual selection validation, and safe full-suite fallback when impact is unknown.
- [Bazel: Query Guide](https://bazel.build/query/guide) — direct, implicit, transitive, and reverse-dependency analysis; Bazel itself remains optional.
- [GitHub: Compare two commits](https://docs.github.com/en/rest/commits/commits#compare-two-commits) — immutable baseline-to-target commit comparison as one input to delta analysis.
- [Develocity: Predictive Test Selection](https://docs.develocity.ai/2026.2/guides/predictive-test-selection/) — selective execution based on changes and test inputs, reporting of selected/skipped tests, and later comprehensive execution where lifecycle assurance requires it; the product and its predictive model are optional.

Apply these references through the V-model, task route, assurance level, and evidence rules of this skill. Where a project standard is stricter and justified, follow it; where a cited example is stack-specific, preserve the principle and use the project's native toolchain.
