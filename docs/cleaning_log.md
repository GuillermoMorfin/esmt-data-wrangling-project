# Cleaning log

| file | problem | symptom | fix |
|---|---|---|---|
| `oecd_share_prices.csv` | the file has 16 columns but most say the same thing on every row (frequency, measure, adjustment...) | wide table where only three columns change | checked each one with `.unique()`, then kept `REF_AREA`, `TIME_PERIOD` and `OBS_VALUE` with clear names |
| `oecd_share_prices.csv` | the value is an index, not a price | `UNIT_MEASURE` is `IX` and `BASE_PER` is `2015` on every row, and every country's 2015 value is 100 | kept as an index with 2015 = 100; `02_clean` asserts the base year and the value 100, and the units below describe it |
| `oecd_share_prices.csv` | groups of countries are mixed in with countries | the code `EA20` (euro area) in `REF_AREA` | removed in `03_combine`, by keeping only codes that are in the ISO table, and recorded in `docs/corrections.csv` |
| `oecd_share_prices.csv` | a country could be missing years | fewer than 11 rows for a country | `04_validate` removes such a country and records it in `docs/corrections.csv` (none in the current download) |
| `worldbank_inflation_page_*.json` | the data comes in several pages | one request only gives the first 1000 records | downloaded every page (the `pages` number is in the first element) and added the records together |
| `worldbank_inflation_page_*.json` | each file is a list of two things, `[meta, data]` | `pd.DataFrame(page)` gives nonsense | took `page[1]` for the records |
| `worldbank_inflation_page_*.json` | country and indicator are nested dictionaries | a column of dictionaries | `pd.json_normalize(records)`, which gives `country.value` and so on |
| `worldbank_inflation_page_*.json` | the year is text | `date` has type `str` | `.astype(int)` |
| `worldbank_inflation_page_*.json` | groups of countries ("World", "Euro area", income groups) are in the same list as countries | about 50 more "countries" than exist, some with an empty country code | dropped rows with an empty code in `02_clean`, the rest in `03_combine` with the ISO table, and each of the 46 recorded in `docs/corrections.csv` |
| `worldbank_inflation_page_*.json` | missing values | `value` is `null` for some countries and years | left as missing in `02_clean`. Countries with a missing year between 2015 and 2024 are removed in `04_validate` |
| `worldbank_inflation_page_*.json` | the join on the three-letter code can't be checked from one source alone | a wrong code would silently join one country's inflation to another's share prices | kept the World Bank's own two-letter code (`country.id`) as `wb_alpha2`; `04_validate` asserts that it equals the ISO two-letter code on every row, then drops it |
| `worldbank_inflation_page_*.json` | country names that don't suit a chart | `Korea, Rep.`, `Turkiye`, `Russian Federation` | renamed with a dictionary and `.replace()` |
| `wikipedia_iso_3166_1.html` | the page has several tables | `read_html` returns a list | picked the table with `match="English short name"`, a column header only this table has (the notebook checks that exactly one table matches) |
| `wikipedia_iso_3166_1.html` | Namibia's two-letter code is `NA` | pandas reads `NA` as a missing value | `keep_default_na=False` |
| `wikipedia_iso_3166_1.html` | long column names | `English short name (using title case)` | replaced by assigning a list of simple names to `.columns` |

## Units

| column | unit | note |
|---|---|---|
| `share_price_index` | index, 2015 = 100 | every country's index is 100 in 2015, so 150 means share prices 50% above their 2015 level. The index is built from share prices in local currency, without dividends, so it isn't adjusted for inflation or exchange rates. Growth can be compared between countries, but the level says nothing about how expensive one market is compared with another |
| `inflation_pct` | percent per year | turned into a factor (`1 + pct / 100`) and multiplied over the ten years in `05_store_and_answer` |
