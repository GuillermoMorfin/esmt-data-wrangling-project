# Project proposal

**Due Monday 16 November, 09:00.** Push this file together with `notebooks/00_first_look.ipynb`.

## Group

| name | GitHub username |
|---|---|
|Alyan Ahmed|alyan-01|
|Peter Vadja|peteravajda-gif|
|Guillermo Morfin Guerrero |GuillermoMorfin |
|Julian Pabon|Jupabon |

## Question

Did share prices beat inflation between 2014 and 2024, and in which countries?

A share index that goes up 50% sounds good, but if prices in the shops went up 60% over the same years, investors lost money in real terms.
We want to compare the growth of each country's share price index with the rise in its consumer prices, for every country where we can
get both.

## Sources

| source | link | API, file or web page |
|---|---|---|
| OECD Data Explorer, *Financial market* dataset (yearly share price index per country) | [https://sdmx.oecd.org/public/rest/data/OECD.SDD.STES,DSD_STES@DF_FINMARK/.A.SHARE......?startPeriod=2014&endPeriod=2024&format=csvfile](https://sdmx.oecd.org/public/rest/data/OECD.SDD.STES,DSD_STES@DF_FINMARK/.A.SHARE......?startPeriod=2014&endPeriod=2024&format=csvfile) | API (parameters for country, frequency, measure and years) |
| World Bank Indicators, *Inflation, consumer prices (annual %)*, `FP.CPI.TOTL.ZG` | https://api.worldbank.org/v2/country/all/indicator/FP.CPI.TOTL.ZG | API (parameters and pages) |
| Wikipedia, ISO 3166-1 table of country codes | https://en.wikipedia.org/wiki/ISO_3166-1 | web page |

The three sources come from three organisations (OECD, World Bank, Wikimedia).

## Joining the sources

All three have the ISO three-letter country code (`DEU`, `GBR`, ...). The OECD calls it `REF_AREA`, the World Bank `countryiso3code` and
Wikipedia "Alpha-3 code".

- Share prices and inflation are joined on **country code and year**.
- Both APIs also return groups of countries (for example "Euro area", "OECD", "World"). The Wikipedia table is the list of real countries,
  so we use it to keep only codes that are countries.