# Sources for the project

This is a list of sources that work well for the project. Every source here is free, can be reached from a Codespace, and allows use for
teaching and research. Read the terms of use for each source you choose, and record them in `docs/sources.md`.

You can also use sources that aren't on this list.

## APIs

| source | what | access | things to know |
|---|---|---|---|
| [Frankfurter](https://frankfurter.dev) | ECB euro reference rates, daily since 1999 | no key | a whole time series in one request |
| [World Bank Indicators](https://datahelpdesk.worldbank.org/knowledgebase/articles/898581-api-basic-call-structures) | thousands of country indicators, yearly | no key | `format=json`, responses as `[meta, data]`, and pages of 50 by default. The data is under CC BY 4.0. |
| [Eurostat](https://ec.europa.eu/eurostat/web/user-guides/data-browser/api-data-access/api-getting-started/api) | EU statistics down to regions (NUTS) and cities | no key | Answers come in JSON-stat, which needs flattening. Filter with dimension codes. |
| [OECD Data Explorer](https://www.oecd.org/en/data/insights/data-explainers/2024/09/api.html) | OECD statistics (SDMX) | no key | The Data Explorer builds the API URL for any table ("Developer API"), and CSV is available. It's rate-limited, so keep to about one request a second and save what you get. |
| [OpenHolidays](https://openholidaysapi.org) | public and school holidays for European countries and their regions | no key | Holidays come as date ranges. Each name is a list with one entry per language. |
| [Open-Meteo](https://open-meteo.com/en/docs) | weather forecasts and history since 1940 for any coordinates | no key | free for non-commercial use, up to 10,000 calls a day, with hourly or daily variables |
| [Energy-Charts](https://api.energy-charts.info/) (Fraunhofer ISE) | electricity generation, prices and emissions for Germany and Europe | no key | CC BY 4.0 with attribution to energy-charts.info, except where the response's `license_info` field says otherwise |
| [SMARD](https://smard.api.bund.dev/) (Bundesnetzagentur) | German electricity market data | no key | Timestamps are in milliseconds, and the data comes in weekly chunks that you request by index. |
| [Overpass API](https://wiki.openstreetmap.org/wiki/Overpass_API) | OpenStreetMap features such as cafés, stations and bike lanes | no key | It has its own query language. Keep well under 10,000 queries a day, send a `User-Agent`, and wait 30 seconds after a 429. The server is often busy. |
| [Wikidata Query Service](https://query.wikidata.org/) | structured facts about almost anything (SPARQL) | no key | Send a `User-Agent`. Queries time out after a minute. |
| [MediaWiki API](https://www.mediawiki.org/wiki/API:Main_page) | Wikipedia page views, revisions and content | no key | The [User-Agent policy](https://meta.wikimedia.org/wiki/User-Agent_policy) applies. |
| [OpenAlex](https://docs.openalex.org/) | scholarly works, authors and institutions | **free key required** (since February 2026) | Results come in pages, and each page gives you a cursor for the next one. Generous but metered. |
| [USGS Earthquakes](https://earthquake.usgs.gov/fdsnws/event/1/) | every recorded earthquake | no key | CSV or GeoJSON, with at most 20,000 events per request, so split by time. The data is in the public domain. |
| [GitHub REST API](https://docs.github.com/en/rest) | repositories, issues and releases | token recommended | 60 requests an hour without a token, and pagination in the `Link` header |
| [Hacker News API](https://github.com/HackerNews/API) | stories, comments and scores | no key | one request per item, so save everything you get |
| [Open Food Facts](https://openfoodfacts.github.io/openfoodfacts-server/api/) | food products, ingredients and nutrition | no key | Send a `User-Agent`. It's crowd-sourced, so it's very messy, which makes it good practice. |

## Files and web pages

| source | what | things to know |
|---|---|---|
| [MobiData BW](https://mobidata-bw.de/) | mobility data for Baden-Württemberg, including bike counters | Monthly files follow a pattern in their names, so a loop can download them. The bike counter data is under the *Datenlizenz Deutschland Namensnennung 2.0*. |
| [Our World in Data](https://ourworldindata.org) | the data behind every chart, as CSV (`…/grapher/<chart>.csv`) | It's already tidy, so it's fine as a third source but not as your main one. |
| [Eurostat bulk download](https://ec.europa.eu/eurostat/databrowser/bulk) | whole datasets as compressed TSV | Values carry flags (`12.3 p`), and `:` means missing. |
| [GovData](https://www.govdata.de/) and [data.europa.eu](https://data.europa.eu/) | German and European open-data portals | Catalogues that point to files on many different servers. Check each licence. |
| [Destatis GENESIS-Online](https://www-genesis.destatis.de/) | German official statistics | Report-style CSVs with titles, footers, semicolons and German numbers, much like Block 1. |
| [ONS](https://www.ons.gov.uk/) and [data.gov.uk](https://www.data.gov.uk/) | UK official statistics and open data | Many Excel workbooks with several sheets and notes. |
| Wikipedia tables | lists of almost anything | Ask for the page with a `User-Agent`, then use `read_html` (Block 2). Watch for footnotes (the recipe is in `CHEATSHEET.md`), and remember that pages change. |

## Example requests

Each of these requests worked in November 2026. Read the source's documentation before you change one.

| source | example request |
|---|---|
| MobiData BW, hourly counts from bike counters, with a gzipped CSV file for each month | `https://mobidata-bw.de/daten/eco-counter/v2/fahrradzaehler_stundenwerten_202503.csv.gz` |
| Open-Meteo, hourly weather history for one place | `https://archive-api.open-meteo.com/v1/archive?latitude=49.41&longitude=8.69&start_date=2025-03-01&end_date=2025-03-31&hourly=precipitation,temperature_2m&timezone=Europe%2FBerlin` |
| OpenHolidays, school holidays in one German state | `https://openholidaysapi.org/SchoolHolidays?countryIsoCode=DE&subdivisionCode=DE-BW&validFrom=2025-01-01&validTo=2025-12-31` |
| Energy-Charts, day-ahead electricity prices | `https://api.energy-charts.info/price?bzn=DE-LU&start=2025-01-01&end=2025-01-31` |
| Energy-Charts, electricity generation by source | `https://api.energy-charts.info/public_power?country=de&start=2025-01-01&end=2025-01-31` |
| USGS, earthquakes of magnitude 5 or more in one year, as CSV | `https://earthquake.usgs.gov/fdsnws/event/1/query?format=csv&starttime=2024-01-01&endtime=2025-01-01&minmagnitude=5` |
| World Bank, population by country and year, in pages | `https://api.worldbank.org/v2/country/all/indicator/SP.POP.TOTL?format=json&date=2015:2024&per_page=1000` |
| Wikipedia, a table on a page, read with `pd.read_html` and a `User-Agent` | `https://en.wikipedia.org/wiki/List_of_ISO_3166_country_codes` |
