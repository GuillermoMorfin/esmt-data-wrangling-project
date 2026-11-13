# Cheat sheet · Common data problems

This is a list of the data problems we ran into in class and how we fixed each one. If something looks wrong when you load your own data,
check here first.

## Files

| symptom | problem | fix |
|---|---|---|
| `UnicodeDecodeError`, or letters like `Ã¼` | the wrong encoding | `encoding="cp1252"`, or whichever one the file was written in |
| `ï»¿` at the start of the first column's name | a byte order mark | `encoding="utf-8-sig"` |
| everything in one column | the wrong separator | `sep=";"`, or `sep="\t"` for tabs |
| `Expected 1 fields in line 5, saw 4` | title lines above the table, or a total below it | `skiprows=4`, and `skipfooter=1` with `engine="python"` |
| numbers are text, or a thousand times too small | a decimal comma and dots between the thousands | `decimal=","` and `thousands="."` |
| a number column is text because of `k.A.` or `-` | missing values written as text | `na_values=["k.A.", "-"]` |
| dates are text, or days and months are swapped | pandas guessed the date format | `pd.to_datetime(col, format="%d/%m/%Y")` |
| an Excel sheet's columns are called `Unnamed: 0`, `Unnamed: 1` and so on | there are notes above the header row | `header=None` to look at it, then `header=` with the right row |
| rows such as `Q1 total` in among the data | the file has subtotal rows | `df[~df["name"].str.contains("total")]` |

## Web pages

| symptom | problem | fix |
|---|---|---|
| a number column from `read_html` is text | footnote markers such as `[a]`, or a dash for "no figure" | the recipe below |
| `read_html` gives one row that says "Loading…" | the page fills its table in with a second request | find that request in the browser's Network tab and ask for it yourself |
| a `403` from Python for a page that opens in a browser | the site refuses programs that don't say who they are | `headers={"User-Agent": "..."}` |
| `429 Too Many Requests` | you are asking too fast | a session with `Retry`, and download each file once |

```python
FOOTNOTE = r"\[.*?\]"    # a regular expression for anything in square brackets

cleaned = col.str.replace(FOOTNOTE, "", regex=True)
cleaned = cleaned.str.replace(",", "")
numbers = pd.to_numeric(cleaned, errors="coerce")    # whatever isn't a number becomes missing
```

## JSON

| symptom | problem | fix |
|---|---|---|
| a column of dictionaries | the records are nested | `pd.json_normalize(records)` |
| a column of lists | one record holds a list of values | `record_path=` for a list of objects, `.explode()` for a list of plain values |

## Combining

| symptom | problem | fix |
|---|---|---|
| half-empty columns after `pd.concat` | the same column has different names in different files | rename each file's columns first, with `df.rename(columns={"old": "new"})` |
| a merge adds rows | the key isn't unique on one side | `validate="many_to_one"`, then look at `df[df["key"].duplicated(keep=False)]` |
| names that should match don't | upper and lower case, spaces at the ends, or a different dash | `.str.lower().str.strip()` on both sides before the merge |
| totals that are far too big or too small | different units or currencies in one column | convert before you stack, and put the unit in the column name |
