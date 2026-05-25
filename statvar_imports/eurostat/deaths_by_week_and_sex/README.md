# Eurostat Weekly Deaths by Sex Import

## Overview
This dataset contains weekly death indicators at the national level, sourced from Eurostat. The data tracks total death counts broken down by sex across various European countries.

**type of place:** Country
**years:** Historical data to present (2000-present, recorded weekly e.g., 2000-W01) 
**place_resolution:** Resolved to DCIDs (e.g., dcid:country/ARM, dcid:country/EST)

## Data Source
**Source URL:**
https://ec.europa.eu/eurostat/databrowser/view/demo_r_mwk_ts/default/table?lang=en

**Provenance Description:**
The data is provided by Eurostat, the statistical office of the European Union. It belongs to the "Demography, population stock and balance" database under the "Deaths by week - special data collection" theme, specifically the "Deaths by week and sex" (DEMO_R_MWK_TS) dataset.

## Refresh Type
Automatic Refresh

The refresh is automated using the provided `run_commands.sh` script, which handles both data download and processing.

## How To Run Import
To execute the complete import process (download and processing), run:
```bash
./run_commands.sh
```

### Script Details:
- **Download**: Uses `curl` to fetch the latest SDMX-CSV data from Eurostat's dissemination API.
- **Processing**: Uses `stat_var_processor.py` to map raw data to Data Commons StatVarObservations using the PV map and metadata configuration.

## Key Files
- `run_commands.sh`: Main execution script for download and processing.
- `deaths_by_week_and_sex_pvmap.csv`: Property-Value mapping for StatVar definitions and dimensions.
- `deaths_by_week_and_sex_metadata.csv`: Configuration parameters for the processor.
- `deaths_by_week_and_sex_places_resolved.csv`: Mapping of place codes to Data Commons DCIDs.
- `deaths_by_week_and_sex_output.csv`: Processed statistical observations.
- `deaths_by_week_and_sex_output.tmcf`: Template MCF mapping the CSV columns to Data Commons schema.


## Validation
To validate the generated data, use the Data Commons import tool (lint mode). Note that you must include the StatVar MCF files to resolve schema references:
```bash
java -jar datacommons-import-tool.jar lint output.csv output.tmcf
```
The resulting reports (`report.json`, `summary_report.html`) in `dc_generated/` provide detailed insights into data quality and validation status.

## Testing
Testing is performed using the `test_data` directory:
- Expected Output: `deaths_by_week_and_sex_output.csv`
- Expected TMCF: `deaths_by_week_and_sex_output.tmcf`
