# 03 — Gaussian States and Covariance

Prerequisite: [[02 - The Optical System]]. Session plan: 15 minutes on covariance, 15 on squeezing/loss, 10 on checks.

## What is compact about a Gaussian state?

Quadratures $q$ and $p$ are two complementary components of an optical field, analogous mathematically to position and momentum. The bracket $\langle\cdot\rangle$ denotes a quantum expectation. The commutator $[q,p]=qp-pq$ expresses their incompatibility; you do not need to derive it for the first proposal draft. A superscript $T$ transposes a row into a column.

Use dimensionless quadratures with $[q,p]=i$ and vacuum variance $1/2$. For $M$ modes, choose the ordering $R=(q_1,p_1,\ldots,q_M,p_M)^T$. The mean is $d_i=\langle R_i\rangle$ and the covariance is

$$
V_{ij}=\frac12\langle(R_i-d_i)(R_j-d_j)+(R_j-d_j)(R_i-d_i)\rangle.
$$

A Gaussian quantum state is determined by its mean vector and covariance. This statement concerns Gaussian states in quadrature phase space. It does not say that the resulting binary click distribution is a multivariate normal distribution, or that binary pairwise moments determine it. The conversion to photon detection is the important extra step. See [The Walrus theoretical background](https://the-walrus.readthedocs.io/en/latest/gbs.html) for Gaussian-state probability conventions.

## Worked one-mode example

For an illustrative squeezed vacuum with squeezing $r$ aligned to these axes,

$$
V=\frac12\begin{pmatrix}e^{-2r}&0\\0&e^{2r}\end{pmatrix}.
$$

The determinant is $1/4$. Smaller fluctuation in one quadrature comes with larger fluctuation in the other. For $e^{2r}=2$, the variances are $1/4$ and $1$.

Uniform loss with transmission $\eta$, modeled by coupling to vacuum, maps this covariance to

$$
V'=\eta V+(1-\eta)\frac{I}{2}.
$$

At $\eta=1/2$, the example becomes $\operatorname{diag}(3/8,3/4)$. At zero transmission it becomes vacuum. These checks help expose convention errors.

## Why conventions matter

Some libraries instead use vacuum covariance $I$, or place all $q$ entries before all $p$ entries. Feeding a correct matrix to an incompatible convention gives wrong probabilities. Record quadrature ordering, units, mode ordering, mean displacement, and the loss/indistinguishability construction before comparing outputs.

Optional extension: physical covariance requires $V+i\Omega/2$ positive semidefinite, where $\Omega$ is the block-diagonal symplectic matrix in this ordering. Ordinary positivity of $V$ alone is insufficient.

## Check your understanding

1. What are the dimensions of $d$ and $V$ for three modes?
2. What does the loss formula give at $\eta=0$ and $\eta=1$?
3. Does a small covariance matrix guarantee easy exact threshold sampling?

> [!answer]- Check after trying
> 1. $d$ has 6 entries; $V$ is $6\times6$.
> 2. Vacuum covariance and the original covariance, respectively.
> 3. No. A compact state description does not guarantee an efficient algorithm for the measurement task.

## Proposal task and checkpoint

List the model artifacts and conventions a reproducer needs. You are ready when you can explain covariance compactness without confusing quadrature statistics with click correlations.

Next: [[04 - Correlations and Hidden Differences]].
