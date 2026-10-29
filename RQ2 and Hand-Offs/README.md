# RQ2: Does reliance on help fade with practice, and differently for students who later struggle?

Part of the LA group project *Early Help-Seeking Transitions* on the ASSISTments 2009–10 data (P(J) skill builder dataset).
RQ2 builds directly on RQ1's outputs: the same seven episode states, the same 7-problem early window (k = 7), the same 2,830 student × skill histories and the same later-performance outcome.

## Contents

| File | What it is |
|---|---|
| `RQ2_reliance_on_help.ipynb` | Full analysis, executed, with the reasoning for each step written above the code |
| `rq2_figures/` | Every figure used in the report, saved by the notebook cell that draws it |
| `requirements.txt` | Python dependencies |

## Input data

The notebook reads RQ1's handoff file `rq1_objects_for_rq2_rq3.pkl` (not committed). Place it at

```
rq1_merged_spm_quade_outputs/rq1_objects_for_rq2_rq3.pkl
```

or edit `HANDOFF_PATH` in the first code cell. It contains:

- `selected_k`: the early window length chosen in RQ1 (7)
- `opt_population`: one row per eligible history (≥ 14 problems), with the later outcome (`later_percent_correct`, `later_struggle` = below 50%) and RQ1's early covariates
- `episode`: one row per problem attempt, labelled with one of seven states (SCAF-PASS, SCAF-STRUGGLE, BOH, HINT-FIRST, ERR-HINT, ERR-SELF, CFA)
- `k3_population`: RQ1's 3-problem-window population, used only for the network replication check

The pickle is loaded with a restricted unpickler that accepts only pandas, numpy and a few builtins, so a modified file cannot run arbitrary code.

## How to run

```bash
pip install -r requirements.txt
jupyter nbconvert --to notebook --execute --inplace RQ2_reliance_on_help.ipynb
```

Bootstraps use fixed seeds, so rerunning reproduces the reported numbers and regenerates `rq2_figures/`.

## Analysis outline

1. **Hint items only.** RQ2 is about the student's choice to use help, so automatically scaffolded problems are excluded.
2. **Stuck problems only.** Later struggle is defined by wrong answers, and every help state requires a wrong answer, so raw help use would restate the outcome. Reliance is measured among problems not correct on the first attempt.
3. **Measures.** Per history and window: bottom-out share (BOH), hint-before-trying share (HINT-FIRST), and self-correction share (ERR-SELF). Change = later share − early share, so each history is compared with itself (2,095 histories, 1,211 students).
4. **Part 1: fading within groups.** Mean change per group with student-level bootstrap 95% CIs.
5. **Part 2: difference at the same starting level.** Stratified comparison within early score, weighted n₁n₀/(n₁+n₀), plus heterogeneity tests across early scores.
6. **Main test.** Quade-type rank ANCOVA as in RQ1: rank(change) ~ rank(later % correct) + RQ1 covariates + skill fixed effects, partial F-test; repeated with the early level of the measure added (regression to the mean).
7. **Robustness.** Later problems split into a behaviour half and an outcome half so no problem is used twice, with adjustment for each half's difficulty.
8. **Network check.** A pre-specified replication of an exploratory transition-network pattern (it did not replicate).

## Main findings

- Students who did not later struggle reduced bottom-out reliance (about −3 points) and fixed more errors on their own (about +9 points); students who later struggled showed neither change.
- At the same early score, strugglers' bottom-out share changed about 8 points more than others', with no difference across early-score levels; this held with behaviour and outcome measured on separate problems and in the rank ANCOVA.
- Hint-before-trying showed a smaller effect that weakened under the split design.
- The exploratory network pattern did not replicate.

All results are associations, not causal effects.
