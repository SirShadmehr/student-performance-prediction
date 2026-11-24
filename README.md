# Student Performance Prediction

[![Python](https://img.shields.io/badge/Python-3.10%2B-3776AB?logo=python&logoColor=white)](https://www.python.org/)
[![scikit-learn](https://img.shields.io/badge/scikit--learn-ML-F7931E?logo=scikitlearn&logoColor=white)](https://scikit-learn.org/)
[![Pandas](https://img.shields.io/badge/Pandas-Data%20Analysis-150458?logo=pandas&logoColor=white)](https://pandas.pydata.org/)
[![Jupyter](https://img.shields.io/badge/Jupyter-Notebook-F37626?logo=jupyter&logoColor=white)](https://jupyter.org/)

A regression project that estimates a student's **Performance Index** from study-related
features. The project focuses on a transparent, reproducible machine-learning workflow:
data quality checks, exploratory analysis, leakage-safe preprocessing, model comparison,
cross-validation, model interpretation, and model export.

## Project structure

```text
student-performance-prediction/
├── data/                   # Place the input CSV here (not committed)
├── models/                 # Exported model artifacts (not committed)
├── notebooks/
│   └── student_performance.ipynb
├── reports/
│   └── figures/             # Saved charts and evaluation visuals
├── src/                     # Reusable project code
├── .gitignore
├── README.md
└── requirements.txt
```

## Dataset

The notebook expects a CSV file at:

```text
data/student_performance_dirty.csv
```

The dataset is intentionally not bundled. Add your authorized local copy to `data/`.
The notebook expects the target column `Performance Index` and the feature columns
`Hours Studied`, `Previous Scores`, `Extracurricular Activities`, `Sleep Hours`,
`Sample Question Papers Practiced`, and `Notes`.

## Key features

- Audits missing values, duplicate rows, data types, and numeric ranges.
- Treats out-of-range numeric values as missing values for downstream imputation.
- Removes duplicate records before splitting the data.
- Explores feature relationships and evaluates whether `Notes` adds useful signal.
- Uses a `ColumnTransformer` and `Pipeline` so preprocessing is fitted on training data.
- Compares a mean baseline, Linear Regression, Random Forest, and Gradient Boosting.
- Reports MAE, RMSE, and R² on train and test splits.
- Uses 5-fold cross-validation and inspects Linear Regression coefficients.
- Refits the selected model on all available rows and exports it with `joblib`.

## Tech stack

- Python
- pandas, NumPy
- Matplotlib
- scikit-learn
- joblib
- Jupyter Notebook

## Getting started

### 1. Clone the repository

```bash
git clone https://github.com/SirShadmehr/student-performance-prediction.git
cd student-performance-prediction
```

### 2. Create and activate a virtual environment

**Windows PowerShell**

```powershell
py -m venv .venv
.\.venv\Scripts\Activate.ps1
```

**macOS / Linux**

```bash
python3 -m venv .venv
source .venv/bin/activate
```

### 3. Install dependencies

```bash
python -m pip install --upgrade pip
pip install -r requirements.txt
```

### 4. Add the dataset

Copy your CSV to:

```text
data/student_performance_dirty.csv
```

### 5. Run the notebook

```bash
jupyter notebook
```

Open `notebooks/student_performance.ipynb` and run the cells from top to bottom.

## Evaluation

The notebook evaluates models using:

| Metric | Meaning |
|---|---|
| MAE | Average absolute prediction error |
| RMSE | Error metric that penalizes larger mistakes more strongly |
| R² | Proportion of target variance explained by the model |

No performance numbers are hard-coded in this README. Run the notebook against the dataset to generate the actual results.

## Process & learnings

The main engineering decision is to keep imputation and categorical encoding inside the
scikit-learn pipeline. This ensures preprocessing is learned from training data only
and is repeated correctly during cross-validation. A simple baseline is included to
check whether more complex estimators add measurable value.

The notebook also demonstrates that model complexity should be justified by validation
results rather than assumed to improve performance.

## Preview / demo

- **Notebook:** `notebooks/student_performance.ipynb`
- **Live demo:** Not deployed yet.
- **Video preview:** Add a short walkthrough link here when available.

## Responsible use

This model estimates patterns in the provided dataset. It is an educational portfolio
project, not a validated tool for grading, admissions, or other high-impact decisions
about students. Predictions should not be used as the sole basis for decisions affecting
individuals.

## License

Choose a license before making the repository reusable by others. If you do not intend
to grant reuse permissions yet, leave this section out or add a license after deciding.
