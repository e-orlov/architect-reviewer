# Next-Safe-Step and Minimum-Sufficient-Gate Rule

## Contents

1. Maintain two explicit scopes
2. Admit a control to the critical path only when justified
3. Recompute residual risk after every material control
4. Prefer the shortest safe vertical path
5. Use bounded human supervision when proportionate
6. Count milestones by lifecycle transitions
7. Apply delta-first evidence selection
8. Put hardening at the correct boundary
9. Governance must earn its cost
10. Interaction with other skill contracts
11. Primary references

Do not confuse the controls required for the **next bounded transition** with the controls desired for the **final unattended operating state**.

A desirable control is not automatically a release gate. Place each control at the earliest lifecycle boundary where the risk it addresses actually becomes reachable—and no earlier.

## 1. Maintain two explicit scopes

For every task, keep separate lists:

- **NEXT-STEP BLOCKERS** — controls without which the next proposed transition would expose an unacceptable, insufficiently contained risk.
- **END-STATE HARDENING** — controls valuable for sustained, unattended, or larger-scale operation but unnecessary for the next bounded and reversible transition.

Only the first list may block the next transition. The second becomes owned follow-up work with a trigger, target boundary, and review date.

A blocker leaves the critical path only when it is closed, new evidence or a material control changes residual risk, or the accountable owner explicitly changes risk tolerance where governing law and policy permit and no explicit non-substitutable safety boundary is violated. Record the reclassification and rationale. A bare risk-acceptance statement never overrides a STOP condition.

A reviewer must not return `NOT CERTIFIED` for missing end-state hardening when the reviewed next step does not yet expose the corresponding risk.

Do not silently narrow the decision that was requested. If the requester asked for unattended production readiness, a reviewer may issue a separate verdict for a smaller supervised transition, but that verdict does not replace the verdict on the original claim unless the accountable owner explicitly accepts the scope change. Preserve the original decision/claim, proposed scope change, authority, and acceptance state.

The critical path still has only one blocking list. When law, contract, governing instructions, or explicit project policy mandates a gate at the exact next boundary, put that gate in `NEXT-STEP BLOCKERS` with basis `GOVERNING_POLICY`. Such a mandate is admitted by precedence when its applicability is proven; it is not a proposed risk control subject to substitution under the five-condition test below. Name the policy and applicable boundary. A policy gate that applies only later belongs in `END-STATE HARDENING` until that boundary.

## 2. Admit a control to the critical path only when justified

A proposed risk control may become a blocking gate only when all of the following are true:

1. It addresses a named failure mode reachable during the **next** transition.
2. Existing preventive, detective, containment, and recovery controls do not already reduce that failure to an acceptable level.
3. A bounded manual observation, hold, permit, feature flag, canary, rate/cost limit, fast stop, or proven rollback cannot safely substitute for it during that transition.
4. Its absence could cause unacceptable harm before the next checkpoint.
5. The required proof is proportionate to the residual risk and observes the correct boundary.

If any condition is false, defer the control to the boundary where it becomes necessary.

`Useful`, `best practice`, `we will eventually need it`, and `it would make us safer` are not sufficient blocking rationales.

## 3. Recompute residual risk after every material control

Do not continue planning from the original incident's uncontrolled risk after new prevention or containment has landed.

After each accepted change:

1. identify which failure modes are now prevented, bounded, or recoverable;
2. recalculate the residual risk of the next transition;
3. demote controls made redundant or premature;
4. promote a deferred control only when the next exposure makes its risk reachable.

Incident severity does not permanently determine process severity.

## 4. Prefer the shortest safe vertical path

The default progression is:

`accepted artifact → exact build → reversible bounded exposure → observation → expand or rollback`

Combine activities that share the same artifact, environment, authority, observation window, and rollback boundary.

Do not create separate milestones for:

- clarification of an existing milestone;
- author correction and re-review;
- evidence packaging;
- build and rehearsal when the exact build can be safely exercised during the bounded deployment;
- producer and consumer changes that are useful only together;
- canary execution and its immediate observation;
- automatically duplicated CI on an identical artifact.

Split work only when a slice is independently useful, independently releasable, or isolates a materially different risk.

## 5. Use bounded human supervision when proportionate

Temporary manual supervision may substitute for unfinished automation when all are true:

- exposure is capped by time, population, calls, cost, or data volume;
- an accountable operator is present;
- stop and rollback are fast and proven;
- effects are observable before expansion;
- no uncontrolled security, privacy, data-loss, or irreversible risk exists;
- the exception has an explicit expiry and next decision point.

Manual supervision is not an acceptable substitute for controls against unbounded paid effects, irreversible mutation, unrecoverable data loss, security/privacy breach, ambiguous external side effects, or absent rollback.

## 6. Count milestones by lifecycle transitions

Count only durable state transitions that deliver externally meaningful progress, such as:

- merged;
- released;
- deployed under containment;
- canary accepted;
- exposure expanded;
- production accepted;
- closed.

Tests, reviews, corrections, reruns, evidence recovery, and decision clarifications belong inside the milestone whose claim they establish. They do not increase the milestone count.

Freeze the milestone denominator once scope is accepted. Change it only when the accountable owner explicitly changes the intended outcome—not whenever new implementation work is discovered.

If evidence proves that the accepted lifecycle topology itself was materially wrong—for example, a mandatory canary, mixed-version interval, backfill, or recovery checkpoint was absent—the owner may approve a non-retroactive rebaseline of the outcome contract. Preserve the old denominator, new denominator, reason, evidence, authority, and UTC date. This exception corrects a false lifecycle model; it does not permit milestone inflation for ordinary implementation work.

## 7. Apply delta-first evidence selection

For each transition:

`delta → transitive impact → reachable risks → invalidated claims → minimum sufficient proof → transition → observe`

Reuse evidence whose dependencies remain unchanged. Run affected tests and, when a named trigger or governing policy justifies one, a convergence gate on the exact final artifact. Do not repeat successful evidence at later boundaries unless the artifact, configuration, environment, or claimed behavior changed.

Automatically triggered post-transition checks are telemetry unless they prove a named blocking claim. Do not wait for, poll, or inspect them merely because they exist.

## 8. Put hardening at the correct boundary

Examples:

- deployment safeguards belong before deployment;
- provider-call safeguards belong before the first provider call;
- unattended alerting belongs before unattended operation, not necessarily before a supervised one-call canary;
- scale safeguards belong before scale increases;
- historical backfill safeguards belong before backfill, not before normal forward processing;
- external watchdogs belong before reliance on autonomous recovery, not before every manual rollout.

## 9. Governance must earn its cost

For every added gate, state:

- the specific reachable risk reduced;
- why existing controls are insufficient;
- the lifecycle boundary where it becomes necessary;
- expected time, execution, and context cost;
- the evidence that will retire the uncertainty.

If the process keeps gaining gates without a corresponding change in artifact, exposure, or residual risk, stop and simplify the critical path before continuing.

The desired final operating model must not become the admission price for learning safely from the next small, reversible step.

## 10. Interaction with other skill contracts

- **Assurance is transition-scoped.** Assign A0–A4 to the next proposed transition using its actual uncertainty, exposure, blast radius, and reversibility. Reassess before every later expansion; do not inherit the end state's assurance controls prematurely.
- **Delta-First selects evidence.** Extend the sequence in [delta-first.md](delta-first.md) through reachable risk: `delta → transitive impact → reachable risks → invalidated claims → minimum sufficient proof`.
- **Convergence is named, not automatic.** When a named trigger or governing policy justifies a convergence gate, it may aggregate the affected proof on the exact final artifact; it becomes a full suite or system gate only when dependency uncertainty, reachable risk, lifecycle claim, or policy requires that breadth.
- **Result Acceptance reconciles actual evidence.** The Result-Acceptance Gate in [evidence-and-gates.md](evidence-and-gates.md) remains mandatory when triggered, but its required gates and material attempts are scoped to the exact next transition and the claims it needs. It does not turn deferred hardening into a blocker.
- **V-model completeness is scoped, not abandoned.** Every blocking claim for the next transition still needs proof at the correct boundary. End-state requirements remain traced with their activation boundary, owner, and review date.
- **Project policy still applies through the blocker list.** A mandatory gate in named law, contract, governing instructions, or project policy is a `NEXT-STEP BLOCKER` when that policy applies at the exact next boundary. Record basis `GOVERNING_POLICY`; `best practice` is not a substitute.
- **Unknown reachable risk broadens or blocks.** If material impact or reachability cannot be established, broaden inspection or return `UNKNOWN`; do not use minimum-sufficient language to hide uncertainty.

Use the Next-Safe-Step Record in [templates.md](templates.md) before assigning blockers, assurance, gates, milestones, or the next authority.

## 11. Primary references

These sources support small reversible transitions, bounded canaries, supervision, and actionable monitoring; this rule generalizes them without importing a vendor process:

- [AWS Well-Architected: Make frequent, small, reversible changes](https://docs.aws.amazon.com/wellarchitected/latest/operational-excellence-pillar/ops_dev_integ_freq_sm_rev_chg.html) connects small reversible changes with reduced impact, faster diagnosis, and simpler recovery.
- [DORA: Working in small batches](https://dora.dev/capabilities/working-in-small-batches/) connects independently testable batches with faster feedback and course correction.
- [Google SRE Workbook: Canarying Releases](https://sre.google/workbook/canarying-releases/) defines canarying as partial, time-limited exposure used to decide whether to expand, and ties risk to cohort size and duration.
- [Google SRE: Production Services Best Practices](https://sre.google/sre-book/service-best-practices/) requires staged, supervised rollouts and permits supervision by the responsible engineer or a demonstrably reliable monitoring system.
- [Google SRE: Monitoring Distributed Systems](https://sre.google/sre-book/monitoring-distributed-systems/) distinguishes observation from actionable human alerts and warns that unnecessary monitoring interruption creates costly noise.
