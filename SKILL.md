---
name: architect-reviewer
description: V-model architecture and independent-review workflow for software, AI/ML, and operational decisions. Use when Codex must design or challenge requirements, architecture, implementation plans, acceptance or test strategies; assess model, prompt, retrieval, tool, agent, cascade, evaluation, or other AI complexity; review code, a pull request, release, migration, incident correction, or production-readiness claim; recover project state or hand off work; define proportionate reliability and risk controls; or issue an evidence-backed GO, STOP, READY, BLOCKED, UNKNOWN, CERTIFIED, or NOT CERTIFIED verdict.
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
| Assurance | How much uncertainty, blast radius, irreversibility, and user exposure exist? | A0–A4 controls and review depth |

Do not substitute one axis for another. A small diff can be A3. A large refactor can be A1. A unit test cannot establish user acceptance. A process checklist cannot compensate for a missing requirement.

## Source concepts active in this skill

These are operational inputs, not decorative citations:

| Source | Concept used here |
|---|---|
| V-model systems engineering | Pair needs, requirements, architecture, and component design with acceptance, system, integration, and component proof; distinguish verification from validation. |
| GitHub Spec Kit | Route features, bugs, and ideas differently; keep WHAT/WHY separate from HOW; clarify uncertainty; use reviewer-owned requirement checklists; converge code, tests, docs, config, and operations. |
| Addy Osmani Agent Skills | Encode a process with steps, gates, red flags, anti-rationalization, verification, bounded doubt, constraints, ratchets, staged rollout, and operator-oriented observability. |
| Ponytail | Trace the actual flow before proposing a solution; then climb the simplicity ladder from no new behavior through reuse and native capability to minimum new code. Protect safety boundaries. |
| Google SRE | Engineer away toil; set user-facing reliability targets and error-budget policy; make monitoring actionable; use progressive rollout, fast rollback, and blameless corrective learning. |
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
3. Make every blocking gate prove one named invariant and demonstrate that it can fail.
4. Distinguish implementation, local verification, integration verification, merge, release, deployment, and real-world acceptance.
5. Convert material uncertainty into `UNKNOWN` or `BLOCKED`, never an optimistic assumption.
6. Define reliability, safety, and recovery completeness before applying KISS or YAGNI.
7. Do not let an author self-certify an A3/A4 change as independently reviewed.
8. Bind mutable repository, CI, release, configuration, and production claims to exact identity and UTC observation time.
9. Treat probes, hooks, plugins, generators, extensions, and automation as executable actors with authority, side effects, persistent state, cleanup, and rollback.
10. Reserve product tradeoffs and residual-risk acceptance for the accountable user or operator.
11. For every executable behavior change, define where each required check runs from local work through real-world acceptance, and record environment differences instead of assuming staging equals production. Use [testing-strategy.md](references/testing-strategy.md).
12. For AI/ML introduction or material complexity growth, require Baseline, Experiment, and Complexity-Promotion gates; do not promote a practically equivalent candidate over a lower-lifecycle-complexity alternative.

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

For cross-session work, create or refresh the State Capsule in [templates.md](references/templates.md). Read [operating-model.md](references/operating-model.md) when continuity, authority, configuration, automation, parallel work, or handoff is material.

### 3. Select task route and assurance

Choose one primary route:

| Work | Route |
|---|---|
| Investment or product question | `intake → research → define → shape → decide` |
| New or materially changed behavior | `constraints → specify → clarify → plan → tasks → implement → converge` |
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
| A2 | Multi-component behavior, persistent data, compatibility, or shared CI |
| A3 | Production, security, privacy, migration, paid/external calls, or material user impact |
| A4 | Irreversible, high-blast-radius, regulated, safety-critical, or existential change |

Promote for uncertainty, not just diff size. Read [task-routes.md](references/task-routes.md) for route-specific controls and proportionality.

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

Do not simplify away security, privacy, accessibility, accounting, data-loss protection, trust-boundary validation, observability, rollback, error handling, or an explicit requirement. Apply Chesterton's Fence before deletion: discover why the mechanism exists, prove the reason is obsolete or covered elsewhere, then remove it with evidence.

Before adopting a package, plugin, hook, skill, generator, or custom harness, inspect provenance, installation, invocation, context injection, files, secrets, network, shared state, update path, disable/uninstall path, and recovery. Require present evidence that custom machinery beats the native or existing option. Obtain authorization before persistent installation or environment change.

For work that introduces AI/ML or materially changes a model, prompt, evaluator, retrieval path, tool, agent, router, cascade, fine-tune, training/evaluation data, or number of model calls, apply the three gates in [ai-complexity-strategy.md](references/ai-complexity-strategy.md): establish the simplest credible baseline and its measured gap; test one named hypothesis on versioned, controlled or explicitly disclosed evidence; then promote added complexity only when no acceptable lower-complexity candidate closes the gap after lifecycle cost and risk are counted. If the baseline already meets the need, stop. Let project evidence define metrics, equivalence margins, and thresholds; never impose universal percentages, sample sizes, technology ladders, or model choices.

### 7. Plan vertical slices and evidence gates

- Split work by user-visible or contract-visible behavior, not horizontal technical layers alone.
- Give each slice one primary invariant, explicit dependencies, acceptance criteria, and paired V-model gates.
- Order slices by dependency graph and risk; make intermediate states safe.
- Execute in reviewable batches with checkpoints, preserving raw evidence and current state.
- Do not rerun unchanged expensive or mutating work merely to feel certain; reuse still-valid evidence by explicit dependency analysis.
- Serialize shared integration, migration, release, and production lanes unless isolation is proven for every shared resource.

Every blocking gate records claim, invariant, exact artifact, scope and expected count, independent oracle, negative control, environment/config identity, action, raw result, UTC time/TTL, invalidation dependencies, owner, verdict, and next authority. Use the Gate Record in [templates.md](references/templates.md).

### 8. Review adversarially and independently

- Review requirements and trace completeness before code style.
- Inventory changed and affected surfaces before claiming coverage.
- Verify the exact production symbol/path and real call path; structural copies and happy-path mocks are weaker evidence.
- Confirm discovered test count is nonzero and expected.
- For bugs, reproduce the original symptom, then prove the repaired behavior and nearby regression boundary.
- Check timeout, retry, idempotency, concurrency, partial success, restart, rollback, and automation races.
- Probe whether every blocking criterion can actually turn red for its target defect.
- Reconcile artifact-derived status; do not trust a stale dashboard, index, or author's conclusion over the exact files and live forge state.
- Evaluate reviewer feedback technically. Findings are evidence to reconcile, not commands to obey blindly.

For A3/A4, use a reviewer with separate context and no authorship of the change. Give the reviewer the artifact, contract, trace matrix, and raw evidence. Run a bounded doubt cycle: `CLAIM → EXTRACT → DOUBT → RECONCILE → STOP`, with no more than three correction rounds unless policy explicitly requires more. If independence is unavailable, label `SELF-REVIEW ONLY` and do not certify independence.

### 9. Issue a typed verdict and durable handoff

Never return a bare `PASS`, `DONE`, `DEPLOYED`, or `CLOSED`. Use:

`<STATE> — <scope and exact identity> — <paired evidence> — <unknowns/residual risk> — <next authority>`

Use lifecycle states from [operating-model.md](references/operating-model.md). If no findings exist, say so and still list untested surfaces and residual uncertainty. A green local or CI gate never implies production acceptance.

End execution and review deliverables with `Errors encountered and corrections` using [templates.md](references/templates.md). Record the failed step, symptom, cause, correction, rerun, evidence impact, and residual risk. If none occurred, write exactly `None`. Use blameless language and improve the control that allowed misleading or incomplete information.

## Project-derived field rules

| Lesson | Required behavior |
|---|---|
| State cannot be recovered from eloquence | Keep a compact, inspectable State Capsule. |
| There is no universal PASS | Name gate, scope, artifact, environment, and lifecycle state. |
| Exit 0 is only a transport signal | Inspect what ran, the count, target, and asserted values. |
| Inventory precedes coverage | Enumerate consumers and surfaces before claiming completeness. |
| Evidence has TTL and dependencies | Reuse only while exact dependencies remain unchanged. |
| Configuration is part of the release | Bind source, build, config, schema, flags, and runtime identity. |
| File isolation is not world isolation | Worktrees do not isolate ports, databases, networks, schedulers, quotas, or release lanes. |
| Retry is a business operation | Model intent identity, idempotency, durable attempts, cost, and ambiguous outcomes. |
| A red test can indict the test | Classify implementation, fixture, oracle, contract, and environment defects separately. |
| Production acceptance is not local proof | Keep local, integration, release, and real-world states distinct. |
| Automation and probes are actors | Define owner, authority, side effects, inhibit, cleanup, and reconciliation. |
| One corrective slice closes one invariant | Keep repairs independently understandable, testable, and reversible. |
| Benchmark arms can contaminate each other | Isolate hooks, plugins, context, caches, services, and shared state. |
| Governance must earn its cost | Track recovery time, redundant reruns, contradictions, escaped defects, and control overhead. |

The complete doctrine is in [operating-model.md](references/operating-model.md).

## Anti-rationalization checks

| Temptation | Required correction |
|---|---|
| "The command exited 0" | Prove intended artifact, expected count, oracle, and invariant. |
| "All tests passed" | Verify discovery, target, falsifiability, and environment. |
| "CI is green" | Bind live required checks to repository, head SHA, config, and UTC time. |
| "The diff is tiny" | Assess blast radius, trust boundaries, and irreversibility. |
| "The same agent reviewed it" | Label self-review; require independence for A3/A4. |
| "It works locally" | Preserve separate deployment and real-world acceptance gates. |
| "A worktree isolates it" | Inventory every shared operational resource. |
| "A full framework is safer" | Import only controls justified by route and assurance. |
| "A retry is harmless" | Reconcile ambiguous effects before retrying. |
| "The test exists" | Demonstrate that it fails for the target defect. |
| "The generated spec matches the old system" | Run executable acceptance against the actual brownfield implementation. |
| "We can reconstruct it later" | Persist state, evidence, identities, and corrections now. |

## Reference map

All files are inside this skill directory; paths below are relative to `SKILL.md`:

- [v-model.md](references/v-model.md): V-model spine, trace matrix, continuous use, and route overlays.
- [operating-model.md](references/operating-model.md): precedence, truth hierarchy, status, authority, handoffs, concurrency, configuration, automation, and full wisdom set.
- [task-routes.md](references/task-routes.md): idea, feature, bug, migration, incident, release, and review routes with A0–A4 controls.
- [evidence-and-gates.md](references/evidence-and-gates.md): falsifiable gates, real-path proof, CI, production, retry, independent review, risk, and STOP conditions.
- [testing-strategy.md](references/testing-strategy.md): stage-by-stage test pipeline, test levels, AAA and Given/When/Then conventions, coverage, regression, API checks, and environment-difference rules.
- [ai-complexity-strategy.md](references/ai-complexity-strategy.md): project-agnostic Baseline, Experiment, and Complexity-Promotion gates for models, data, prompts, retrieval, tools, agents, cascades, and fine-tuning.
- [templates.md](references/templates.md): State Capsule, V trace matrix, architecture packet, gate, AI complexity decision, verdict, risk, release, error, registry, side-effect, and handoff templates.
- [source-synthesis.md](references/source-synthesis.md): requested-source ledger, adoption/adaptation/rejection decisions, immutable source snapshots, and documented limits.
