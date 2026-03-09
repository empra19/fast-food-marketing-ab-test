# Fast Food Marketing Campaign - A/B/C Test Analysis

Three promotional campaigns tested across 137 fast food outlets over four weeks. The goal was to identify which promotion to roll out nationally, and whether a single recommendation could apply across all market sizes.

Dataset: [Fast Food Marketing Campaign](https://www.kaggle.com/datasets/chebotinaa/fast-food-marketing-campaign-ab-test) via Kaggle.

---

## Approach

The raw dataset has 548 rows — four weekly observations per outlet. Before any significance testing, these were aggregated to 137 outlet-level averages. Weekly rows from the same location are not independent observations, and treating them as such would artificially inflate the sample size and understate p-values.

Market size (Small/Medium/Large) was then tested as a structural variable before any promotion comparison. It proved highly significant (Kruskal-Wallis H=70.1, p<0.000001) — Large outlets average roughly twice the sales of Small outlets. Running a pooled promotion test across all market sizes would conflate the two effects, so all promotion testing was run within segments separately.

A composition check confirmed the three promotion groups had balanced market size distributions, ruling out confounding from uneven assignment.

Within each segment, pairwise Mann-Whitney U tests were run with Bonferroni correction across three comparisons. Rank-biserial correlation was used as the effect size measure.

---

## Results

|  | P1 vs P2 | P1 vs P3 | P2 vs P3 |
|---|---|---|---|
| **Large markets** | Sig · r=0.625 | Not sig · r=0.190 | Sig · r=0.760 |
| **Medium markets** | Sig · r=0.568 | Not sig · r=0.190 | Sig · r=0.494 |

Large and Medium segments converge on identical conclusions. The effect size for P1 vs P3 is r=0.190 in both segments — a consistent small effect that falls short of significance in either. Small markets had only 4–6 outlets per group and were excluded from the recommendation as underpowered.

Weekly trends were stable across all four test weeks, confirming the performance gap is structural rather than a novelty effect.

---

## Recommendation

Eliminate Promotion 2. Roll out Promotion 1 or Promotion 3 based on cost or operational factors. There is no statistically significant difference between them in either segment. 

Estimated gross revenue uplift of £10.8k per outlet per week against the P2 baseline, equating to ~£110m annually under a base scenario of 850 outlets across 12 promotional weeks. Net uplift ~£89.8m after illustrative promotion costs (~£2k per outlet per week, derived from a 3–6% of revenue industry benchmark — replace with actual figures before any investment decision).

An 8–12 week regional pilot is recommended before full national rollout.

---

## Tools

Python · pandas · scipy · matplotlib · Power BI