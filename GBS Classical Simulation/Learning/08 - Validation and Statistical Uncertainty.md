# 08 — Validation and Statistical Uncertainty

Prerequisites: [[01 - Probability and Click Records]], [[04 - Correlations and Hidden Differences]]. Session plan: 15 minutes on uncertainty, 15 on diagnostics, 10 on decisions.

## Sampling fluctuation versus systematic mismatch

For independent binary observations with probability $p$, the estimated probability $\widehat p$ has standard error approximately $\sqrt{p(1-p)/N}$. A plug-in estimate uses $\widehat p$. This approximation needs care near boundaries and with sparse events.

If two independent datasets estimate $p$ and $q$, their difference has approximate standard error

$$
\mathrm{SE}_{\mathrm{diff}}=\sqrt{\frac{p(1-p)}{N_P}+\frac{q(1-q)}{N_Q}}.
$$

Shared samples, correlated records, or estimated calibration parameters require an appropriate dependence/uncertainty treatment. Do not assume independence merely because the data are in two files.

## Worked example

Two independent samples of size 10,000 estimate 0.50 and 0.52. The standard error of their difference is about $0.00707$, giving a standardized residual about $2.83$. Increasing each sample size fourfold halves this error and doubles the residual for the same difference. The systematic discrepancy did not grow; the evidence became more precise.

A standardized residual for a single statistic is not automatically the paper's reported $Z$ score. The phase-space paper also converts distribution-level discrepancies to significance scores. The project specification's generic $Z_j$ notation is a teaching abstraction until each statistic's original definition is implemented. Neither a universal “three sigma” rule nor an uncorrected maximum across many tests is a substitute for a source-matched protocol.

## Diagnostics and their limits

| Diagnostic | Information retained | Main limit |
| --- | --- | --- |
| Total/grouped click counts | How many clicks occur in chosen groups | Many spatial patterns share counts. |
| Correlations | Selected detector dependencies | Unmeasured orders/groups can differ. |
| Subsystem likelihood comparison | Relative support for named models on selected records | It does not compare against every distribution. |
| Full TVD on tractable small cases | Every outcome probability in that case | It does not provide full-scale TVD. |

A Bayesian likelihood score favoring one hypothesis over another is a relative comparison, not a universal fidelity certificate. If conditioning or subsystem selection changes, so does the evaluated task.

For Jiuzhang correlation comparisons, the paper reports fitted slope $K$ and $\Delta K=|K-1|$. Preserve the original fit conventions and also inspect scatter/residuals: a good slope alone can hide discrepancies. See [the experimental paper's Figure 2 discussion](https://arxiv.org/html/2508.09092).

## Check your understanding

1. What happens to a binomial standard error when $N$ increases ninefold?
2. Why can searching many tests make an uncorrected extreme score misleading?
3. Does agreement within uncertainty mean the distributions are identical?

> [!answer]- Check after trying
> 1. It becomes one third as large under the same assumptions.
> 2. More opportunities for random extremes; the test family and multiplicity treatment must be declared.
> 3. No. The data may be insufficient to resolve a difference, and only selected observables were tested.

## Proposal task and checkpoint

Name each diagnostic, sample count, reference, uncertainty method, and acceptance rule. Mark source definitions still needing verification. You are ready when you can explain why sample size changes significance and why passing tests has a bounded interpretation.

Next: [[09 - Reproduction and Fair Comparisons]].
