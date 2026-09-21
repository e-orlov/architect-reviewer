# Source synthesis, decisions, and limits

## Contents

1. Scope and method
2. V-model basis
3. Requested sources at a glance
4. GitHub Spec Kit
5. Addy Osmani Agent Skills
6. Ponytail
7. Google SRE
8. Claude SDLC Harness
9. SDLC Studio
10. Flutter-Craft
11. Risk Assessment Templates
12. Hack23 risk-assessment skill
13. Cross-source synthesis
14. Practices intentionally not imported
15. Verified source snapshots

## 1. Scope and method

All nine sources requested by the user are represented in the active method. The review used each repository's canonical README plus the high-signal workflow, review, verification, planning, or risk files relevant to this skill. It is a concept and control synthesis, not a claim that every historical file, issue, release, or empirical assertion in each repository was exhaustively adopted.

For each source:

1. extract the behaviorally important concepts;
2. map them to an explicit control or workflow step;
3. adapt them to a project-agnostic form;
4. reject stack-specific, product-specific, organization-specific, or weakly supported prescriptions;
5. preserve primary links and content identities so later updates can be diffed.

Sources were checked on 2026-09-21. Recheck live primary documentation before relying on current versions, commands, product behavior, repository state, or empirical performance claims.

## 2. V-model basis

The V-model is the structural spine of this skill, not an attribution to one of the nine requested repositories. Its systems-engineering basis is the pairing of definition and decomposition with integration, verification, and validation. The supporting primary reference is the [NASA Systems Engineering Handbook, NASA/SP-2016-6105 Rev. 2](https://ntrs.nasa.gov/citations/20170001761).

Adopted:

- pair need with real-world validation;
- pair system requirements with system verification;
- pair architecture and interfaces with integration/contract verification;
- pair component design with component verification;
- pair implementation with unit/static verification;
- keep requirement-to-implementation-to-evidence traceability;
- distinguish “built to the specified contract” from “solves the actual need.”

Adapted:

- use the V recursively for small vertical slices instead of imposing a single long waterfall;
- combine it with task-specific routes so a bug, idea, incident, and feature do not receive identical ceremony;
- combine it with A0–A4 assurance so verification depth follows risk and uncertainty.

Not imported:

- heavyweight milestone bureaucracy by default;
- domain-specific NASA governance, documentation, or approval structure;
- the claim that late testing is acceptable. Right-side proof is planned with the left side and executed as soon as the paired implementation exists.

Active locations: SKILL.md sections “The method at a glance” and “Build the V-model trace”; references/v-model.md; trace template in references/templates.md; gate pairing in references/evidence-and-gates.md.

## 3. Requested sources at a glance

| Requested source | Main contribution | Active location |
|---|---|---|
| [GitHub Spec Kit](https://github.com/github/spec-kit) | Task routes, WHAT/WHY before HOW, clarification, requirement checklists, dependency-ordered tasks, consistency analysis, convergence | SKILL.md, task-routes.md, v-model.md |
| [Addy Osmani Agent Skills](https://github.com/addyosmani/agent-skills) | Process-shaped skills, bounded doubt, anti-rationalization, vertical slices, constraints/ratchets, rollout, observability | SKILL.md, evidence-and-gates.md, task-routes.md |
| [Ponytail](https://github.com/DietrichGebert/ponytail) | Actual-flow inspection, simplicity ladder, narrow owning boundary, protected safety edges, benchmark isolation | SKILL.md, operating-model.md, evidence-and-gates.md |
| [Google SRE introduction](https://sre.google/sre-book/introduction/) | Reliability engineering, toil, SLO/error-budget thinking, actionable monitoring, safe change, incident learning | SKILL.md, evidence-and-gates.md, release/incident routes |
| [Claude SDLC Harness](https://github.com/BaseInfinity/claude-sdlc-harness) | Plan/test/review discipline, confidence escalation, separate review, native-before-custom, process measurement | SKILL.md, assurance and independent-review controls |
| [SDLC Studio](https://github.com/DarrenBenson/sdlc-studio) | Executable acceptance, author/reviewer separation, test validation, artifact reconciliation, brownfield proof, partial-audit semantics | SKILL.md, task-routes.md, evidence-and-gates.md |
| [Flutter-Craft](https://github.com/vp-k/flutter-craft) | Planning/execution/verification separation, evidence before claims, checkpoints, technical feedback processing, safe parallelism | SKILL.md, task routes, concurrency rules |
| [Risk Assessment Templates](https://github.com/henu-wang/risk-assessment-templates) | Living risk register, triggers, warnings, mitigation, contingency, treatment, FMEA/change risk | risk record and gate contract |
| [Hack23 risk-assessment skill](https://github.com/Hack23/homepage/blob/master/.github/skills/governance/risk-assessment/SKILL.md) | Asset/threat/vulnerability analysis, inherent/residual risk, control types/effectiveness, ownership, reassessment | risk record and gate contract |

## 4. GitHub Spec Kit

Reviewed scope: [README](https://github.com/github/spec-kit), [spec-driven development](https://github.com/github/spec-kit/blob/main/spec-driven.md), [quickstart](https://github.com/github/spec-kit/blob/main/docs/quickstart.md), [bugfix guide](https://github.com/github/spec-kit/blob/main/docs/guides/bugfix.md), [assessment guide](https://github.com/github/spec-kit/blob/main/docs/guides/assessment.md), [existing projects](https://github.com/github/spec-kit/blob/main/docs/guides/existing-projects.md), and [contract-driven development](https://github.com/github/spec-kit/blob/main/docs/guides/contract-driven-development.md).

Adopted:

- independent entry routes instead of forcing every task through a feature process;
- feature flow: governing principles, specify, clarify, requirement checklist, plan, tasks, consistency analysis, implement, converge;
- bug flow centered on assessment, repair, and verification, with the original symptom as essential evidence;
- idea/assessment flow that can terminate in GO, CLARIFY, or STOP;
- specification states WHAT and WHY before implementation HOW;
- uncertainty is marked and resolved rather than silently invented;
- a requirements checklist reviews requirement quality, not implementation quality;
- tasks follow dependency order and prefer vertical, independently verifiable slices;
- convergence includes code, tests, documentation, configuration, contracts, and operational artifacts;
- brownfield work reads the actual repository and behavior rather than inventing missing standards;
- a contract has one authoritative owner, version identity, failure semantics, timeout/retry/idempotency behavior, and provider/consumer/integration proof.

Adapted:

- “constitution” becomes existing governing principles and constraints; create one only when the project lacks them;
- commands and generated folders become conceptual checkpoints, not required tooling;
- analysis is proportionate and can be compact for A0/A1.

Not imported:

- universal library-first architecture;
- a mandatory CLI or generated directory layout;
- a single test-order doctrine for every codebase;
- any assumption that a generated spec is true before it is checked against brownfield behavior.

## 5. Addy Osmani Agent Skills

Reviewed scope: [repository README](https://github.com/addyosmani/agent-skills), [Doubt-Driven Development](https://github.com/addyosmani/agent-skills/blob/main/skills/doubt-driven-development/SKILL.md), [Code Review and Quality](https://github.com/addyosmani/agent-skills/blob/main/skills/code-review-and-quality/SKILL.md), [Code Simplification](https://github.com/addyosmani/agent-skills/blob/main/skills/code-simplification/SKILL.md), planning/incremental-delivery guidance, [Shipping and Launch](https://github.com/addyosmani/agent-skills/blob/main/skills/shipping-and-launch/SKILL.md), and [Observability and Instrumentation](https://github.com/addyosmani/agent-skills/blob/main/skills/observability-and-instrumentation/SKILL.md).

Adopted:

- a useful skill encodes an executable process: trigger, steps, checkpoints, exit criteria, red flags, anti-rationalization, and verification;
- progressive disclosure: core behavior in SKILL.md, detailed contracts in referenced files;
- plans expose dependencies and split work into small vertical tasks with acceptance and verification;
- incremental loop: implement, test, verify, checkpoint; do not blindly repeat unchanged expensive work;
- bounded doubt: CLAIM → EXTRACT artifact and contract → DOUBT with adversarial context → RECONCILE → STOP;
- reviewer output is evidence to reconcile, not an automatic verdict;
- review axes include correctness, security, data/recovery, compatibility, operability, test adequacy, and simplicity;
- simplification preserves behavior, follows Chesterton's Fence, and stays inside the requested scope;
- constraints should become measurable checks, commands, budgets, or ratchets when the project supports them;
- shipping uses staged exposure, explicit abort/rollback, and post-release observation;
- observability begins with operator questions, then chooses logs, metrics, and traces; alerts should describe actionable symptoms;
- RED/USE-style thinking, cardinality limits, sensitive-data controls, and ownership are considered where relevant.

Adapted:

- three doubt rounds are a default bound, not a universal law; stop earlier when evidence converges and extend only by explicit policy;
- numeric quality, coverage, latency, and rollout thresholds are examples until the project and risk owner define real values;
- a different model or agent is advisory independence, not delegated merge, release, or risk authority.

Not imported:

- external reviewer access or mutation authority without user permission;
- context-free percentage targets;
- broad simplification that removes security, accessibility, data safety, observability, or contractual behavior.

## 6. Ponytail

Reviewed scope: [repository README](https://github.com/DietrichGebert/ponytail), core skill, review/audit guidance, [agentic benchmark](https://github.com/DietrichGebert/ponytail/blob/main/benchmarks/results/2026-06-18-agentic.md), and the benchmark correctness correction.

Adopted:

- trace the actual code and runtime flow before suggesting a design;
- ask whether new behavior is needed at all;
- reuse project code, then standard library, native platform capability, and installed dependencies before adding custom code;
- prefer the smallest clear expression and minimum new code;
- place a fix at the narrowest shared boundary that owns the invariant;
- prefer deletion or consolidation when it preserves required behavior;
- never cut validation, security, accessibility, trust boundaries, data-loss protection, or required error handling for line-count reduction;
- isolate benchmark treatment and control arms from hooks, plugins, injected context, caches, and shared state;
- inspect the benchmark gate itself: malformed code fences, wrong deliverables, or mismatched scorers can create false results.

Adapted:

- the simplicity ladder runs only after reliability, safety, recovery, and explicit requirements define completeness;
- simplicity is one review lens, not the sole verdict.

Not imported:

- repository-specific benchmark percentages as universal expectations;
- plugin installation as a prerequisite;
- “fewer lines” as evidence of better architecture by itself.

## 7. Google SRE

Reviewed scope: the official [SRE Book introduction](https://sre.google/sre-book/introduction/) and the concepts it introduces for later chapters.

Adopted:

- SRE applies software engineering to operational problems and seeks to replace recurring manual work with safer systems;
- track and bound toil so reliability work is not silently consumed by repetitive operations;
- reliability includes availability plus latency, performance, efficiency, change management, monitoring, emergency response, and capacity planning;
- reliability targets are product decisions; an error budget makes the velocity/stability tradeoff explicit;
- monitoring should produce actionable alerts, tickets, or diagnostic records, with a human paged only when action is required;
- change should be progressive, observable, rapidly detectable, and safely reversible;
- playbooks reduce recovery ambiguity;
- postmortems are blameless learning artifacts with owned corrective actions.

Adapted:

- use an SLI/SLO and error budget when applicable, or an explicit domain-equivalent threshold when it is not;
- an alert is incomplete without a decision threshold, owner, and response;
- automation is treated as an actor with inhibit, restart, reconciliation, and audit behavior.

Not imported:

- Google's staffing split, outage percentages, or other empirical figures as universal targets;
- 100% reliability as the default objective;
- organization-specific scale, staffing, or infrastructure assumptions.

## 8. Claude SDLC Harness

Reviewed scope: [repository README](https://github.com/BaseInfinity/claude-sdlc-harness), SDLC workflow, architecture guidance, competitive audit, and [wizard](https://github.com/BaseInfinity/claude-sdlc-harness/blob/main/CLAUDE_CODE_SDLC_WIZARD.md).

Adopted:

- plan before code and require tests/evidence before shipping;
- escalate when confidence is low or risk is high;
- same-context self-review is weaker than review with separate context;
- high-stakes work benefits from independent or cross-model challenge;
- custom automation must demonstrate value over native or existing capability;
- measure whether the process improves outcomes instead of assuming more controls are better;
- user/accountable owner remains the authority for business tradeoffs and residual risk.

Adapted:

- assurance lanes A0–A4 replace harness-specific scoring;
- independent review requirements follow impact and uncertainty, not a named model;
- custom-vs-native proof includes lifecycle, permissions, cost, failure, and rollback.

Not imported:

- product-specific hooks, model selections, installation steps, or numerical scores;
- maintainer benchmark claims as general evidence;
- automatic authority for a reviewer to mutate, merge, release, or deploy.

## 9. SDLC Studio

Reviewed scope: [repository README](https://github.com/DarrenBenson/sdlc-studio), main skill, [reference philosophy](https://github.com/DarrenBenson/sdlc-studio/blob/main/.claude/skills/sdlc-studio/reference-philosophy.md), review, audit, reconciliation, and test-validation guidance.

Adopted:

- flow from specification to criteria, plan, review, and evidence;
- author and reviewer separation is a mechanical gate for consequential work;
- acceptance criteria should be executable;
- a test must be shown capable of failing for its target defect;
- brownfield requirements are provisional until tests pass against the existing implementation;
- exact files and artifacts are source of truth; indexes/status views are derived and reconciled;
- invalidate evidence at the exact surface it proved, rather than reflexively discarding or reusing a whole report;
- release review asks the live forge whether required checks passed for the current head;
- audit uses explicit lenses and a refutation panel;
- incomplete, timed-out, or budget-excluded review candidates are UNJUDGED, not refuted or approved;
- material findings are written to the durable artifact or explicitly declined with reason;
- expensive fan-out and partial coverage require visible scope, budget, and approval.

Adapted:

- compact templates replace a mandatory backlog/persona/document hierarchy;
- file-or-decline is applied to material findings, not every transient observation;
- evidence invalidation remains subject to project policy that may require a full suite.

Not imported:

- the complete persona, backlog, or command framework;
- large fan-out by default;
- status derived from prose when exact artifacts or live state disagree.

## 10. Flutter-Craft

Reviewed scope: [repository README](https://github.com/vp-k/flutter-craft), planning, executing plans, verification, receiving review, worktree, and parallel-work guidance.

Adopted:

- separate planning, execution, verification, and finishing so claims do not outrun evidence;
- execute in reviewable batches with checkpoints;
- require fresh evidence before completion claims;
- process review feedback technically: verify, correct, clarify, or decline with evidence instead of reflexive agreement;
- parallelize only independent discovery or tasks with isolated outputs and resources;
- use isolated workspaces to reduce file/branch conflicts.

Adapted:

- isolation inventory includes ports, services, emulators, networks, databases, queues, schedulers, credentials, quotas, and release lanes;
- batch size follows task/risk and is not fixed numerically.

Not imported:

- Flutter-specific packages, architecture layers, test priorities, or tooling;
- the claim that a worktree isolates runtime resources. It isolates checked-out files and branch state, not the world.

## 11. Risk Assessment Templates

Reviewed scope: [repository README and templates](https://github.com/henu-wang/risk-assessment-templates).

Adopted:

- risk is a scenario with a trigger, affected asset/process, owner, likelihood and impact rationale;
- maintain mitigation, contingency, early-warning indicators, status, review date, and change log;
- treatment choices are avoid, mitigate, transfer, or accept;
- include change risk and FMEA-style failure mode/effect/detection thinking when appropriate;
- keep the register alive through review events instead of treating it as a one-time form.

Adapted:

- likelihood and impact use project-defined scales;
- scores rank attention but do not create measured probabilities;
- concise records are allowed for A1/A2 while A3/A4 require fuller rationale and evidence.

Not imported:

- example monetary, probability, timing, emoji, or escalation thresholds as universal rules;
- risk acceptance without an accountable owner.

## 12. Hack23 risk-assessment skill

Reviewed scope: the exact [risk-assessment SKILL.md](https://github.com/Hack23/homepage/blob/master/.github/skills/governance/risk-assessment/SKILL.md).

Adopted:

- analyze assets, threats, vulnerabilities, and concrete scenarios systematically;
- distinguish inherent risk before controls from residual risk after controls;
- classify controls as preventive, detective, or corrective;
- ask for evidence of control effectiveness, not just control existence;
- name owner, treatment, review status, and acceptance authority;
- reassess on cadence and on material change or incident.

Adapted:

- use the minimum risk taxonomy that preserves the important decision;
- combine cybersecurity reasoning with operational, data, compatibility, financial, and user-harm risks as the task requires.

Not imported:

- mandatory 5×5 matrices;
- AWS-specific control assumptions;
- EUR thresholds, regulatory mappings, or review cadence from another organization;
- cost-benefit conclusions without the current project's costs and consequences.

## 13. Cross-source synthesis

The combined method is:

1. **Establish truth and authority.** Recover exact live state and identify who may decide or mutate.
2. **Route the work.** Choose idea, feature, bug, migration, incident, release, or review instead of a universal lifecycle.
3. **Build the V trace.** Pair each definition with boundary-matched proof and connect requirement, risk, design owner, implementation, criterion, evidence, and state.
4. **Define completeness.** Add reliability, security, privacy, data integrity, accessibility, compatibility, observability, recovery, and residual-risk requirements.
5. **Minimize safely.** Trace the actual path, use the narrow owning boundary, reuse existing/native mechanisms, and add minimum new code.
6. **Execute incrementally.** Use dependency-ordered vertical slices, checkpoints, and evidence reuse only when dependencies are unchanged.
7. **Prove the proof.** Inventory surfaces, assert nonzero expected counts, exercise the real path, use independent oracles, and demonstrate negative controls.
8. **Challenge independently.** Separate author and reviewer at A3/A4, bound the doubt cycle, and reconcile findings technically.
9. **Release as an operational experiment.** Bind identity, expose gradually, monitor user-facing thresholds, abort or roll back on breach, and validate in the real environment.
10. **Preserve state and learning.** Use typed lifecycle states, durable handoffs, risk review, errors/corrections, and blameless corrective action.

Precedence when concepts conflict:

1. explicit user decisions, product requirements, law, and accountable operational constraints;
2. V-model completeness and bounded risk;
3. security, privacy, data integrity, accessibility, accounting, and trust boundaries;
4. reliability, observability, rollout, rollback, and recovery;
5. KISS/YAGNI/reuse/minimum code;
6. optional source-framework conventions.

## 14. Practices intentionally not imported

| Rejected universal prescription | Reason |
|---|---|
| One workflow for every change | Ideas, bugs, incidents, releases, and features have different questions and terminal states. |
| V-model as late, sequential testing | It hides learning and moves failure discovery to the end; this skill pairs and verifies continuously. |
| Full framework adoption | It adds roles, files, commands, and ceremony without proving additional assurance. |
| Fixed coverage, SLO, risk, or rollout percentages | Source numbers are examples or local policy, not facts about the target system. |
| Model/vendor-specific reviewer requirement | Independence and competence matter; named tools change and do not own risk. |
| Green local/CI result as release acceptance | Artifact, environment, and V-level identities differ. |
| Same-author independent certification | Shared assumptions create correlated blind spots. |
| Generated brownfield specification as truth | It must be validated against the actual implementation and consumers. |
| Worktree as complete isolation | Runtime and organizational resources remain shared. |
| Fewer lines as the primary objective | Completeness and safety precede minimization. |
| Risk score as probability or decision | Scores prioritize; accountable owners decide with rationale and uncertainty. |
| Blind retries | Ambiguous external effects require intent identity and reconciliation. |

## 15. Verified source snapshots

The identifiers below are Git blob SHAs observed through authenticated repository reads on 2026-09-21. They identify file content, not a repository commit or release. Branch links remain convenient; the SHA allows a later reader to detect content drift.

| Repository | Artifact | Git blob SHA |
|---|---|---|
| github/spec-kit | README.md | 2cd0045f4c6065c8d67631b0f68989c9b93ef3ae |
| github/spec-kit | spec-driven.md | 28259ae28f95d7dc0ec79977108f8a574731d98d |
| github/spec-kit | quickstart | 692d725a55a7acfeb5e22014fb4cf5fdddcd77f8 |
| github/spec-kit | bugfix guide | b1f0effff36d15d908bd8275b1fbd40408e16dd0 |
| github/spec-kit | assessment guide | 171de767e7e0bdd279d90f7ab91913650f5d3ab5 |
| github/spec-kit | existing-projects guide | 9736557316e85107330dc8122f2aee153e2c38c0 |
| github/spec-kit | contract-driven guide | 1a5102b8f306f53f03ec61085c199fbdf5e38179 |
| addyosmani/agent-skills | README.md | 6361def414ade46622e6cd527d1faeea2b234224 |
| addyosmani/agent-skills | doubt-driven development | 472c35ab9f32e8ec8b592e5cc7d228ad8cdce278 |
| addyosmani/agent-skills | code review and quality | 7dfa56362fa65fff450ee5aa02393b85b9c26d85 |
| addyosmani/agent-skills | incremental delivery | 9c4f49bc841adb3c0f98baaa9eabd435a5b64ef9 |
| addyosmani/agent-skills | shipping and launch | f3fba8a01265db5547a8755c81902d0aa56c4104 |
| addyosmani/agent-skills | observability and instrumentation | 84d9cb373467fe0e15236e190833ecc90f840c38 |
| addyosmani/agent-skills | planning | 296249b64334bcfd1aeaefd27b9e3e5494e38ec0 |
| DietrichGebert/ponytail | README.md | 6b25e496dbb467bd4d8ed065ce10e13992790591 |
| DietrichGebert/ponytail | core skill | 02c0712c86277d49d18a77da3a2b825657bf02d1 |
| DietrichGebert/ponytail | review guidance | e137a855bd87119a4517895a1000a59b0999e1b8 |
| DietrichGebert/ponytail | audit guidance | 5582d10335daff5b5947f9b77927fbc97f2047f3 |
| DietrichGebert/ponytail | agentic benchmark | 1a602f7e49369841cef39d5b764e1247f78d2bb9 |
| DietrichGebert/ponytail | benchmark correctness correction | 7fa12dbdfc019d5dea071fe9bd8dd56aed1bd1d6 |
| BaseInfinity/claude-sdlc-harness | README.md | 14b18529d2a1eb0bf486a0c457ddf392a2f6a6ed |
| BaseInfinity/claude-sdlc-harness | SDLC workflow | c98549054aad032bc85a01f0f88795dd4acc9cad |
| BaseInfinity/claude-sdlc-harness | architecture guidance | 28af834ec81bdcad2bbae55398d5d44dad418bc5 |
| BaseInfinity/claude-sdlc-harness | competitive audit | b2f19b3f5ecfc34bead66d50b46ff06e3c79aee1 |
| BaseInfinity/claude-sdlc-harness | wizard | 3d77132df4f1060ce3feffe3355c16aa435429bc |
| DarrenBenson/sdlc-studio | README.md | 9b21662fe159b3fb8a376d61e00ee7ee2d747a25 |
| DarrenBenson/sdlc-studio | main skill | f7048f4c69d4d2420e842fc9314cc91d6af135cc |
| DarrenBenson/sdlc-studio | reference philosophy | e2c3edba816de7ea454ac741b595d51ca99250a6 |
| DarrenBenson/sdlc-studio | review guidance | 096edfeb068c7483fdb26a27c718b51b87dd9216 |
| DarrenBenson/sdlc-studio | audit guidance | 8df00aca3e310e784bdd19ba1bf2e1bc3e4a9eac |
| DarrenBenson/sdlc-studio | reconciliation guidance | d1eba1d6da0077e392678bd2182de56acf15656c |
| DarrenBenson/sdlc-studio | test validation | 48a3e031b7a220095ce86347f27b51cf9435fa83 |
| vp-k/flutter-craft | README.md | 7efa9488632495e6e8c9f99faea09e3d2e58c606 |
| vp-k/flutter-craft | planning | 09dd9749067062e465e2ab3dc09d4bcea1f4c477 |
| vp-k/flutter-craft | executing | 61d48a97648f0aa58c42cf2e4791e823938a68e5 |
| vp-k/flutter-craft | verification | 4edf689c8ba75b837942c49f52c22ca4b8b836a7 |
| vp-k/flutter-craft | receiving review | d7708c1aa9bda2e75dec4bdf67247d48439ca3d2 |
| vp-k/flutter-craft | worktrees | b01eb953e6fe09e193fa7bd845ff2dbd3fbd2faa |
| vp-k/flutter-craft | parallel work | 95c4f0fa8838415d399dbfd5ae3494a89fdc7f6 |
| henu-wang/risk-assessment-templates | README.md | 9125c01882726b042a995979edb93e980039dea6 |
| Hack23/homepage | risk-assessment SKILL.md | 55b62d52dc1c312ab31e026a31a08828f1f12ec5 |

The Google SRE and NASA handbook sources are authoritative web publications rather than reviewed GitHub blobs, so this ledger records their URLs and observation date instead of inventing a content SHA.
