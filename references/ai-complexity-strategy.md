# AI/ML complexity strategy

## Contents

1. Scope and invariant
2. Three-gate protocol
3. Baseline Gate
4. Experiment Gate
5. Complexity-Promotion Gate
6. Complexity and comparator inventory
7. Mechanism-specific overlays
8. V-model and assurance integration
9. STOP conditions and anti-rationalization

## 1. Scope and invariant

Apply this strategy when work introduces AI/ML or materially changes any of the following:

- model, provider, learned feature, training, fine-tuning, or inference path;
- prompt, evaluator, retrieval, embedding, index, grounding, or context assembly;
- tool use, routing, cascade, fallback, agent, multi-agent coordination, or autonomous side effect;
- number of model calls, external dependencies, persistent stores, queues, retries, or decision branches;
- evaluation data, labels, decision thresholds, or production monitoring used to justify the system.

The invariant is:

> Use the least lifecycle complexity that satisfies the validated need and its safety, reliability, and recovery constraints.

Do not translate this invariant into a universal technology ladder. A simple heuristic can be the right baseline, while a growing rule engine can be more complex than a small learned model. Compare complete candidates in their actual context.

Define project-specific metrics, thresholds, uncertainty treatment, data requirements, and risk tolerance. Use quantitative measures when they validly represent the decision; otherwise predeclare an observable qualitative rubric and adjudication method rather than inventing precision. Never import a fixed accuracy, coverage, sample-size, significance, latency, cost, or uplift threshold from another system.

## 2. Three-gate protocol

Run the gates in order whenever AI/ML complexity is introduced or materially increased:

1. **Baseline Gate:** establish the simplest credible comparator and name the gap it leaves.
2. **Experiment Gate:** test a named hypothesis on versioned evidence under controlled or explicitly disclosed differences.
3. **Complexity-Promotion Gate:** permit added complexity only when it closes the measured gap better than acceptable lower-complexity alternatives after lifecycle cost and risk are included.

Record each gate using the generic Gate Record plus the AI Complexity Decision Record in [templates.md](templates.md). A gate verdict remains `PASS`, `FAIL`, `BLOCKED`, or `UNKNOWN`; the resulting decision may be `STOP`, `READY_FOR_EXPERIMENT`, `EXPERIMENT_ONLY`, `APPROVED_LIMITED`, or `PROMOTED`.

Do not use these gates to simplify away security, privacy, accessibility, data integrity, human oversight, observability, fallback, rollback, or an explicit requirement.

## 3. Baseline Gate

Answer:

> What is the least-complex credible way to address the need, and what measured gap remains?

Select the simplest credible comparator; do not implement every possible rung. Depending on the task, use one of:

- no change, no automation, or current production behavior;
- a human or manual workflow;
- an existing product or platform capability;
- deterministic validation, rules, search, SQL, calculation, or a small script;
- a simple statistical or ML model;
- a single existing model call without additional retrieval, routing, tools, agents, or training.

Record:

- user or business need, non-goals, and prohibited outcomes;
- baseline design and why it is credible;
- exact baseline artifact, configuration, data, and environment identity;
- evaluation-set identity, provenance, scope, exclusions, and known limitations;
- primary outcome metric plus safety, quality, cost, latency, and operational guardrails that matter;
- raw baseline result and uncertainty;
- the named acceptance gap, if one remains.

Pass only when the baseline is reproducible enough for the decision and a material unmet gap is evidenced. Then return `READY_FOR_EXPERIMENT`.

Return `STOP` when the baseline already meets the validated need and guardrails. Return `BLOCKED` or `UNKNOWN` when the comparator, evaluation set, metric, or evidence is not decision-capable. Do not invent a universal target such as “the baseline must solve 70%.”

## 4. Experiment Gate

Answer:

> Does the candidate close the named gap, and can the observed difference be attributed as claimed?

State the hypothesis before interpreting results:

`Changing <primary mechanism> is expected to improve <metric/gap> for <scope> without breaching <guardrails>.`

Bind each experiment arm to the relevant identities:

- code and dependency identity;
- model, provider, endpoint, version, and model settings;
- system/developer prompt, templates, schemas, tools, and routing policy;
- training, fine-tuning, retrieval, evaluation, and label data versions;
- split logic, exclusions, deduplication, leakage controls, and temporal cutoff;
- index, embedding model, knowledge snapshot, and retrieval configuration;
- evaluator, grader, rubric, human-review protocol, and aggregation logic;
- runtime, serving, feature flags, seed where applicable, and observation time.

Use one primary explanatory variable per experiment when practical. Hold other material factors constant or disclose them. If several coupled elements must change together, treat the result as a composite-candidate comparison and do not claim which element caused the result. Use ablation when promotion depends on the value of one element.

Before running or accepting the comparison:

1. Predeclare the primary metric or rubric, guardrails, practical-equivalence margin or qualitative decision boundary, scope, and decision rule.
2. Verify that the evaluation set represents the intended task and important slices.
3. Keep tuning data separate from final decision evidence where feasible; disclose reuse and contamination risk.
4. Address nondeterminism with repeated trials, paired comparison, uncertainty intervals, or another justified method.
5. Use an independent oracle where possible and show that the evaluation can reject a known-bad candidate.
6. Inspect regressions and prohibited outcomes, not only the average score.
7. Preserve raw per-case results or an auditable equivalent, subject to privacy and retention constraints.

A data-centric experiment is one valid route when error analysis points to coverage, labels, duplication, freshness, leakage, or representativeness. Do not turn “data-centric” into a rule that code and model must always remain fixed; change the axis supported by evidence.

Pass only when the evidence supports the hypothesis strongly enough for the project-defined decision and no blocking guardrail is breached. Otherwise return `FAIL`, `BLOCKED`, or `UNKNOWN` without promoting complexity.

## 5. Complexity-Promotion Gate

Answer:

> Is the measured benefit worth the additional lifecycle complexity, and is there no acceptable lower-complexity candidate?

Require a passed Baseline Gate and Experiment Gate. Then record:

- the baseline gap being closed;
- the proposed mechanism and every new component or dependency it introduces;
- lower-complexity alternatives considered and why they are insufficient;
- measured improvement, uncertainty, practical significance, and affected slices;
- lifecycle cost: build, evaluation, inference, latency, data, maintenance, monitoring, incident response, migration, and retirement;
- new security, privacy, safety, vendor, data-governance, and compliance exposure;
- new failure modes, correlated failures, ambiguous outcomes, and blast radius;
- observability, owner, budget, fallback, rollback, and decommission path;
- target-topology verification and staged-release plan when production exposure is material.

Choose the least-complex candidate on the admissible quality/cost/risk frontier. When candidates are practically equivalent within the predeclared margin or qualitative decision boundary and uncertainty, choose the one with lower lifecycle complexity. Do not equate simplicity only with parameter count, feature count, lines of code, or number of services.

Use these decision states:

| State | Meaning |
|---|---|
| `STOP` | The baseline is sufficient or the added mechanism has no evidenced need. |
| `EXPERIMENT_ONLY` | Evidence is promising but insufficient for operational adoption. |
| `APPROVED_LIMITED` | Promotion is justified only for a bounded cohort, traffic slice, task class, or canary. |
| `PROMOTED` | Benefit, lifecycle completeness, and risk controls are evidenced for the stated scope. |
| `BLOCKED` / `UNKNOWN` | A required comparator, oracle, identity, control, or owner is missing. |

These are scoped AI-complexity decisions, not artifact lifecycle states. Continue to use the lifecycle model in [operating-model.md](operating-model.md) for implementation, verification, merge, release, and acceptance progress.

Product tradeoffs and residual-risk acceptance remain with the accountable owner. The reviewer can certify evidence quality, not accept business risk.

## 6. Complexity and comparator inventory

Count complexity across the whole lifecycle. Inventory at least the applicable dimensions:

| Dimension | Examples |
|---|---|
| Decision path | rules, classifiers, routers, policy layers, branches, abstention |
| Models | count, size, provider, fine-tunes, embeddings, graders, fallbacks |
| Calls | calls per task, tokens, concurrency, retries, timeouts, paid operations |
| Context and data | prompts, retrieval, indexes, training data, labels, freshness, provenance |
| State | memory, caches, queues, ledgers, checkpoints, reconciliation |
| Integrations | tools, external APIs, credentials, network and trust boundaries |
| Operations | deployment, monitoring, drift detection, incident response, rollback, retirement |
| Human system | review burden, escalation, override, appeal, content or decision moderation |

Compare end-to-end systems, not isolated model benchmark scores. Include preprocessing, routing, retrieval, policy layers, post-processing, humans, and fallbacks in both the measured outcome and cost.

## 7. Mechanism-specific overlays

### Heuristics and classical ML

- Use a simple heuristic as a credible baseline when it captures useful domain knowledge.
- Do not grow a brittle rule system merely to avoid ML; compare maintainability and lifecycle cost.
- Start with interpretable models where they meet the need and materially improve debugging or control.
- Use held-out and temporally appropriate evidence; inspect generalization, calibration, leakage, and overfitting where relevant.
- Use feature ablation or regularization when feature complexity is material. Retain extra features only when their value exceeds their lifecycle cost and risk.

### LLM, retrieval, tools, and agents

- Compare against a single-call or otherwise simpler baseline when credible.
- Add retrieval only for a named grounding, freshness, coverage, or provenance gap; measure retrieval and answer quality separately and end to end.
- Add tools only for capabilities or evidence access the model cannot reliably provide alone; define authority and side effects.
- Add an agent loop only when bounded iteration or action is required; define termination, budget, state, recovery, and ambiguous-outcome handling.
- Add multiple agents only when separation of responsibility, context, competence, or trust boundary has measured value beyond one orchestrated process. Include coordination cost and correlated error.

These are comparison obligations, not a mandatory sequence. Skip an inapplicable comparator with a recorded reason.

### Cascades and routers

Before promoting a cascade or router, require:

- evidence that the workload contains distinguishable classes that benefit from different paths;
- router quality, calibration, threshold, uncertainty, and misrouting analysis;
- safe abstention or fallback for uncertain and failed routing;
- end-to-end quality and guardrails, not only component scores;
- latency and cost including routing, retries, fallbacks, and duplicated calls;
- per-route telemetry, drift monitoring, override, rollback, and a single-path recovery mode.

Do not call a cascade simpler merely because most requests use a smaller model. The routing and operational system is additional complexity that must earn its cost.

### Fine-tuning and custom models

Before promotion, compare against credible prompt, schema, data-quality, retrieval, policy, and existing-model alternatives. Account for training-data rights, provenance, reproducibility, evaluation, serving, drift, retraining, rollback, and retirement. Preserve access to an appropriate untuned or previous baseline for diagnosis when feasible.

## 8. V-model and assurance integration

Pair AI/ML definitions with matching proof:

| Definition | Matching proof |
|---|---|
| User/business outcome | Real-world acceptance against the baseline and product guardrails |
| System behavior and limits | End-to-end evaluation in deployment-like conditions and important slices |
| Architecture: retrieval, routing, tools, agents, fallbacks | Integration, failure, security, recovery, and compatibility tests |
| Component: parser, feature, retriever, router, prompt, grader | Component contract tests and falsifiable evals |
| Implementation and configuration | Unit, schema, static, identity, and deterministic invariant checks |

Apply assurance proportionately:

- A0/A1 may use a concise record when no runtime or consequential decision is affected.
- A2 requires a durable decision record, versioned evidence, integration checks, and owned limitations.
- A3/A4 requires target-like evaluation, independent review, staged exposure, monitoring, fallback/rollback, and accountable residual-risk acceptance.

Promotion evidence expires when a material identity or assumption changes. Invalidate only affected claims unless project policy requires broader revalidation.

## 9. STOP conditions and anti-rationalization

Stop promotion or return `BLOCKED/UNKNOWN` when:

- no credible baseline or named gap exists;
- metrics or thresholds were chosen after seeing results without disclosure and revalidation;
- experiment arms differ in material undisclosed ways;
- evaluation data is contaminated, unrepresentative, identity-unknown, or too weak for the claim;
- improvement does not cross the practical-equivalence margin or qualitative decision boundary, or is indistinguishable from measurement uncertainty;
- an average improvement hides a blocking slice or prohibited outcome;
- lifecycle cost, ownership, fallback, rollback, or monitoring is missing;
- a cascade, agent, or tool can create unbounded calls, cost, state, or side effects;
- complexity is justified only by novelty, flexibility, future use, benchmark prestige, or vendor claims.

| Temptation | Required correction |
|---|---|
| “An LLM is more flexible.” | Name the present gap and compare it with the simplest credible alternative. |
| “We will add evals later.” | Define the decision-capable evaluation before promotion. |
| “Only the prompt changed.” | Bind prompt, model, tools, data, evaluator, and runtime identities. |
| “The average score improved.” | Inspect uncertainty, important slices, regressions, and guardrails. |
| “One experiment was green.” | Check repeatability, contamination, oracle validity, and practical significance. |
| “Data-centric means changing only data.” | Change the evidence-supported primary axis and disclose all other differences. |
| “A cascade is cheaper.” | Include router, retries, fallbacks, misroutes, latency, and operational cost. |
| “Multi-agent is modular.” | Prove value beyond one process and account for coordination and correlated failure. |
| “The bigger model is safer.” | Demonstrate the relevant safety outcome and operational controls against the baseline. |
