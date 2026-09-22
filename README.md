# House Prices — Ames Housing

Kaggle competition: *House Prices: Advanced Regression Techniques*.

## Problem

Predict `SalePrice` for residential homes in Ames, Iowa using 79 features, including:

- Lot and location details
- Quality ratings
- Year built
- Basement details
- Garage details

The dataset contains 1,460 labeled training rows and 1,459 test rows.

## Models

All tree-based models were compared using identical folds.

| Model | Role |
|---|---|
| `DecisionTreeRegressor` | Baseline; unconstrained and prone to overfitting |
| Pre-pruned decision tree | `max_depth`, `min_samples_leaf`, and `min_samples_split` selected with `GridSearchCV` |
| Post-pruned decision tree | `ccp_alpha` selected by cross-validation over the pruning path |
| `RandomForestRegressor` | `max_features` tested with `{√p, p/3, p/2, p}`; `p` corresponds to bagging |
| `GradientBoostingRegressor` | Learning rate and depth selected with `GridSearchCV`; number of estimators selected using `staged_predict` early stopping |

The target is modeled as `log1p(SalePrice)`:

- Original skew: `1.88`
- Transformed skew: `0.12`
- Predictions are converted back using `expm1`

## Validation

- **Split:** Stratified 80/20 split based on price quartiles.
- **Selection:** Five-fold `KFold` cross-validation using MSE.
- **Leakage control:** All learned transformations are contained within a `Pipeline` and refitted for every training fold.
- **Feature alignment:** Training and test data are never concatenated. `handle_unknown="ignore"` keeps encoded columns aligned.

## Kaggle Score

**MSE:** `91,683,741.376`  
**Approximate RMSE:** `$9,575`

## Reproducing

Create and activate a virtual environment:

```bash
python -m venv .venv
.venv\Scripts\activate
```

Install the dependencies:

```bash
pip install numpy pandas scikit-learn matplotlib seaborn jupyter ipykernel
```

Place the following files in `data/raw/`:

- `train.csv`
- `test.csv`
- `sample_submission.csv`

Then run all cells in `house_prices.ipynb`.

The project uses `RANDOM_SEED = 42` throughout.

## Outputs

- `SUBMISSIONS/submission.csv`
- `experiment_results.csv`
- Plots in `figures/`