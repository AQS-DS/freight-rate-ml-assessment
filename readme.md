# Freight Rate Prediction

Tabular regression solution for predicting freight load rates. The training target is
`posted_rate`; final predictions are written to the `predicted_rate` column.

The main work is in:

- `notebooks/eda.ipynb` — data exploration and data-quality checks
- `notebooks/model.ipynb` — temporal validation, model comparison, final fit and predictions

The final model uses a linear regression pipeline. Model selection uses a temporal
holdout because the provided validation and December datasets occur after the
training period.

## Setup

```bash
python -m venv .venv
source .venv/bin/activate   # Windows: .venv\Scripts\activate
python -m pip install -r requirements.txt
```



## Data layout

The original assessment datasets are not committed to this repository.
Place them under `data/` with the following names:

```text
data/
  train-test.csv
  validation.csv
  validation-predictions-template.csv
  december-chart-inputs.csv
```



## Run

Open `notebooks/model.ipynb` and run all cells from top to bottom.

This produces:

```text
validation_predictions.csv
data/december-chart-inputs-predicted.csv
```

`notebooks/eda.ipynb` contains the exploratory analysis that informed the
validation and feature-selection decisions.

## Validate outputs and generate December chart

From the repository root:

```bash
python score.py \
  --predictions validation_predictions.csv \
  --december-predictions data/december-chart-inputs-predicted.csv
```

The scorer validates both output files and generates:

```text
scorer_results/candidate_december.png
```

Final validation metrics are calculated by Spotter after submission.