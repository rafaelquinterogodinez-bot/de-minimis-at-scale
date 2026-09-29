# **De minimis at Scale – Replication Materials**

Replication materials for *De minimis at Scale: Legal Thresholds and the Political Visibility of Programmed Compliance*.

This package reproduces the paper's patent counts, keyword screening, and average monthly U.S. general imports using the supplied data.

## Files

| Folder | File | Contents |
| --- | --- | --- |
| `data/` | `patents_script1_.csv` | 1,328 patent records from the first search strategy. |
| `data/` | `patents_script2_.csv` | 827 patent records from the second search strategy. |
| `data/` | `patent_screening.csv` | Exclusion reasons and source links for the 17 direct-search records. |
| `data/` | `census_imports_monthly_totals.csv` | 920 country-month observations from January 2016 to July 2025. |
| `scripts/` | `patent_replication(1).ipynb` | Patent query definitions, deduplication, counts, and keyword screening. |
| `scripts/` | `trade_replication(1).ipynb` | Census data validation and monthly import averages. |

## **Run the analysis in Google Colab**

1. **Open [Google Colab](https://colab.research.google.com/), select File → Upload notebook, and upload `patent_replication(1).ipynb` from `scripts/`.**

2. **Connect to a runtime. In the Files panel on the left, upload `patents_script1_.csv` and `patents_script2_.csv` from `data/` into Colab's default working directory, `/content`.**

3. **Keep `RUN_COLLECTION = False` and select Runtime → Run all.**

4. **Upload `trade_replication(1).ipynb` to Colab. In that notebook's Files panel, upload `census_imports_monthly_totals.csv` into `/content`.**

5. **Keep `REFRESH = False` and select Runtime → Run all.**

**With these settings, both notebooks reproduce the analysis from the supplied CSVs without API keys.** They display the main results and create a `results/` folder for generated CSV files.

**To retrieve patent data anew, set `RUN_COLLECTION = True` and enter your own SerpAPI key when prompted. To retrieve Census data anew, set `REFRESH = True` and enter your own Census Bureau API key when prompted.**

**Download the generated CSV files from `results/` through Colab's Files panel.**

## Patent analysis

The patent records were retrieved from Google Patents through SerpAPI. The patent notebook contains both original search strategies: 45 query specifications in the first and 151 in the second.

The notebook combines the two datasets and identifies unique publications by `publication_number`.

| Measure | Expected result |
| --- | ---: |
| Records in the first dataset | 1,328 |
| Records in the second dataset | 827 |
| Records before cross-dataset deduplication | 2,155 |
| Publications shared by both datasets | 172 |
| Unique publications | 1,983 |
| Unique Amazon publications | 44 |
| Direct-search publications | 17 |

Keyword screening searches the titles and snippets supplied in the CSVs. Both the regular-expression and literal-term searches identify the same publication, `US20120030136A1`, whose use of “de minimis” concerns securities taxation.

`patent_screening.csv` provides supplementary documentation of the exclusion reasons for the 17 direct-search records. It is not an input to the automated counts or keyword searches.

## Census import analysis

The Census data cover China, Hong Kong, Taiwan, Vietnam, Thailand, Malaysia, Singapore, and Mexico, with 115 monthly observations per country.

Source: U.S. Census Bureau, [International Trade Imports by End-Use API](https://api.census.gov/data/timeseries/intltrade/imports/enduse).

`GEN_VAL_MO` records monthly U.S. general import values in dollars. Each observation is a country total, identified by `I_ENDUSE = "-"` and `COMM_LVL = "-"`.

The trade notebook checks country-month coverage and calculates each country's arithmetic mean over January 2016–July 2025.

| Country | Average monthly imports, USD billions | Rounded as reported in the paper |
| --- | ---: | ---: |
| China | 39.041753330 | 39.0 |
| Mexico | 32.602601427 | 32.6 |
