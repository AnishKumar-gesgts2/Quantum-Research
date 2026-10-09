# 09 — Reproduction and Fair Comparisons

Prerequisites: [[06 - Phase Space and the Proposed Sampler]], [[08 - Validation and Statistical Uncertainty]]. Session plan: 15 minutes on artifacts, 15 on gates, 10 on fairness cases.

## Reproduction starts with the inputs

Before a production run, identify the exact covariance/calibration, records, detector model, published algorithm, and metric definitions. Record source URLs, versions, checksums, units, mode ordering, and selected physical condition. Publicly linked code is not proof that every necessary input or output is available. The active research specification makes this an early feasibility gate.

An artifact table should contain: item, source, version/hash, purpose, availability, compatibility check, and unresolved gap. If a required covariance is missing, inventing one cannot support an experimental reproduction. A labeled synthetic study can still answer a different question.

## Staged gates

1. **Artifact gate:** establish whether the exact method and target are reproducible from available materials.
2. **Numerical gate:** verify small probability/observable calculations against an independent reference under identical conventions.
3. **Published-result gate:** reproduce a lower-scale reported benchmark with its model, metric, sample size, and uncertainty.
4. **Scale-control gate:** profile the next configurations and check accuracy, memory, and failure modes.
5. **Locked-target gate:** evaluate the declared L1024 condition after implementation and tuning choices are frozen.

Passing an easier configuration does not satisfy the final gate. Failing a gate calls for diagnosis, a documented blocker, or a clearly relabeled fallback. Each gate should have an artifact demonstrating its outcome.

## Development and evaluation

Tune code and any selection/hyperparameter choices on development cases. Freeze the algorithm and test family before final evaluation. Fixing a discovered implementation bug may require rerunning tests, but disclose the fix and renewed evaluation. Repeatedly changing a method after inspecting final errors turns that dataset into development evidence.

The earlier audit is a caution: adding stronger controls after the first results was scientifically useful, but those same instances do not become a fresh held-out suite.

## Worked fairness case

Sampler A produces one million unconditioned records in 60 seconds after 300 seconds of setup. Sampler B produces one hundred thousand fixed-count records in 10 seconds. The two times cannot establish which is better for a ten-million-record unconditioned task. Match the model, detector, conditioning, output count, acceptance accuracy, hardware, and setup accounting first.

Classify each baseline as faithfully rerun, published context only, or unavailable/incomparable. A missing strong baseline is a limitation to disclose rather than replace silently with a weaker control.

## Check your understanding

1. What evidence is needed before calling a run a lower-scale reproduction?
2. If a covariance is unavailable, what should the proposal's fallback claim be?
3. Why freeze observable choices before the final run?

> [!answer]- Check after trying
> 1. Matching inputs/conventions and reproduction of a reported observable within its declared uncertainty, with inspectable logs and outputs.
> 2. A precisely documented reproduction limitation and/or a reproduction on an earlier fully specified target; not an invented L1024 result.
> 3. To prevent selecting favorable diagnostics after seeing outcomes.

## Proposal task and checkpoint

Write a staged methods plan and artifact checklist, including stop/go criteria and fallback. You are ready when you can identify an unfair comparison and explain how to repair it.

Next: [[10 - Scaling and Resource Budgets]].
