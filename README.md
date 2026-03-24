# German Insolvency Analysis (2020–2025)

Data pipeline and Tableau dashboard analyzing German insolvency trends using official statistics from the Federal Statistical Office (Destatis).

## Overview

This project cleans and transforms raw Destatis CSV exports into analysis-ready datasets, which feed a Tableau Public dashboard. The analysis covers 662,000+ insolvency filings across 6 years, broken down by region, industry, and company size.

## Data Sources

All data comes from [Destatis (Statistisches Bundesamt)](https://www.destatis.de):

| Table | Description |
|-------|-------------|
| 52411-0001 | Monthly insolvency totals for Germany |
| 52411-0014 | Corporate insolvencies with affected employees |
| 52411-0018 | Insolvencies by industry sector (WZ08) |
| 52411-0013 | Insolvencies by company size |
| 52411-0110 | Insolvencies by Bundesland |
| 52111-0003 | Business register (active companies by industry) |

## Project Structure

```
├── insolvency_analysis.ipynb   # Data cleaning pipeline (Python/Pandas)
├── data/
│   ├── *.csv                   # Raw Destatis exports
│   └── clean/                  # Cleaned CSVs for Tableau
├── README.md
└── LICENSE
```

## Pipeline

The Jupyter notebook handles all data preparation:

1. **Load** — Read raw Destatis CSVs, which use German headers and hierarchical row structures
2. **Clean** — Parse nested year/month/category rows, handle missing values, standardize formats
3. **Enrich** — Merge insolvency data with business register to calculate insolvency rates per active company
4. **Export** — Write 7 clean CSV files ready for Tableau ingestion

## Output Datasets

| File | Rows | Description |
|------|------|-------------|
| `germany_clean.csv` | 72 | Monthly national totals |
| `bundesland_clean.csv` | 1,152 | Monthly by federal state |
| `industry_clean.csv` | 1,368 | Monthly by industry sector |
| `industry_register_clean.csv` | 1,368 | Industry data enriched with insolvency rates |
| `size_clean.csv` | 432 | Monthly by company size class |
| `germany_unternehmen_clean.csv` | 72 | Corporate insolvencies with employee impact |
| `germany_combined_clean.csv` | 72 | Combined national overview |

## Tools

- **Python 3** with Pandas and NumPy for data cleaning
- **Tableau Public** for visualization

## How to Run

```bash
# Clone the repository
git clone https://github.com/MaSchulmann/insolvency-germany-tableau.git
cd insolvency-germany-tableau

# Install dependencies
pip install pandas numpy jupyter

# Run the notebook
jupyter notebook insolvency_analysis.ipynb
```

## Author

**Maria Schulmann** — [GitHub](https://github.com/MaSchulmann)

## License

This project is licensed under the MIT License. See [LICENSE](LICENSE) for details.
