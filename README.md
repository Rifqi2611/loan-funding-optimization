#  Optimizing Bank Profit Using Random Forest & Bayesian Optimization

## 📌 Project Overview

This project aims to optimize the allocation of **credit (Kredit)** by segment and **funding (DPK)** by product to **maximize profit (Laba)** using a combination of:
- Regression Analysis
- Random Forest Modeling
- Bayesian Optimization (Gaussian Process)

By simulating proportional scenarios under realistic constraints, this analysis identifies the most profitable segment mix.

---

## Tools & Libraries

- Python
- Pandas, NumPy
- Scikit-learn (Random Forest)
- Statsmodels (Regression Analysis)
- Scikit-optimize (`skopt`) for Bayesian Optimization
- Matplotlib (for visualization)

---

##  Data Preprocessing

- Loaded data from Excel (Kredit, DPK, and Profit data).
- Engineered proportion variables:
  - `giro_pct`, `tabungan_pct`, `deposito_pct`
  - `konsumer_pct`, `ritel_pct`, `komersial_pct`, `korporasi_pct`, `umkm_pct`, `internasional_pct`, `kpr_kkb_pct`
- Normalized values to ensure the sum of proportions ≈ 100% for Kredit and DPK groups.

---

##  Regression Analysis

- Performed **Ordinary Least Squares (OLS)** regression to understand the linear impact of each segment on `laba`.
- Analyzed:
  - Coefficients and statistical significance (p-values).
- This step provided insights into which variables to prioritize or constrain during optimization.

---

##  Random Forest Modeling

- Trained a **Random Forest Regressor** to predict `laba` using proportion features.
- Reason:
  - Captures non-linear relationships and interaction effects.
  - Robust to overfitting due to ensembling.
- Used this model as the foundation for prediction during the optimization phase.

---

## Bayesian Optimization

- Defined a **search space** for each variable using `skopt.space.Real`.
- Implemented an **objective function** that:
  - Uses the trained Random Forest to predict profit.
  - Returns a high penalty (`1e5`) if the sum of proportions violates business constraints (≠ 100%).
- Ran `gp_minimize` for a specified number of iterations (e.g., 50) to:
  - Explore combinations efficiently.
  - Converge on the most profitable mix.

---

## Results

| Segment/Product         | Optimal Proportion |
|-------------------------|--------------------|
| `giro_pct`              | *e.g. 0.18*        |
| `tabungan_pct`          | *e.g. 0.35*        |
| `deposito_pct`          | *e.g. 0.47*        |
| `konsumer_pct`          | *e.g. 0.28*        |
| `ritel_pct`             | *e.g. 0.12*        |
| `komersial_pct`         | *e.g. 0.15*        |
| `korporasi_pct`         | *e.g. 0.19*        |
| `umkm_pct`              | *e.g. 0.07*        |
| `internasional_pct`     | *e.g. 0.03*        |
| `kpr_kkb_pct`           | *e.g. 0.08*        |
| **Predicted Profit**    | **e.g. 3,260**     |

---

## Insight & Recommendation

- The analysis suggests that decreasing proportions in certain segments (e.g., `korporasi_pct`, `komersial_pct`, `komersial_pct`) leads to higher profit, while others may reduce it.
- These insights can help shape **portfolio strategy** at a bank-wide level.

---

## Outcome

- Optimized Kredit & DPK allocation mix.
- Predicted profit from best configuration.
- Analytical foundation for simulation-based profit planning.

---

