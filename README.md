# modelStudio

Interactive model explainability demos using [modelStudio](https://modelstudio.drwhy.ai/) — an R package built on [DALEX](https://modelstudio.drwhy.ai/DALEX.html).

![modelStudio](https://github.com/wsamuelw/model-studio/blob/main/image/modelStudio.png)

## Why Model Explainability?

A high-accuracy model is useful. Being able to explain *why* it made a specific prediction is better. modelStudio generates interactive dashboards showing:

- **Break Down plots** — how each feature pushes a prediction up or down
- **Shapley values** — global feature importance across the dataset
- **Ceteris Paribus profiles** — how changing one feature affects the outcome
- **Partial Dependence** — marginal effect of features on predictions

## What's Inside

| # | Script | Model | Task | Dataset |
|---|--------|-------|------|---------|
| 1 | `1, random forest - regression.R` | Random Forest (`ranger`) | Regression | World Happiness |
| 2 | `2, logistic regression - classification.R` | Logistic Regression (`glm`) | Classification | Titanic |
| 3 | `3, XGBoost - regression.R` | XGBoost (`tidymodels`) | Regression | `mpg` |
| 4 | `4, XGBoost - classification.R` | XGBoost (`tidymodels`) | Classification | Bank Churners |

## Requirements

- R (>= 4.0)
- R packages:

```r
install.packages(c("DALEX", "modelStudio", "ranger", "tidymodels", "tidyverse"))
```

## How to Run

Clone the repo and source any script:

```bash
git clone https://github.com/wsamuelw/model-studio.git
cd model-studio
```

```r
source("1, random forest - regression.R")
```

Each script:
1. Loads or fits a model
2. Creates a DALEX explainer
3. Launches an interactive modelStudio dashboard in your browser

## Datasets

| Dataset | Source | Used In |
|---------|--------|---------|
| World Happiness | [Kaggle](https://www.kaggle.com/unsdsn/world-happiness) | Script 1 |
| Titanic | `DALEX::titanic_imputed` | Script 2 |
| `mpg` | `ggplot2::mpg` (built-in) | Script 3 |
| Bank Churners | `data/bank_churners.csv` (included) | Script 4 |

## Key Concepts

**Explainer** — a DALEX object that wraps your model, data, and predictions into a standardised format. This is what modelStudio uses to generate explanations.

```r
explainer <- DALEX::explain(
  model = my_model,
  data = my_data,
  y = my_data$target,
  label = "My Model"
)
```

**New Observations** — pass specific rows to `modelStudio()` to see per-instance explanations:

```r
modelStudio(explainer, new_observations = my_data[1:3, ])
```

## References

- [modelStudio documentation](https://modelstudio.drwhy.ai/)
- [DALEX: Explainers for Complex Models](https://modelstudio.drwhy.ai/DALEX.html)
- [DrWhy AI](https://modelstudio.drwhy.ai/) — the Explainable AI family of R packages

## License

MIT
