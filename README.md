# GOase Activity Processing

This repository converts plate reader raw data outputs into a structured GOase activity dataset.

The workflow is intended to support reproducible processing of plate reader data associated with the publication.

## Repository Structure

```text
GOase-activity-processing/
├── GOase_plate_reader_processing.ipynb
├── README.md
├── requirements.txt
├── processed_GOase_activity_dataset.csv
└── data/
    ├── Plate1.xlsx
    ├── Plate2.xlsx
    └── Plate3.xlsx
```

## Input Data

Raw plate reader exports are stored as Excel workbooks in `data/`. The current dataset includes:

- `data/Plate1.xlsx`
- `data/Plate2.xlsx`
- `data/Plate3.xlsx`

Each workbook is a Tecan i-control export with a `Raw` worksheet. The notebook discovers all `.xlsx` files in `data/`, reads the kinetic absorbance table, normalizes well labels, and reshapes the measurements into tidy long format.

`example_output.csv` is used to infer the required output schema and to validate the generated output structure.

## Output Data

The notebook writes:

- `processed_GOase_activity_dataset.csv`

The output columns match `example_output.csv`:

- `plate`
- `well`
- `cycle_nr`
- `time_s`
- `temperature_C`
- `raw_value`
- `mutant`

Note: the raw Excel files do not contain a complete well-to-mutant layout. The notebook derives known mutant assignments from `example_output.csv` and leaves unavailable assignments blank.

## How to Run

From the repository root:

```bash
python3 -m venv .venv
source .venv/bin/activate
pip install -r requirements.txt
jupyter notebook GOase_plate_reader_processing.ipynb
```

Run all notebook cells. The final section writes `processed_GOase_activity_dataset.csv` and validates the generated schema against `example_output.csv`.

## Required Python Packages

- pandas
- openpyxl
- numpy
- jupyter

## Citation / Publication

[Placeholder: link to associated publication]
