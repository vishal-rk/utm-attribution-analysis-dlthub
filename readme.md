# UTM Source Attribution Analysis

This repository contains a Jupyter Notebook for analyzing acquisition source quality using a dlt → DuckDB pipeline, cohort/retention analysis, and composite quality scoring.

- Notebook: [utm_attribution_analysis.ipynb](utm_attribution_analysis.ipynb)

## What it does

- Ingests CSV data and builds a DuckDB dataset via dlt.
- Computes acquisition volume, engagement, and retention metrics by utm_source.
- Produces cohort-based weekly/monthly retention heatmaps.
- Builds a composite quality score with configurable weights.
- Exports detailed results and a summary report.

## Inputs and outputs

- Input CSV (expected at repo root): `WorkingStudentDataTask-dlthub.csv`
- DuckDB database: `utm_attribution_pipeline.duckdb` (schema: `user_attribution`)
- Exports:
  - `utm_source_quality_analysis.csv` (per-source metrics and scores)
  - `utm_attribution_summary.csv` (high-level summary)

## Requirements

- Python 3.9+ (recommended 3.10+)
- pip
- VS Code (or Jupyter)

## Quick start

1) Create and activate a virtual environment
```bash
python -m venv .venv
# Windows
.venv\Scripts\activate
# macOS/Linux
source .venv/bin/activate
```

2) Install dependencies
```bash
pip install "dlt[duckdb]" pandas matplotlib seaborn plotly scipy scikit-learn
```

3) Place your CSV at the project root as `WorkingStudentDataTask-dlthub.csv` (or update CONFIG in the notebook).

4) Open the notebook in VS Code
- Open folder in VS Code.
- Open [utm_attribution_analysis.ipynb](utm_attribution_analysis.ipynb).
- Select your Python interpreter (the venv) and Run All.

## Configuration

In the notebook (Step 1), adjust CONFIG as needed:
- Quality score weights: volume_weight, engagement_weight, retention_weight
- Tier thresholds: high_quality_threshold, medium_quality_threshold
- Retention rules: retention_min_events, retention_min_days, retention_month_days
- Paths: input_file, output_quality_file, output_summary_file, database_name, dataset_name

## What to expect

- Tables created in DuckDB (schema `user_attribution`): contacts, events, utm_attribution.
- Visualizations: acquisition volume, engagement scatter, retention heatmaps and curves, cohort trends, funnels.
- Statistical test: t-test between top sources’ engagement.

## Troubleshooting

- No/invalid dates: the notebook sanitizes event dates; cohort charts require valid event_date.
- Empty charts: ensure minimum sample size (CONFIG['min_users_for_analysis']) is met.
- File not found: update CONFIG['input_file'] to your CSV path.

## Repository structure

- [utm_attribution_analysis.ipynb](utm_attribution_analysis.ipynb) — full analysis notebook
- Outputs and DB are generated after running the notebook

## License

MIT