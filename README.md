# modelStudio

Comparing model explainability across algorithms — Random Forest, Logistic Regression, and XGBoost — using [modelStudio](https://modelstudio.drwhy.ai/) and [DALEX](https://modelstudio.drwhy.ai/DALEX.html).

![modelStudio](https://github.com/wsamuelw/model-studio/blob/main/image/modelStudio.png)

## Problem

Training a model is the easy part. Explaining *why* it made a specific prediction — and whether that reasoning holds across different algorithms — is where real insight lives. This project builds 4 models across regression and classification tasks, then uses interactive explainability dashboards to compare how each one arrives at its predictions.

## Approach

| # | Script | Model | Task | Dataset |
|---|--------|-------|------|---------|
| 1 | `1, random forest - regression.R` | Random Forest | Regression | World Happiness |
| 2 | `2, logistic regression - classification.R` | Logistic Regression | Classification | Titanic |
| 3 | `3, XGBoost - regression.R` | XGBoost | Regression | `mpg` |
| 4 | `4, XGBoost - classification.R` | XGBoost | Classification | Bank Churners |

Each script follows the same flow: fit model → create DALEX explainer → launch interactive dashboard. The consistency makes it easy to compare how different algorithms explain the same type of problem.

## What the Dashboards Show

- **Break Down** — feature contributions to individual predictions (local explainability)
- **Shapley Values** — global feature importance (which features matter most overall)
- **Ceteris Paribus** — how changing one feature affects the outcome (what-if analysis)
- **Partial Dependence** — marginal effect of each feature across the dataset

## Key Findings

- **Random Forest** distributes importance more evenly across features — no single feature dominates
- **XGBoost** concentrates importance in fewer features — more aggressive feature selection
- **Logistic Regression** provides coefficient-based explanations — easy to interpret but less flexible with non-linear relationships

## Setup

```bash
git clone https://github.com/wsamuelw/model-studio.git
cd model-studio
```

```r
install.packages(c("DALEX", "modelStudio", "ranger", "tidymodels", "tidyverse"))
source("1, random forest - regression.R")
```

Each script launches an interactive dashboard in your browser.

## Data

| Dataset | Source | Records | Task |
|---------|--------|---------|------|
| World Happiness | [Kaggle](https://www.kaggle.com/unsdsn/world-happiness) | 150+ countries | Predict happiness score |
| Titanic | `DALEX::titanic_imputed` | 2,207 | Predict survival |
| `mpg` | `ggplot2::mpg` (built-in) | 234 | Predict highway fuel economy |
| Bank Churners | `data/bank_churners.csv` (included) | 10,127 | Predict customer churn |

## Tech Stack

- **DALEX** — model-agnostic explainability framework
- **modelStudio** — interactive explainability dashboards
- **ranger** — fast Random Forest implementation
- **tidymodels** — unified modelling framework (used for XGBoost)
- **tidyverse** — data wrangling and visualisation

## Key Concepts

**Explainer** — wraps any model into a standardised format for explainability:

```r
explainer <- DALEX::explain(
  model = my_model,
  data = my_data,
  y = my_data$target,
  label = "My Model"
)
```

**Per-instance explanations** — pass specific observations to see how the model reasons about individual cases:

```r
modelStudio(explainer, new_observations = my_data[1:3, ])
```

## References

- [modelStudio documentation](https://modelstudio.drwhy.ai/)
- [DALEX: Explainers for Complex Models](https://modelstudio.drwhy.ai/DALEX.html)
- [DrWhy AI](https://modelstudio.drwhy.ai/) — the Explainable AI family of R packages

## License

MIT
