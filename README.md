# ghostfolio-goldensgf-ppr
Integration for Golden SGF PPRs (portuguese retirement savings plans, a sort of "mutual funds") into [Ghostfolio](https://github.com/ghostfolio/ghostfolio).

This project downloads the PPR history from the [Golden SGF](https://goldensgf.pt/) website (only available as a xlsx excel file) and generates json, csv and html sample websites which can be then imported as manual scrapers into [Ghostfolio](https://github.com/ghostfolio/ghostfolio). Provides the latest UP value as well as all available historical data for each of the PPRs.

A github action is set to update the output folder daily (at midnight).

## Usage

```
usage: generator.py [-h] [-p PPR] [-l] [-o OUTPUT]

Simple graber for golden SGF PPR historical data. Usage:

options:
  -h, --help            show this help message and exit
  -p PPR, --ppr PPR     PPR name (e.g. "SGF DR FINANÇAS")
  -l, --list            List available PPRs
  -o OUTPUT, --output OUTPUT
                        Output format ("json", "html", "csv"). Use "all" for all.
```

## Example

To generate a single PPR:

`python3 generator.py -p "SGF DR FINANÇAS" -o all`

To generate data for all PPRs

`python3 generator.py -o all`


## Configuration for GhostFolio

In the self-hosted version create a manual scraper by going to:

> Admin Control -> Market Data -> + (Add Asset Profile) -> Add Manually

and fill the symbol with your PPR name:

 ![Add asset profile](/docs/addassetprofile.png "Add Asset Profile")

In the scraper configuration fill the URL and and the selector:

- **Locale:** US (this is due to the format of the market value number)
- **Mode:** Lazy (Golden SGF only updates the original file weekly and any updates will only reflect daily anyway)
- **URL**: Use the html page from the output folder as raw document (e.g. https://raw.githubusercontent.com/enen92/ghostfolio-goldensgf-ppr/refs/heads/main/output/sgfdrfinancas.html)
- **Selector**: Use `#currentMarketPrice_upvalue`


 ![scraperconfig](/docs/configurationscraper.png "Scraper Config")

Save

Historical data has the be imported manuallly (currently Ghostfolio does not support remote imports).
Use the `.csv` file in the output folder for the corresponding PPR - it's already in the expected format.

 ![historicaldata](/docs/historicaldata.png "Historical data")

Hit import to fill the historical data

 ![graph](/docs/graph.png "graph")

Use like any other standard activity (via `Buy Activities`) and Ghostfolio will track the PPR as part of your portfolio valuation:

![activity](/docs/activity.png "activity")

![activitylist](/docs/activitylist.png "activitylist")

![valuation](/docs/valuation.png "valuation")