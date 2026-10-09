# 05 — Exact and Approximate Sampling

Prerequisite: [[04 - Correlations and Hidden Differences]]. Session plan: 15 minutes on computational tasks, 15 on sampling, 10 on comparisons.

## Probability evaluation, observable estimation, and sampling

An exact small-system calculation can construct a full probability table. An observable estimator may obtain moments without generating valid detector records. A sampler must output records from a specified distribution. Comparing times across these different tasks can create a false speed advantage.

Threshold GBS probabilities have an exact Torontonian formulation; read the abstract of [Quesada, Arrazola, and Killoran](https://arxiv.org/abs/1807.01639). Our small reference calculations also use subset vacuum probabilities and inclusion–exclusion. These methods provide tractable reference checks on small instances. They do not make full experimental-scale exact sampling easy.

## A valid distribution is a requirement

An approximate model $Q$ must have nonnegative probabilities summing to one. Negative estimated probabilities cannot simply be used for ordinary sampling. Clipping or renormalizing them changes the method and its distribution; any such step needs explicit source support or must be reported as a deviation.

For any distribution, the chain rule gives

$$
Q(x)=Q(x_1)\prod_{i=2}^M Q(x_i\mid x_1,\ldots,x_{i-1}).
$$

This is an identity, not an efficiency guarantee. Evaluating its conditionals can be expensive. Truncating the information used in them introduces approximation.

## Worked table-sampling example

For probabilities $(0.4,0.1,0.1,0.4)$ in the order 00, 01, 10, 11, the cumulative boundaries are $(0.4,0.5,0.6,1)$. Draw $u$ uniformly in $[0,1)$ and choose the interval containing it. A draw $u=0.57$ yields 10.

This produces valid independent samples from the stored table, but preparing and storing the table scales with the number of outcomes. Fast draws after expensive setup do not establish cheap end-to-end sampling.

## Families to recognize

Correlation-based models approximate selected detector dependencies. Tensor-network methods compress a state with an accuracy–cost parameter. Phase-space methods use stochastic representations of optical states. Simple state mockups substitute a tractable physical model. A useful baseline is one that addresses the same model, output task, and accuracy target; an algorithm name alone does not establish comparability.

Read the project's skeptical audit before treating any named method as a reproduced baseline: [[Sources and Project Map]].

## Check your understanding

1. Which record corresponds to $u=0.92$ in the example?
2. Is fast sampling from an enumerated table evidence of scalable preparation?
3. Why might the exact method be a strong baseline at ten modes but unusable at thousands?

> [!answer]- Check after trying
> 1. 11.
> 2. No. Preparation and storage still need to be measured.
> 3. Small exponential computations can be cheap; their cost grows rapidly with size.

## Proposal task and checkpoint

State what your method outputs and how you will verify valid sampling. You are ready when you can distinguish the three computational tasks and explain setup versus generation cost.

Next: [[06 - Phase Space and the Proposed Sampler]].
