# 06 — Phase Space and the Proposed Sampler

Prerequisites: [[03 - Gaussian States and Covariance]], [[05 - Exact and Approximate Sampling]]. Session plan: 15 minutes on representations, 15 on the toy example, 10 on source reading.

## The method to reproduce

Positive-P represents quantum states using paired complex stochastic variables. Its trajectories estimate quantum observables; they are not directly detector records. Goodman et al. convert them into approximate threshold probabilities by taking the real part of a vacuum estimator and clipping to $[0,1]$. They then alternate whitening–coloring corrections with projection, using ten iterations. The procedure adjusts low-order statistics but does not establish exact full-distribution sampling. See the “Sampling from phase space” section and equations 8–12 in [the paper](https://arxiv.org/html/2604.12330).

You need to understand where the approximation enters before understanding every representation-theory detail. “Positive” in the representation's name does not mean every trajectory's detector estimator is a real physical probability.

## Teaching example: legal probabilities can still be biased

Consider an invented two-draw estimator of no-click probability with values $-0.2$ and $0.8$, each equally weighted. Its mean is $0.3$. Clipping the draws to the physical interval gives 0 and 0.8, with mean $0.4$. Making each draw legal changed the expected observable.

This arithmetic illustrates a mechanism of projection error. It is not a derivation of the paper's quantum trajectories or a reproduction result.

## Teaching example: correcting moments can break the range

For an ordinary real random variable $Y$ with mean $m$ and standard deviation $s>0$, an affine transformation

$$
Y'=m_*+\frac{s_*}{s}(Y-m)
$$

has mean $m_*$ and standard deviation $s_*$. Suppose $Y$ is equally likely to be 0.2 or 0.8. Then $m=0.5$, $s=0.3$. Targeting $m_*=0.5$ and $s_*=0.6$ produces $-0.1$ and $1.1$. A moment correction can leave the probability interval, and clipping it again alters moments.

This is a scalar analogy for the tension between moment matching and legal probabilities. The published multivariate algorithm has specific matrix definitions and numerical requirements that this analogy does not replace.

## Your reproduction checklist

Locate the implementation of trajectory generation, projection, the repeated transformations, and conversion to detector draws. Record random seeds, batch handling, matrix conventions, and numerical treatments. Compare against small independent references and a reported lower-scale benchmark before production. The authors' [XQSIM repository](https://github.com/peterddrummond/xqsim) is an implementation lead; these lessons do not assert that every required artifact has been obtained or run.

## Check your understanding

1. In the clipping example, what is the implied click probability before and after clipping the estimator?
2. Why do ten correction iterations not constitute proof of full-distribution accuracy?
3. Why is replacing the published procedure with a plausible new transformation a methodological change?

> [!answer]- Check after trying
> 1. One minus the no-click mean: $0.7$ versus $0.6$.
> 2. An iteration count specifies a procedure, not its accuracy on every observable or target.
> 3. A reproduction must preserve the specified algorithm; a new procedure needs separate validation and labeling.

## Proposal task and checkpoint

Write a method paragraph containing representation, detector conversion, approximation, and verification. You are ready when you can explain why observable estimation and detector sampling differ.

Next: [[07 - The Preliminary Study and Its Audit]].
