# Bloomfield Rental Price Forecasting (NJ)

Predict monthly rent prices for apartments in **Bloomfield, New Jersey** using real listing data I collected manually (from rental platforms) and structured into a clean dataset.

## Project Goal
Given a new apartment listing (bedrooms, bathrooms, square feet, laundry type, location zone, parking), the model predicts:
- **Estimated Rent (USD)**
- **Expected range** (based on cross-validation error)

## Dataset (How I collected it)
I manually collected listings and extracted key attributes:
- Bedrooms, Bathrooms
- Square feet
- Laundry type (In-unit / On-site / Not available)
- Parking type (Included / Premium / Standard / Not available)
- Bloomfield zone (North_North, North_South, South_West, South_East)

Then I cleaned:
- typos / inconsistent category values
- missing values handling
- consistent zone naming

✅ Final cleaned file used for modeling:
`data/bloomfield_rent_clean.csv`

## Features Used (No Leakage)
Main features:
- Bedrooms
- Bathrooms
- Square_Feet
- Laundry_Type
- Location_Zone
- Parking

Engineered features:
- Room_Ratio = Bedrooms / (Bathrooms + 0.001)
- Size_per_Bedroom = Square_Feet / (Bedrooms + 1)

 **Leakage Warning**
`Price_per_SqFt = Rent_Price_USD / Square_Feet` is NOT used because it directly contains the target (Rent_Price_USD).  
That would inflate performance and break real-world prediction.

## Model
Best model selected based on validation performance:
**RandomForestRegressor (regularized)**

Why Random Forest?
- handles non-linear relationships well (rent vs sqft, zone effects, etc.)
- works great with mixed numeric + categorical data
- robust on small datasets

## Performance (Cross-Validation)
5-Fold CV (cost-based):
- **MAE ≈ $247 ± $18**
- **RMSE ≈ $314 ± $24**
- **R² ≈ 0.750 ± 0.033**

## Repository Structure

Bloomfield-Rental-Price-Forecasting 2/
│
├── data/
│   ├── bloomfield_rent_clean.csv
│   └── (raw files if you want)
│
├── Notebooks/
│   ├── Bloomfield_Rental_Price_Forecasting_GithubReady.ipynb
│   └── artifacts/
│       ├── random_forest_pipeline.joblib
│       ├── metrics_summary.json
│       ├── feature_schema.json
│       └── feature_cols.json
│
├── Outputs/
│   └── results/
│       ├── model_comparison.csv
│       └── final_predictions_sample.csv
│
├── README.md
├── requirements.txt
└── .gitignore


## How to Run the Project Locally

1. Clone the repository:
```bash
git clone https://github.com/your-username/Bloomfield-Rental-Price-Forecasting.git
cd Bloomfield-Rental-Price-Forecasting