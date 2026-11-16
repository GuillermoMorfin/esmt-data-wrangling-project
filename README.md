# Inflation and Stock Prices

*Data Wrangling through Analytics with Python* · ESMT Berlin, MAAI 2028 · Group 4 Pinot Nero

## The question

Between 2014 and 2024, did each country's share prices grow faster than its consumer prices? In other words, in which countries did investors gain in real terms, and in which did inflation eat the gains?

## The answer

One chart (`data/processed/…png`) and one or two sentences.

## Sources

| source | link | what we used | terms of use |
|---|---|---|---|
| OECD Data Explorer | https://data-explorer.oecd.org (dataset *Financial market*, `DSD_STES@DF_FINMARK`) | yearly share price index per country, 2014 to 2024 | free to use with attribution, see `docs/sources.md` |
| World Bank Indicators API | https://api.worldbank.org/v2/country/all/indicator/FP.CPI.TOTL.ZG | inflation, consumer prices (annual %), 2014 to 2024 | CC BY 4.0 |
| Wikipedia | https://en.wikipedia.org/wiki/ISO_3166-1 | table of ISO 3166-1 country codes | CC BY-SA 4.0 |

All three are downloaded by `notebooks/01_acquire.ipynb`. Nothing was downloaded by hand.

## What's where

| | |
|---|---|
| `notebooks/` | one notebook for each stage, run in order |
| `docs/cleaning_log.md` | what was wrong with each source and how we fixed it |
| `data/processed/DATA_DICTIONARY.md` | what each column of the final table means |

## Team and contributions

| name | contributions |
|---|---|
| | |
