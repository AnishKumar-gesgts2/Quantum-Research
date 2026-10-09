# 10 — Scaling and Resource Budgets

Prerequisite: [[09 - Reproduction and Fair Comparisons]]. Session plan: 15 minutes on scaling, 15 on storage/time, 10 on budget justification.

## Scaling is a model to test

If a component costs $aM^2$, increasing modes from 1,152 to 8,176 multiplies that component by about $50.4$. This conditional arithmetic does not predict the full runtime. Input count, batch size, matrix decompositions, number of records, memory traffic, and implementation details also matter. Identify which kernel has which dependence, and verify it through profiling.

Do not equate a paper's quadratic-scaling prediction with measured end-to-end scaling on our target. A dense matrix decomposition can have a different dependence from drawing one batch of trajectories.

## Worked storage budget

An $M\times M$ real float64 array uses $8M^2$ bytes. At $M=8176$, this is 534,775,808 bytes, about 510 MiB. A $2M\times2M$ covariance at that precision is four times larger, about 2.0 GiB. Complex arrays, multiple copies, spectral modes, and work buffers change the budget.

Ten million 8,176-bit records use 10,220,000,000 bytes, or 10.22 GB, if packed into bits without metadata. One byte per binary entry instead requires 81.76 GB. Text output can be larger. Streaming summary statistics saves storage, but retaining reproducible records or deterministic generation may be necessary for later diagnostics; decide this before production.

## End-to-end cost

Use a decomposition such as

$$
T_{\mathrm{total}}=T_{\mathrm{load}}+T_{\mathrm{prepare}}+T_{\mathrm{generate}}+T_{\mathrm{write}}+T_{\mathrm{evaluate}}.
$$

Report the parts as well as the total, and identify overlapping work if the pipeline is asynchronous. Separate one-time shared setup from each run's work without omitting either from the appropriate comparison. Include rejected draws, fitting, transformations, independent seeds, and failed runs.

If setup takes 300 seconds and throughput is 20,000 valid records per second, ten million records take an illustrative 800 seconds before extra writing/evaluation. This is a toy calculation, not a project runtime estimate.

## Provisional requests versus measurements

The application draft's token and GPU-hour selections are planning allocations. They are not observed requirements or promised speedups. CPU/RAM needs follow from profiling the reference method; GPU acceleration is an optional implementation whose output must be checked. A QPU allocation is not required for a project using published records and classical software.

## Check your understanding

1. Why is batching useful, and what does it not eliminate?
2. If setup takes 500 seconds and generation 100 seconds, what is the end-to-end time before I/O and evaluation?
3. What measurements make a resource request defensible?

> [!answer]- Check after trying
> 1. It can bound sample-array memory. It does not eliminate fixed matrices or reduce total arithmetic automatically.
> 2. 600 seconds.
> 3. Peak process memory, kernel and end-to-end times, throughput, output volume, machine specifications, and repeated-run variability on representative cases.

## Proposal task and checkpoint

Draft a resource paragraph with measured facts, conditional estimates, and provisional caps labeled separately. You are ready when you can calculate a storage estimate and explain why a per-sample time is insufficient.

Next: [[11 - Drafting and Defending the Proposal]].
