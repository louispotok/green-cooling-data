This repo contains a dump of the data that is used in the Green Cooling Initiative's [Country Data](https://www.green-cooling-initiative.org/country-data) map.

The data was accessed with the following command:
```
curl 'https://www.green-cooling-initiative.org/typo3conf/ext/worldmaptool/Resources/Public/Javascript/countries.json' --output raw.json
```

The output is stored as `raw.json`, which contains the following fields:
* `data`: 73944 rows of data. Each row here is a country-year-sector-scenario combination.
* `mapping`: column names for `data`: `['scenario', 'country', 'sector', 'year', 'indirect', 'direct', 'stock', 'sales', 'value', 'consumption']`.
* `identifiers`: the list `['scenario', 'country', 'sector', 'year']`, confirming our finding about the uniqueness of rows in `data`
* `entities`: the list `['country', 'scenario', 'sector', 'subsector', 'region', 'regionSelect']`. I don't know what this means.
* `oldEntities`: auxiliary data that maps to the identifiers used in `data`. For example, the `country` column in `data` uses a country id, and this contains the full country dataset.

A few notes about this dataset:
* There is no distinction made between past data and projections. The 2 scenarios have almost identical data up to and including 2016, so I believe everything 2018 and later is a projection.
* The `year` field in the raw data is "years since 2000". In the output files we change this to be the full year.
* This does not include detailed documentation on the meaning of the columns. The best I see is in `oldEntities['labels']` which has:
```
{
    "indirect": "Indirect emissions",
    "direct": "Direct emissions",
    "total": "Total emissions",
    "erp": "Emission reduction potential",
    "stock": "Appliances in use",
    "sales": "Unit sales",
    "value": "Value",
    "allSectors": "cooling sector"
}
```

This repo contains the following files:
* `raw.json`: the raw data that is sent to your browser to construct the map (the result of the curl command above)
* `data.csv`: the full dataset in csv form
* `cleaned.csv`: like `data.csv` but aggregated on the country-year level, only for past data. Uses country names instead of ids.
* `main.ipynb`: a jupyter notebook that takes `raw.json` and outputs the remaining files, plus shows how to load some of the other useful data (countries and sectors).

# Update June 2024
Green Cooling Initiative has released updated data, dumped here as `updated.json`. If you're interested in cleaned/csv versions of that data please let me know.
