# DATA5321 Bike Share Daily Data

**Authors:** Dan Nguyen, Duy Nguyen
**Course:** DATA5321

## Project Overview

Statistical analysis of bike-sharing daily rental data comparing multiple regression modeling approaches to predict total daily bike rentals (`cnt`). The analysis uses 2011 data for model training and 2012 data as a holdout test set.

## Dataset

**File:** `bike_sharing_daily.csv` — 731 daily observations (2011–2012)

| Variable | Description |
|---|---|
| `cnt` | Total bike rentals (target) |
| `casual` / `registered` | Rentals by user type |
| `temp` / `atemp` | Temperature / feels-like temperature |
| `hum` | Humidity |
| `windspeed` | Wind speed |
| `season` / `mnth` | Season and month |
| `weathersit` | Weather situation (1=clear → 4=heavy rain) |
| `weekday` / `workingday` / `holiday` | Day-of-week indicators |

## Analysis Structure

### Part 1 — EDA & Backward Selection (`part1.pdf`)
1. Exploratory data analysis on continuous and categorical variables
2. Univariate linear models to rank individual predictors
3. Interaction models (`temp×season`, `mnth×weathersit`)
4. Backward selection via `regsubsets()` to find optimal feature subset
5. Holdout evaluation on 2012 data (RMSE & R²)

### Part 2 — Advanced Methods (`final_project.pdf`)
1. Shrinkage & dimensionality reduction comparison:
   - **Lasso** (`glmnet`, α=1): Variable selection with CV-tuned λ
   - **Ridge** (`glmnet`, α=0): Coefficient shrinkage, retains all predictors
   - **PCR**: Principal Component Regression
   - **PLS**: Partial Least Squares
2. **GAM**: Generalized Additive Model with smooth spline terms (`s()`) for continuous predictors
3. Model comparison table across all methods on 2012 test data

## Key Findings

- **GAM** achieves the best generalization to 2012 (highest test R², lowest RMSE), with training R² of 0.89
- **Temperature** and **season/month** are the strongest predictors of daily rentals
- Smooth spline terms in GAM capture non-linear temperature and humidity effects
- Backward selection (Part 1) overfits 2011 training data relative to GAM
- Day-of-week and humidity show relatively weak signal

## Getting Started

### Prerequisites
Install required R packages:
```r
install.packages(c("tidyverse", "leaps", "glmnet", "pls", "gam", "patchwork"))
```

### Run the Analysis

**RStudio:** Open `final_project.Rmd` and click **Knit**

**Command line:**
```bash
Rscript -e "rmarkdown::render('final_project.Rmd')"
```

This produces `final_project.pdf` (or `.html` depending on the YAML output setting).

## Files

| File | Description |
|---|---|
| `final_project.Rmd` | Main analysis document (R Markdown) |
| `bike_sharing_daily.csv` | Raw dataset |
| `final_project.pdf` | Compiled Part 2 output |
| `part1.pdf` | Compiled Part 1 output |
