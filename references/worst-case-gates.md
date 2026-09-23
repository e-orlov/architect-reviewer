# Worst-Case Is Not a Blocking Gate Rule

A theoretical maximum, timeout, capacity limit, retry horizon, or worst-case scenario is an input to risk analysis—not automatically a prerequisite, waiting period, safety margin, or release gate.

Never derive a blocking gate merely by adding worst-case values together. In particular:

- a maximum duration is not a required minimum gap;
- a maximum exposure is not the expected exposure;
- a possible overlap is not an unacceptable overlap;
- an upper bound is not proof that the system will consume that bound.

Apply this rule to **proposed risk controls**. A named law, contract, governing instruction, or explicit project-policy gate applicable at the next boundary takes precedence under [the operating model](operating-model.md#1-precedence); record its authority and applicability as `GOVERNING_POLICY`. Do not invent a policy gate from a theoretical bound or use this exception to waive a real mandate.

## Blocker-admission test

A worst-case-derived risk control may block the next transition only when all of the following are demonstrated:

1. **Reachability:** the failure mode can actually occur during the exact next transition through a traced causal path.
2. **Residual harm:** after accounting for existing limits, isolation, monitoring, supervision, stop controls, and rollback, unacceptable harm can still occur before the next checkpoint.
3. **No bounded substitute:** a smaller cohort, shorter exposure, dynamic guard, permit, rate/cost cap, HOLD, deadline, fast stop, or rollback cannot contain the risk.
4. **Boundary fit:** the proposed gate prevents or detects that failure at the lifecycle boundary where it becomes reachable.
5. **Proportionality:** the gate's delay, execution cost, and complexity are proportionate to the residual risk it removes.

If any condition is false, the proposed risk gate is non-blocking. Convert the worst-case concern into an exposure cap, deadline, STOP condition, rollback trigger, monitoring condition, or owned later hardening item when one is useful; retire a redundant control rather than deferring it forever. This does not waive proof for a separate admitted blocker or applicable governing policy.

## Counterfactual requirement

For every proposed risk blocker, answer:

> If this gate is removed but all existing bounded controls remain, what specific unacceptable harm can occur before the next checkpoint?

If that question has no concrete, falsifiable answer, reject the proposed gate.

## No double-counting

Do not protect against the same failure twice without proving incremental risk reduction. Once a control bounds or makes a failure recoverable, recompute residual risk before adding another prerequisite.

For example, do not require a theoretical maximum idle interval when a dynamic guard can stop exposure before the next conflicting event.

## Prefer dynamic boundaries

Prefer controls tied to actual state—active work, observed usage, real deadlines, queue state, health, or the next conflicting event—over fixed delays derived from theoretical maxima.

Use observed representative behavior and existing production evidence to size a bounded transition. Retain worst-case values as hard ceilings and STOP triggers **when enforcement is proven**; otherwise treat them as assumptions and verify the stop mechanism before relying on it. Do not treat either a ceiling or representative behavior as assumed normal behavior. Representative observations support sizing; they do not waive a failure mode reachable before the checkpoint.

## Handling uncertainty

Material uncertainty requires targeted evidence recovery. It does not justify an arbitrary waiting period.

Block the **claimed transition** only when the uncertainty cannot be safely bounded within it. A separately defined, smaller reversible diagnostic exposure may resolve the uncertainty if its own admission criteria, applicable policy gates, limits, checkpoint, and stop/rollback controls are satisfied. The original claim remains `UNKNOWN` until evidence closes it; a diagnostic `GO` is not acceptance of that claim.

## Mandatory gate record

Every proposed **risk-control** blocker, including a rejected proposal, must record:

`next transition → named failure → reachable causal path → existing containment → residual harm before checkpoint → why no bounded substitute works → gate cost/delay → decision`

Also record the counterfactual, the bound's source and meaning, actual representative observations where available, incremental benefit over existing controls, and the resulting dynamic boundary or STOP condition. Use the [Next-Safe-Step Record](templates.md#15-next-safe-step-record).

A proposed risk gate without this record is non-blocking by default. If the missing analysis leaves the **underlying transition** materially unsafe or its reachability unknown, mark that transition `UNKNOWN` and recover evidence or define a separately bounded diagnostic transition. An applicable `GOVERNING_POLICY` gate retains its independent authority and record.
