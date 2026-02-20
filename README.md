# NYC Healthcare Access Equity Analysis

**More hospitals don't mean healthier neighborhoods. The Bronx has more healthcare facilities per capita than any NYC borough, and the worst health outcomes. This analysis of 2,368 census tracts reveals why income, not access, drives health disparities and where healthcare investment is needed most.**

[![Tableau Dashboard](https://img.shields.io/badge/Tableau-Dashboard-2B5329?style=flat-square&logo=tableau&logoColor=white)](https://public.tableau.com/app/profile/jess.duong/viz/NYCHealthcareAccessEquityAnalysis/NYCHealthcareAccessEquityAnalysis)
[![Final Report](https://img.shields.io/badge/Excel-Final_Report-2B5329?style=flat-square&logo=microsoftexcel&logoColor=white)](reports/)
[![Notebooks](https://img.shields.io/badge/Jupyter-Notebooks-6AAB73?style=flat-square&logo=jupyter&logoColor=white)](scripts/)
[![Visualizations](https://img.shields.io/badge/Charts-Visualizations-C4A84D?style=flat-square&logo=python&logoColor=white)](visualizations/)

---

## Project Background

NYC invests billions in healthcare infrastructure, yet health outcomes vary dramatically by neighborhood. The conventional assumption is that expanding facility access will improve outcomes, but this analysis proves otherwise. Across 2,368 census tracts and five boroughs (2018-2022), the Bronx has the highest facility rate per capita (6.7 per 100K) and the worst diabetes prevalence (14.2%), while Manhattan has fewer facilities but the best outcomes (8.5% diabetes). Income, not access, is the primary driver.

By merging CDC health data, Census demographics, and NYC Open Data facility records, then applying linear regression and K-means clustering, this analysis identified four distinct neighborhood health profiles. The most vulnerable communities, with $53K median income, 14.8% diabetes, and 34.3% obesity, are concentrated in the South Bronx and Central Brooklyn. The recommendation to NYC Department of Health leadership: stop building more clinics and start investing in barrier reduction, insurance navigation, and integrated economic support in the neighborhoods that need it most.

## Data Structure

Three datasets were merged into a master analytical file, plus one independent time series:

**Datasets merged:** CDC PLACES health outcomes (10,699 tract-year observations) | U.S. Census ACS demographics (borough-level income and population) | NYC Open Data healthcare facilities (aggregated to borough level)

**Independent dataset:** FRED NYC unemployment rate (NEWY636URN), monthly, Jan 2000 - Dec 2024, 300 observations

**Master dataset:** 10,699 rows | 2,368 unique census tracts | 5 boroughs | 5 years (2018-2022) | 14 variables

**Analytical methods applied:** Linear regression (income vs. diabetes prevalence) | K-means clustering (k=4, 9 standardized variables, n=8,582) | Time series decomposition and stationarity testing | Geospatial choropleth mapping

## Executive Summary

**The central finding is counterintuitive: income, not facility access, is the primary driver of health outcomes in NYC.** The Bronx has the highest healthcare facility rate per capita yet the worst health outcomes across every metric. Meanwhile, K-means clustering revealed four distinct neighborhood profiles, with the most vulnerable communities concentrated in the South Bronx and Central Brooklyn. Economic shocks like COVID-19 disproportionately impact these same neighborhoods.

### Top Findings

**1. Income drives health outcomes, not facility access (The Bronx Paradox).** The Bronx has the highest facility rate per capita (6.7 per 100K) yet the worst diabetes rate (14.2%). Manhattan has fewer facilities per capita but the best health outcomes (8.5% diabetes). Regression confirms income significantly predicts diabetes (p < 0.0001), with an R-squared of 0.16 due to the granularity mismatch between borough-level income and tract-level health data.

**2. Four distinct neighborhood health profiles exist across NYC.** K-means clustering identified four community types ranging from High-Income Healthiest (Cluster 0: $102K income, 9.0% diabetes) to High-Need Under-Resourced (Cluster 3: $53K income, 14.8% diabetes, 34.3% obesity). Health outcomes worsen consistently as income decreases.

**3. Health disparities are geographically concentrated.** Cluster 3 (worst outcomes) concentrates in the South Bronx and parts of Brooklyn. Cluster 0 (best outcomes) dominates Manhattan and Staten Island. Queens has the lowest facility density and highest uninsured rate (7.4%), representing a distinct coverage gap.

**4. Economic shocks disproportionately impact vulnerable communities.** NYC unemployment hit 17.6% during COVID (May 2020), exceeding the national peak. Recovery is slowest in the same Cluster 3 neighborhoods that already have the worst health outcomes and fewest economic resources.

## Insights Deep Dive

### The Bronx Paradox

![The Bronx Paradox](visualizations/bronx_paradox_paired_bar.png)

The Bronx has more healthcare facilities per 100K residents than any other borough (6.7), yet it also has the highest diabetes prevalence (14.2%), the highest obesity rate (33.2%), and the highest stroke rate (3.8%). Manhattan, with a moderate facility rate (6.1 per 100K), has the lowest diabetes rate at 8.5%. This pattern holds across every health metric measured — more facilities do not equal better outcomes. Income is the real driver, with the Bronx's $48.7K median income compared to Manhattan's $103.9K explaining the disparity far more than facility access.

### Four Neighborhood Health Profiles

![Cluster Profiles](visualizations/cluster_radar_profiles.png)

K-means clustering (k=4) identified four distinct neighborhood profiles across NYC. The radar chart normalizes all five dimensions to a 0-1 scale, with income inverted so higher values represent greater need. Cluster 3 (High-Need, Under-Resourced) dominates across every dimension — these neighborhoods have the lowest income ($53K), highest diabetes (14.8%), highest obesity (34.3%), and highest stroke rates (4.1%). The clear expansion from inner to outer profiles reinforces that health disparities follow a consistent income gradient.

| Profile | Tracts | Avg. Income | Diabetes | Obesity | Uninsured |
|---------|--------|-------------|----------|---------|-----------|
| High-Income Healthiest | 1,583 | $102,357 | 9.0% | 23.1% | 4.1% |
| Urban Core Moderate Access | 2,897 | $80,023 | 10.3% | 25.5% | 5.6% |
| Coverage Gap Communities | 2,598 | $86,150 | 11.7% | 25.9% | 7.4% |
| High-Need Under-Resourced | 1,504 | $52,657 | 14.8% | 34.3% | 6.9% |

### Geographic Concentration

![Cluster Map](visualizations/cluster_map_tableau.png)

The most vulnerable communities are geographically concentrated. Cluster 3 (darkest green) fills the South Bronx and extends into parts of Central Brooklyn. Cluster 0 (lightest green) dominates Manhattan and Staten Island. Queens is predominantly Cluster 2 (gold), representing a distinct coverage gap — it has the highest uninsured rate (7.4%) and the lowest facility density (4.4 per 100K). This geographic concentration means targeted interventions can reach the most vulnerable populations efficiently.

## Recommendations

**Target Investment in Cluster 3 Neighborhoods.** Prioritize South Bronx and Central Brooklyn where $53K median income coincides with 14.8% diabetes prevalence. These neighborhoods need integrated health and economic support, not just more clinics.

**Shift Resources from Facility Expansion to Barrier Reduction.** The Bronx Paradox shows more facilities alone do not improve outcomes. Redirect investment toward transportation access, health literacy programs, and preventive care outreach that address the real barriers.

**Expand Insurance Navigation in Queens.** Queens has the highest uninsured rate (7.4%) and lowest facility density. Insurance enrollment services and community health workers could close this specific coverage gap.

**Build Proactive Surge Capacity for Economic Downturns.** NYC unemployment hit 17.6% during COVID. Cluster 3 communities have the fewest resources to absorb economic shocks. Healthcare planning must account for economic volatility with flexible staffing and emergency funding mechanisms.

## Tools & Skills

| Tool | Use |
|------|-----|
| Python (pandas, scikit-learn, statsmodels) | Data cleaning, merging, regression, K-means clustering |
| Tableau Desktop & Public | Interactive dashboard with 5 story points, choropleth maps, calculated fields |
| matplotlib, seaborn, Folium | Static visualizations, correlation heatmaps, interactive choropleth maps |
| Jupyter Notebook | Analysis pipeline across 6 notebooks |
| Excel | 10-sheet companion report with full documentation |

**Analytical techniques:** Multi-source data integration (CDC, Census, NYC Open Data) | Linear regression with train/test split | K-means clustering with elbow optimization | Time series decomposition and stationarity testing (ADF) | Geospatial choropleth mapping | Per-capita rate calculation | Stakeholder-ready dashboard design

## Deliverables

| Document | Description |
|----------|-------------|
| [Tableau Dashboard](https://public.tableau.com/app/profile/jess.duong/viz/NYCHealthcareAccessEquityAnalysis/NYCHealthcareAccessEquityAnalysis) | Interactive 5-story-point storyboard with maps, scatterplots, cluster analysis, and recommendations |
| [Final Analysis Report](reports/) | 10-sheet Excel workbook documenting data integration, cleaning, all analytical results, and recommendations |
| [Python Notebooks](scripts/) | 6 Jupyter notebooks covering the full analysis pipeline from data prep through time series |
| [Visualizations](visualizations/) | Choropleth maps, correlation heatmaps, cluster scatterplots, regression plots, time series charts |

## Author

**Jessica Duong**

Data Analyst | [LinkedIn](https://www.linkedin.com/in/jess-duong/) | [Portfolio](https://jess-duong.github.io/) | duong.t.jess@gmail.com

---

*Data sources: CDC PLACES (2020-2024 releases), U.S. Census American Community Survey, NYC Open Data Health Facility dataset, FRED NYC Unemployment Rate (NEWY636URN).*

## Acknowledgments

AI tools were used to support portions of this project, including project planning, dataset evaluation, and documentation. All analysis, code execution, interpretation, and recommendations are my own.
