# Hospital Aggregation Project

## Overview

This project contains a Jupyter notebook that aggregates COVID-19 related condition data from FHIR JSON bundles stored in hospital-specific folders. The notebook extracts COVID diagnoses from Condition resources, consolidates them into a single Pandas DataFrame, and exports the result as a CSV file.

## Files Included

- `Hospital_Aggregation (1).ipynb` - Main notebook for importing, filtering, and aggregating COVID condition records from FHIR JSON files.
- `Architecture Development Part 1 (1) (1).pdf` through `Architecture Development Part 6 (1).pdf` - Supporting architecture documentation.
- `response.code (1).png` - Additional image asset.

## Data Source

The notebook is configured to read from Google Drive in a Google Colab environment:

- `main_folder = "/content/drive/MyDrive/fhir"`

Each hospital should have its own subfolder under this path, and each subfolder should contain FHIR bundle JSON files.

## What It Does

The notebook performs the following steps:

1. Mounts Google Drive using `google.colab.drive`.
2. Scans each hospital folder under the main FHIR directory.
3. Loads each `.json` file and reads the FHIR `entry` array.
4. Keeps only `Condition` resources.
5. Filters records where the condition text contains `COVID` or `CORONAVIRUS`.
6. Extracts fields such as hospital name, file name, patient reference, condition text, onset date, and encounter reference.
7. Creates a Pandas DataFrame and exports it to CSV.

## Output

The aggregated data is written to:

- `/content/aggregated_covid_data.csv`

This CSV can be used directly in reporting tools such as Google Looker Studio.

## Requirements

The notebook uses the following Python libraries:

- `pandas`
- `json`
- `os`
- `google.colab`

If running locally, install dependencies with:

```bash
pip install pandas
```

## Usage

### In Google Colab

1. Open `Hospital_Aggregation (1).ipynb` in Google Colab.
2. Run the cell that mounts Google Drive.
3. Confirm the FHIR data path is correct: `/content/drive/MyDrive/fhir`.
4. Execute all cells.
5. Download the generated CSV from `/content/aggregated_covid_data.csv`.

### In Local Jupyter

To run locally, update the `main_folder` path to a local directory and remove or replace the Google Drive mount cell.

Example:

```python
main_folder = "C:/path/to/fhir"
```

## Notes

- The notebook currently filters condition text using string matching on `COVID` or `CORONAVIRUS`.
- If your FHIR data uses coded values instead of plain text, the filter logic may need to be updated.
- The included architecture PDFs appear to document development phases and may be used for design reference.

## Suggested Improvements

- Add error handling for malformed JSON files.
- Extend filtering to support coded conditions or additional COVID-related terms.
- Parameterize input folder and output path.
- Add a notebook cell to summarize data by date or hospital.
