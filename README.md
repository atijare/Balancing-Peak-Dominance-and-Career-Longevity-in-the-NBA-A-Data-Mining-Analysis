The Peak–Longevity Frontier: Era-Adjusted NBA Career Analysis

An Intro to Data Mining project measuring who best combines peak dominance and career longevity across NBA eras.

🔎 Research Question

Which NBA players best balance peak dominance with sustained excellence, once we account for differences in era (rules, style, and league scoring levels)?

We answer this by constructing:

an era-adjusted scoring metric,
a peak metric (best 4-year stretch),
longevity and durability measures, and
a single Balance score that blends them.

📦 Dataset
Source: Kaggle — Historical NBA Data and Player Box Scores
Link: https://www.kaggle.com/datasets/eoinamoore/historical-nba-data-and-player-box-scores/data?select=PlayerStatistics.csv

Table used: PlayerStatistics.csv (game-level box scores per player)

Note: you’ll need a Kaggle account to download the data.

🗂️ Repo Structure (suggested)
.
├── notebooks/
│   └── project1_nba_peak_longevity.ipynb     # Main analysis notebook
├── data/
│   └── PlayerStatistics.csv                   # (not tracked) place after download
├── figs/
│   ├── league_scoring_trend.png
│   ├── lebron_mj_era_adjusted.png
│   └── peak_vs_longevity.png
├── tables/
│   └── top25_balance.csv
├── README.md
└── requirements.txt


If you prefer, add a .gitignore to avoid committing large data files.

⚙️ Environment

Create and activate a virtual environment, then install requirements.

# using uv/venv/conda—pick your favorite; here’s venv:
python -m venv .venv
source .venv/bin/activate      # Windows: .venv\Scripts\activate
pip install -r requirements.txt


requirements.txt (example)

pandas>=2.0
numpy>=1.24
matplotlib>=3.7

🚀 Quickstart

Download data from Kaggle and place PlayerStatistics.csv under data/.

Open notebooks/project1_nba_peak_longevity.ipynb.

Run all cells. The notebook will:

Parse dates and create a season label (e.g., 2017-18).

Filter to Regular Season.

Aggregate to player-season totals (summing points, games, minutes, etc.).

Compute the league’s games-weighted PPG per season.

Compute era-adjusted PPG (player PPG divided by that league baseline).

Build peak (best 4-year average), longevity (# of eligible seasons), and durability (avg games per season).

Produce a Balance ranking and export figures/tables.

Outputs are saved to:

figs/league_scoring_trend.png

figs/lebron_mj_era_adjusted.png

figs/peak_vs_longevity.png

tables/top25_balance.csv

🧠 Method (one-paragraph summary)

We compute the league’s games-weighted PPG each season by dividing total points scored by all players by the total number of player-games. A player’s era-adjusted PPG is their own PPG divided by that league games-weighted PPG. Peak dominance is the player’s best 4-year rolling average of era-adjusted PPG, considering only seasons with at least 41 games to avoid small-sample spikes. Longevity is the number of such eligible seasons, and durability is average games per eligible season (scaled by 82). The Balance score multiplies these three components: best 4-year era-adjusted PPG, the natural log of (1 + eligible seasons) to reward longevity with diminishing returns, and average games per season divided by 82 to account for availability.

📊 Figures You’ll See

League Scoring Trend (Weighted): shows why era adjustment is necessary; league baselines shift over time.

LeBron vs. Jordan (Era-Adjusted): same timeline, highlighting “higher peak vs. longer prime.”

Peak vs. Longevity Scatter: x = career seasons (≥ 41 GP), y = best 4-year era-adjusted PPG; bubble size = durability; color = career-start decade. The upper-right frontier identifies players who did both: peak high and last long.

⚖️ Config & Reproducibility

At the top of the notebook:

MIN_GAMES = 41   # eligibility threshold
WINDOW    = 4    # rolling window for peak


Change these to run sensitivity checks (e.g., 30/50/60 games, 3/5-year windows). We recommend reporting Top-25 overlap (Jaccard) and rank correlation (Spearman) relative to the baseline to show robustness.

🧩 Notes & Gotchas

Team changes mid-season: player-season totals are collapsed across teams so each player appears once per season.

Avoiding small samples: eligibility requires ≥ 41 games; this prevents one-game outliers (e.g., play-in explosions) from corrupting leaderboards.

Weighted league average: don’t average per-player averages—sum points ÷ sum games per season removes small-sample bias.

🧪 (Optional) Efficiency Lens

As an appendix, you can compute TS% and an era-adjusted TS+ (player TS% divided by league TS%). Recreate the scatter and table using TS+ to show that your conclusions aren’t driven by volume alone.

🧭 Limitations & Impact

Focuses on scoring; does not capture defense/playmaking/on-off impact.

Regular season only; playoffs omitted by design.

Era adjustment via league PPG is one defensible lens; per-possession or efficiency-weighted variants may tell different stories.

Rankings shape narratives; present Balance as a lens, not a verdict.

📚 References

Kaggle Dataset: Historical NBA Data and Player Box Scores — https://www.kaggle.com/datasets/eoinamoore/historical-nba-data-and-player-box-scores?select=PlayerStatistics.csv

Libraries: pandas, numpy, matplotlib

🧾 License

Add your preferred license (e.g., MIT) here.

🗣️ Acknowledgments

Thanks to the dataset author(s) and the open-source Python community.
