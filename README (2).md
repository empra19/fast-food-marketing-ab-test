# Fast Food Marketing Campaign — A/B/C Test Analysis

Analysis of a three-way promotional campaign test across 137 fast food outlets to determine which promotion to roll out nationally. Dataset sourced from IBM Watson Analytics sample data.

---

## The question

Three promotions (P1, P2, P3) were tested across outlets of varying market sizes over four weeks. Which should be rolled out nationally?

---

## Approach

The raw dataset has 548 rows — four weekly observations per outlet. The first step was aggregating to 137 outlet-level observations to avoid treating repeat measurements from the same location as independent data points.

Before testing promotions, market size (Small/Medium/Large) was tested as a structural variable. It proved highly significant (Kruskal-Wallis H=70.1, p<0.000001), meaning any pooled promotion comparison would be confounded. All promotion testing was run within market size segments separately.

A composition check confirmed the three promotion groups had balanced market size distributions — no compositional bias.

**Tests used:**
- Kruskal-Wallis as the omnibus test (non-parametric, no normality assumption)
- Pairwise Mann-Whitney U with Bonferroni correction (3 comparisons per segment)
- Rank-biserial correlation for effect sizes

---

## Results

|  | P1 vs P2 | P1 vs P3 | P2 vs P3 |
|---|---|---|---|
| **Large markets** | Sig · r=0.625 | Not sig · r=0.190 | Sig · r=0.760 |
| **Medium markets** | Sig · r=0.568 | Not sig · r=0.190 | Sig · r=0.494 |

Both segments converge on the same conclusion. Small markets (n=4-6 per group) were underpowered and excluded from the recommendation.

---

## Recommendation

Eliminate Promotion 2. Roll out Promotion 1 or Promotion 3 — there is no statistically significant difference between them in either segment. Choose based on cost or operational factors.

Estimated gross revenue uplift of £10.8k per outlet per week against the P2 baseline, equating to ~£110m annually under a base scenario of 850 outlets across 12 promotional weeks. Net uplift ~£89.8m after illustrative promotion costs.

---

## Files

| File | Description |
|---|---|
| `fast_food_campaign_analysis.ipynb` | Full analysis pipeline with visualisations |
| `WA_Marketing-Campaign.csv` | Raw dataset |
| `stakeholder_dashboard.pdf` | Power BI dashboard export |
| `stakeholder_dashboard.pbix` | Power BI file (update data source path on first open) |

---

## Tools

Python · pandas · scipy · matplotlib · Power BI
