# Cooperation vs Competition in Student Group Work

**Is graded group work a Prisoner's Dilemma, a Snowdrift game or no dilemma at all?**
An empirical game-theory study of 46 postgraduate students, built from a primary survey.

Semester 1 Microeconomics coursework (November 2025), rebuilt as a fully reproducible Python analysis.
Team: Dhriyaman Adak, Nandan Lunawat, Rashtra Mitra.

---

## Key findings

1. **The original Snowdrift conclusion does not survive an audit.** The submitted presentation reported
   T > R > S > P (a Snowdrift game). On inspection the four payoffs were measured on different scales, three of them
   used an outcome partly built from the cooperation questions themselves, and the decisive gap (S − P = 0.06) has
   a 95% bootstrap interval of [−0.23, 0.35], so the data cannot say whether S is above P at all.
2. **With one consistent payoff (self-reported marks), the data lean towards a Harmony game.** Cooperators report
   higher marks than non-cooperators whether or not they faced free-riders. T > R, which both the Prisoner's Dilemma
   and Snowdrift require, holds in about 1% of bootstrap resamples.
3. **Cooperation is linked to higher reported marks; free-riding is not linked to anything measured.** One extra
   point on the Cooperation Index goes with about 0.7 of a marks band (OLS with HC3 errors, p = 0.03; ordered logit
   odds ratio 2.6, p = 0.03). Free-riding does not change the return to cooperating (interaction p = 0.76).
4. **Cooperation and competition are not opposites.** The two indices are essentially uncorrelated
   (Spearman ρ = 0.07, p = 0.63).
5. **Measurement matters.** The Competition Index is acceptable (Cronbach's α = 0.66) and passes a validity check
   against students' stated preferences. The Cooperation Index is not reliable (α = 0.33), so results that use it are
   treated as suggestive.

| Rebuilt payoff matrix (mean marks band, 1 to 6) | Others cooperate | Others free-ride |
|---|---|---|
| **I cooperate** | R = 5.50 (n = 2) | S = 4.52 (n = 21) |
| **I defect** | T = 3.67 (n = 6) | P = 4.10 (n = 10) |

![Rebuilt payoff matrix](outputs/figures/fig4_payoff_matrix_rebuilt.png)
![Marks against cooperation](outputs/figures/fig5_marks_vs_cooperation.png)

---

## Repository structure

```
├── data/
│   ├── raw/survey_responses_anonymised.csv   # survey export, identifying columns removed
│   └── clean/survey_clean.csv                # produced by notebook 01
├── notebooks/
│   ├── 01_data_cleaning.ipynb                # range checks, recoding, documented decisions
│   └── 02_analysis.ipynb                     # indices, reliability, audit, payoffs, regression
├── outputs/
│   └── figures/                              # charts used in this README
├── requirements.txt
└── README.md
```

## Method

**Data.** A Google Form survey of 46 students (40 first-year, 6 second-year), November 2025. All respondents
consented to anonymised use. Timestamp, gender and age were removed before publication because, in a class of 46,
they could identify individuals together.

**Indices.** Cooperation Index = mean of Q8 (enjoy group work), Q9 (share notes) and Q10 (rely on others).
Competition Index = mean of Q5 (enjoy competition), Q6 (outperform others) and Q7 (try harder when competing).
All items on a 1 to 5 agreement scale.

**Payoff design.** A student's own action is cooperate if their Cooperation Index is at or above the median.
The other players' action is taken from Q13, whether the student has observed free-riding. The payoff is the
self-reported marks band, chosen because grades are the real stake in graded group work and because it is not built
from any cooperation item.

**Statistics.** Cronbach's alpha, Pearson and Spearman correlation, Fisher's exact test, Kruskal-Wallis,
non-parametric bootstrap (5,000 resamples of students), OLS with HC3 robust standard errors including an
interaction term, and an ordered logit as a robustness check.

**Main data-cleaning decisions** (full table in notebook 01):

| Issue | Decision |
|---|---|
| Q8 exported with the label "5)" | Renamed by content |
| Q8 values of 7 and 8 on a 1 to 5 scale (3 rows) | Set to missing |
| Two answers ticked on single-choice Q15 (2 rows) | Set to missing |
| Free-riding "Not Sure" (7 rows) | Kept as its own category instead of coding it 0.5 |

## What changed from the original submission

The analysis originally ran in Excel, with derived columns pasted into the CSV and a notebook that only re-displayed
them. This repository rebuilds every number from the raw answers in code. The original Excel-derived columns are kept
in the raw file with the prefix `orig_` so the comparison is transparent. The payoff values, the PD vs Snowdrift test and the
takeaways in the original presentation are superseded by notebook 02.

## How to run

```bash
git clone https://github.com/<your-username>/cooperation-vs-competition-survey.git
cd cooperation-vs-competition-survey
pip install -r requirements.txt
jupyter notebook
```

Run `01_data_cleaning.ipynb`, then `02_analysis.ipynb`. All figures are regenerated in `outputs/figures/` and all tables (CSV and LaTeX) in `outputs/tables/`.
Random seeds are fixed, so bootstrap results reproduce exactly.

## Limitations

- Small, single-class sample (n = 46). Only 8 students reported no free-riding, so the R and T cells are thin.
- Outcomes are self-reported and were not checked against actual grades.
- The Cooperation Index has low internal consistency.
- "Others' action" is a proxy: having observed free-riding is not the same as a specific partner's choice.
- Cross-sectional data, so the associations are not causal and repeated-game strategies cannot be tested.

## Possible extensions

- Link responses to recorded assignment grades, with consent.
- Replace the cooperation items with an established, validated scale.
- Run a short public-goods experiment in class to observe choices directly.

## Skills demonstrated

Survey data cleaning and validation · scale reliability and validity testing · non-parametric inference and
bootstrapping · regression with robust errors and interaction terms · ordered logit · applied game theory ·
reproducible analysis in Python (pandas, SciPy, statsmodels, matplotlib).
