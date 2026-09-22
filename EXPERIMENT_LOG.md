# Experiment Log — Ames House Prices

Target modeled as `log1p(SalePrice)`; MSE is therefore in log-price space
(equivalent to Kaggle's RMSLE up to a square root). Hold-out = stratified 80/20
split, `random_state=42`. CV = 5-fold `KFold`, shuffled, same seed.
**Lower is better.** Fill the result columns after running the notebook — the
final cell writes `experiment_results.csv` with exactly these fields.

| # | Experiment | Params | Hold-out MSE | CV MSE ± std | Source |
|---|---|---|---|---|---|
| 1 | Baseline tree | `DecisionTreeRegressor()` defaults | | | — |
| 2 | Post-pruned tree | `ccp_alpha` from CV over the pruning path | | | ISLP Alg. 8.1 |
| 3 | Pre-pruned tree | `max_depth` / `min_samples_leaf` / `min_samples_split` via GridSearchCV | | | Géron Ch. 6 + Ch. 2 |
| 4 | Random Forest | `n_estimators=500`, `max_features` = best m | | | ISLP §8.2.1–8.2.2 |
| 5 | Gradient Boosting | B via early stopping, λ and d via GridSearchCV, `subsample=0.8` | | | ISLP §8.2.3 + Géron Ch. 7 |

## Methodology notes

**Why the pipeline is structured the way it is.** Géron Ch. 2 requires that any
transformer learning a statistic (a median, a mode, a category set) be fit on
training data only. Concatenating train and test before imputing — the
convenient shortcut — leaks test information into training and produces
optimistic validation scores. Here every learned step lives inside a
`Pipeline`/`ColumnTransformer` that `cross_val_score` and `GridSearchCV` refit
on each training fold. Only the structural recoding (NaN → `"None"` / `0` where
the data dictionary says the feature is absent) is applied outside the split,
because it is a fixed lookup rather than an estimate.

**Why pruning is done twice.** Géron Ch. 6 pre-prunes during growth (`max_depth`,
`min_samples_leaf`, ...). ISLP §8.1 argues post-pruning is better, because
stopping early whenever a split fails to reduce RSS is short-sighted — a
seemingly worthless split can be followed by a very good one. Algorithm 8.1 is
implemented literally: grow a large tree, take the exact cost-complexity pruning
path from `cost_complexity_pruning_path`, CV-select α over that path. Both
strategies are run so the comparison is empirical rather than asserted.

**Why `m` is swept.** ISLP §8.2.2 makes `m` the entire distinction between
bagging (m = p) and a random forest (m < p), and the decorrelation argument is
specific: if one predictor is very strong, every bagged tree splits on it first,
the trees end up highly correlated, and averaging correlated quantities barely
reduces variance. Section 8a puts m ∈ {√p, p/3, p/2, p} on identical folds so
that argument is tested, not assumed.

**Why B is selected differently for forests and boosting.** ISLP notes B is not
a critical parameter for bagging/random forests — a large B will not overfit
(check the flattening curve in `figures/rf_n_estimators.png`). Boosting *can*
overfit if B is too large, so B is chosen by CV. Géron Ch. 7 supplies the
mechanism: `staged_predict()` replays the ensemble's predictions after each
successive tree, so one fit yields the whole validation-error curve and `argmin`
gives the optimal B.

**Boosting's three parameters** come from ISLP §8.2.3: B (above), λ (shrinkage —
they suggest 0.01 or 0.001, noting very small λ needs large B), and d
(interaction depth — often d = 1 stumps suffice). The grid tests λ ∈ {0.001,
0.01, 0.05, 0.1} × d ∈ {1, 2, 3, 4} rather than taking the suggestion on faith.
Géron Ch. 7 adds `subsample=0.8` (Stochastic Gradient Boosting).

## Known gaps

- **Metric assumption.** MSE is computed in log space. If the assignment
  requires raw-dollar MSE, drop the `log1p`/`expm1` pair in Sections 5 and 10;
  every number above changes and the model ranking may change with it.
- **No feature engineering.** No derived features (total square footage, house
  age at sale, total bathrooms). Géron Ch. 2 spends real effort on attribute
  combinations; this notebook does none, and that is the most likely source of
  further gains.
- **Outliers untouched.** The two very large `GrLivArea` houses that sold cheap
  are a known quirk of this dataset and are left in.
- **`sample_submission.csv` is reconstructed**, not Kaggle's original — it has
  the right `Id` column and format but placeholder prices, so it is only usable
  as a format check.

## Submission

`submissions/submission.csv` — best model by CV MSE, refit on the full 1460-row
training set, predicting the 1459 test rows, un-logged via `expm1`.
Format-checked against `sample_submission.csv`: matching column names, row
count, `Id` order, no NaNs, all prices positive.
