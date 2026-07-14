# Cross-National Variation in LGBT+ Rights Support Across 28 EU Countries

![R](https://img.shields.io/badge/-R-276DC3?style=flat-square&logo=r&logoColor=white) ![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg?style=flat-square)

A multilevel (GLMM) analysis of individual- and country-level drivers of support for LGBT+ rights across the European Union, using Eurobarometer 2019 and V-Dem data.

## Overview

The European Commission's 2019 Eurobarometer survey found support for equal rights for gay, lesbian, and bisexual people ranging from around 31% in Slovakia to 98% in Sweden, a nearly 70-point spread, with 9 countries (Bulgaria, Czech Republic, Denmark, Ireland, Hungary, Italy, Croatia, Malta, and Slovakia) showing a decline relative to 2015. This project uses a multilevel modelling framework to understand this cross-national variation, considering both individual-level and country-level factors simultaneously.

## Data

- **Individual level:** Special Eurobarometer 493 (wave 91.4, fielded May 2019 across all 28 EU member states, N = 27,438), covering socio-demographics, political orientation, religion and minority identity, LGBT-specific attitudes, and media use.
- **Country level:** V-Dem dataset (Maerz et al., 2025), filtered to 2019, providing measures of LGBT political power, freedom of expression, polarisation, online hate speech, educational equality, and GDP per capita.
- Countries matched via ISO2 codes across all 28 EU member states.

## Methodology

1. **Per-country logistic regressions** to visualize heterogeneity in individual-level effects across the 28 countries before formal multilevel modelling
2. **Null random-intercept model** to decompose variance between individual and country levels (Variance Partition Coefficient)
3. **Random-intercept model with individual-level predictors** (socio-demographics, political orientation, religion, LGBT contact, etc.)
4. **Random-intercept model adding country-level V-Dem predictors** to assess how much country-level variance is explained by national context versus individual composition

All models estimated as binomial GLMMs using the `lme4` package.

## Key Findings

- The **null model** shows 30% of total variance in LGBT+ support is attributable to country-level differences, justifying the multilevel approach
- Adding **individual-level predictors** compresses this to 18%, part of the national divergence is compositional (LGBT+ friends, religion, education matter)
- Adding **country-level predictors** reduces it further to 9%, driven almost entirely by one variable: **LGBT political power**. GDP per capita, freedom of expression, polarisation, and educational equality were not significant once individual composition was controlled for
- **Having LGBT+ friends** is the strongest individual-level predictor throughout, and its effect is consistent regardless of a country's LGBT political power, contact and institutional representation operate independently and accumulate
- The 9 declining countries show no single pattern: Denmark and Ireland sit above the EU mean in the final model (decline likely driven by country-specific factors outside the model), while Hungary, Bulgaria, Croatia, Slovakia, and Czech Republic show persistently negative intercepts that survive all controls

## Repository Structure

```
lgbt-rights-multilevel-model/
├── multilevel_lgbt_rights.qmd   # Full analysis (Quarto document)
├── data/
│   └── merged_data_dummy.csv    # Merged Eurobarometer + V-Dem data used to fit the models
├── README.md
├── LICENSE
└── .gitignore
```

## Requirements

`R` (>= 4.2) with: `tidyverse`, `lme4`, `lmerTest`, `broom.mixed`, `ggeffects`, `sjPlot`, `kableExtra`

```r
install.packages(c("tidyverse", "lme4", "lmerTest", "broom.mixed", "ggeffects", "sjPlot", "kableExtra"))
```

## How to Run

```bash
git clone https://github.com/palomanavarro22/lgbt-rights-multilevel-model.git
cd lgbt-rights-multilevel-model
```

Open `multilevel_lgbt_rights.qmd` in RStudio and render. The script reads `data/merged_data_dummy.csv` directly.

## Limitations & Future Research

Even after accounting for individual composition and national context, 9% of country-level variance remains unexplained, likely reflecting dynamics not captured in survey or V-Dem data, such as anti-LGBT+ mobilization or the political role of religious organizations beyond individual religiosity. The cross-sectional design cannot establish causality between LGBT political power and public support, these likely reinforce each other over time. Future work could incorporate panel data across Eurobarometer waves to model this dynamic directly.

## Author

**Paloma Navarro**
MSc in Computational Social Science, UC3M
[LinkedIn](https://www.linkedin.com/in/paloma-navarro-3b7927280/)

## Citation

If you use this analysis, please cite:

```
Navarro, P. (2026). Cross-National Variation in LGBT+ Rights Support Across 28 EU Countries: A Multilevel Analysis.
GitHub repository: https://github.com/palomanavarro22/lgbt-rights-multilevel-model
```

Underlying data: European Commission (2019). Special Eurobarometer 493. Maerz, S. et al. (2025). V-Dem Dataset v15.

## License

This project is licensed under the MIT License, see the [LICENSE](LICENSE) file for details.

---

*Coursework for the Multilevel Modeling course, MSc in Computational Social Science, UC3M.*

