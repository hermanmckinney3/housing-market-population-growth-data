# Southeast Housing Market & Population Analysis

Exploring how population growth relates to home prices and sales activity across five Southeastern states and six cities, using interactive Plotly visualizations.

| | |
|---|---|
| **Course** | Data Visualization (IAN-605), UNCG (Spring 2026) Informatics & Analytics | 
| **States** | North Carolina, South Carolina, Tennessee, Virginia, West Virginia |
| **Cities** | Charlotte, Raleigh, Greensboro, Winston-Salem, Knoxville, Nashville |
| **Time span** | 2012–2025 |
| **Tools** | Python, pandas, Plotly |
| **Data sources** | [Redfin Data Center](https://www.redfin.com/news/data-center/) (housing) · [FRED](https://fred.stlouisfed.org/) (population) |

---

## Table of Contents
1. [Overview](#overview)
2. [Key Findings](#key-findings)
3. [Population](#population)
4. [Home Prices](#home-prices)
5. [Sales Activity](#sales-activity)
6. [Visualization Design](#visualization-design)
7. [Data Dictionary](#data-dictionary)
8. [Limitations](#limitations)
9. [Repository Structure](#repository-structure)
10. [How to Run](#how-to-run)

---

## Overview

Deciding where to live is one of the biggest financial decisions people make. Southeastern states have grown quickly in recent years and are often seen as more affordable than major metros elsewhere. This project asks:

- How have median home prices changed over time across these cities and states?
- Is population growth associated with rising home prices?
- How does sales activity (homes sold) differ across regions and times of year?
- Which cities remain more affordable relative to their growth?

**What this project demonstrates**
- Cleaning and combining two data sources with different formats and time scales (monthly Redfin housing data, annual FRED population data)
- Converting messy text fields (e.g. `$325K`, `1,234`) into usable numbers
- Building consistent, readable interactive charts with Plotly
- Using color consistently across charts so states and cities are easy to track

---

## Key Findings

- **Cities fall into clear price tiers.** In 2025, Raleigh and Nashville averaged around **$510K**, Charlotte about **$455K**, and Knoxville, Greensboro, and Winston-Salem roughly **$295K–$317K**.
- **Prices rose sharply after 2020.** Average median prices in every city rose about **48–71%** from 2020 to 2025. Knoxville had the largest jump (about $186K to $317K).
- **Raleigh was the only city to dip from 2024 to 2025** (about $516K to $508K), yet it is still the second most expensive city in the group, behind Nashville.
- **Virginia is the most expensive state and West Virginia the least.** In 2025, Virginia averaged about $481K and West Virginia about $249K. NC, SC, and TN were tightly grouped around $400K–$405K.
- **SC and NC are the fastest-growing states; West Virginia is shrinking.** In 2025, South Carolina grew about 1.5% and North Carolina about 1.3%, while West Virginia's population declined slightly, continuing a multi-year trend.
- **Raleigh added the most people.** Its population grew from about 1.2M in 2012 to 1.6M, the largest gain of the five cities.
- **Home sales are seasonal.** Sales in most cities peak in late spring and early summer, then drop steadily through winter, so spring is the best time for buyers to start looking.

Population growth and price growth generally move together, but not one-to-one. Raleigh grew the most and is among the most expensive, while Knoxville saw the fastest price growth with more modest population growth.

---

## Population

![State population map](images/1map_state_pop.png)

![State population comparison](images/2bargraph_state_pop.png)

![Population growth rate by state](images/3linechart_state_growth_pop.png)

North Carolina is the largest of the five states at about 11.2M people. NC and SC have grown the fastest, while West Virginia is the only state with a declining population.

![Population over time by city](images/6linechat_city_pop_growth.png)

![Latest population by city](images/7barchart_city_pop.png)

![Population table by city](images/8table_city_pop.png)

All five cities grew steadily. Raleigh (1.6M) and Charlotte (1.2M) are the largest and have grown the most.

> **Note:** City population figures cover each city's broader area as people usually mean it: Charlotte is Charlotte/Mecklenburg County, and the other cities use their surrounding metro area. Nashville has housing data but no population data in this project.

---

## Home Prices

![Average median home price per year by state](images/9linechart_state_avg_median_overtime.png)

![Median home price by state, 2024 vs 2025](images/4dbarchart_state_median_price_.2024_v_2025.png)

Every state's average median price rose from 2024 to 2025. Virginia stands well above the rest, West Virginia well below, and NC, SC, and TN are nearly identical.

![Average median home price per year by city](images/12linechart_city_median_price_overtime.png)

![Median home price by city, 2024 vs 2025](images/5dbarchart_city_median_price_.2024_v_2025.png)

City prices rose steadily through the 2010s and accelerated after 2020. Three tiers are visible:

| Tier | Cities | 2025 avg. median price |
|---|---|---|
| Higher | Nashville, Raleigh | ~$508K–$511K |
| Middle | Charlotte | ~$455K |
| More affordable | Knoxville, Greensboro, Winston-Salem | ~$295K–$317K |

Raleigh and Nashville are both state capitals, which may contribute to stronger job markets and housing demand. Charlotte sits between the tiers as a large, in-demand market that hasn't reached capital-city price levels.

---

## Sales Activity

![Homes sold, NC vs TN](images/10linechart_tn_nc_homes_sold.png)

![Homes sold over time by city](images/11linechart_city_homes_sold.png)

Monthly sales follow a strong seasonal pattern: they climb through spring, peak around May–June, and fall off from late summer into January. Buyers will generally find the most activity in spring and early summer.

---

## Visualization Design

- **Consistent colors.** Each state uses its flagship university's color (UNC blue, Gamecock garnet, Tennessee orange, Virginia Tech maroon, WVU navy), and each city uses a local university's color. The same colors carry across every chart. Knoxville switches to gray in the housing charts so Tennessee orange isn't shared with Nashville.
- **Grouping for comparison.** 2024 vs. 2025 bars are grouped side by side so year-over-year changes are easy to see.
- **Dark theme** throughout for a consistent look.
- **What I'd change:** make the gridlines more subtle so attention stays on the data.

---

## Data Dictionary

<details>
<summary><b>Key columns</b></summary>

| Column | Source | Description |
|---|---|---|
| `Median Sale Price` | Redfin | Median price of single-family homes sold that month (USD), converted from text like `$325K` |
| `Homes Sold` | Redfin | Number of single-family homes sold that month |
| `Region` | Redfin | State name, or city as `City, ST` (split into `City` and `State`) |
| `Month of Period End` | Redfin | Month of the data (e.g. `January 2024`), converted to a date |
| `Population` | FRED | Annual population estimate, converted from thousands to full values |
| `observation_date` | FRED | Date of the population estimate |
| `Pop_Growth_%` | Calculated | Year-over-year population change by state |

</details>

<details>
<summary><b>Data files (<code>data/</code>)</b></summary>

| File | Contents |
|---|---|
| `redfin_state_housing.csv` | Monthly single-family housing data for NC, SC, TN, VA, WV |
| `redfin_cities_housing_sinfam.csv` | Monthly single-family housing data for the six cities |
| `redfin_national_single_family.csv` | Monthly national single-family housing data |
| `fred_nc_population.csv`, `fred_sc_population_data.csv`, `fred_tn_population.csv`, `fred_va_population_data.csv`, `fred_wv_popupation_data.csv` | Annual state population (thousands) |
| `fred_charlotte_population.csv`, `fred_raleigh_population.csv`, `fred_greensboro_population.csv`, `fred_ws_population.csv`, `fred_knoxville_population.csv` | Annual city population (thousands) |
| `*_cleaned.csv`, `city_pop_combined.csv`, `combined_pop_data.csv` | Cleaned outputs written by the notebook |

Redfin files are exported as UTF-16, tab-separated text.

</details>

---

## Limitations

- **Population data is annual; housing data is monthly.** Population trends are broad and can't explain short-term price swings.
- **Correlation, not causation.** Prices are also driven by interest rates, income, jobs, and housing supply, none of which are included here.
- **Partial 2026 data was excluded.** Redfin data runs through February 2026, so yearly averages and time-series charts stop at 2025 to avoid misleading two-month averages.
- **Mixed geographic definitions.** Charlotte's population is Charlotte/Mecklenburg County while the other cities use metro areas, and Redfin's city boundaries may not match FRED's exactly.
- **Small set of regions.** Five states and six cities, chosen for regional interest, not as a representative sample.

---

## Repository Structure

```
├── code_visualizations.ipynb   # Data cleaning and all visualizations
├── requirements.txt
├── data/                       # Raw Redfin and FRED files, plus cleaned outputs
└── images/                     # Chart exports used in this README
```

---

## How to Run

```bash
git clone https://github.com/hermanmckinney3/<housing-market-population-growth-data
>.git
cd <housing-market-population-growth-data>
pip install -r requirements.txt
jupyter notebook code_visualizations.ipynb
```

The `data/` folder is included, so the notebook runs as is. Charts are interactive Plotly figures and display when the notebook is run locally (GitHub's notebook preview doesn't render them, which is why static images are included here).

---

**Herman McKinney**<br>
M.S. Informatics & Analytics, University of North Carolina at Greensboro<br>
[LinkedIn](https://www.linkedin.com/in/herman-mckinney-090b93214) · [hermanmckinney3@gmail.com](mailto:hermanmckinney3@gmail.com)
