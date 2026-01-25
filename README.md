# 🏠 Bloomfield Rental Price Forecasting (NJ)

Predict **monthly apartment rent prices in Bloomfield, New Jersey** using **real listings I personally collected**, cleaned, and modeled with machine learning.

This repository focuses on the **modeling + evaluation + saved artifacts** (deployment-ready).  
Raw scraped data is intentionally not published.

---

## Project Objective

Predict:
- **Estimated monthly rent (USD)**
- **Expected rent range** (uncertainty-aware estimate)

### Inputs
- Bedrooms
- Bathrooms
- Square footage
- Laundry type
- Parking availability
- Bloomfield location zone

---

## Data Collection (Manual, Real Listings)

This dataset was **not downloaded from Kaggle** or a public dataset.

I collected listings manually by:
- browsing real rental platforms,
- capturing listing information (price, size, rooms, amenities, location),
- standardizing and validating entries to reflect **real market conditions**.

### Data Availability
To avoid sharing scraped/raw listing content publicly, the **raw dataset is not included** in this repo.  
This repo includes:
- the notebook,
- evaluation outputs,
- and **trained model artifacts** for reproducibility and demonstration.

---

## Data Cleaning & Preparation

Key steps:
- standardized inconsistent categories (laundry, parking, zones),
- handled missing values responsibly,
- removed unrealistic or invalid records,
- validated ranges (ex: square footage sanity checks).

---

## Feature Engineering (Leakage-Safe)

### Core Features
- `Bedrooms`, `Bathrooms`, `Square_Feet`
- `Laundry_Type`, `Parking`, `Location_Zone`

### Engineered Features
- `Room_Ratio = Bedrooms / (Bathrooms + 0.001)`
- `Size_per_Bedroom = Square_Feet / (Bedrooms + 1)`

### Leakage Prevention
`Price_per_SqFt = Rent_Price_USD / Square_Feet` was **excluded** because it directly uses the target (`Rent_Price_USD`) and would artificially inflate performance.

---

## Model Selection

### Final Model
**RandomForestRegressor (regularized)**

### Why Random Forest?
- captures **non-linear** relationships (zone effects, size interactions),
- handles mixed feature types well after encoding,
- robust for **small/medium real-world datasets**,
- regularization reduces overfitting.

Regularization used:
- max depth limits,
- min samples split/leaf constraints.

---

## Model Evaluation

### Cross-Validation (5-Fold)

| Metric | Result |
|------:|:------|
| MAE | **$247 ± $18** |
| RMSE | **$314 ± $24** |
| R² | **0.750 ± 0.033** |

Interpretation: predictions are typically within **~$250** of true rent.

### Diagnostics
- residuals centered around zero,
- residuals vs predicted show no strong systematic pattern,
- hypothesis tests suggest **no significant prediction bias**.

---

## Project Structure
<img width="607" height="421" alt="image" src="https://github.com/user-attachments/assets/41ac88f1-cf4d-422d-a873-a2caf30c58b4" />


