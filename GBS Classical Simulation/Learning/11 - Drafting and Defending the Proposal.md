# 11 — Drafting and Defending the Proposal

Prerequisites: Lessons 00–10, especially [[07 - The Preliminary Study and Its Audit]] and [[09 - Reproduction and Fair Comparisons]]. Session plan: 15 minutes on the outline, 30–45 on a draft, then a separate review session.

## Your final deliverable

Write a 600–900-word working proposal before compressing it into actual application fields. The word range is a learning exercise, not a grant requirement. Use [[Sources and Project Map]] to consult the current specification, audit, and existing form draft. Preserve your own wording and reasoning; copying the draft is not the mastery test.

## Build the proposal from six questions

| Section | Question you must answer | Evidence or decision needed |
| --- | --- | --- |
| Problem and gap | Which published prediction remains untested? | Named method, omitted target, precise source passage. |
| Objective | What will your study determine? | Model/data targets, output task, scope. |
| Method | What will you reproduce and run? | Artifact audit, independent numerical checks, staged gates. |
| Evaluation | What counts as success, failure, or inconclusive? | Frozen diagnostics, uncertainty, comparable baselines. |
| Preliminary evidence | What have you already done? | Synthetic study and skeptical audit, including negative result. |
| Resources and outputs | What is needed, and what will be released? | Profile-supported budgets, reproducible artifacts, bounded conclusions. |

For each factual sentence, keep a small evidence ledger: claim, supporting source and section, status (reported/completed/proposed), limitation, and wording that follows. A hypothesis needs a test, not a citation pretending it is an established result.

## Worked revision

Overclaim: “Our method is 37% more accurate and will break the Jiuzhang advantage using GPUs.”

Defensible revision: “In a synthetic small-system study, selected correlation corrections reduced mean TVD relative to a pairwise baseline. A stronger audit found no computational advantage for the enumerative implementation. We now propose a faithful reproduction of a published phase-space sampler and a staged test of its accuracy and resource cost on the specified experimental target.”

The revision separates prior evidence from future work, identifies the comparator, retains the unfavorable control, and avoids inventing GPU performance or an experimental result.

## Define outcomes before you know them

- **Positive:** the faithful sampler completes the locked task and meets source-matched diagnostic criteria; a cost advantage additionally requires a comparable measured baseline.
- **Mixed:** some diagnostics pass, others fail, or fidelity is achieved without a resource benefit.
- **Negative:** a validated implementation fails accuracy or resource gates under the declared conditions.
- **Blocked:** essential artifacts or method details cannot support a faithful reproduction; document the missing item and use the declared fallback.

These outcomes differ. Insufficient data to reproduce a result is not evidence that its algorithm failed.

## Review rubric

Score each item 0 (missing), 1 (vague), or 2 (specific and supported): research gap; physical/output task; model versus data distinction; method/approximation; reproduction gates; metrics/uncertainty; fair baselines; preliminary boundaries; resource evidence; outcomes/deliverables. A high total cannot compensate for a fabricated fact. Repair every zero and every unsupported factual claim.

## Oral defense and final checkpoint

Answer without reading:

1. Why this method and this experiment?
2. Where does the approximation enter?
3. What do passing tests fail to prove?
4. What did your earlier audit reject?
5. What is the first reproduction gate?
6. What makes the cost comparison fair?
7. What will you publish if the main target is unavailable or fails?

Ask a tutor to challenge one paragraph at a time and request your revision before supplying theirs. You are ready to revise the real proposal when you can defend these answers, trace its claims to evidence, and specify the outstanding checks honestly. Before submitting, inspect the actual form, deadline, eligibility, and resource labels; this curriculum does not verify them.

Return to [[Learning Path]] and update [[Learning Progress]] based on demonstrated understanding.
