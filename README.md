# Market & User Behavior Analysis — Ice Videogame Store

## Overview
Analysis of global video game sales data for an online retailer operating 
worldwide. The goal is to identify patterns that determine commercial success 
across platforms, genres, and regions to support data-driven acquisition and 
advertising strategies for 2017.

## Note on Language
The Jupyter notebook and internal comments are currently in Spanish.
An English version is in progress.

## Tools & Libraries
Python · Pandas · SciPy · Seaborn · Matplotlib

## Dataset
Provided by TripleTen. Contains historical sales data through 2016 across 
platforms, genres, and regions, including critic and user scores and ESRB 
ratings.

**Key fields:** `platform`, `genre`, `year_of_release`, `na_sales`, 
`eu_sales`, `jp_sales`, `other_sales`, `critic_score`, `user_score`, `rating`

## Methodology

### 1. Data Preparation
- Standardized column names to snake_case.
- Corrected data types: release year converted to integer.
- Missing scores and TBD values converted to NaN (retained for scatter plots 
  where functions handle nulls natively).
- ESRB ratings: missing values assigned to new `unrated` category.
- Critic and user scores normalized to a unified 100-point scale.
- Added `total_sales` column as sum of all regional sales.

### 2. Exploratory Data Analysis
- Data filtered from 2005 onward: captures a full console generation cycle 
  (Xbox 360 launch year) and maximizes score data availability.
- Peak release years: 2008–2009. Declining post-2012, likely due to longer 
  development cycles for newer platforms.
- Console lifecycle: approximately 10 years, with sales peaking ~5 years 
  after launch (Xbox 360: 2010, PS3: 2011, Wii: 2009).
- Wii showed faster decline than competitors; WiiU showed weak performance 
  vs. PS4 and Xbox One.
- Critic score correlation with sales: low-moderate (r ≈ 0.4). 
  User score correlation: near zero (r ≈ 0.1).
- Top genres by average sales (preferred over totals to reduce volume bias): 
  Shooter, Platform, Sports, Racing, Role-Playing.

### 3. Regional User Profiles

| Region | Top Platforms | Top Genres | Notes |
|---|---|---|---|
| North America | X360, Wii, PS3 | Action, Sports, Shooter | PS4 gaining ground; E and M ratings dominant |
| Europe | PS3, X360, Wii | Action, Sports, Shooter | Racing genre appears; PS3 leads over X360 |
| Japan | DS, 3DS, PS3 | Role-Playing, Action | Portable consoles dominant; no Microsoft platforms in top 5; high unrated share |

### 4. Hypothesis Testing

**H1: Xbox One vs. PC user ratings**
- H₀: Average user ratings for Xbox One and PC are equal.
- H₁: Average user ratings for Xbox One and PC are different.
- Test: Welch's t-test (unequal sample sizes, equal variance assumed).
- Result: **Rejected H₀** (p = 0.0037 < α = 0.05). Ratings differ 
  significantly — platforms should not be analyzed as equivalent audiences.

**H2: Action vs. Sports user ratings**
- H₀: Average user ratings for Action and Sports genres are equal.
- H₁: Average user ratings for Action and Sports genres are different.
- Test: Welch's t-test.
- Result: **Rejected H₀** (t = 6.21, p ≈ 0 < α = 0.05). Ratings differ 
  significantly — genres should not be grouped in user preference analysis.

## Key Findings
- **Most promising platforms for 2017:** PS4 and Xbox One (upward trend); 
  PC stable but lower volume.
- **Regional strategies should differ:** Japan requires a distinct approach 
  (portable platforms, RPG focus, no Microsoft).
- **Genre focus by platform:** Shooters perform better on Xbox; sports titles 
  on PlayStation; family titles on Nintendo.
- **Critic reviews have limited but non-negligible impact** on sales; 
  user scores show almost no correlation.

## Project Structure
```
├── datasets/
│   └── games.csv               # Raw dataset
├── Global-E-commerce-Gaming-.ipynb              # Full analysis (Spanish)
└── README.md
```
