# Documentation of Academic Assistance and Work (DAAW)

**Name:** CDT Zander Bos, C2, Class of 2029
**Course / Section:** MA289A,
**Instructor:** Major Kuiper
**Assignment:** Kaggle House Prices — Ames Housing regression project
**Date Submitted:** 22 September 2026

---

## Sources of Assistance

### 1. Claude (Anthropic), large language model — extensive

Used across multiple sessions for code generation, explanation, and debugging.
Specifically:

**Code authorship.** Claude wrote the substantial majority of
`house_prices.ipynb`, including the preprocessing pipeline
(`structural_recode`, `NeighborhoodMedianImputer`, `OrdinalMapper`,
`ColumnTransformer` configuration), the ordinal encoding maps, all model-fitting
and hyperparameter-search cells, the plotting code, and the submission
generation and format checks. I specified the ten-section project structure and
the required outputs; Claude produced the implementation.

**Methodology.** Claude read the two reference texts (below), extracted the
relevant guidance, and selected the methods applied — cost-complexity pruning
per ISLP Algorithm 8.1, the `max_features` sweep contrasting bagging and random
forests, `staged_predict` early stopping, stratified splitting, and the
pipeline-based leakage discipline. It also identified and corrected a data
leakage error in an earlier version of the code that had imputed on a
concatenated train/test frame.

**Explanation.** I asked Claude to explain concepts I did not initially
understand, including one-hot versus ordinal encoding, LOOCV and why k = 5 is
preferred, the meaning of `TA` in the quality scales, the behavior of
`missingness_report`, and the rationale behind several code blocks. These
explanations informed my understanding but are not reproduced in the submitted
work except where noted below.

**Written text.** Several markdown cells in the notebook are Claude's prose.
Passages I retained verbatim are marked inline with `- CLAUDE` or a similar
attribution tag. The Section 8 overview of ensemble methods is labeled as
Claude's summary of the textbook material. The README was also drafted by
Claude.

**Troubleshooting.** Claude diagnosed a stalled virtual environment creation in
VS Code.

### 2. Aurélien Géron, *Hands-On Machine Learning with Scikit-Learn and TensorFlow* — reference text

Chapters 2 (End-to-End ML Project), 6 (Decision Trees), and 7 (Ensemble
Learning and Random Forests). Source of the pipeline/`ColumnTransformer`
pattern, the fit-on-training-data-only discipline, stratified sampling,
`GridSearchCV` over manual loops, regularization parameters, shrinkage, and
`staged_predict` early stopping. Accessed as a PDF and read by Claude at my
direction.

### 3. Gareth James et al., *An Introduction to Statistical Learning with Python* (ISLP) — reference text

Chapters 5 (Resampling Methods) and 8 (Tree-Based Methods). Source of
Algorithm 8.1 (cost-complexity pruning), the bagging/random forest
decorrelation argument, the three boosting tuning parameters, and the k = 5
or 10 cross-validation guidance. Accessed as a PDF and read by Claude at my
direction.

### 4. Dataset

Kaggle *House Prices: Advanced Regression Techniques* (Ames, Iowa housing data,
compiled by Dean De Cock). `train.csv` and `test.csv` are the standard
competition files.

### 5. Software libraries

NumPy, pandas, scikit-learn, matplotlib, seaborn.

---

## Statement

I have documented all assistance received on this project. The code and written
analysis in this submission were produced with substantial assistance from
Claude as described above; I directed the project structure, made the final
decisions on what to retain, and verified the results by executing the notebook
and submitting to Kaggle.
Link: https://claude.ai/share/7a7dd843-79bb-48d3-bcb6-89e25a183738