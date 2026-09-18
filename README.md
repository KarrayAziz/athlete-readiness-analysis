# Daily Athlete Health, Readiness and Nutrition Analysis

This repository contains a participant-day analysis of athlete health, activity, sleep, injury reporting, wellness and food-image data.

The main workflow is contained in a single notebook and produces a cleaned daily dataset where each row represents one participant on one calendar day.

## Repository structure

```text
.
├── technical_test.ipynb
├── test_dataset.csv
├── requirements.txt
├── README.md
├── data/
│   └── README.md
└── outputs/
    └── tables/
        ├── food_nutrition_per_image.csv
        └── nutrition_alcohol_adjustments.csv
```

The raw dataset is not included in the repository.

## Setup

Python 3.12 is recommended.

### Recommended setup with uv

If `uv` is installed, create a Python 3.12 environment with:

Linux/macOS:

```bash
uv python install 3.12
uv venv --python 3.12 .venv
source .venv/bin/activate
uv pip install -r requirements.txt
```

Windows PowerShell:

```powershell
uv python install 3.12
uv venv --python 3.12 .venv
.\.venv\Scripts\Activate.ps1
uv pip install -r requirements.txt
```

### Alternative setup with standard Python

Linux/macOS:

```bash
python3 -m venv .venv
source .venv/bin/activate
python -m pip install --upgrade pip
python -m pip install -r requirements.txt
```

On Debian/Ubuntu, if virtual-environment support is missing, install it first with:

```bash
sudo apt install python3-venv
```

Windows PowerShell:

```powershell
py -m venv .venv
.\.venv\Scripts\Activate.ps1
python -m pip install --upgrade pip
python -m pip install -r requirements.txt
```

## Data setup

Place the participant folders directly inside `data/`:

```text
data/
├── p01/
├── p03/
└── p05/
```

Each participant folder should preserve the original internal structure, including folders such as:

```text
fitbit/
pmsys/
googledocs/
food-images/
```

See `data/README.md` for more details.

Alternatively, the raw-data directory can be specified with the `PMDATA_RAW_DIR` environment variable.

Linux/macOS:

```bash
export PMDATA_RAW_DIR=/path/to/data
```

Windows PowerShell:

```powershell
$env:PMDATA_RAW_DIR="C:\path\to\data"
```

## Running the analysis

Start Jupyter:

```bash
jupyter lab
```

Open:

```text
technical_test.ipynb
```

Then restart the kernel and run all cells from top to bottom.

The notebook performs:

- raw-source inspection and daily aggregation;
- data cleaning and missingness analysis;
- injury-target construction and modeling;
- wellness-derived performance-readiness modeling;
- food-image metadata extraction and nutrition aggregation;
- final dataset export.

## Nutrition estimates

Food-image nutrition estimates are stored as cached per-image results in:

```text
outputs/tables/food_nutrition_per_image.csv
```

Normal notebook execution does not call an external API.

The cached estimates are aggregated by participant and date. Daily nutrition values represent estimates from the images that were recorded and should not be interpreted as complete dietary intake.

## Output

Running the complete notebook produces:

```text
test_dataset.csv
```

The final dataset contains one row per participant-day over the study period.

The notebook also includes the main exploratory figures, model evaluation results and methodological notes used to interpret the analysis.

## Reproducibility notes

- Python 3.12 is the recommended runtime.
- Randomized models use a fixed random seed.
- Train/validation splits are chronological.
- Missing-value imputation is fitted using training data only.
- Raw data is never modified by the notebook.
- External nutrition inference is not required for normal execution because cached per-image estimates are included.
