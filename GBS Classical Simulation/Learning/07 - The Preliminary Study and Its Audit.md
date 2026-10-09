# 07 — The Preliminary Study and Its Audit

Prerequisites: [[04 - Correlations and Hidden Differences]], [[05 - Exact and Approximate Sampling]]. Session plan: 10 minutes on the history, 15 on numbers, 15 on claim revision.

## Two preliminary studies, then a pivot

The initial information probe used nine exact eight-mode distributions and maximum-entropy models matching moments through progressively higher orders. It asked how much full-distribution information those constraints retained. It was not a published-sampler reproduction.

The subsequent selective-correction study used 144 synthetic instances: 36 development and 108 held-out cases. It tested which additional triple dependencies improved an enumerated probability model. The first draft and retrospective skeptical audit must be read together. Their paths and authority are in [[Sources and Project Map]].

## Read the numbers correctly

| Method in the original comparison | Mean held-out TVD |
| --- | ---: |
| Pairwise baseline | 0.10575 |
| Selected correction | 0.06641 |
| Uniform third-order fit | 0.05269 |

The selected correction reduced mean error by approximately $0.03934$, or 37.2% relative to the pairwise baseline. Rounding the displayed means differs slightly from using the original unrounded values. This is not a fraction of correctly simulated shots and not a speed improvement. Uniform third-order fitting had lower mean error, while the correction also required more resources than the pairwise model.

The audit introduced an exact competitor. It had better accuracy in all 108 held-out cases and strictly beat the selected approximation on accuracy, measured preprocessing time, and traced memory in 102. Traced memory excludes some native allocations and is not complete resident process memory. The audit rejected the enumerative architecture as a computational improvement at the tested sizes.

## What remains useful?

The independent Torontonian audit supports the small reference probabilities. Selection improved over random feature choices within the tested synthetic family. These are real results with bounded significance. They do not establish transfer to new physical regimes or experimental-scale performance.

The audit reused the earlier held-out instances. New retrospective controls are useful, but they do not create a new independent confirmation set. This matters when describing the strength of evidence.

The active phase-space project is a pivot toward reproducing a strong published method and testing a specific omitted target. It should not present the earlier feature-selection method as its current sampler.

## Check your understanding

1. Calculate the relative reduction from the two displayed baseline/correction means.
2. Why is the exact control important even though it cannot scale to the full device?
3. Name one supported and one unsupported claim about the preliminary study.

> [!answer]- Check after trying
> 1. $(0.10575-0.06641)/0.10575\approx0.372$.
> 2. It tests whether the proposed approximation offered a benefit on the sizes actually measured.
> 3. Supported: selected information improved the pairwise fit in this family. Unsupported: the implementation demonstrated competitive experimental-scale GBS sampling.

## Proposal task and checkpoint

Draft 100–150 words of preliminary evidence including the improvement, stronger control, negative conclusion, and reason for the pivot. You are ready when you can defend that paragraph without concealing an unfavorable result.

Next: [[08 - Validation and Statistical Uncertainty]].
