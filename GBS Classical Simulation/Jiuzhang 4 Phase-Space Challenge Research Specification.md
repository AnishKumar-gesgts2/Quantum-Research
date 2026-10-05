# Adversarial Reproduction of a Scalable Phase-Space Sampler on Jiuzhang 4.0

**Research specification — version 1.0 — October 3, 2026**  
**Status:** proposal and execution protocol; no Jiuzhang 4.0 reproduction has yet been run.  
**Program fit:** BlueQubit Quantum Flywheel, Track 2, “Breaking quantum advantage claims.”  
**Target claim:** the positive-P phase-space sampler of Goodman et al. can extend to Jiuzhang 4.0 with a moderate resource increase and no change to the algorithm, despite that experiment being excluded from their study.

This specification supersedes the *future-work direction* in [[GBS Classical Simulation Project Description]] as the active project question. It does not erase the initial selective-correction experiment or its audit. Those are preliminary work and remain documented in [[First Research Draft]] and [[Skeptical Audit and Stronger Benchmarks]].

## 1. Research question

**Primary question.** Can an independent, reproducible implementation of the published positive-P phase-space sampler generate threshold-detector output samples for the largest published Jiuzhang 4.0 configuration (L1024; 1,024 squeezed inputs and 8,176 output qumodes) within a declared classical resource budget, while reproducing the paper’s prespecified distributional validation results at the same sample count and with the same calibrated lossy, partially distinguishable Gaussian-state model? If it can, how does its accuracy–cost frontier compare with the classical mockups and samplers already tested against this experiment?

**Plain-language version.** A new paper says a classical phase-space method should scale to the biggest Jiuzhang experiment, but leaves that experiment out. We will test that specific prediction on the published device data, check whether the classical samples pass the experiment’s own checks, and measure the complete computing cost. We will report both where the method succeeds and where it fails.

This is a test of a **classical sampling claim and its resource cost**. It is not a proof that every classical algorithm fails or succeeds, and the result alone cannot prove or disprove computational hardness. A simulator matching selected validation statistics is not thereby shown to reproduce the full output distribution.

Formally, for the frozen calibrated model $P_{\theta}$ and the phase-space sampler $Q_{\phi}$, each shot is a click record $x\in\{0,1\}^{8176}$. For each prespecified statistic $f_j$ (a count-bin indicator, grouped-count indicator, or correlation observable), estimate $\mu_j(P)=\mathbb{E}_{P}[f_j(x)]$ and $\mu_j(Q)=\mathbb{E}_{Q}[f_j(x)]$ from independent samples. The test family is $\mathcal{F}=\{f_1,\ldots,f_J\}$, fixed from the source paper before the L1024 output is examined. The primary statistical discrepancy is the standardized residual

$$Z_j=\frac{\widehat{\mu}_j(Q)-\widehat{\mu}_j(P)}{\widehat{\mathrm{SE}}_j},$$

with the standard-error estimator and any dependence correction documented for each statistic. The resource outcome is the vector $C(Q)=(T_{10^7},M_{\mathrm{peak}},B)$: end-to-end time for $10^7$ records, peak resident memory, and cloud cost where available. We seek the accuracy–cost frontier over sampler settings; we do not collapse accuracy and cost into an arbitrary weighted score. The global total-variation distance on $2^{8176}$ patterns is not an estimand in this project because it cannot be computed from available data.

## 2. Why this is a specific, consequential gap

Jiuzhang 4.0 reports three configurations that share a circuit: S64 (4,336 output modes), M256 (5,104), and L1024 (8,176). In L1024, the experiment reports coincidence events up to 3,050 photons. Its paper compares the hardware with a lossy, partially distinguishable ground-truth model and with classical mockups. The paper reports total click-count distributions, Bayesian tests on growing output subsystems, and second- and third-order correlation tests. It states that 10 million samples were used for the largest-run correlation comparisons. [Liu et al., *Robust quantum computational advantage with programmable 3050-photon Gaussian boson sampling*](https://arxiv.org/html/2508.09092)

Goodman et al. introduce a positive-P phase-space sampler with threshold-detector projection followed by ten whitening–coloring iterations. Their paper reports comparisons through 1,152 modes, but explicitly excludes Jiuzhang 4.0 because of its scale and leaves it as future work. They state that its quadratic scaling should allow Jiuzhang 4.0 sampling with a moderate resource increase. Their experimental data and XQSIM code are public; the paper’s positive-P sample data are available upon reasonable request. This gives us a falsifiable target and a reproducibility risk to resolve early. [Goodman et al., *Gaussian boson sampling: Benchmarking quantum advantage*](https://arxiv.org/html/2604.12330)

The comparison landscape is not empty. The Jiuzhang 4.0 paper already tested squashed-state, thermal, distinguishable-photon, greedy, independent-pairs-and-singles, treewidth, and MPS-based mockups. A later Gaussian-MPS paper reports Jiuzhang 4.0 covariance processing and a central-tensor benchmark, but that is not by itself a matching end-to-end sampler benchmark. We will not treat a tensor-preparation time as though it were a complete sample-generation time. [Liu et al., *Efficient simulation of low-entanglement bosonic Gaussian states in polynomial time*](https://arxiv.org/abs/2512.10643)

The research contribution is therefore an **independent, apples-to-apples extension and audit of a published classical method on an explicitly omitted, larger experimental target**. The paper can be valuable whether the method succeeds, fails, or reveals that the public information is insufficient for an independent reproduction, provided the outcome is documented rigorously.

## 3. Scope and claim boundaries

The primary target is the L1024 dataset at the highest pump setting used in the Jiuzhang 4.0 correlation comparison (7 nJ), because the original paper identifies this setting and fixes the published sample count at 10 million for those tests. The S64 and M256 configurations are scale-up controls. If the exact 7 nJ covariance and calibration artifacts cannot be reconstructed from public supplementary data, we will record the missing inputs and test only the closest fully specified published condition; we will not silently substitute an easier circuit or claim a full L1024 reproduction.

Two targets must be kept separate throughout:

1. **Characterized-model target:** sample from the published lossy, partially distinguishable Gaussian-state model, using the experiment’s released covariance/calibration inputs. This tests whether the sampler approximates the stated quantum model.
2. **Observed-data target:** compare independent classical samples with the fixed hardware dataset using the paper’s declared tests. This tests agreement with observed records, including finite-sample uncertainty and any model mismatch.

Agreement with observed hardware data does not establish agreement with the full model, and agreement with a model does not establish reproduction of all hardware behavior. Any fit of physical parameters to hardware data must be limited to the paper’s reported calibration procedure or a separately designated training subset; the held-out data used for evaluation cannot tune the sampler.

We will not claim a faster or cheaper algorithm merely because a generated distribution looks close on one statistic. A cost claim requires the same input model, output task, acceptance criteria, number of samples, and resource accounting. If a published comparator does not provide enough detail or code to reproduce an end-to-end sampler, its published figure can be discussed as literature context but cannot serve as a measured head-to-head cost baseline.

## 4. Hypotheses and decision rules

**H1 — scalability.** The published positive-P algorithm can process the L1024 covariance and produce 10 million valid 8,176-bit threshold records within the available Track 2 compute envelope, without changing the mathematical algorithm or dropping modes. We will report preprocessing, covariance loading, all ten whitening–coloring iterations, sample generation, and evaluation separately and end to end.

**H2 — validation fidelity.** At equal sample counts, the sampler’s estimates for the prespecified Jiuzhang 4.0 observables are statistically consistent with the characterized-model target at the uncertainty expected from 10 million samples. The primary pass rule is the paper’s maximum absolute $Z$-score criterion of at most 3 over the frozen observable family, with a declared family-wise correction if we expand that family. For the published correlation tests, we also report $K$, $\Delta K$, and uncertainty. Separately, we test whether it matches or exceeds the hardware’s own agreement with that target on the same observables.

**H3 — useful classical challenge.** At the accuracy threshold required by H2, the sampler has a lower measured classical cost than at least one strong published end-to-end classical baseline on the same configuration and task. If no baseline can be rerun under matched conditions, H3 remains untested; a comparison of unlike workloads will not count as support.

**Positive result.** H1 and H2 pass on the locked L1024 evaluation, and H3 passes against at least one reproducible, relevant baseline. For H3, the cost difference must exceed run-to-run uncertainty at the matched accuracy threshold; otherwise the result is a tie or inconclusive. The claim is limited to those observed outputs, model, tests, and hardware budget.

**Mixed result.** The method runs but fails one or more validation families, or reproduces the statistics only at a cost that does not improve on strong baselines. This supports a measured boundary or no-go result, not a quantum-advantage refutation.

**Negative result.** The full sampler cannot run within the budget, or it fails the prespecified checks despite a faithful implementation. We publish the failed scaling or accuracy result with the implementation and resource trace if it is reproducible.

**Reproduction-blocked result.** Required covariance, code, or sampler details are unavailable and cannot be inferred without inventing choices. We stop the Jiuzhang 4.0 claim, report the missing artifact precisely, and pivot to a complete reproduction on the largest earlier dataset that the paper and public materials support. We do not describe an implementation based only on a partial method description as a faithful reproduction.

## 5. Locked evaluation protocol

### 5.1 Models, code, and data

Before measuring performance, freeze and publish a manifest containing source URLs and checksums for the experimental data, covariance matrices, calibration parameters, published reference outputs, simulator source, dependencies, and compiler/runtime. Record all conventions: mode ordering, quadrature ordering, covariance normalization, detector model, partial-distinguishability representation, transmission, squeezing, threshold rule, and any postselection.

First reproduce a configuration for which Goodman et al. report numerical results. This is the implementation check: reproduce at least one Jiuzhang 2 or 3 panel and its reported observable and sample count within its stated Monte Carlo uncertainty. We do not proceed to a Jiuzhang 4 claim until this check passes or a documented reproduction blocker is established.

Use the authors’ XQSIM repository where applicable. The positive-P algorithm described in the paper must be implemented exactly enough to preserve the published transformations and projection. Document every deviation. Compare our finite-size outputs with the authors’ released outputs if they become available. If those outputs are not accessible, seek no undisclosed assistance; label the result an independent reproduction and report that direct output-to-output comparison was unavailable.

### 5.2 Primary metrics

The primary statistics are those the Jiuzhang 4.0 paper already used, recomputed using the same data selections and definitions:

- total click-count distribution (and the grouped-count distributions used in the phase-space paper where they are defined for threshold detectors);
- two-mode and three-mode correlation comparisons, including the published fitted slope $K$ and deviation $\Delta K=|K-1|$; use the original paper’s weighting and fit conventions;
- Bayesian score $\Delta H$ for the same nested output subsystems for which the likelihood calculation is available;
- standardized residuals or $Z$-scores against the characterized model, with finite-sample uncertainty.

We will report all observable families, not only the best one. The full click-string distribution has $2^{8176}$ outcomes, so full-system total variation distance is unavailable and will not be implied. The correlation and count tests are projections of distribution quality, not a complete certificate of sampling fidelity.

For every score, compare four quantities where computable: (a) the original paper’s hardware samples; (b) independent samples from the characterized-model target, as a statistical reference; (c) the phase-space sampler; and (d) the published classical baselines. Use bootstrap or repeated seeds to report uncertainty. A score difference smaller than uncertainty is inconclusive, not a win.

### 5.3 Baselines

The baseline ladder is fixed before evaluation:

1. The paper’s simplest relevant state mockups: squashed-state and thermal or distinguishable-photon models.
2. The tested algorithmic mockups: greedy and independent-pairs-and-singles samplers.
3. The published treewidth method at the original paper’s reported setting, including the stated regime where only approximation quality was evaluated and full practical execution was infeasible.
4. Published lossy-GBS MPS results and code, when an end-to-end sampler for the same model and output tests can be run. Report the MPS preparation step and sampling step separately.
5. The newer Gaussian-MPS covariance/tensor-preparation approach, only for the task it actually reports unless its authors’ implementation supports full same-task sampling.
6. Exact or high-precision Torontonian-based calculations on tractable subinstances as an independent reference check, not as a claimed full-scale competitor.

We will not assume every baseline can run at L1024. For each one, report whether it was (i) faithfully rerun, (ii) assessed from published results only, or (iii) not comparable. Do not replace a missing baseline with a weaker in-house straw baseline.

### 5.4 Cost and fairness

Use one recorded machine allocation for all runnable samplers where possible. The BlueQubit program describes classical allocations in the range of 16–120 CPU cores and GPU resources; the actual selected allocation is not guaranteed at proposal time. The preregistration will state exact CPU model, core count, GPU model, RAM, storage, software versions, thread settings, wall-clock limit, and cloud cost basis before the evaluation run.

Report both time-to-first-sample and the complete cost of producing 10 million valid records, including preprocessing, covariance transformations, fitting or calibration specific to the algorithm, discarded or rejected draws, postprocessing, and metric computation. Report peak resident memory, CPU/GPU utilization, throughput, output volume, energy or cloud-cost estimate if measurable, and any failed or timed-out runs. Separate one-time setup from per-run cost, but include both in an end-to-end total.

For algorithm comparisons, match the target covariance, detector model, output format, sample count, conditioning, and statistical tests. When a baseline cannot meet the 10-million-sample target, report its maximum completed workload and do not compare its partial runtime as if it produced the same result. Random seeds and all retained runs will be released.

## 6. Analysis plan

The primary analysis is a joint accuracy–cost profile, not a single success score. For each sampler and configuration, plot prespecified test error with uncertainty against total wall time and peak memory. Report the cost needed to reach the hardware’s observed error on the same model tests, when interpolation is supported by the measurements. Otherwise state that the threshold was not reached.

The main test uses a single locked L1024 condition. S64 and M256 provide scale controls and debugging cases, not substitutes for the main test. Any tuning of whitening–coloring settings, projection, stopping rules, or physical model parameters uses only the published defaults or a designated development set. Once defaults and analysis code pass on development data, hash and freeze them before the L1024 evaluation.

Correlation rows are dependent and numerous. The analysis must retain the paper’s weighting and also report unweighted residual summaries so a few large theoretical correlations cannot hide poor agreement elsewhere. Confidence intervals are generated by resampling shots and simulator seeds at the correct unit. If the source data lack raw shots and provide only aggregates, uncertainty calculations will use the released summary information and disclose that limitation.

No multiple-test fishing: the primary observable families and any correction for testing many orders/subsystems must be set before viewing L1024 sampler results. Exploratory plots are labeled exploratory and do not determine the primary conclusion.

## 7. Preliminary evidence: what exists and what it means

The prior project produced an exact small-system information-allocation study and then audited its own conclusion. On 144 synthetic 6-, 8-, and 10-mode instances, including 108 held-out cases, selecting a subset of triple-click moments reduced mean full-distribution TVD from 0.10575 for a pairwise model to 0.06641. Uniform third-order fitting was better at 0.05269. The prototype explicitly enumerated every output string.

An independent The Walrus Torontonian calculation agreed with the reference probabilities to a maximum full-distribution TVD of $5.33\times10^{-13}$. Stronger exact and feature-selection controls then showed that exact vacuum probabilities plus a fast inclusion–exclusion transform beat the current selected approximation on accuracy in all 108 held-out cases and on the measured time and traced-memory criteria in 102 of 108. Repeated random-selection controls support a real selection effect within that synthetic family, but they do not establish an efficient sampler or a result on an experimental system. The current implementation is a **no-go as a computational improvement** on its tested grid. The results and artifacts are preserved in [[First Research Draft]] and [[Skeptical Audit and Stronger Benchmarks]].

This preliminary work demonstrates that we can calculate small exact threshold distributions, independently verify them, retain held-out controls, and measure full pipeline costs. It does **not** demonstrate Jiuzhang-scale simulation, validate positive-P sampling, beat a published simulator, or weaken the Jiuzhang 4.0 claim. Those questions remain untested. The unusually favorable initial percentage was relative to a deliberately weak pairwise approximation; the stronger exact control explained why it looked too good.

The new proposal is promising because it is anchored to an explicit omission and a quantitative prediction in recent literature, and because the experiment provides public observables and data. Its feasibility still hinges on reconstructing the full L1024 covariance and faithfully implementing the phase-space sampler. The first weeks are designed to decide that quickly.

## 8. Work plan and stop/go gates

**Weeks 1–2: artifact and model audit.** Obtain the supplement, raw or aggregated data, covariance inputs, XQSIM source, dependencies, and any positive-P sample artifacts. Build the manifest and document conventions. **Go** only if an adequate state description and reproducible evaluation data exist. Otherwise record the exact gap and pivot to the largest fully specified configuration.

**Weeks 2–4: implementation reproduction.** Reproduce at least one published Jiuzhang 2/3 benchmark panel and confirm the metric code against a second implementation or authors’ data. Validate the phase-space detector projection, all ten whitening–coloring iterations, numerical stability, and seed reproducibility. **Go** only after matching the published result within its stated statistical uncertainty or resolving the discrepancy.

**Weeks 4–6: scale audit.** Run S64 and M256, profile covariance memory, iteration stability, throughput, output volume, and accuracy. Extrapolation to L1024 is a planning aid only, never a reported L1024 result. Stop if resource growth contradicts the advertised moderate increase or if errors grow with scale.

**Weeks 6–9: locked L1024 evaluation.** Freeze implementation and analysis. Generate the declared 10 million records within the predeclared budget, compute every primary observable, run seeds/uncertainty analysis, and compare only runnable matched baselines.

**Weeks 9–12: paper and artifacts.** Publish a reproducible repository with environment lock, source checksums, configs, sample/statistic outputs where licensing permits, cost logs, and a paper draft. Release non-sensitive derived data and exact reproduction instructions. State clearly whether this is a sampler reproduction, a validation-statistics challenge, or a resource-scaling result.

The phases can overlap where independent, but the gates are sequential: do not spend the full L1024 budget before the model, metric implementation, and published-method reproduction have passed.

## 9. Expected paper contribution

The paper is publishable in principle as a reproducibility and adversarial-benchmarking study, but publication is not guaranteed by a grant-ready proposal. Its strongest outcome would be an independently verified, end-to-end classical sampler that runs on L1024, meets the experiment’s prespecified validation criteria, and does so with lower measured classical cost than a strong method at equal workload. A useful negative outcome would be a faithful reproduction showing the promised scaling, accuracy, or both do not transfer to the omitted configuration. A third useful outcome would be a reproducibility analysis establishing that the public artifacts do not support the claimed test independently.

The project does not currently propose a new sampling algorithm. The previous selective-correlation route failed its practical comparison, so it should not be promoted as the main method. A new correction or hybrid may be explored only after the baseline sampler is reproduced, and only if the change is declared, ablated, and tested against the unchanged published method on held-out conditions. Any claimed “better and cheaper” alternative must win the matched accuracy–resource comparison above.

## 10. Main risks and mitigations

**Missing model artifacts.** Published data may not include a complete L1024 covariance or all device calibration parameters. Resolve this before implementation; do not infer missing values and call them published calibration.

**Unavailable sampler outputs.** The positive-P sample data are described as available on request. A code-based independent reproduction remains possible if the algorithm and inputs are complete; inability to compare against author outputs must be disclosed.

**Metric mismatch.** Similar names can conceal different weighting, subsystem selection, or conditioning. Reimplement the equations and data selections from source, verify a reported figure, and keep an immutable metric manifest.

**Validation is not full-distribution fidelity.** The complete distribution cannot be compared directly at 8,176 modes. Use several independent published diagnostics and bound the conclusion to them.

**Unfair runtime comparisons.** Hardware, preprocessing, sample counts, and optimization budgets may differ across papers. Rerun the baseline on common hardware where code permits; otherwise label published costs as context.

**No algorithmic novelty.** An independent extension to an omitted hard instance can still provide useful evidence, but it may not meet every venue’s novelty bar. The study should emphasize the falsifiable scaling prediction, careful reproduction, and complete matched benchmarking rather than relabeling the earlier feature-selection method.

## 11. BlueQubit Track 2 case

Track 2 explicitly seeks adversarial classical simulation of published quantum-advantage results. This project fits that scope more directly than the earlier small synthetic experiment: it names the published Jiuzhang 4.0 result, targets a published classical algorithm that explicitly deferred that experiment, and defines equal-task accuracy, resource, reproducibility, and failure criteria. BlueQubit describes a three-month program, cloud classical resources, and open publishable artifacts. The public call lists October 14, 2026 as the application deadline; selection and award are not assured by scientific fit alone. [BlueQubit Quantum Flywheel](https://www.bluequbit.io/quantum-flywheel)

For an application, the credible preliminary package is the completed small-system study **plus its skeptical audit**, the public papers and artifacts establishing the omitted-test gap, and the staged implementation gates above. Do not present the preliminary TVD reduction as a Jiuzhang result or as evidence that this project has already broken a quantum-advantage claim.

## References

1. H.-L. Liu et al., [*Robust quantum computational advantage with programmable 3050-photon Gaussian boson sampling*](https://arxiv.org/html/2508.09092), arXiv:2508.09092 (2025; subsequently published in Nature).
2. N. Goodman et al., [*Gaussian boson sampling: Benchmarking quantum advantage*](https://arxiv.org/html/2604.12330), arXiv:2604.12330 (2026).
3. T. Liu et al., [*Efficient simulation of low-entanglement bosonic Gaussian states in polynomial time*](https://arxiv.org/abs/2512.10643), arXiv:2512.10643 (2025).
4. [BlueQubit Quantum Flywheel](https://www.bluequbit.io/quantum-flywheel), official program page, accessed October 3, 2026.

## Cross-links

- [[GBS Classical Simulation Project Description]] — original broader concept and earlier stages.
- [[First Research Draft]] — initial 144-instance selective-correction study.
- [[Skeptical Audit and Stronger Benchmarks]] — current interpretation and stronger controls.
- [[Correlation-Based Classical Simulation of GBS]] — earlier technical plan and prototype.
