# 04 — Correlations and Hidden Differences

Prerequisites: [[01 - Probability and Click Records]], [[03 - Gaussian States and Covariance]]. Session plan: 10 minutes on moments, 20 on parity, 10 on exercises.

## Moments and connected correlations

For binary outputs, a first moment is $\mathbb E[x_i]=P(x_i=1)$. A second moment is $\mathbb E[x_ix_j]=P(x_i=x_j=1)$. Their connected correlation is

$$
\kappa_{ij}=\mathbb E[x_ix_j]-\mathbb E[x_i]\mathbb E[x_j].
$$

For the two-detector table in Lesson 01, $\kappa_{12}=0.4-0.25=0.15$. A joint moment and a connected correlation are different quantities. At third order the connected correlation also subtracts lower-order contributions; always check what a paper means by “correlation.”

## Worked counterexample: same pairs, different triples

Let $P$ be uniform over 000, 011, 101, 110, and let $Q$ be uniform over 001, 010, 100, 111. These are teaching distributions, not asserted physical GBS states.

Each individual bit is equally likely to be 0 or 1 under either distribution. For any pair, 00, 01, 10, and 11 each occur with probability $1/4$. Thus every one-bit and two-bit marginal agrees. But the first distribution has even parity and the second odd parity. Their supports do not overlap.

Full total variation distance is

$$
D_{\mathrm{TV}}(P,Q)=\frac12\sum_x|P(x)-Q(x)|=1.
$$

The third moment differs: $\mathbb E_P[x_1x_2x_3]=0$, while $\mathbb E_Q[x_1x_2x_3]=1/4$. Higher-order tests reveal a difference that all pair tests missed.

This demonstrates a general logical limit of low-order validation. It does not prove that every physically allowed GBS instance realizes this extreme example. Physical constraints can provide additional structure, which must be studied rather than assumed.

## Why more information costs more

There are $\binom{M}{k}$ groups of order $k$. Storing every group through order $K$ means $\sum_{k=1}^K\binom{M}{k}$ entries. Selective information can reduce this list, but selecting useful terms and constructing a reliable sampler also cost resources. More accurate moments do not automatically produce a faster sampler.

## Check your understanding

1. Verify the pair marginal for bits 1 and 2 in both parity distributions.
2. Explain the TVD calculation without using a calculator.
3. What conclusion is justified if a sampler passes all measured pair tests?

> [!answer]- Check after trying
> 1. Each pair outcome occurs once among four equiprobable records.
> 2. Eight absolute differences of $1/4$ sum to 2; halving gives 1.
> 3. Agreement on the measured pair observables within the stated uncertainty. Full-distribution agreement requires more evidence.

## Proposal task and checkpoint

Write a sentence describing what your chosen diagnostics cannot certify. You are ready when you can explain the parity counterexample and distinguish a moment from a cumulant.

Next: [[05 - Exact and Approximate Sampling]].
