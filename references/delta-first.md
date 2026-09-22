# Delta-First Evidence and Test-Selection Rule

Do not begin by rereading every artifact or running every available test.

First determine what changed, what depends on it, which claims that change invalidates, and which evidence is necessary to restore confidence in those claims.

Use this sequence:

`delta → transitive impact → reachable risks → invalidated claims → required proof → targeted execution → final convergence if justified`

Delta-first is dependency-based, not file-based. An unchanged file, test, or component may still be affected through a shared contract, schema, adapter, configuration, migration, workflow, generated artifact, or runtime dependency.

## 1. Establish the exact delta

Bind:

- last accepted immutable baseline;
- exact target identity;
- source, schema, configuration, workflow, dependency, and environment changes between them;
- changed generated artifacts and external interfaces.

Do not use the working-tree diff alone when commits, generated files, migration state, image contents, or configuration also matter. If no independently accepted baseline exists, use the `NO_PRIOR_ACCEPTED_BASELINE` convention and limits defined in [evidence-and-gates.md](evidence-and-gates.md).

## 2. Build the impact graph

Trace each changed artifact to:

- contracts and invariants it owns;
- direct consumers;
- transitive consumers;
- persistent data and migrations;
- background jobs and automation;
- build, CI, and release paths;
- operator and user-visible behavior;
- rollback and recovery paths.

If the dependency boundary is unknown, classify it as uncertainty and broaden inspection. Do not assume that an unchanged consumer is unaffected.

## 3. Classify existing evidence

For every relevant claim or gate, assign exactly one state:

- **Invalidated (`INVALIDATED`)** — a dependency, oracle, environment, or target identity changed; rerun is required.
- **Partially invalidated (`PARTIALLY_INVALIDATED`)** — only a defined subset changed; run focused proof for that subset.
- **Reusable (`REUSABLE`)** — all material dependencies, oracle, environment, TTL, and target assumptions remain valid; cite the existing evidence and explain why.
- **Newly required (`NEWLY_REQUIRED`)** — the change introduces a new claim, failure mode, or boundary with no prior proof.
- **N/A** — the gate does not apply, with an explicit reason.
- **Unknown (`UNKNOWN`)** — dependency impact cannot be established.

Hash equality proves artifact identity, not relevance. A sealed artifact need not be reread in full when unchanged, but the sections governing an invalidated claim must be read and understood.

## 4. Select only necessary tests

Run the smallest test set that proves every invalidated or newly introduced claim at its matching V-model boundary:

- changed local logic → focused unit and regression tests;
- changed component contract → component and contract tests;
- changed shared boundary → tests for every direct and transitive consumer;
- changed database schema or migration → fresh, upgrade, repeat/no-op, data-preservation, and rollback-compatibility tests;
- changed workflow or test harness → workflow execution, discovery counts, skipped-step protection, and a negative control proving the gate can fail;
- changed runtime configuration or deployment topology → configuration, system, rollback, and staged real-world checks;
- repaired defect → original reproducer, corrected behavior, and nearby regression boundary;
- changed test oracle → mutation or negative control proving the revised test still detects the prohibited behavior.

Do not run unrelated tests merely to create a larger `PASS` count.

Do not omit affected tests merely because their source files were unchanged.

## 5. Escalate to broader testing only when justified

A full suite or broad convergence gate is required when:

- a shared foundation, framework, adapter, schema, build system, lockfile, or global configuration changed;
- the dependency graph is incomplete or unreliable;
- multiple components or persistence boundaries changed together;
- targeted tests expose unexpected coupling;
- the release policy explicitly requires final convergence;
- A3/A4 risk requires system-level proof;
- the next transition is a release, migration, deployment, or production acceptance boundary whose named reachable risk or explicit policy requires broad convergence.

Record why broad testing is necessary. `More tests feel safer` is not sufficient justification.

Run an expensive broad gate once on the exact final target unless a later change invalidates it.

## 6. Order tests by information value

Prefer:

1. static and structural checks;
2. focused unit/regression tests;
3. contract and integration tests;
4. migration and recovery tests;
5. system/end-to-end tests;
6. staged production or real-world acceptance.

Stop early on a blocking failure. Do not continue expensive downstream gates whose prerequisites failed unless diagnostic evidence specifically requires it.

## 7. Control evidence and context cost

- Preserve complete raw logs outside the active context.
- Load summaries, counts, and relevant failure intervals first.
- Expand raw evidence only when a claim, anomaly, or contradiction requires it.
- Reference unchanged sealed evidence instead of reproducing it.
- Avoid repeating the same full suite locally, in CI, and in review without an explicit independence reason.
- Estimate expensive reads and test runs before execution.
- If the evidence plan materially exceeds its expected budget, checkpoint and justify the expansion before continuing.

Cost reduction must never remove a proof required by risk, trust boundary, persistence, rollback, security, accounting, or real-world acceptance.

## 8. Produce a Delta Evidence Plan

Before implementation or review, record:

| Field | Required content |
|---|---|
| Baseline | Last accepted immutable identity |
| Target | Exact identity under work or review |
| Delta | Source, schema, config, workflow, dependency, and environment changes |
| Impact | Direct and transitive affected surfaces |
| Next transition | Exact proposed lifecycle transition, exposure cap, checkpoint, and rollback boundary |
| Reachable risks | Failure modes that can become real before that checkpoint after current controls |
| Invalidated claims | Claims whose earlier evidence can no longer be reused |
| Reused evidence | Exact evidence plus dependency-based reuse rationale |
| Required tests | Smallest sufficient test set and matching V-model level |
| Broad gates | Any full-suite or system gate and why it is necessary |
| Expansion triggers | Conditions that require broader inspection or testing |
| Evidence budget | Expected expensive reads, executions, and context load |

No implementation, review certification, or downstream `GO` may proceed without this plan for A2+ work.

## 9. Interaction with next-step scope and evidence lineage

Delta-First determines what changed and which proof was invalidated. [next-safe-step.md](next-safe-step.md) determines which of those controls and claims are required before the exact next transition rather than before a later unattended or scaled end state.

- Select proof for every invalidated claim material to the next transition and every applicable governing-policy gate; record both in `NEXT-STEP BLOCKERS`.
- Do not omit affected proof merely because exposure is bounded.
- Do not add unrelated proof merely because the desired end state will eventually need it.
- Recompute residual risk after each accepted control; a changed next transition or newly reachable risk invalidates the affected selection plan.
- Automatically triggered post-transition checks are telemetry unless they prove a named blocker or policy claim.

The Delta Evidence Plan is the prospective selection contract: it determines which claims and gates need new proof before work or review. The Result-Acceptance Gate in [evidence-and-gates.md](evidence-and-gates.md) is the retrospective acceptance contract: it reconciles what actually ran, including every relevant failure, skip, retry, rerun, correction, and invalidated result.

- A Delta Evidence Plan never erases an attempt from the bounded evidence lineage.
- A new failure, contradiction, unexpected coupling, or unplanned change invalidates the affected part of the plan; update the impact graph and test selection before continuing.
- Targeted evidence cannot waive a project-required convergence gate, and a broad gate cannot compensate for a missing affected test.
- Reused evidence must remain linked to its exact identity, dependencies, TTL, oracle, and environment.

## Verdict consequences

- Missing impact analysis makes reuse claims `UNKNOWN`.
- An invalidated gate that was not rerun remains `IMPLEMENTED_UNVERIFIED`.
- Unexplained selection of only nearby tests is insufficient for shared or transitive changes.
- Repeating unaffected tests does not compensate for a missing affected test.
- If all invalidated claims receive matching proof and reusable evidence remains valid, unrelated tests and documents should not be reread or rerun.

## Anti-rationalization rule

Neither of these statements is acceptable:

> Run everything to be safe.

> Only test the files that changed.

The required statement is:

> Run every test needed to prove the claims invalidated by the transitive impact of the change, and no unrelated test without a stated convergence or policy reason.

## Primary references

These sources support the dependency and test-selection mechanics; they do not mandate a particular tool:

- [Microsoft Test Impact Analysis](https://learn.microsoft.com/en-us/azure/devops/pipelines/test/test-impact-analysis?view=azure-devops) selects relevant tests from dependency mappings, includes new and previously failing tests, and falls back to the full set when impact cannot be understood.
- [Bazel Query Guide](https://bazel.build/query/guide) documents direct, implicit, transitive, and reverse-dependency analysis, including finding what depends on a changed target.
- [GitHub Compare Commits API](https://docs.github.com/en/rest/commits/commits#compare-two-commits) provides an immutable baseline-to-target commit comparison; it is one delta input, not a complete runtime-impact graph.
- [Develocity Predictive Test Selection](https://docs.develocity.ai/2026.2/guides/predictive-test-selection/) documents change-aware selective execution, the need to capture all relevant test inputs, and later comprehensive execution when release assurance requires it.
