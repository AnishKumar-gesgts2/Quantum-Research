# 01 — Probability and Click Records

Prerequisite: [[00 - The Project and Its Claims]]. Session plan: 10 minutes on distributions, 15 on the example, 10 on exercises, then the writing task.

## A sample is an outcome, not a probability

For $M$ threshold outputs, one record is $x=(x_1,\ldots,x_M)$ with $x_i\in\{0,1\}$. The value 1 means click. A distribution $P(x)$ assigns probabilities to the possible records. Valid probabilities are nonnegative and sum to one. A sampler draws records; a probability evaluator answers how likely a specified record is. These are different computational tasks.

The number of possible records is $2^M$, but the computer does not need to store a table of all outcomes to sample. Independent fair bits are an easy example: generate each bit with probability $1/2$, producing a uniform distribution over exponentially many strings.

## Worked two-detector example

Consider this illustrative distribution, not experimental data:

| Record | $P(x)$ |
| --- | ---: |
| 00 | 0.4 |
| 01 | 0.1 |
| 10 | 0.1 |
| 11 | 0.4 |

Both detectors click with marginal probability $0.5$. Yet their joint click probability is $0.4$, rather than the $0.25$ predicted by independence. The marginal is found by summing over the unwanted coordinate:

$$
P(x_1=1)=P(10)+P(11)=0.5.
$$

Let $C=x_1+x_2$ be the total click count. Its distribution is $P(C=0)=0.4$, $P(C=1)=0.2$, and $P(C=2)=0.4$. A count histogram combines the 01 and 10 outcomes; it discards which detector clicked.

Conditioning changes the task. Given $C=1$, $P(01\mid C=1)=0.1/0.2=0.5$. A sampler conditioned on a fixed count is not automatically comparable to an unconditional sampler. Rejected draws also affect cost.

## Expectations and estimates

For an observable $f$, its expectation is $\mathbb E_P[f]=\sum_x P(x)f(x)$. From $N$ records, estimate it by $N^{-1}\sum_{s=1}^N f(x^{(s)})$. The estimate fluctuates even if the sampler is exact. Keep the mathematical expectation separate from its empirical estimate.

## Check your understanding

1. Compute $\mathbb E[C]$ in the table.
2. A program returns only $P(11)$. Has it generated a click record?
3. Two distributions share the count histogram. Must they assign the same probability to 01?

> [!answer]- Check after trying
> 1. $0(0.4)+1(0.2)+2(0.4)=1$.
> 2. No. Probability evaluation is not a draw from the distribution.
> 3. No. Probability can move between patterns with the same count.

## Proposal task and checkpoint

Define the output format, detector model, number of records, and any conditioning. You are ready when you can compute a marginal, expectation, and conditional probability from a small table.

Next: [[02 - The Optical System]].
