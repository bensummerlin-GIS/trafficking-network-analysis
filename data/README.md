# Data

This folder is where the input data goes. The raw dataset is not included in this repository.

## CTDC Global Synthetic Dataset (required)

The Counter-Trafficking Data Collaborative (CTDC), hosted by the International Organization for Migration (IOM), publishes the Global Synthetic Dataset. Its terms of use do not allow the original dataset to be redistributed, so you need to download it yourself.

1. Go to https://www.ctdatacollaborative.org/page/global-synthetic-dataset
2. Download the Global Synthetic Dataset (CSV), and read the codebook and data dictionary on the same page.
3. Save it here as `data/ctdc_global_synthetic_data_v2026.csv`.

The analysis used the 2026 release (268,515 records, 2002 to 2024). Later releases may give slightly different numbers.

Terms of use: https://www.ctdatacollaborative.org/page/terms-use

Source: Counter-Trafficking Data Collaborative (CTDC), May 2026. https://www.ctdatacollaborative.org/page/global-synthetic-dataset

## Country centroids (needed for notebook E only)

Notebook E reads `data/GEOG594A_D8_F1_NodeCentroids.csv`, a table of 71 countries with the columns `ISO3, ISO2, country_name, lon, lat, source`. It holds one longitude and latitude point per country and no trafficking data.
