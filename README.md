#  Bloomfield Rental Price Forecasting (NJ)

This project predicts **monthly apartment rental prices in Bloomfield, New Jersey** using **real listings that I personally collected**, transformed into a clean dataset, and modeled with machine learning.

The project follows a **real-world, end-to-end data science workflow**, from raw data collection to deployment-ready artifacts.

---

## 1️ Project Objective

The goal of this project is to predict:

- **Estimated monthly rent (USD)**
- **Expected rent range**, based on model uncertainty

### Inputs Used for Prediction
- Bedrooms
- Bathrooms
- Square footage
- Laundry type
- Parking availability
- Bloomfield location zone

---

## 2️ Data Source & Collection Strategy

 **Important clarification**

The dataset used in this project was **not downloaded from Kaggle or any public dataset**.

### Manual Data Collection
I collected the data myself by:
- browsing real rental platforms,
- taking **screenshots of apartment listings**,
- identifying key attributes such as:
  - price,
  - square footage,
  - number of rooms,
  - amenities,
  - and location information.

This approach ensures the data reflects **real market conditions**.

---

## 3️ Data Extraction Automation (Separate Project)

To make data collection scalable, I built a **separate AI-based chatbot** that:

- takes screenshots or photos of rental listings as input,
- extracts structured information using OCR and text processing,
- converts the extracted information into **Excel / CSV files**.

 This OCR and image-to-table extraction system is implemented in a **separate repository** dedicated exclusively to data ingestion.

**This repository focuses on modeling and prediction only**, while data extraction happens upstream.

---

## 4️ Data Cleaning & Preparation

Once extracted, the data was cleaned by:
- correcting typos and inconsistent category values,
- standardizing laundry, parking, and location zone names,
- handling missing values,
- removing invalid or unrealistic records.

 **Final cleaned dataset used for modeling:**

---

## 5️ Feature Engineering (Leakage-Safe)

### Core Features
- Bedrooms  
- Bathrooms  
- Square_Feet  
- Laundry_Type  
- Parking  
- Location_Zone  

### Engineered Features
- `Room_Ratio = Bedrooms / (Bathrooms + 0.001)`
- `Size_per_Bedroom = Square_Feet / (Bedrooms + 1)`

###  Data Leakage Prevention
The feature  
`Price_per_SqFt = Rent_Price_USD / Square_Feet`  
was **intentionally excluded**, because it directly contains the target variable and would inflate performance artificially.

---

## 6️ Model Selection

### Final Model
**RandomForestRegressor (regularized)**

### Why Random Forest?
- Captures **non-linear relationships** (rent vs size, zone effects)
- Works well with **mixed numeric and categorical data**
- Robust on **small to medium real-world datasets**
- Less sensitive to outliers than linear models

Regularization was applied using:
- limited tree depth,
- minimum samples per split,
- minimum samples per leaf.

---

## 7️ Model Evaluation & Validation

### Cross-Validation (5-Fold, Cost-Based)

| Metric | Result |
|------|------|
| MAE | **$247 ± $18** |
| RMSE | **$314 ± $24** |
| R² | **0.750 ± 0.033** |

 Interpretation:  
On average, predictions are within **approximately $250** of the true rent.

### Residual Diagnostics
- residual distributions are centered around zero,
- residuals vs predictions show no systematic pattern,
- statistical hypothesis testing confirms **no significant prediction bias**.

This indicates the model generalizes well.

---

## 8️ Model Deployment (Separate Project)

A second chatbot-style application was built for **deployment purposes**.

That deployment project:
- loads the trained model and preprocessing pipeline,
- validates user inputs (realistic ranges),
- returns:
  - predicted rent,
  - confidence intervals,
  - and user-friendly explanations.

 Deployment is handled in a **separate repository**, keeping this project focused on analysis and modeling.

---

## 9️ Project Structure

<img width="774" height="464" alt="image" src="https://github.com/user-attachments/assets/5a6eaf86-725a-4d75-92ed-2492f7c4242e" />

---

### Limitations

- Model does not capture seasonal rental dynamics
- Limited data volume (~500 listings)
- Potential bias from scraped listings
- Parking and laundry encoded as categorical proxies

## 10 How to Run the Project Locally

```bash
### step 1  Clone the repository

git clone https://github.com/your-username/Bloomfield-Rental-Price-Forecasting.git
cd Bloomfield-Rental-Price-Forecasting



