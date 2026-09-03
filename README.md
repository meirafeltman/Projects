[README (2).md](https://github.com/user-attachments/files/31770296/README.2.md)
# Measuring the Impact of the 2023 MLB Rule Changes

DS-399 Major Capstone Project · Meira Feltman · Instructor: Sharath Kumar Jagannathan · May–July 2026

## Overview
This project examines whether MLB's three 2023 rule changes (the pitch clock, the shift ban, and larger bases) actually did what they were intended to do. Using a quasi-experimental before/after design across five seasons (2021–2025), the analysis separates real effects from ordinary year-to-year variation through statistical testing, causal-inference checks, and cross-validated predictive models.

## Data
All data is publicly available with no licensing restrictions:
- **Baseball Savant (Statcast)**: batting stats, player speed, handedness (pybaseball)
- **FanGraphs**: strikeout rate, walk rate, slugging %
- **Retrosheet Game Logs**: game duration, used to test the pitch clock

Scale: 670 player-seasons · ~9,700 games · 2,874 sprint speed records · 2021–2025

## Methodology
Two pre-rule seasons (2021–2022) are compared against three post-rule seasons (2023–2025). Five hypotheses were written before looking at the data:
- **H1**: Did games get shorter? (pitch clock)
- **H2**: Did stolen base attempts increase? (larger bases)
- **H3**: Did left-handed hitters get more hits? (shift ban)
- **H4**: Did strikeouts go down? (pitch clock)
- **H5**: Did any effects persist into 2024–2025?

Analysis pipeline:
1. EDA and descriptive stats by hypothesis (H1–H4)
2. H3 subgroup analysis (LHB vs. RHB)
3. OLS regression: predicting BABIP and stolen-base success rate
4. Bootstrap confidence intervals
5. Difference-in-differences (DiD)
6. Placebo test (fake 2022 "rule change" as a falsification check)
7. Player fixed-effects panel regression
8. Cross-validated model comparison (Linear Regression, Elastic Net, Random Forest) with permutation importance

## Key Findings
- **H1 — Games got shorter: YES.** Average game time dropped from 3h 5m (2022) to 2h 41m (2023), a 24-minute drop (Cohen's d = −1.22). Held up through every causal check, including the placebo test and player fixed effects, the strongest, most robust finding in the study.
- **H2 — Stolen bases increased: PARTLY.** Total steals rose 22.5% (1,055 → 1,292) with success rate up from 77% to 80%, continuing to grow through 2025. The aggregate trend is real; player-level significance was borderline.
- **H3 — Shift ban helped lefty hitters: PARTLY.** BABIP rose slightly (.296 → .302) in the raw data, but once player skill is controlled for, the shift-ban effect mostly disappears, speed and slugging % explain more than the rule change itself.
- **H4 — Strikeouts dropped: NO.** K% actually rose slightly (19.7% → 21.0%); walk rate stayed flat. Pitchers adapted to the pitch clock without losing effectiveness.
- **H5 — Effects persisted: YES.** Both the game-time drop and stolen-base increase continued trending through 2024–2025, not a one-year blip.
- **Models:** Elastic Net outperformed Linear Regression and Random Forest for both BABIP and steal-success prediction (5-fold CV). BABIP R² ≈ 13% (expected, BABIP is notoriously hard to predict). For steal success, the post-rules indicator was the second-strongest predictor, the clearest model-level evidence the rules mattered.

**Bottom line:** the pitch clock was a clear, robust success. Stolen bases rose meaningfully. The shift ban's effect is more complicated than it first appears once individual skill is accounted for.

## Repository Contents
- `Capstone_Final.ipynb`: full analysis pipeline (EDA through cross-validated models)
- `README.md`: this file

## How to Run
1. Clone the repository, or download `Capstone_Final.ipynb` directly
2. Install dependencies:
   `pip install pybaseball pandas numpy matplotlib seaborn scipy statsmodels scikit-learn`
3. Open `Capstone_Final.ipynb` in Jupyter Notebook, JupyterLab, or Google Colab
4. Run all cells in order. Data is loaded from `/ds399/data/clean/` (batting, game logs, sprint speed); update the path if running outside the original Colab/Drive setup.

## Author
Meira Feltman
