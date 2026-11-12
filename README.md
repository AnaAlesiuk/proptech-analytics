# proptech-analytics
PropTech analytics for the Swiss housing market — EDA of price drivers (location, age, house type), with groundwork for AI-based valuation.

# PropTech Analytics: Swiss Housing Market

Exploratory data analysis of Swiss house prices: data quality audit, postal-code-to-canton mapping
and price-per-m² analysis by location, building age and house type.

*Developed under the R&D initiative at **BelaZayka Engineering Consulting**.*

## Project Goal

A non-commercial research and learning project exploring which factors drive house prices
in Switzerland, and building the groundwork for AI-based property valuation.

---

## Key Findings

- **Location is the strongest price driver.** Median price per m² ranges from ~3,400 CHF (Jura)
  to ~12,100 CHF (Geneva), a ~3.6× spread, much larger than the differences by building age or house type.
- **Old houses are cheaper, but partly because of what they are and where they are.** Houses built
  before 1919 have a median of ~4,900 CHF/m² vs. ~7,000–8,000 for later periods. This group contains
  more farm houses and multi-family buildings, and many are in rural areas.
- **The cheapest listings per m² are real properties, not data errors:** mostly old rural houses
  in Jura and Valais, often with very large living space.

## Data Cleaning Approach

| Step | Result |
|---|---|
| Raw listings | 973 |
| Rows with missing or invalid (≤ 0) values in key columns → `df_quarantine` | 338 |
| Clean dataset used for analysis → `df_clean` | 635 |

- Rows with problems are **kept aside, not deleted**, so they can be reviewed or imputed later.
- `Balcony`: missing values are labelled `Unknown`, not `No`. The data contains explicit `False` values,
  so a missing value means "not reported", not "no balcony".
- Medians are used instead of means because prices are heavily right-skewed.
- Cantons with fewer than 10 listings are excluded from the canton ranking.

## Data

| File | Description |
|---|---|
| `house_prices_switzerland_2024.csv` | Swiss house listings, 2024. **Not included in this repository** — download it from Kaggle (see below) |
| `swiss_postal_codes.csv` | Postal code → canton → region lookup (3,360 postal codes). Source: [GeoNames](https://www.geonames.org/), CC BY 4.0 |

**Dataset:** [House Prices Switzerland 2024]([Kaggle URL]) by Etienne Kaiser,
licensed under [CC BY-NC-SA 4.0](https://creativecommons.org/licenses/by-nc-sa/4.0/).
Download the file and place it next to the notebook.

Regions follow the 7 statistical regions (*Grossregionen*) of the Swiss Federal Statistical Office.

## How to Run

1. Download the dataset from Kaggle and rename it to `house_prices_switzerland_2024.csv`
2. Place it in the same folder as the notebook, together with `swiss_postal_codes.csv`
3. Install dependencies and start Jupyter:

```bash
pip install -r requirements.txt
jupyter lab PropTech.ipynb
```

Requires Python 3.11+.

## Roadmap

- Outlier detection for price per m²
- Price comparison within cantons (age and house type, controlling for location)
- Imputation of missing values in the quarantine dataset
- AI-based valuation: a model or LLM agent estimating prices for listings without a price,
  validated against listings with known prices

```text
├── PropTech.ipynb                      # Main analysis notebook
├── house_prices_switzerland_2024.csv   # Raw listings
├── swiss_postal_codes.csv              # Postal code → canton reference
├── requirements.txt                    # Dependencies
└── README.md
```
