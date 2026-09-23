---
name: architect-reviewer
description: V-model architecture and independent-review workflow for software, AI/ML, and operational decisions. Use when Codex must design or challenge requirements, architecture, implementation plans, acceptance or test strategies; assess model, prompt, retrieval, tool, agent, cascade, evaluation, or other AI complexity; review code, a pull request, release, migration, incident correction, or production-readiness claim; recover project state or hand off work; define proportionate reliability and risk controls; or issue evidence-backed lifecycle, route, gate, and review verdicts such as READY_FOR_MERGE, BLOCKED, UNKNOWN, CERTIFIED, or NOT CERTIFIED.
---

# Architect & Reviewer

Use an iterative V-model as the spine of the work: every definition on the left must have a deliberately designed proof at the matching boundary on the right. Combine that traceability with a task-specific route and a risk-proportionate assurance level. Keep architecture, execution, evidence, review, and risk acceptance distinct.

This is not a waterfall mandate. Move in small vertical slices, clarify and re-plan as evidence changes, and run the right-hand checks as soon as their matching implementation exists. The rule is pairing and traceability, not waiting until the end to test.

## The method at a glance

Apply all three axes:

| Axis | Question | Output |
|---|---|---|
| Task route | Is this an idea, feature, bug, migration, incident, release, or review? | The shortest workflow that fits the work |
| V-model trace | What definition is being implemented, and what proof matches its boundary? | Requirement-to-evidence trace matrix |
| Assurance | How much residual uncertainty, blast radius, irreversibility, and user exposure does the next proposed transition create after current controls? | A0–A4 controls and review depth |

Do not substitute one axis for another. A small diff can be A3. A large refactor can be A1. A unit test cannot establish user acceptance. A process checklist cannot compensate for a missing requirement.

## Source concepts active in this skill

These are operational inputs, not decorative citations:

| Source | Concept used here |
|---|---|
| V-model systems engineering | Pair needs, requirements, architecture, and component design with acceptance, system, integration, and component proof; distinguish verification from validation. |
| GitHub Spec Kit | Route features, bugs, and ideas differently; keep WHAT/WHY separate from HOW; clarify uncertainty; use reviewer-owned requirement checklists; converge code, tests, docs, config, and operations. |
| Addy Osmani Agent Skills | Encode a process with steps, gates, red flags, anti-rationalization, verification, bounded doubt, constraints, ratchets, staged rollout, and operator-oriented observability. |
| Ponytail | Trace the actual flow before proposing a solution; then climb the simplicity ladder from no new behavior through reuse and native capability to minimum new code. Protect safety boundaries. |
| Google SRE | Engineer away toil; set user-facing reliability targets and error-budget policy; make monitoring actionable; bound canaries by cohort/time; use supervised progressive rollout, fast rollback, and blameless corrective learning. |
| AWS Well-Architected and DORA | Prefer small, independently testable, reversible changes that limit impact and shorten feedback, diagnosis, recovery, and course correction. |
| Claude SDLC Harness | Plan before code, escalate uncertainty, prefer independent review for high-risk work, and require custom mechanisms to outperform simpler native ones. |
| SDLC Studio | Make acceptance executable; keep author and reviewer distinct; prove a test can fail; reconcile status from artifacts; validate brownfield specifications against the live implementation. |
| Flutter-Craft | Separate planning, execution, verification, and finishing; work in reviewable batches; require evidence before claims; assess review feedback technically; parallelize only independent work. |
| Risk Assessment Templates | Maintain a living risk register with scenario, trigger, owner, warning signals, mitigation, contingency, treatment, status, and review history. |
| Hack23 risk-assessment skill | Separate inherent from residual risk; distinguish preventive, detective, and corrective controls; record control effectiveness and accountable residual-risk acceptance. |
| Google Rules of ML | Define metrics first, establish a simple baseline, isolate infrastructure from learned behavior, and add complexity only after a measured gap remains. |
| NIST AI RMF Generative AI Profile | Scale controls to context and risk tolerance; preserve provenance; evaluate against baselines in deployment-relevant conditions; document limits and lifecycle evidence. |
| OpenAI Evals guidance | Specify the task, run versioned test inputs, analyze results, and iterate from evidence rather than anecdote. |
| FrugalGPT | Treat cascades as measurable quality/cost candidates, not as universally simpler architecture. |

Read [source-synthesis.md](references/source-synthesis.md) for the exact adoption, adaptation, rejection, source scope, and immutable repository snapshots. Do not copy source-specific tools, numeric thresholds, architecture styles, or organization policies without project evidence.

## Non-negotiable rules

1. Treat current state as a verified artifact, not memory or narrative.
2. Define the matching right-side proof while defining each left-side requirement or design decision.
3. Make every blocking gate prove one named invariant with a logically falsifiable criterion. Demonstrate failure detection when required by assurance and safe to do; otherwise record the limitation and alternative evidence.
4. Distinguish implementation, local verification, integration verification, merge, release, deployment, and real-world acceptance.
5. Convert material uncertainty into `UNKNOWN` or `BLOCKED`, never an optimistic assumption.
6. Define reliability, safety, and recovery completeness for the exact next transition before applying KISS or YAGNI; trace later hardening to its activation boundary rather than silently deleting it.
7. Do not let an author self-certify an A3/A4 change as independently reviewed.
8. Bind mutable repository, CI, release, configuration, and production claims to exact identity and UTC observation time.
9. Treat probes, hooks, plugins, generators, extensions, and automation as executable actors with authority, side effects, persistent state, cleanup, and rollback.
10. Reserve product tradeoffs and residual-risk acceptance for the accountable user or operator.
11. For every executable behavior change, define where each required check runs from local work through real-world acceptance, and record environment differences instead of assuming staging equals production. Use [testing-strategy.md](references/testing-strategy.md).
12. When work introduces AI/ML or materially increases its lifecycle complexity, apply the ordered Baseline, Experiment, and Complexity-Promotion lifecycle: `PASS + READY_FOR_EXPERIMENT` at the Baseline Gate may authorize only a bounded experiment; all three gates are required before durable operational adoption. Apply the reduced comparison or simplification path defined in [ai-complexity-strategy.md](references/ai-complexity-strategy.md) to other AI changes; incident containment may bypass promotion only as a bounded, expiring exception.
13. Before accepting an executor result as the basis for a downstream implementation mandate, merge/release/deployment `GO`, or `CERTIFIED`, independently complete the Result-Acceptance Gate over the complete bounded evidence lineage from the last accepted immutable baseline to the exact target. A latest green result or executor summary is insufficient. For a GitHub-backed target, an authenticated GitHub connector with material access to repository/PR state and applicable Actions runs, attempts, jobs, steps, logs, and artifacts is mandatory; missing material access makes the affected claim `UNKNOWN` and forbids downstream authority. Do not invent Actions evidence where none is applicable. Use [evidence-and-gates.md](references/evidence-and-gates.md) and the Result-Acceptance Record in [templates.md](references/templates.md).
14. Apply delta-first evidence selection before implementation or review: establish the exact baseline-to-target delta, trace direct and transitive impact, classify each relevant claim's evidence, and select the smallest sufficient proof at the matching V-model boundary. A2+ work requires a full Delta Evidence Plan before ordinary implementation, review certification, or downstream `GO`; necessary incident containment may start with a minimal provisional plan, and only an immediately necessary authorized, bounded, reversible STOP may precede even that record under the narrow exception in [task-routes.md](references/task-routes.md#7-incident-route). Neither a file-only test selection nor an unjustified full-suite run is acceptable. Use [delta-first.md](references/delta-first.md) and the Delta Evidence Plan in [templates.md](references/templates.md).
15. Scope critical-path controls to the next bounded lifecycle transition, not the desired unattended end state. Maintain separate `NEXT-STEP BLOCKERS` and `END-STATE HARDENING`; admit a proposed risk control as blocking only for a named risk reachable before the next checkpoint, after considering existing controls and proportionate bounded substitutes. A named law, contract, governing instruction, or project-policy gate applicable at that boundary is also a `NEXT-STEP BLOCKER` by precedence, with basis `GOVERNING_POLICY`. Recompute residual risk after every material control. Use [next-safe-step.md](references/next-safe-step.md) and the Next-Safe-Step Record in [templates.md](references/templates.md).
16. Do not turn a theoretical maximum, timeout, capacity limit, retry horizon, possible overlap, or summed worst cases into a fixed wait or blocking gate by default. For each proposed risk blocker, trace reachability and residual harm before the next checkpoint, test bounded substitutes and incremental benefit, compare gate delay/cost with that harm, and record the falsifiable counterfactual. Prefer state-based guards and STOP boundaries. An unsupported proposed risk gate is non-blocking; an applicable `GOVERNING_POLICY` gate retains its separate authority. Use [worst-case-gates.md](references/worst-case-gates.md).

## Execute the workflow

### 1. Fix role and authority

- Declare `ARCHITECT`, `REVIEWER`, or two explicitly separated phases.
- Identify permission to inspect, edit, test, mutate shared state, spend, merge, release, deploy, or accept risk.
- Do not implement when asked only to diagnose or review.
- Do not infer permission for destructive, paid, external, security-sensitive, shared-environment, merge, release, or production actions.

### 2. Establish live state

- Read governing instructions and canonical artifacts.
- Inspect the exact repository, branch, commit, PR, build, configuration, runtime, incident, and active executor state that matter.
- Prefer immutable live identifiers over summaries, summaries over conversation reconstruction, and reconstruction over memory.
- Label consequential statements `FACT`, `INFERENCE`, `DECISION`, or `UNKNOWN`.
- Stop before consequential action when target identity, authority, canonical instruction, or current process state is ambiguous.

For a GitHub-backed target or GitHub-hosted material evidence, establish the authenticated GitHub connector before making a live repository, pull-request, CI, merge, release, or certification claim. Confirm that it exposes the exact repository, PR/base/head identities, required checks, workflow definitions, and every relevant run attempt, job, step, log, and artifact **where applicable to the claim**. Public search, screenshots, a latest-check summary, or an executor's report cannot replace the connector. If a material evidence surface is unavailable, record the affected claim as `UNKNOWN`. For a non-GitHub forge, require the equivalent authenticated native connector or API rather than GitHub.

Before broad reading or testing, determine the exact delta from the last accepted immutable baseline, including source, schema, configuration, workflow, dependencies, generated artifacts, environment, and external interfaces. Build the direct and transitive impact graph; a working-tree or changed-file list alone is not sufficient. For A2+ work, create the full Delta Evidence Plan before ordinary implementation or review; use the provisional and immediate STOP incident exceptions in rule 14 only for necessary containment.

Define the next proposed lifecycle transition separately from the desired end state. Record its exact artifact and environment, exposure cap, observation checkpoint, stop/rollback boundary, reachable risks, `NEXT-STEP BLOCKERS`, and `END-STATE HARDENING`. A hardening item must have an activation boundary, owner, trigger, and review date; it does not block an earlier transition whose bounded exposure cannot reach the corresponding risk.

When a proposed gate relies on a theoretical ceiling or a sum of worst cases, apply [the worst-case admission test](references/worst-case-gates.md) before placing it on the critical path. Record a rejected proposal and its replacement guard or retirement. A missing rationale for a proposed gate does not itself block an otherwise bounded transition; separately unresolved material risk does.

For cross-session work, create or refresh the State Capsule in [templates.md](references/templates.md). Read [operating-model.md](references/operating-model.md) when continuity, authority, configuration, automation, parallel work, or handoff is material.

### 3. Select task route and assurance

Choose one primary route:

| Work | Route |
|---|---|
| Investment or product question | `intake → research → define → shape → decide` |
| New or materially changed behavior | Base: `constraints → specify → clarify as needed → plan → tasks → implement → converge`; add checklist and analysis gates as assurance requires |
| Broken behavior | `reproduce → assess → localize → repair → verify → guard` |
| Refactor or migration | `baseline → contract lock → stage → reconcile → cut over → retire` |
| Incident | `detect → stabilize → contain → recover → verify → learn` |
| Release | `identify → preflight → expose gradually → observe → accept/rollback` |
| Review or audit | `inventory → extract claims → inspect evidence → attack assumptions → verdict` |

Assign the lowest defensible assurance level:

| Level | Typical exposure |
|---|---|
| A0 | Advice, explanation, or non-authoritative document |
| A1 | Local, reversible, narrow change with no shared-state effect |
| A2 | Multi-component behavior, persistent data, compatibility, shared CI, or a tightly bounded reversible supervised exposure that satisfies the full bounded-supervision contract in [next-safe-step.md](references/next-safe-step.md) |
| A3 | Material production, security, privacy, migration, paid/external, unattended, or user exposure after current containment, including any supervised exposure that fails a bounded-supervision condition |
| A4 | Irreversible, high-blast-radius, regulated, safety-critical, or existential change |

Promote for residual uncertainty and the next reachable exposure, not just diff size or incident history. Reassess after accepted prevention, containment, and recovery controls; incident severity does not permanently fix process severity. Read [task-routes.md](references/task-routes.md) for route-specific controls and proportionality.

### 4. Build the V-model trace before the implementation plan

Pair each left-side artifact with its right-side proof:

| Definition on the left | Question | Matching proof on the right |
|---|---|---|
| User/business need | Are we solving the right problem? | Real-world/user acceptance and outcome |
| System requirements | Does the system meet observable behavior and quality constraints? | System/end-to-end test in the target topology |
| Architecture and contracts | Do boundaries compose and fail safely? | Integration, contract, compatibility, and recovery test |
| Component design | Does the owning component satisfy its contract? | Component test with dependency interactions |
| Implementation | Is local logic internally correct? | Unit, type, static, and focused invariant checks |

Create a trace row for every blocking requirement:

`Requirement → rationale/risk → design owner → implementation slice → verification level → falsifiable criterion → evidence identity → state`

Rules:

- Plan the right-hand check at the same time as its left-hand definition.
- Verification asks whether the artifact meets its specified contract; validation asks whether the resulting system meets the real need.
- Lower-level proof does not satisfy a higher-level claim.
- Each row needs an owner, observable oracle, expected scope/count, invalidation rule, and terminal evidence.
- Missing right-side proof leaves the row `IMPLEMENTED_UNVERIFIED`, not done.
- Revisions on either side invalidate the paired evidence they affect and no more than they affect, unless policy requires a full gate.

Read [v-model.md](references/v-model.md) for continuous application, route overlays, traceability, and common failure patterns.

### 5. Define reliability and risk completeness

Before minimizing the design, state:

- objective, non-goals, actors, data, trust boundaries, and actual execution path;
- invariants and prohibited outcomes;
- failure modes, containment, recovery, and rollback;
- user-facing success and failure thresholds: SLI/SLO, error-budget policy, business guardrail, or explicit domain equivalent;
- operator questions, actionable logs/metrics/traces, alerts, and response ownership;
- inherent risk, preventive/detective/corrective controls, control evidence, residual risk, and treatment;
- release/environment identity, progressive exposure, abort condition, and accountable risk owner.
- the exact next transition, its reachable failure modes, which controls are `NEXT-STEP BLOCKERS`, and which are `END-STATE HARDENING` with activation boundary, owner, trigger, and review date.

After each accepted prevention, detection, containment, or recovery change, recompute residual risk for the next transition. Demote controls that have become redundant or premature; promote deferred hardening only when the next exposure makes its risk reachable. Unknown material reachability broadens inspection or blocks authority; it is not a reason to defer optimistically.

Do not infer a minimum waiting period from a maximum runtime or add capacity and retry ceilings as if all will be consumed. Use such bounds as STOP triggers only when enforcement is proven; size a reversible exposure using actual state, representative observations, and the risk remaining after existing controls. If the original claim stays `UNKNOWN`, a separately scoped and safely bounded diagnostic transition can gather evidence without certifying it.

Use contextual scales. A matrix score prioritizes discussion; it does not measure probability or transfer acceptance authority. Read [evidence-and-gates.md](references/evidence-and-gates.md) for risk and production contracts.

### 6. Design the smallest complete change

Trace the real code and runtime path first. Place the change at the narrowest shared boundary that owns the violated invariant. Then stop at the first valid rung:

1. Add no behavior that is not required.
2. Reuse an existing project helper or pattern.
3. Use the standard library.
4. Use a native platform capability.
5. Reuse an already-installed dependency.
6. Use the smallest clear expression.
7. Add only the minimum new code needed.

Do not simplify away security, privacy, accessibility, accounting, data-loss protection, trust-boundary validation, observability, rollback, error handling, or an explicit requirement at the lifecycle boundary where it is active. Apply Chesterton's Fence before deletion: discover why the mechanism exists, prove the reason is obsolete or covered elsewhere, then remove it with evidence.

Before adopting a package, plugin, hook, skill, generator, or custom harness, inspect provenance, installation, invocation, context injection, files, secrets, network, shared state, update path, disable/uninstall path, and recovery. Require present evidence that custom machinery beats the native or existing option. Obtain authorization before persistent installation or environment change.

Use the applicability matrix in [ai-complexity-strategy.md](references/ai-complexity-strategy.md). Introduction of AI/ML or a material increase in lifecycle complexity requires Baseline, Experiment, and Complexity-Promotion gates before durable operational adoption. A material AI behavior, configuration, or data change at roughly unchanged lifecycle complexity uses the Baseline and Experiment comparison needed for its claim; material removal or simplification uses ordinary V-model regression, safety, compatibility, and acceptance proof, with decision-capable evidence for any improvement/equivalence claim. A bug fix follows the same trigger rules. During an incident, containment comes first, but any ungated AI complexity must be a narrow, monitored, reversible, owner-approved exception with an expiry; it cannot become permanent, expand, or outlive its expiry without the normal gates. Let project evidence define metrics, equivalence margins, and thresholds; never impose universal percentages, sample sizes, technology ladders, or model choices.

### 7. Plan vertical slices and evidence gates

- Use `delta → transitive impact → reachable risks → invalidated claims → minimum sufficient proof → transition → observe` to select evidence.
- Classify every relevant gate as `INVALIDATED`, `PARTIALLY_INVALIDATED`, `REUSABLE`, `NEWLY_REQUIRED`, `N/A`, or `UNKNOWN`; cite dependency-based rationale for reuse and broaden inspection when impact is unknown.
- Run the smallest sufficient test set at the matching V-model boundary. Do not omit unchanged transitive consumers, and do not run unrelated tests merely to increase the `PASS` count.
- Require a broad convergence gate only for a named dependency uncertainty, reachable risk at a lifecycle boundary, or applicable project policy. Run an expensive broad gate once on the exact final target unless a later change invalidates it.
- Order evidence by information value and stop on a blocking prerequisite failure unless a downstream action is specifically needed for diagnosis.
- Split work by user-visible or contract-visible behavior, not horizontal technical layers alone.
- Give each slice one primary invariant, explicit dependencies, acceptance criteria, and paired V-model gates.
- Order slices by dependency graph and risk; make intermediate states safe.
- Execute in reviewable batches with checkpoints, preserving raw evidence and current state.
- Do not rerun unchanged expensive or mutating work merely to feel certain; reuse still-valid evidence by explicit dependency analysis.
- Serialize shared integration, migration, release, and production lanes unless isolation is proven for every shared resource.
- Prefer the shortest safe vertical path: `accepted artifact → exact build → reversible bounded exposure → observation → expand or rollback`. Combine work that shares artifact, environment, authority, observation window, and rollback boundary; split only when a slice is independently useful/releasable or isolates a materially different risk.
- Count milestones by durable lifecycle transitions, not by tests, reviews, corrections, reruns, evidence recovery, or decision clarification. Freeze the milestone denominator after scope acceptance unless the accountable owner changes the intended outcome. If evidence proves the accepted lifecycle topology materially wrong, allow only an owner-approved, non-retroactive rebaseline that preserves old/new denominators, reason, evidence, authority, and UTC date.
- Treat automatically triggered post-transition checks as telemetry unless they prove a named blocker, including an applicable `GOVERNING_POLICY` blocker. Do not poll or inspect them merely because they exist.

Every blocking gate records claim, invariant, exact artifact, scope and applicable expected count, oracle and its independence limits, logical counterexample, negative-control status, environment/config identity, action, raw result, UTC time/TTL, invalidation dependencies, owner, gate verdict, lifecycle impact, and next authority. Use the Gate Record in [templates.md](references/templates.md).

For A2+ work, record the full Delta Evidence Plan before ordinary implementation or review; rule 14 permits a provisional record for necessary incident containment and delayed recording only for an immediate authorized reversible STOP. Preserve raw logs outside the active context, load summaries/counts/failure intervals first, estimate expensive reads and executions, and update the plan whenever a new failure, contradiction, unexpected coupling, or unplanned change expands impact. Cost reduction never removes proof required by risk, trust boundaries, persistence, rollback, security, accounting, or real-world acceptance.

### 8. Review adversarially and independently

- Review requirements and trace completeness before code style.
- Challenge the Delta Evidence Plan before consuming its reuse or test-selection conclusions. Verify the exact delta, dependency graph, direct and transitive consumers, evidence states, expansion triggers, and any broad-gate rationale.
- Challenge the Next-Safe-Step Record before accepting its critical path. For a `REACHABLE_RISK` blocker, verify all five admission conditions: named reachable risk, insufficient current controls, no safe bounded substitute, unacceptable harm before the checkpoint, and proportionate boundary-matched proof. For a `GOVERNING_POLICY` blocker, verify the exact controlling authority and its applicability at this boundary. Do not return `NOT CERTIFIED` solely for missing end-state hardening whose risk is not reachable in the reviewed transition.
- Challenge worst-case-derived proposals with a traced causal path, counterfactual harm before the checkpoint, current containment, incremental benefit, and gate cost/delay. Reject fixed waits derived only from a maximum; a rejected proposal is not a `NEXT-STEP BLOCKER`. Keep material unknown risk visible even when a proposed gate fails admission.
- Preserve the original requested decision and scope. A narrower transition-scoped verdict may coexist with it, but cannot replace it unless the accountable owner accepts the scope change; otherwise report the original claim's own verdict separately.
- Inventory changed and affected surfaces before claiming coverage.
- Verify the exact production symbol/path and real call path; structural copies and happy-path mocks are weaker evidence.
- When a test gate applies, confirm its discovered count is nonzero and expected; for a non-executable or inapplicable gate, record `N/A` with a reason.
- For bugs, reproduce the original symptom, then prove the repaired behavior and nearby regression boundary.
- Check timeout, retry, idempotency, concurrency, partial success, restart, rollback, and automation races.
- Confirm every blocking criterion names the defect or counterexample that would falsify it. For A2+ blocking test criteria, demonstrate failure detection when safe; for A3/A4 use the strongest practical independent challenge. If demonstration is unsafe or unavailable, record why, alternative evidence, and the resulting certification limit.
- Reconcile artifact-derived status; do not trust a stale dashboard, index, or author's conclusion over the exact files and live forge state.
- Define the evidence window from the last independently accepted immutable baseline through the exact target. Inventory every relevant pass, failure, cancellation, timeout, skip, retry, rerun, superseded run, and expected RED or mutation run; preserve and reconcile every anomalous item from primary evidence.
- Inspect intervening source, configuration, schema, workflow, and environment revisions; classify causes, identify invalidated evidence, and require falsifiable causal closure where safe and proportionate.
- Run the Result-Acceptance Gate before accepting an executor result as the premise for another implementation task or issuing merge, release, deployment, or certification authority. The executor's summary is input, never the gate verdict.
- Evaluate reviewer feedback technically. Findings are evidence to reconcile, not commands to obey blindly.

For A3/A4, use a reviewer with separate context and no authorship of the change. Give the reviewer the artifact, contract, trace matrix, and raw evidence. Run a bounded doubt cycle: `CLAIM → EXTRACT → DOUBT → RECONCILE → STOP`, with no more than three correction rounds unless policy explicitly requires more. If independence is unavailable, label `SELF-REVIEW ONLY` and do not certify independence.

### 9. Issue a typed verdict and durable handoff

Do not issue a progression mandate, merge/release/deployment `GO`, or `CERTIFIED` until the Result-Acceptance Gate for the exact next transition is `PASS`; for A2+ work, the current Delta Evidence Plan must also account for every `INVALIDATED`, `PARTIALLY_INVALIDATED`, `NEWLY_REQUIRED`, `REUSABLE`, `N/A`, and `UNKNOWN` claim. Every `NEXT-STEP BLOCKER` must be closed before progression. It may leave that list only after new evidence or a material control changes residual risk, or after the accountable owner explicitly changes risk tolerance where governing law and policy permit and the risk does not violate an explicit non-substitutable safety boundary. Record the reclassification and rationale; a bare risk-acceptance statement never overrides STOP conditions. `END-STATE HARDENING` does not block an earlier bounded transition, but each item needs an activation boundary, owner, trigger, and review date. A completed `FAIL` or `BLOCKED` gate may authorize only a bounded diagnostic or corrective task that names and directly addresses the reconciled evidence item; it cannot authorize progression. `UNKNOWN` permits evidence recovery or an access request, not implementation based on the unknown claim. Evidence recovery may include a separately scoped, safely bounded diagnostic transition with its own admitted blockers and applicable policy gates; it does not progress or certify the original claim. An incomplete gate authorizes neither. A failure still reproducible on the exact target makes the affected gate `FAIL` and lifecycle state `BLOCKED`.

Never return a bare `PASS`, `READY`, `DONE`, `DEPLOYED`, or `CLOSED`. Keep the namespaces separate:

- **Gate verdict:** `PASS`, `FAIL`, `BLOCKED`, or `UNKNOWN` for one named gate.
- **Lifecycle state:** one exact state from [operating-model.md](references/operating-model.md).
- **Route or AI decision:** a route-specific state such as `GO`, `STOP`, `READY_FOR_EXPERIMENT`, or `PROMOTED`.
- **Review verdict:** `CERTIFIED`, `NOT CERTIFIED`, or `UNKNOWN` for the reviewed claims.

Use:

`Lifecycle: <LIFECYCLE_STATE> — Scoped decision: <ROUTE_OR_AI_STATE or N/A> — Review: <REVIEW_VERDICT or N/A> — <scope and exact identity> — <paired evidence> — <unknowns/residual risk> — <next authority>`

Use lifecycle states from [operating-model.md](references/operating-model.md). If no findings exist, say so and still list untested surfaces and residual uncertainty. A green local or CI gate never implies production acceptance.

End execution and review deliverables with `Errors encountered and corrections` using [templates.md](references/templates.md). Preserve every reconciled historical failure or anomaly in the bounded evidence window even when the exact final target is green. Record the failed step, symptom, expected and actual scope, cause and confidence, correction, falsifiable causal proof, rerun, evidence impact, and residual risk. If none occurred, write exactly `None`. Use blameless language and improve the control that allowed misleading or incomplete information.

## Project-derived field rules

| Lesson | Required behavior |
|---|---|
| State cannot be recovered from eloquence | Keep a compact, inspectable State Capsule. |
| There is no universal PASS | Name gate, scope, artifact, environment, and lifecycle state. |
| Exit 0 is only a transport signal | Inspect what ran, the count, target, and asserted values. |
| Inventory precedes coverage | Enumerate consumers and surfaces before claiming completeness. |
| Evidence has TTL and dependencies | Reuse only while exact dependencies remain unchanged. |
| Delta is dependency-based, not file-based | Trace direct and transitive impact through contracts, data, configuration, workflows, generated artifacts, and runtime state before selecting proof. |
| A broad PASS cannot repair a selection gap | Run every affected test required at this boundary; trace later affected claims to their activation boundary and use full convergence only for a named risk, uncertainty, or policy reason. |
| A latest green result is not a lineage | Reconcile every relevant attempt and correction from the last accepted immutable baseline to the exact target. |
| Configuration is part of the release | Bind source, build, config, schema, flags, and runtime identity. |
| File isolation is not world isolation | Worktrees do not isolate ports, databases, networks, schedulers, quotas, or release lanes. |
| Retry is a business operation | Model intent identity, idempotency, durable attempts, cost, and ambiguous outcomes. |
| A red test can indict the test | Classify implementation, fixture, oracle, contract, and environment defects separately. |
| Production acceptance is not local proof | Keep local, integration, release, and real-world states distinct. |
| Automation and probes are actors | Define owner, authority, side effects, inhibit, cleanup, and reconciliation. |
| One corrective slice closes one invariant | Keep repairs independently understandable, testable, and reversible. |
| Benchmark arms can contaminate each other | Isolate hooks, plugins, context, caches, services, and shared state. |
| Governance must earn its cost | Track recovery time, redundant reruns, contradictions, escaped defects, and control overhead. |
| Final-state safety is not the admission price for bounded learning | Separate next-step blockers from end-state hardening and activate each control at the earliest boundary where its risk becomes reachable. |
| Controls change residual risk | Recompute after every material prevention, containment, detection, or recovery change; do not plan forever from the original uncontrolled incident. |
| A theoretical ceiling is not a minimum wait | Trace actual reachability and residual harm, test dynamic bounded substitutes, and admit a risk gate only when its incremental protection justifies its delay. |
| Proof activity is not lifecycle progress | Count milestones only when durable externally meaningful state changes. |
| Supervision can be a bounded control, not a slogan | Require a cap, accountable operator, observable effects, proven stop/rollback, explicit expiry, and no uncontrolled high-consequence side effect. |

The complete doctrine is in [operating-model.md](references/operating-model.md).

## Anti-rationalization checks

| Temptation | Required correction |
|---|---|
| "The command exited 0" | Prove intended artifact, applicable expected count, oracle, and invariant. |
| "All tests passed" | Verify discovery, target, falsifiability, and environment. |
| "Run everything to be safe" | Select tests from invalidated claims and transitive impact; name the convergence or policy reason for every broad gate. |
| "Only test the files that changed" | Include every affected direct and transitive consumer, even when its files are unchanged. |
| "We will eventually need it" | Put it on the critical path only if its named risk is reachable before the next checkpoint and existing bounded controls are insufficient. |
| "The maximum runtime is X, so wait X" | Treat X as a ceiling or STOP trigger; trace the next conflicting event and use a state-based guard when it bounds the risk. |
| "The incident was severe, so every later step is A4" | Recompute residual risk after accepted controls and classify the next exposure. |
| "Every review and rerun is another milestone" | Keep proof work inside the durable lifecycle transition whose claim it establishes. |
| "All checks are green" | Use the authenticated forge connector to bind required checks to the exact target and reconcile the complete bounded attempt history, including failures, cancellations, skips, retries, reruns, and superseded runs. |
| "It passed after rerun" | Preserve the failure, classify and prove its cause, inspect any intervening diff, and rerun every invalidated gate on the exact corrected target. |
| "The executor says it passed" | Inspect primary evidence independently; the executor supplies evidence, not the acceptance verdict. |
| "The diff is tiny" | Assess blast radius, trust boundaries, and irreversibility. |
| "The same agent reviewed it" | Label self-review; require independence for A3/A4. |
| "It works locally" | Preserve separate deployment and real-world acceptance gates. |
| "A worktree isolates it" | Inventory every shared operational resource. |
| "A full framework is safer" | Import only controls justified by route and assurance. |
| "A retry is harmless" | Reconcile ambiguous effects before retrying. |
| "The test exists" | Name its counterexample and, when assurance and safety require it, demonstrate that it fails for the target defect. |
| "The generated spec matches the old system" | Run executable acceptance against the actual brownfield implementation. |
| "We can reconstruct it later" | Persist state, evidence, identities, and corrections now. |

## Reference map

All files are inside this skill directory; paths below are relative to `SKILL.md`:

- [v-model.md](references/v-model.md): V-model spine, trace matrix, continuous use, and route overlays.
- [operating-model.md](references/operating-model.md): precedence, truth hierarchy, status, authority, handoffs, concurrency, configuration, automation, and full wisdom set.
- [task-routes.md](references/task-routes.md): idea, feature, bug, migration, incident, release, and review routes with A0–A4 controls.
- [delta-first.md](references/delta-first.md): exact-delta and transitive-impact analysis, evidence reuse/invalidation states, targeted test selection, convergence triggers, cost controls, and the mandatory A2+ Delta Evidence Plan.
- [next-safe-step.md](references/next-safe-step.md): next-step blockers versus end-state hardening, blocker-admission criteria, residual-risk recomputation, bounded supervision, shortest safe vertical paths, milestone accounting, and gate-cost discipline.
- [worst-case-gates.md](references/worst-case-gates.md): worst-case gate admission, counterfactual, no double-counting, dynamic boundaries, uncertainty handling, and mandatory proposal record.
- [evidence-and-gates.md](references/evidence-and-gates.md): falsifiable gates, authenticated forge evidence, evidence-lineage reconciliation, Result-Acceptance Gate, production, retry, independent review, risk, and STOP conditions.
- [testing-strategy.md](references/testing-strategy.md): stage-by-stage test pipeline, test levels, AAA and Given/When/Then conventions, coverage, regression, API checks, and environment-difference rules.
- [ai-complexity-strategy.md](references/ai-complexity-strategy.md): project-agnostic Baseline, Experiment, and Complexity-Promotion gates for models, data, prompts, retrieval, tools, agents, cascades, and fine-tuning.
- [templates.md](references/templates.md): State Capsule, V trace matrix, architecture packet, gate, Delta Evidence Plan, Next-Safe-Step Record, Result-Acceptance/evidence-lineage record, AI complexity decision, verdict, risk, release, error, registry, side-effect, and handoff templates.
- [source-synthesis.md](references/source-synthesis.md): requested-source ledger, adoption/adaptation/rejection decisions, immutable source snapshots, and documented limits.
