# 02 — The Optical System

Prerequisite: [[01 - Probability and Click Records]]. Session plan: 15 minutes on the optical chain, 10 on detector examples, 10 on exercises.

## From optical inputs to records

A **mode** is a distinguishable optical degree of freedom, such as a spatial channel or time bin. Several modes can use the same physical detector at different times. Mode count therefore differs from physical detector count.

In GBS, squeezed optical states enter an interferometer, which mixes their amplitudes. Detection turns the output state into random records. Squeezing redistributes fluctuations between two field quadratures; it does not mean that every input contains a fixed number of photons.

Interference involves adding amplitudes before taking probabilities. As an elementary example, amplitudes $1/2$ and $1/2$ combine to probability $|1|^2=1$, while $1/2$ and $-1/2$ combine to zero. This example illustrates phase sensitivity; it is not a complete normalized interferometer calculation. Independent particle routes do not capture all quantum interference.

Loss can occur in preparation, propagation, and detection. Partial distinguishability means that photons have differing unresolved properties, reducing some interference. A characterized model must state how each is represented. “Lossy” alone is not a complete model specification.

## Threshold versus photon-number-resolving detection

A threshold detector distinguishes vacuum from one or more photons. A photon-number-resolving detector can distinguish counts. The photon occupations $(0,2,1)$ produce the threshold record $(0,1,1)$. The record has two clicks and the occupation has three photons. A threshold click count cannot reconstruct the occupation.

The target experiment uses spatial and temporal modes. Its L1024 configuration has 1,024 squeezed inputs and 8,176 output modes; S64 and M256 are other configurations. The reported largest detection event is not the number of photons in every shot. These facts come from the [Jiuzhang 4.0 paper](https://arxiv.org/html/2508.09092), especially the apparatus description and Figure 2.

## Check your understanding

1. Map photon occupations $(2,0,3,1)$ to a threshold record and compare photons with clicks.
2. Why is 8,176 output modes not automatically 8,176 physical detectors?
3. Why is increasing loss to make simulation easier a change to the benchmark?

> [!answer]- Check after trying
> 1. $(1,0,1,1)$: three clicks, six photons.
> 2. Time bins can be measured by reused physical detection channels.
> 3. It changes the target optical state and output distribution. Such a sensitivity study must be labeled separately.

## Proposal task and checkpoint

Write a short physical-system paragraph. Include inputs, mixing, measurement, and the calibrated imperfections. You are ready when you can explain why inputs, output modes, photons, and clicks are four different quantities.

Next: [[03 - Gaussian States and Covariance]].
