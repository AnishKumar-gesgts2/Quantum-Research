# BlueQubit Track 2 Grant Form Responses — Draft

**Drafted:** October 5, 2026

**Updated:** October 7, 2026

**Status:** draft answers to the fields supplied by Anish; not submitted. Full-scale reproduction and data/code feasibility checks remain pending. Public prior-work links were verified through GitHub on October 5, 2026.

**Grant response form:** [BlueQubit Quantum Flywheel application form](https://docs.google.com/forms/d/e/1FAIpQLSdGwhevKLEn71C9bRBf8eGHCJ3rp4XwiaDayhMuaId5H8rAEQ/viewform?usp=dialog)
**Program page:** [BlueQubit Quantum Flywheel](https://www.bluequbit.io/quantum-flywheel)

## Track

AI for Breaking quantum advantage claims (adversarial classical simulation)

## Project abstract

Jiuzhang 4.0 implements Gaussian boson sampling (GBS) with 1,024 squeezed inputs and 8,176 output modes, testing classical mockups through count distributions, subsystem likelihoods, and detector correlations. Goodman et al. recently introduced an approximate positive-P phase-space sampler and argued that it should extend to Jiuzhang 4.0 with a moderate resource increase, but explicitly deferred that experiment. I propose to test this scaling prediction through an independent reproduction and adversarial benchmark, determining whether the method can reproduce the experiment's published validation statistics at competitive classical cost.

The project will first audit the released state descriptions, calibration parameters, experimental records, and XQSIM implementation, then reproduce a reported Jiuzhang 2 or 3 benchmark. After this gate passes, I will evaluate the S64 and M256 configurations before targeting L1024. The main workload will generate ten million threshold-click records using the characterized lossy, partially distinguishable model. Evaluation will preserve the original observable definitions, conditioning rules, and sample counts, with uncertainty from independent seeds and resampling. Comparators will include reproducible squashed-state, greedy, and MPS-based methods where their implementations support the same task. I will record preprocessing, sampling, peak resident memory, and total compute cost, retaining failures and incomplete runs.

AI coding agents will assist with translating published algorithms into inspectable implementations, constructing differential tests, profiling numerical kernels, and exploring memory-efficient batching and acceleration. Candidate optimizations will be verified against independent numerical references and frozen before final evaluation. AI-generated code will be assessed through reproducible numerical checks rather than treated as evidence of correctness.

My preliminary work comprises a 144-instance synthetic GBS study, including 108 held-out cases, and an independent Torontonian audit. Although selective correlation fitting improved on a pairwise baseline, an exact method was more accurate in all held-out cases and cheaper on the measured criteria in 102 of 108. This result motivates the present emphasis on faithful baselines and complete resource accounting; it does not establish experimental-scale performance.

The deliverables are a reproducible benchmark repository, an accuracy–cost comparison, and a preprint reporting whether phase-space sampling supports a credible classical challenge or encounters a quantitative scaling or accuracy barrier. Conclusions will distinguish passing selected validation tests from approximating the full output distribution.

## Related Work

My most relevant prior work is the public [Quantum-Research repository](https://github.com/AnishKumar-gesgts2/Quantum-Research), particularly the [first GBS study](https://github.com/AnishKumar-gesgts2/Quantum-Research/blob/main/GBS%20Classical%20Simulation/First%20Research%20Draft.md) and [skeptical audit](https://github.com/AnishKumar-gesgts2/Quantum-Research/blob/main/GBS%20Classical%20Simulation/Skeptical%20Audit%20and%20Stronger%20Benchmarks.md). These contain code, configurations, and results for a 144-instance synthetic study with 108 held-out cases. The audit independently checked the reference probabilities using The Walrus Torontonian implementation and added stronger controls. It found a real correlation-selection effect but no practical advantage for the enumerative prototype.

The proposal builds on [Goodman et al., Gaussian boson sampling: Benchmarking quantum advantage](https://arxiv.org/abs/2604.12330), the authors' [XQSIM code](https://github.com/peterddrummond/xqsim), and the [Jiuzhang 4.0 experiment](https://arxiv.org/abs/2508.09092). Goodman et al. explicitly defer Jiuzhang 4.0. The proposed contribution is an independent test of that omitted configuration, using the experiment's validation protocol and measured end-to-end resources. It extends my preliminary work from exact small-system diagnostics to a published sampling method and experimental-scale benchmarking. It does not assume a new sampling algorithm or an existing quantum-advantage refutation.

## Resource selections

- **AI output tokens:** 1M–10M tokens. Planning estimate: approximately 3 million output tokens across the three-month project, for implementation, differential testing, profiling, optimization, and manuscript/reproduction documentation. This is a planning allocation, not measured consumption or an AI-training requirement.
- **QPU:** Won't need a QPU. The study uses published photonic data and classical GBS simulation; IBM hardware is not needed for this target.
- **GPU:** Planning estimate: approximately 300 GPU-hours. Select the middle tier only if its intended range is 100–1,000 hours. The supplied label “1000–1000 hours” is ambiguous and must be verified before selection. Do not describe the budget as a measured requirement.

## Resource rationale and limits

The published reference implementation is MATLAB/XQSIM and reports CPU runs. CPU resources are the primary requirement. A high-memory CPU allocation and sufficient storage for batched sample generation should be requested wherever the form permits a compute explanation. Actual RAM and runtime requirements must be profiled before final production; no matched L1024 workload has yet been run locally.

The GPU allocation is a provisional cap: 40 hours for profiling and reference checks, 60 for testing acceleration and batching, 140 for the scale-control and L1024 production runs that pass the feasibility gates, and 60 for independent seeds, ablations, and recovery. These are budget shares, not runtime predictions. GPU use is contingent on a validated accelerated implementation; there is no presumed speedup. Unneeded allocation should remain unused.

The AI allocation allows roughly 100 substantial implementation/review cycles at 10,000–20,000 output tokens each, plus optimization and writing passes. Output-token accounting excludes input/context tokens. If the form has no CPU-request field, state the CPU priority in an available resource comment rather than treating GPU hours as a substitute for CPU compute.

## Sources for the application claims

- [Jiuzhang 4.0 experimental paper](https://arxiv.org/html/2508.09092): configurations, modes, detector records, and published validation protocol.
- [Goodman et al. phase-space sampler paper](https://arxiv.org/html/2604.12330): algorithm, explicit Jiuzhang 4.0 omission, source-code availability, and published CPU runs.
- [[Skeptical Audit and Stronger Benchmarks]]: completed preliminary evidence and computational no-go result.

## Review before submission

Confirm the malformed GPU tier label, the official deadline, and whether additional form pages contain CPU/storage or eligibility fields. Run the data/code feasibility gate and, if feasible before submission, a faithful smaller published-method reproduction. Update the abstract's preliminary paragraph only after those new results exist.
