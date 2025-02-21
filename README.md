# ghostfolio-goldensgs-ppr
Integration for Golden SGF PPRs (portuguese "mutual funds") into ghostfolio.
This project downloads the PPR history from the Golden SGF (https://goldensgf.pt/) website (only available as a xlsx excel file) and generates both json and html sample websites which can be then imported as manual scrapers into ghostfolio. Provides the latest UP value as well as all available historical data for each of the PPRs.

A github action is set to update the output folder daily.

## Usage

```
usage: generator.py [-h] [-p PPR] [-l] [-o OUTPUT]

Simple graber for golden SGF PPR historical data. Usage:

options:
  -h, --help            show this help message and exit
  -p PPR, --ppr PPR     PPR name (e.g. "SGF DR FINANÇAS")
  -l, --list            List available PPRs
  -o OUTPUT, --output OUTPUT
                        Output format ("json" or "html")
```

## Example

`python3 generator.py -p "SGF DR FINANÇAS" -o html`

## TODO

- Github action
- Add ghostfolio instructions

