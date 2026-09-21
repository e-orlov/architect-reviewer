# Architect Reviewer

**Evidence-first architecture and independent review for software, AI/ML, releases, migrations, incidents, and operational decisions.**

## Is this the best architect and reviewer skill?

**Architect Reviewer is designed to be an unusually complete, project-agnostic, high-assurance architect and reviewer without imposing high ceremony on every task.** It combines:

- an iterative V-model that designs the matching proof with each requirement;
- different routes for ideas, features, bugs, migrations, incidents, releases, and audits;
- assurance levels that scale controls to uncertainty, blast radius, reversibility, and exposure;
- exact artifact and environment identity instead of narrative “green” claims;
- delta-first evidence selection from transitive impact rather than file proximity or indiscriminate full-suite execution;
- bounded evidence-lineage reconciliation from the last accepted immutable baseline to the exact target;
- independent challenge for high-risk work;
- explicit reliability, recovery, residual-risk, and real-world acceptance controls;
- Baseline, Experiment, and Complexity-Promotion gates against AI overengineering;
- KISS and YAGNI only after safety, correctness, observability, and recovery are complete.

That combination makes the skill a strong candidate when the cost of a plausible but unproved answer is higher than the cost of disciplined evidence.

## What problem it solves

Architecture and review often fail in predictable ways: requirements are not testable, tests prove the wrong boundary, changed files are mistaken for complete impact, full suites are repeated without information value, a green CI result is treated as production acceptance, reviewers inspect only the diff, operational risk is deferred, and AI complexity is promoted because it is impressive rather than necessary.

Architect Reviewer turns those failure modes into explicit controls. It asks four separate questions:

1. **What state is the work actually in?**
2. **What claim is being made, at which system boundary?**
3. **What evidence could falsify or support that claim?**
4. **Who has authority to approve the next lifecycle transition or accept residual risk?**

It never treats implementation, verification, merge, release, deployment, and real-world acceptance as synonyms.

## Quick start

Ask the agent to use `architect-reviewer` explicitly, then name the artifact and decision you need. For example:

```text
Use architect-reviewer to design this payment retry feature. Produce the V-model trace,
risk register, testing strategy, rollout/rollback contract, and unresolved decisions.
```

```text
Use architect-reviewer to review this pull request for production readiness.
Do not modify it. Bind every finding and verdict to the exact commit and raw evidence.
```

```text
Use architect-reviewer to decide whether this LLM agent is justified over the current
rules-based baseline. Apply the Baseline, Experiment, and Complexity-Promotion gates.
```

## The operating model

The method combines three axes. None substitutes for another.

| Axis | Decision | Result |
|---|---|---|
| Task route | Is this an idea, feature, bug, migration, incident, release, or review? | The shortest workflow appropriate to the work |
| V-model trace | Which definition is being implemented, and what proof matches its boundary? | Requirement-to-evidence traceability |
| Assurance | How uncertain, irreversible, exposed, or high-impact is the change? | Proportionate A0–A4 controls and review depth |

The V-model is continuous rather than a late-testing waterfall:

| Definition | Matching proof |
|---|---|
| User or business need | Real-world/user acceptance and outcome |
| System requirements | System or end-to-end proof in the declared topology |
| Architecture and contracts | Integration, compatibility, failure, and recovery proof |
| Component design | Component behavior at the owning boundary |
| Implementation | Unit, type, static, and focused invariant checks |

Every blocking row follows this chain:

```text
Requirement → rationale/risk → design owner → implementation slice →
verification level → falsifiable criterion → evidence identity → state
```

## Main concepts and their sources

This is a synthesis, not a wholesale copy of any framework. Source-specific commands, numeric targets, architectures, and organization policies are adapted or rejected unless the target project supplies evidence for them.

| Primary source | Concept adopted or adapted in this skill |
|---|---|
| [NASA Systems Engineering Handbook](https://ntrs.nasa.gov/citations/20170001761) | The systems-engineering basis for the V-model spine: pair definition and decomposition with integration, verification, and validation; distinguish “built to specification” from “solves the real need.” The skill makes this iterative and slice-based instead of a late waterfall. |
| [GitHub Spec Kit](https://github.com/github/spec-kit) | Separate routes for feature development, bug repair, and idea assessment; define WHAT/WHY before HOW; clarify uncertainty; use requirement-quality checklists; order work by dependency; converge code, tests, docs, contracts, configuration, and operations. |
| [Addy Osmani Agent Skills](https://github.com/addyosmani/agent-skills) | Process-shaped skills with checkpoints, exit criteria, red flags, anti-rationalization, bounded doubt, incremental delivery, staged rollout, and operator-oriented observability. |
| [Ponytail](https://github.com/DietrichGebert/ponytail) | Trace the actual flow before changing it; ask whether new behavior is needed; reuse existing/native mechanisms; place the fix at the narrowest boundary that owns the invariant; protect safety edges from line-count simplification. |
| [Google SRE](https://sre.google/sre-book/introduction/) | Software engineering for operations, toil reduction, product-owned reliability targets, error-budget thinking, actionable monitoring, progressive change, fast rollback, playbooks, and blameless corrective learning. |
| [Claude SDLC Harness](https://github.com/BaseInfinity/claude-sdlc-harness) | Plan and test before shipping, escalate consequential uncertainty, prefer separate-context review for high-risk work, measure process outcomes, and require custom machinery to beat native or existing capability. |
| [SDLC Studio](https://github.com/DarrenBenson/sdlc-studio) | Executable acceptance, mechanical author/reviewer separation, proof that a test can detect its target defect, artifact-derived status, evidence invalidation by dependency, and brownfield validation against the live implementation. |
| [Flutter-Craft](https://github.com/vp-k/flutter-craft) | Separate planning, execution, verification, and finishing; use reviewable batches and checkpoints; require evidence before completion claims; process feedback technically; parallelize only genuinely independent work. Flutter-specific architecture and packages are not imported. |
| [Risk Assessment Templates](https://github.com/henu-wang/risk-assessment-templates) | A living risk register with scenario, trigger, owner, warning signals, mitigation, contingency, treatment, status, and review history; contextual rather than universal scoring. |
| [Hack23 risk-assessment skill](https://github.com/Hack23/homepage/blob/master/.github/skills/governance/risk-assessment/SKILL.md) | Systematic asset/threat/vulnerability analysis; inherent versus residual risk; preventive, detective, and corrective controls; evidence of effectiveness; accountable treatment and acceptance. Its fixed matrix, currency thresholds, and organization-specific cadence are not imported. |
| [Google Rules of Machine Learning](https://developers.google.com/machine-learning/guides/rules-of-ml) | Metrics first, a credible no-AI/heuristic/simple-model baseline, independently testable infrastructure, simple early models, and complexity only after a measured gap remains. |
| [NIST AI RMF Generative AI Profile](https://doi.org/10.6028/NIST.AI.600-1) | Risk-proportionate AI controls, provenance, deployment-relevant measurement, baseline comparison, lifecycle TEVV evidence, documented limitations, monitoring, fallback, and recovery. The skill does not claim NIST certification. |
| [OpenAI eval guidance](https://developers.openai.com/api/docs/guides/evals) | Describe the task and expected behavior, run versioned test inputs, analyze results, and iterate from evaluation evidence rather than anecdotal demonstrations. |
| [FrugalGPT](https://arxiv.org/abs/2305.05176) | Treat routing and model cascades as empirical cost/quality candidates. A cascade is never presumed simpler: router errors, fallback, latency, operational cost, and recovery are part of the comparison. |

The detailed source ledger records what was adopted, adapted, and intentionally rejected, together with reviewed repository blob identities: [references/source-synthesis.md](references/source-synthesis.md).

## Controls against AI overengineering

AI/ML introduction or a material increase in lifecycle complexity must pass three gates:

| Gate | Required question | Possible decision |
|---|---|---|
| Baseline | What is the simplest credible comparator, and what material gap remains? | `STOP` if the baseline already meets the validated need; otherwise `READY_FOR_EXPERIMENT` |
| Experiment | Does a predeclared candidate close that gap on decision-capable, versioned evidence without hiding regressions or contamination? | `VALIDATED_NO_PROMOTION`, `READY_FOR_PROMOTION_REVIEW`, `EXPERIMENT_ONLY`, `STOP`, `BLOCKED`, or `UNKNOWN` |
| Complexity Promotion | Is the demonstrated benefit still material after total lifecycle cost, latency, safety, ownership, monitoring, fallback, rollback, and retirement are counted? | `APPROVED_LIMITED`, `PROMOTED`, `EXPERIMENT_ONLY`, `STOP`, `BLOCKED`, or `UNKNOWN` |

The comparison is project-specific. The skill deliberately rejects universal claims such as “70% is enough,” “agents are more flexible,” “a larger model is safer,” “data-centric means change only data,” or “a cascade is automatically cheaper.” Read [references/ai-complexity-strategy.md](references/ai-complexity-strategy.md) for the full protocol.

## Delta-first evidence and test selection

Before implementation or review, the skill applies:

```text
delta → transitive impact → invalidated claims → required proof →
targeted execution → final convergence if justified
```

The analysis is dependency-based rather than file-based. It includes source, schemas, configuration, workflows, dependencies, generated artifacts, environment state, external interfaces, direct consumers, and transitive consumers. Every relevant claim is classified as `INVALIDATED`, `PARTIALLY_INVALIDATED`, `REUSABLE`, `NEWLY_REQUIRED`, `N/A`, or `UNKNOWN`.

For A2+ work, a Delta Evidence Plan is mandatory before implementation, review certification, or downstream `GO`. It records the exact baseline and target, impact graph, evidence-reuse rationale, smallest sufficient test set, justified broad gates, expansion triggers, and expected evidence/context cost. A full suite is still required when shared foundations, incomplete dependency knowledge, multiple persistence boundaries, A3/A4 exposure, release boundaries, or project policy justify convergence. It is not run merely to produce a larger `PASS` count.

This design is consistent with dependency-based selection and safe fallback described by [Microsoft Test Impact Analysis](https://learn.microsoft.com/en-us/azure/devops/pipelines/test/test-impact-analysis?view=azure-devops), direct/transitive/reverse-dependency analysis in the [Bazel Query Guide](https://bazel.build/query/guide), immutable baseline comparison through the [GitHub Compare Commits API](https://docs.github.com/en/rest/commits/commits#compare-two-commits), and lifecycle-aware selective/comprehensive execution in [Develocity Predictive Test Selection](https://docs.develocity.ai/2026.2/guides/predictive-test-selection/). These are supporting mechanics, not required products.

The full rule is in [references/delta-first.md](references/delta-first.md).

## Testing and acceptance

The testing strategy separates **test level** from **execution stage**. Unit, component, contract, integration, system/E2E, regression, and acceptance checks prove different boundaries; local, CI, shared integration, preproduction, and progressive production are places where evidence is produced.

Core rules include:

- derive test selection from the exact delta, transitive impact, and invalidated claims;
- design each blocking test from a requirement or risk, not from a desire to fill every layer;
- use AAA or Given–When–Then when they improve clarity, not as mandatory tooling;
- require applicable nonzero test discovery or a justified `N/A`;
- demonstrate that a blocking test detects its target defect when assurance and safety require it;
- use coverage as supporting evidence, never as a universal percentage target;
- call staging **target-like**, then record configuration, data, topology, identity, dependency, load, and operational differences from production;
- keep merge, release, deployment, and real-world acceptance as separate states.

See [references/testing-strategy.md](references/testing-strategy.md).

Its primary testing references include [Microsoft's unit-testing guidance](https://learn.microsoft.com/en-us/dotnet/core/testing/unit-testing-best-practices), the [Cucumber Gherkin reference](https://cucumber.io/docs/gherkin/reference/), [OWASP source-code analysis guidance](https://owasp.org/www-community/Source_Code_Analysis_Tools), [Google's code-coverage guidance](https://testing.googleblog.com/2020/08/code-coverage-best-practices.html), and [Playwright's browser-testing practices](https://playwright.dev/docs/best-practices). These contribute principles, not mandatory tools.

## Evidence and verdicts

The skill prevents ambiguous “PASS” or “DONE” claims by keeping four namespaces separate:

| Namespace | Examples | Meaning |
|---|---|---|
| Gate verdict | `PASS`, `FAIL`, `BLOCKED`, `UNKNOWN` | Result for one named invariant and exact evidence scope |
| Lifecycle state | `IMPLEMENTED_UNVERIFIED`, `READY_FOR_MERGE`, `RELEASED_UNACCEPTED` | Current state of the artifact, not a quality adjective |
| Route or AI decision | `GO`, `STOP`, `READY_FOR_EXPERIMENT`, `PROMOTED` | Decision inside one task-specific route |
| Review verdict | `CERTIFIED`, `NOT CERTIFIED`, `UNKNOWN` | Whether the reviewed claims are supported within the declared scope |

Evidence is bound to source/build/configuration/environment identity, observation time, expected scope, oracle, negative-control status, dependencies, and invalidation rules. A local or CI success cannot silently become a production-readiness claim.

### Result-Acceptance Gate and mandatory GitHub connection

A latest green result is a current-state fact, not sufficient review evidence. Before the architect or reviewer accepts an executor result, issues the next implementation mandate, authorizes merge/release/deployment, or declares `CERTIFIED`, the Result-Acceptance Gate traces the complete bounded evidence lineage from the last independently accepted immutable baseline to the exact final target. Every relevant pass, failure, cancellation, timeout, skip, retry, rerun, superseded run, expected RED run, and mutation run remains visible until independently reconciled from primary evidence.

For a GitHub-backed target, an authenticated GitHub connector is mandatory. It must expose the exact repository, PR, base/head commits, required checks, workflow definitions, all relevant workflow attempts, jobs, steps, discovered counts, logs, and artifacts. An executor summary, screenshot, public search result, or latest-check view is not a substitute. If any material surface is unavailable or an anomaly remains unexplained, the affected claim is `UNKNOWN`; the skill forbids progression or `GO` and permits only evidence recovery or an access request. A failure still reproducible on the exact target makes the gate `FAIL` and the lifecycle state `BLOCKED`; only a bounded diagnostic or corrective task may then address the reconciled item.

This requirement follows the evidence surfaces and semantics documented by GitHub for [workflow runs](https://docs.github.com/en/rest/actions/workflow-runs), [workflow jobs and all executions](https://docs.github.com/en/rest/actions/workflow-jobs), [run logs](https://docs.github.com/en/actions/how-tos/monitor-workflows/use-workflow-run-logs), [artifacts](https://docs.github.com/en/rest/actions/artifacts), [`continue-on-error`](https://docs.github.com/en/actions/reference/workflows-and-actions/workflow-syntax#jobsjob_idcontinue-on-error), and [required status checks](https://docs.github.com/en/repositories/configuring-branches-and-merges-in-your-repository/managing-protected-branches/about-protected-branches). For a non-GitHub forge, the equivalent authenticated native connector or API is required. Connection is read-only evidence authority by default; it does not grant permission to rerun, edit, merge, release, or deploy.

## What the skill deliberately refuses

- One heavyweight workflow for every task.
- Late, sequential V-model testing.
- Same-author “independent” certification for A3/A4 work.
- “Run everything to be safe” without a convergence, risk, boundary, or policy reason.
- “Only test the files that changed” without tracing direct and transitive impact.
- Evidence reuse based only on hash equality, freshness, or an unchanged file.
- A latest green run or executor summary treated as the complete evidence record.
- Historical failures, cancellations, skips, timeouts, or reruns erased by a later pass.
- GitHub live-state acceptance without an authenticated connector and material Actions evidence.
- Universal coverage, SLO, rollout, risk, uplift, or sample-size thresholds.
- Generated brownfield specifications treated as truth without live validation.
- Staging described as production-identical without exact evidence.
- Worktrees treated as isolation for databases, networks, queues, credentials, quotas, or release lanes.
- AI agents, RAG, fine-tuning, larger models, multi-agent systems, or cascades adopted without a measured need.
- Simplicity that removes security, privacy, accessibility, accounting, observability, error handling, recovery, or an explicit requirement.

## Repository map

| File | Purpose |
|---|---|
| [SKILL.md](SKILL.md) | Authoritative core workflow and non-negotiable rules |
| [references/v-model.md](references/v-model.md) | Continuous V-model trace and route overlays |
| [references/task-routes.md](references/task-routes.md) | Idea, feature, bug, migration, incident, release, and review routes |
| [references/delta-first.md](references/delta-first.md) | Exact-delta analysis, transitive impact, evidence states, targeted selection, convergence triggers, and cost controls |
| [references/testing-strategy.md](references/testing-strategy.md) | Delta-driven test selection, test levels, execution pipeline, scenario design, environment differences, and acceptance |
| [references/ai-complexity-strategy.md](references/ai-complexity-strategy.md) | Baseline, Experiment, and Complexity-Promotion gates |
| [references/evidence-and-gates.md](references/evidence-and-gates.md) | Evidence contracts, mandatory forge connection, failure reconciliation, Result-Acceptance, risk, production, and review gates |
| [references/operating-model.md](references/operating-model.md) | Authority, precedence, lifecycle states, continuity, and concurrency |
| [references/templates.md](references/templates.md) | Reusable Delta Evidence Plan, trace, gate, evidence-lineage, risk, state, and decision records |
| [references/source-synthesis.md](references/source-synthesis.md) | Source-by-source adoption, adaptation, rejection, and provenance ledger |

## Limits

- This is an engineering decision aid, not a guarantee that defects or risks will be found.
- `CERTIFIED` is a scoped review verdict defined by this skill, not legal, regulatory, safety, security, or standards-body certification.
- Projects and accountable owners still define requirements, thresholds, policy, risk tolerance, and approval authority.
- Source projects do not endorse this synthesis, and their names do not transfer their claims or certifications to it.
- Source links and snapshots can age; recheck primary documentation before relying on current commands, product behavior, or empirical performance claims.

`SKILL.md` is the authoritative agent instruction. This README is a human-facing explanation and is intentionally not part of the runtime reference chain.
