# GBS Glossary

Return to [[Learning Path]]. Definitions here are for reading the lessons; implementation must follow each source's conventions.

| Term or symbol | Meaning | Lesson |
| --- | --- | --- |
| GBS | Gaussian boson sampling: optical preparation, mixing, and detector sampling | 00–02 |
| Classical simulator | Software performing a specified model calculation or sampling task | 00, 05 |
| Mode / qumode | An optical degree of freedom, including a spatial channel or time bin | 02 |
| Squeezed input | An optical state with reduced fluctuation in one quadrature and increased fluctuation in its conjugate | 02–03 |
| Interferometer | An optical network mixing mode amplitudes | 02 |
| Threshold detector | Distinguishes no photon from one or more detected photons | 02 |
| Photon-number-resolving detector | Distinguishes detected photon counts | 02 |
| Click record $x$ | Binary output string; $x_i=1$ means detector output $i$ clicked | 01 |
| Click count $C$ | $\sum_i x_i$; differs from occupation photon count when there are collisions | 01–02 |
| Coincidence event | Detections recorded together within the defined trial/window | 02 |
| $M$, $N$ | Number of measured modes and number of sample records | 01, 08 |
| $P$, $Q$ | Declared target distribution and simulator distribution | 01, 04 |
| Marginal | Distribution after summing over unwanted outputs | 01 |
| Conditioning | Restricting to an event and renormalizing its probabilities | 01 |
| Expectation $\mathbb E[f]$ | Probability-weighted average of an observable | 01 |
| Gaussian state | A quantum state specified by Gaussian quadrature statistics, characterized by first and second quadrature moments | 03 |
| Mean $d$, covariance $V$ | Quadrature mean vector and symmetrized covariance matrix | 03 |
| $r$, $\eta$ | Squeezing parameter and transmission fraction in our teaching formulas | 03 |
| Partial distinguishability | Unresolved differences between photons that reduce interference | 02–03 |
| Joint moment | Expected product of variables, such as $\mathbb E[x_ix_j]$ | 04 |
| Connected correlation / cumulant | Dependence remaining after subtracting lower-order contributions | 04 |
| TVD | $\frac12\sum_x|P(x)-Q(x)|$, between 0 and 1 | 04 |
| Torontonian | Matrix function used for Gaussian threshold-detection probabilities | 05 |
| Maximum-entropy fit | Distribution maximizing entropy subject to specified moment constraints | 07 |
| Positive-P | Stochastic phase-space representation using paired complex variables | 06 |
| Projection / clipping | Mapping an estimator into a permitted range; can change its moments | 06 |
| Whitening–coloring | Transforming stochastic variables to adjust covariance statistics | 06 |
| MPS | Matrix product state, a tensor-network representation with tunable compression | 05 |
| Baseline | A named comparison method for the same declared task | 05, 09 |
| Standard error | Estimated fluctuation of a statistic's estimator across repeated samples | 08 |
| Standardized residual | Difference divided by an appropriate uncertainty estimate | 08 |
| $K$, $\Delta K$ in correlation tests | Fitted comparison slope and its deviation from one | 08 |
| Held-out evaluation | Assessment on cases not used to select/tune the method | 07, 09 |
| Accuracy–cost frontier | Nondominated tradeoffs between error and resource use | 07, 10 |
| End-to-end cost | All declared preparation, generation, I/O, and evaluation costs | 10 |
| Peak resident memory | Maximum process RAM in use, distinct from partial traced allocations | 07, 10 |
| Artifact gate | Check that the required data, model, algorithm, and metric inputs exist | 09 |
| L1024 | Named Jiuzhang 4.0 target configuration; a label, not the output-mode count | 00, 02 |

Do not reuse symbols without context: $K$ can mean correlation cutoff order in an earlier study and fitted slope in an experimental test. The lessons use the meaning appropriate to their topic.
