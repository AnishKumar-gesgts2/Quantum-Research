# 00 — The Project and Its Claims

Prerequisites: none. Session plan: 10 minutes on the question, 15 on the distinctions below, 10 on exercises, then your proposal paragraph.

## Learning goal

Explain the active project without implying that it has already succeeded.

Gaussian boson sampling (GBS) is a task in which an optical device generates random detector records. A classical simulator tries to generate records with the appropriate statistics. Research compares how faithfully each performs the declared task and what resources it uses.

Our active question is: **Can a faithful implementation of a published approximate phase-space sampler reproduce the chosen Jiuzhang 4.0 validation results at a measured, competitive classical cost?** The project is an independent extension and audit. It need not invent an algorithm to answer a useful question.

The reason to investigate is a specific omission: Goodman et al. defer Jiuzhang 4.0 while predicting that their sampler should scale to it. Treat that as a published prediction to test, rather than a result we possess. Read the experimental-description section of [their paper](https://arxiv.org/html/2604.12330).

## Three objects to keep separate

| Object | Meaning | What can go wrong? |
| --- | --- | --- |
| Ideal model | A theoretical optical system under ideal assumptions | It can omit experimental imperfections. |
| Characterized model | A model built from specified calibration and imperfections | Its parameters or physical assumptions can be inaccurate. |
| Hardware records | The measured experimental outputs | They contain finite-sample fluctuation and behavior beyond the model. |

A simulator can agree with one and disagree with another. “Ground truth” in a paper often means a declared model; it does not make every modeling assumption infallible.

## Worked claim audit

Suppose a classical sampler matches a count histogram but misses three-detector correlations. The supported statement is “It reproduced the count statistic under the tested conditions.” Saying “It reproduced GBS” would hide the failed diagnostic. Saying “It disproved quantum advantage” would require a much stronger account of the task, fidelity, resources, and computational claim.

Likewise, a fast program on a substituted easier covariance is evidence about that substituted model. It is not a reproduction of the requested experimental condition.

## Check your understanding

1. Is the current project primarily an optical hardware build, algorithm invention, or reproduction and benchmark?
2. If a simulator matches hardware but fails the characterized model, what two possibilities should you investigate?
3. Why can a negative outcome still make a useful research contribution?

> [!answer]- Check after trying
> 1. Reproduction and benchmark of a published classical sampler.
> 2. The sampler may be approximating hardware behavior absent from the model, or a comparison/model/implementation may be wrong. Agreement with hardware alone does not settle which.
> 3. A faithful failed run can establish an accuracy or resource boundary. Missing essential artifacts can establish a precise reproducibility limitation.

## Proposal task and checkpoint

Write three sentences: the task, the published prediction, and the test you propose. Use future tense for work not done. You are ready when you can name the model target and observed-data target separately.

Next: [[01 - Probability and Click Records]].
