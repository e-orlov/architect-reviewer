# Task routes and assurance levels

## Contents

1. Route selection
2. V-model overlay
3. Idea route
4. Feature route
5. Bug route
6. Refactor and migration route
7. Incident route
8. Release route
9. Review and audit route
10. AI/ML complexity overlay
11. Assurance controls
12. Proportionality and parallelism

## 1. Route selection

Choose one primary route. Add a secondary route only when the work genuinely crosses a boundary, such as a bug fix that requires a production release.

| Need | Primary route | Required terminal result |
|---|---|---|
| Decide whether to invest | Idea | `GO`, `CLARIFY`, or `STOP`, with evidence |
| Add or materially change behavior | Feature | Verified requirements and implementation evidence |
| Repair broken behavior | Bug | Assessed cause, scoped repair, original-symptom verification |
| Improve structure or move data/contracts | Refactor/migration | Behavior lock, compatibility and rollback evidence |
| Restore degraded service | Incident | Stabilized service, verified recovery, follow-up controls |
| Move an artifact toward users | Release | Exact identity, staged exposure, monitoring, rollback, acceptance |
| Judge an existing claim or artifact | Review/audit | Findings, evidence gaps, typed verdict, residual risk |

Do not force a full feature lifecycle onto a narrow bug. Do not start a significant feature with code before defining what and why.

## 2. V-model overlay

The route chooses the sequence; the V-model checks completeness inside it. For every route:

1. identify the highest left-side definition needed: outcome, requirement, architecture contract, component contract, or local invariant;
2. define the matching right-side proof at the same time;
3. trace the row through design owner, implementation slice, criterion, evidence, and lifecycle state;
4. keep verification of the specified contract distinct from validation of the real need;
5. reject a terminal claim while any blocking row is orphaned, uses the wrong proof level, or has stale evidence;
6. use [delta-first.md](delta-first.md) to map the exact delta through direct and transitive impact, classify existing evidence, and select the smallest sufficient proof; record the Delta Evidence Plan before A2+ implementation or review;
7. before using an executor result to authorize the next implementation task or any merge/release/deployment/certification decision, complete the Result-Acceptance Gate across the bounded evidence lineage in [evidence-and-gates.md](evidence-and-gates.md); only `PASS` permits progression, while a completed non-pass verdict permits only the bounded response defined by that contract.
8. use [next-safe-step.md](next-safe-step.md) to scope controls and proof to the exact next lifecycle transition; separate `NEXT-STEP BLOCKERS` from `END-STATE HARDENING`, and recompute residual risk after each accepted control.

Use [v-model.md](v-model.md) for the full traceability contract.

## 3. Idea route

Use: `intake → research → define → shape → decide`.

1. Capture the problem, beneficiaries, constraints, and decision deadline.
2. Separate facts from hypotheses.
3. Research the current state, alternatives, costs, risks, and reversibility.
4. Define the smallest outcome worth buying, not a preferred implementation.
5. Shape at least one credible alternative and a do-nothing baseline.
6. Decide `GO`, `CLARIFY`, or `STOP`; list the evidence that would change the decision.

A stopped idea with a documented reason is a valid result.

## 4. Feature route

Use one of two proportional paths:

- **Base:** `constraints → specify → clarify as needed → plan → tasks → implement → converge`.
- **Enhanced:** `constraints → specify → clarify → plan → checklist → tasks → analyze → implement → converge`.

The base path normally fits A0/A1 work. Use the enhanced path for A3/A4 and for A2 when material ambiguity, multiple components, compatibility, persistent data, or consequential boundaries make checklist and cross-artifact analysis decision-relevant. If A2 omits either quality gate, record why the base path is sufficient. Project policy may always require the enhanced path.

1. Confirm governing principles and quality constraints; define them once if missing.
2. Specify WHAT and WHY: observable behavior, non-goals, users, interfaces, data, and failure semantics; defer HOW until planning.
3. Clarify material ambiguity before planning; on the base path, clarify only what is decision-relevant. Preserve unresolved points as `UNKNOWN`, not invented detail.
4. Map requirements to acceptance criteria and paired V-model verification before choosing implementation structure.
5. Plan architecture, compatibility, observability, rollout, rollback, and risk.
6. On the enhanced path, have a reviewer-owned requirements checklist test clarity, completeness, consistency, measurability, and boundary coverage after the plan exposes the relevant design context. It reviews requirements, not implementation completion.
7. Split the dependency graph into small vertical tasks with one primary invariant each; give every task acceptance and verification.
8. On the enhanced path, analyze consistency across requirements, plan, checklist, tasks, risks, and trace rows before implementation.
9. For A2+ work, complete the Delta Evidence Plan: exact delta, transitive impact, evidence states, targeted proof, convergence reasons, expansion triggers, and evidence/context budget.
10. Implement incrementally, collecting evidence at the matching boundary and checkpointing reviewable batches. Update the Delta Evidence Plan when actual changes or discoveries expand impact.
11. Converge code, docs, tests, configuration, contracts, release controls, and operational artifacts only where the final delta or policy invalidates them.

Do not call the feature complete when required verification is absent.

## 5. Bug route

Use: `reproduce → assess → localize → repair → verify → guard`.

1. Capture the original symptom and exact environment.
2. Reproduce it or state why reproduction is unavailable.
3. Trace the real path and classify the narrowest owning cause.
4. Trace direct and transitive consumers of the violated invariant; classify which prior proof is invalidated, reusable, or newly required.
5. Make the criterion logically falsifiable. Execute a negative control when the assurance level requires it and doing so is safe; otherwise record the limitation and alternative evidence.
6. Repair the cause, not only the visible symptom.
7. Verify the original symptom, corrected behavior, affected consumers, and nearby regression surface; broaden only when impact is unknown or a convergence trigger applies.
8. Add the smallest durable guard against recurrence.

Classify red evidence before editing production code: implementation defect, stale fixture, invalid expectation, oracle defect, or environment mismatch.

## 6. Refactor and migration route

Use: `baseline → contract lock → stage → reconcile → cut over → retire`.

1. Record existing behavior and consumers.
2. Define compatibility, data-integrity, and rollback invariants.
3. Establish the exact baseline-to-target delta and a baseline that can detect unintended change.
4. Map direct/transitive consumers, migrations, mixed versions, build/release paths, and recovery dependencies in the Delta Evidence Plan.
5. Stage reversible steps and preserve mixed-version compatibility when needed.
6. Reconcile data and configuration before cutover.
7. Cut over with exact identity, monitoring, and a tested rollback.
8. Remove old paths only after consumers and recovery obligations are closed.

For destructive migrations, require backup/restore proof and accountable risk acceptance.

## 7. Incident route

Use: `detect → stabilize → contain → recover → verify → learn`.

1. Establish incident command, impact, time, and current system state.
2. Stabilize the service and stop harmful automation or propagation.
3. Contain blast radius; preserve evidence.
4. Recover to a known-good state using the safest reversible action.
5. Verify user-visible service, data integrity, and automation recovery.
6. Write a blameless postmortem with owned preventive actions.

After stabilization and after each material control lands, reassess the next proposed transition from the new residual risk. The original incident severity does not permanently set the assurance level or keep every desirable control on the critical path.

Do not let deep root-cause exploration delay necessary containment.

For urgent A2+ containment, record a minimal provisional Delta Evidence Plan before mutation: observed delta/state, suspected impact, protected boundaries, immediate proof, rollback, and expansion triggers. Complete the full plan after stabilization and before making the containment permanent, expanding it, or issuing release/acceptance authority.

If containment temporarily adds AI/ML lifecycle complexity before normal gates can run, record a break-glass exception with incident/owner, exact identity, narrow scope, start/expiry, monitoring and abort thresholds, fallback/rollback, and post-stabilization gate owner. The exception cannot justify permanent adoption, expansion, reuse, or operation past expiry; remove it or complete the normal gates first.

## 8. Release route

Use: `identify → preflight → expose gradually → observe → accept or roll back`.

1. Bind source, build, config, schema, and target-environment identities.
2. Define the exact next release transition, exposure cap, checkpoint, rollback boundary, reachable risks, `NEXT-STEP BLOCKERS`, and deferred `END-STATE HARDENING`; confirm every blocker passes the admission criteria in [next-safe-step.md](next-safe-step.md).
3. Confirm the final Delta Evidence Plan covers the actual release-candidate delta, every claim required for this transition, deferred affected claims, reused evidence, and justified convergence gates. Confirm ownership, required checks, rollback, and a `PASS` Result-Acceptance Gate; require a change window or backup where a named reachable risk or applicable policy makes it necessary at this boundary. Challenge any fixed wait derived only from a worst-case ceiling under [worst-case-gates.md](worst-case-gates.md). For GitHub-backed work, use the authenticated GitHub connector defined in [evidence-and-gates.md](evidence-and-gates.md).
4. Start with the smallest meaningful exposure: dry run, canary, shadow, or cohort.
5. Monitor user-facing invariants and failure signals at every stage.
6. Hold or roll back automatically or manually on a predefined breach.
7. Perform real-world acceptance on the deployed identity.
8. Record the terminal state separately from merge and deployment; activate deferred hardening before the first later boundary where its risk becomes reachable.

## 9. Review and audit route

Use: `inventory → define evidence window → map delta and impact → select required proof → inspect lineage → attack assumptions → reconcile → result acceptance → verdict`.

1. Inventory changed files, interfaces, surfaces, consumers, data, configuration, and operational dependencies.
2. Define the bounded evidence window from the last independently accepted immutable baseline to the exact target.
3. Inspect or construct the Delta Evidence Plan; independently verify the exact delta, direct/transitive impact, evidence states, targeted proof, convergence reasons, expansion triggers, and budget.
4. Extract explicit claims and map each to required evidence.
5. Inspect the Next-Safe-Step Record: challenge next-transition scope, reachable risks, blocker-admission reasoning, bounded substitutes, deferred-hardening triggers, milestone accounting, and residual-risk recomputation.
6. Inspect the exact artifact, current mutable state, and every relevant execution attempt in the window. When the target or material evidence is forge-hosted, use the mandatory authenticated GitHub connector, or the equivalent native connector for another forge.
7. Challenge correctness, safety, recovery, compatibility, observability, simplicity, test adequacy, delta coverage, and evidence-lineage completeness.
8. For A2+ blocking test claims, run or inspect a safe negative control; when that is unsafe or unavailable, inspect the logical counterexample, alternative failure-detection evidence, and stated certification limit.
9. Reconcile every failure, cancellation, skip, timeout, retry, rerun, superseded execution, expected RED, and mutation result; preserve corrections and invalidated evidence.
10. Run the Result-Acceptance Gate for the reviewed next transition. Executor feedback is input, never its verdict.
11. Report findings by severity; distinguish defects and evidence gaps from non-blocking hardening.
12. Issue a typed, scoped verdict and name the next authority only when Next-Safe-Step, Delta-First, and Result-Acceptance consequences permit it. Do not return `NOT CERTIFIED` solely because later end-state hardening is incomplete outside the reviewed transition. Preserve the original requested decision; a narrower verdict is separate unless the accountable owner accepts the scope change.

For code review, prioritize behavioral and operational consequences over formatting preferences.

When review scope is budgeted, list inspected candidates and carry all remaining candidates as `UNJUDGED`. For every material finding, either write it to the durable review artifact or explicitly decline it with a reason; do not leave decisive findings only in transient chat.

## 10. AI/ML complexity overlay

Apply this overlay to every primary route, including bug and incident work, according to the trigger matrix in [ai-complexity-strategy.md](ai-complexity-strategy.md):

1. When AI/ML is introduced or lifecycle complexity materially increases, run `Baseline → Experiment → Complexity-Promotion` before durable operational adoption.
2. For a material AI behavior, configuration, or data change without a complexity increase, run the Baseline comparison and Experiment needed to support the claimed improvement, equivalence, or preserved behavior; do not invent a promotion gate.
3. For removal or simplification, use ordinary V-model regression, safety, compatibility, and acceptance proof; a promotion gate is not required merely to reduce complexity.
4. A bug fix follows the trigger matching its actual change. During an incident, containment may use only the bounded, expiring break-glass exception defined above; normal gates are required before permanence, expansion, reuse, or expiry.
5. Stop when the baseline already meets the validated need. Treat equivalent results within the predeclared margin and uncertainty as a reason to prefer lower lifecycle complexity.
6. Do not treat RAG, an agent, multi-agent coordination, a cascade, fine-tuning, a larger model, or a data-only change as self-justifying. Each is a candidate mechanism whose claims need evidence.

Use [ai-complexity-strategy.md](ai-complexity-strategy.md) for the complete gate contracts and [templates.md](templates.md) for the decision record.

## 11. Assurance controls

| Control | A0 | A1 | A2 | A3 | A4 |
|---|:---:|:---:|:---:|:---:|:---:|
| Explicit objective and non-goals | ✓ | ✓ | ✓ | ✓ | ✓ |
| Current target identity | if mutable | ✓ | ✓ | ✓ | ✓ |
| Delta Evidence Plan | optional | concise when impact is material | required | full + budget/expansion controls | full + strongest independent impact challenge |
| Next-Safe-Step scope | two lists, may be empty; concise/inlined | two lists; concise/inlined | durable record required | full blocker-admission + bounded-exposure proof | full + strongest independent challenge and accountable risk decision |
| Acceptance criteria | concise | ✓ | ✓ | ✓ | ✓ |
| Automated verification | optional | targeted | targeted + integration | required | required + adversarial |
| Negative control/falsifiability | logical counterexample; execution optional | execute when useful and safe | blocking test criteria; execute when safe | execute when safe, otherwise alternative proof + certification limit | strongest safe independent challenge; otherwise alternative proof, accountable exception, and no `CERTIFIED` if material capability remains unproven |
| Risk record | optional | concise | concise | full | full + accountable acceptance |
| Rollback/recovery | n/a | simple | defined | tested | rehearsed or formally justified |
| Observability | n/a | result evidence | relevant signals | rollout + user signals | continuous + escalation |
| Independent review | no | optional | recommended for material boundaries | required | required, strongest available independence |
| Real-world acceptance | n/a | if user-facing | if environment-sensitive | required | required with explicit owner |
| Completed Result-Acceptance Gate before triggered downstream authority | required | required | required | required | required + independent review |
| Durable handoff/evidence | optional | concise | required | required | required + retention/integrity |

These are minimums, not a substitute for domain controls. Classify assurance from the residual risk and exposure of the next transition after accepted controls. Promote when that transition can materially touch security, privacy, money, persistent data, external side effects, shared systems, production, or irreversible state; do not keep it promoted merely because an earlier uncontrolled incident was severe.

## 12. Proportionality and parallelism

Scale depth, not truthfulness:

- A one-line A1 fix can use one criterion and one targeted test.
- An A3 migration needs identity, risk, recovery, observability, independent review, and real-world acceptance even if the diff is small.
- A broad diff can remain A1 if it is generated, reversible, and isolated, but verify that assumption.
- A bounded supervised canary may defer unattended-operation hardening when exposure is capped, effects are observable, stop/rollback is proven, and no uncontrolled security, privacy, data-loss, irreversible, paid, or ambiguous external-side-effect risk remains.
- Count tests, reviews, corrections, reruns, and evidence recovery inside the lifecycle transition they prove; they are not separate milestones.

Parallelize research, inventory, and independent read-only reviews. Serialize conflicting edits and every unisolated shared mutation lane. Merge parallel evidence only after reconciling artifact identities and assumptions.
