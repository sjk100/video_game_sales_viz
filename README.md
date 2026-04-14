# Video Game Market Entry Analysis — Interactive Dashboard

> A four-part Tableau Public dashboard exploring the video game market (2006–2016) to identify the most viable entry strategy for a new publisher. Built on top of a full SQL analysis pipeline — see the [SQL project repository](https://github.com/sjk100/video_game_sales) for the full methodology, data pipeline, and findings.

---

## Live Dashboard

**[View on Tableau Public](https://public.tableau.com/app/profile/sam.kidd1822/viz/video_game_sales_viz/Dashboard1)**

**[View on GitHub Pages](https://sjk100.github.io/video_game_sales_viz/)**

---

## What This Dashboard Answers

A single business question drives all four dashboards:

**Where is the best opportunity to enter the video game market as a new publisher?**

The dashboard is structured as a guided story across four screens, each building on the last toward a final investment recommendation.

---

## Dashboard Walkthrough

### 1 of 4 — Market Size
*Which genres generate revenue and which platforms carry them?*

Establishes the shape of the market before any judgement is made. Shows genre market share trends over the decade, typical revenue per game title by genre, platform sales efficiency, and the platform lifecycle — which consoles are rising, which are fading.

**Key observation:** Action and shooter have grown consistently in market share since 2011. PS4 leads all current-generation platforms on sales per release.

---

### 2 of 4 — Competition
*Are some genres locked up by a handful of publishers, which are open?*

Introduces two measures of market control: an attractiveness score (median sales adjusted down for concentrated markets) plotted against title-level competition, and publisher concentration showing how much of each genre's revenue the top five publishers control. Regional skew data reveals where the global picture doesn't apply.

**Key observation:** Shooter looks attractive on headline metrics but publisher concentration exceeds 75%. Action and role-playing are the least controlled genres. Role-playing is over-indexed in Japan by +16.82% — a significant regional niche invisible in global figures.

---

### 3 of 4 — Entry Risk
*Where would a new entrant have a chance?*

The most analytically original section. Measures breakout rate — the percentage of first-time publishers in each genre who matched or exceeded their genre-year median sales — to test whether attractive genres actually deliver for new entrants.

**Key observation:** Shooter's 11.11% breakout rate is the decisive finding. Despite leading on attractiveness and trend metrics, fewer than 1 in 9 new entrants in the genre reach the typical sales level. Action's 38.71% breakout rate makes it the clearest path in. Role-playing sits at 18.18% — moderate but more forgiving than shooter.

---

### 4 of 4 — Invest
*Where should a new publisher invest?*

Synthesises all signals into a summary matrix and two concrete strategic options, supported by genre-platform performance data and decade-long market trend slopes.

| Signal | Action | Role-playing | Shooter |
|---|---|---|---|
| Attractiveness Score | ✅ High | ✅ Moderate | ✅ Highest |
| Market Share Trend | ✅ +1.8 | ✅ +0.4 | ✅ +1.6 |
| New Entrant Breakout Rate | ✅ 38.71% (High) | ✴️ 18.18% (Moderate) | ❌ 11.11% (Low) |
| Publisher Concentration | ✅ <50% | ✴️ 67% | ❌ >75% |
| Japan Regional Niche | ❌ | ✅ +16.82% | ❌ |
| Top Genre on PS4 & XOne | ✅ | ❌ | ✅ |

**Option A — Action on PS4 & XONE**
Growing market share, lowest publisher concentration of the three shortlisted genres, and a moderate new entrant success rate. The genre's high game count means differentiation is essential — a generic action title is unlikely to succeed, but a distinctive one has a more level playing field than shooter.

**Option B — Role-playing on PC & 3DS, Japan-led**
More forgiving competitive conditions and a significant regional tailwind in Japan. Lower total revenue ceiling than action but a more clearly defined audience. A successful Japanese launch could serve as a beachhead for broader expansion. Expand to PS4 later if successful enough to capture global interest.

**Avoid:** Shooter, Platform, Strategy, Simulation, Racing, Adventure.

---

## How It Was Built

### Data & SQL Pipeline
The underlying data is the [VGChartz dataset from Kaggle](https://www.kaggle.com/datasets/gregorut/videogamesales) — approximately 16,500 games with regional and global sales figures by platform, genre, and publisher.

The raw CSV was ingested into PostgreSQL, normalised across five relational tables, cleaned, and analysed through three query files covering genre dynamics, publisher competition, and market opportunities. Results were exported as CSVs and connected to Tableau Public.

The full pipeline — schema design, ETL, cleaning decisions, exploratory queries, and all analysis SQL — is documented in detail in the **[SQL project repository](https://github.com/sjk100/video_game_sales)**, including reproduction instructions.

---

### Tools
- **PostgreSQL** — data storage, normalisation, cleaning, and analysis
- **Tableau Desktop** — visualisation and dashboard
- **GitHub Pages** — hosting

---

## Key Metrics Explained

**Attractiveness Score** — a genre's typical sales (median, not mean) weighted down by two concentration penalties: title-level HHI and top-10 title dominance. Weights are derived from the standard deviation of each component across genres rather than set manually, so the data determines how much each factor matters.

**Breakout Rate** — the percentage of first-time publishers in a genre who matched or exceeded their genre-year median sales on their debut title. Genre-year median is used as the baseline rather than a fixed threshold so the bar adjusts for the market conditions at the time of release.

**HHI (Herfindahl-Hirschman Index)** — measures market concentration. Values near 0 mean sales are spread across many titles or publishers; values near 1 mean one or two dominate. Applied at both title level (genre analysis) and publisher level (publisher dominance).

**Market Share** — genre sales as a percentage of total market revenue per year, rather than raw sales. This removes the effect of overall market growth and makes year-on-year comparisons valid.

**Regional Skew** — a region's genre share minus the global genre share. A positive value means that region over-indexes on that genre relative to the global average.

---

## Limitations

**Physical sales only.** The dataset captures physical retail sales. Digital sales — which grew substantially across 2006–2016, particularly on PC — are not reflected. PC performance is likely understated and genres with a stronger digital presence (strategy, simulation) may appear weaker than they were.

**Estimates, not audited data.** VGChartz figures are retail sampling estimates, not publisher-verified sales data. Regional figures are extrapolated from a subset of tracked markets. All figures should be treated as directional rather than precise.

**Scope.** Analysis covers 2006–2016. The recommendations reflect the market as it stood at end of 2016. Platform lifecycles and genre trends have shifted since, particularly with the Nintendo Switch launch and continued digital growth.

Full limitations are documented in the [SQL project README](https://github.com/sjk100/video_game_sales/blob/main/README.md).

---

## Repository Structure

```
├── index.html        # GitHub Pages entry point with embedded dashboard
├── README.md         # This file
└── LICENSE           # MIT
```

---

## Related

[video_game_sales Repository](https://github.com/sjk100/video_game_sales) — full pipeline, methodology, cleaning decisions, and raw query files.

---

## Data Source

[Video Game Sales — Kaggle](https://www.kaggle.com/datasets/gregorut/videogamesales)
Gregory Smith, scraped from VGChartz. ~16,500 games with regional and global sales figures by platform, genre, and publisher.
