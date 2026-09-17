# NYC Taxi Fare Prediction

Predicting New York City taxi fares using engineered trip features (distance, pickup time, airport proximity) and comparing three regression models: Linear Regression, Random Forest, and XGBoost.

## Overview

This project uses the [NYC Taxi Fare Prediction](https://www.kaggle.com/datasets/dansbecker/new-york-city-taxi-fare-prediction) dataset to predict `fare_amount` from pickup/dropoff coordinates, passenger count, and timestamp. Raw coordinates alone are weak predictors, so most of the work is in feature engineering.

## Features Engineered

| Feature | Description |
|---|---|
| `hour`, `day_of_week`, `month`, `year` | Extracted from `pickup_datetime` |
| `is_weekend` | Binary flag for Saturday/Sunday pickups |
| `distance_km` | Haversine (great-circle) distance between pickup and dropoff |
| `pickup_dist_jfk/lga/ewr` | Distance from pickup point to each NYC airport |
| `dropoff_dist_jfk/lga/ewr` | Distance from dropoff point to each NYC airport |
| `is_airport_trip` | Flag for trips within 2 km of any airport (often flat-rate fares) |

## Data Cleaning

- Removed rows with `fare_amount <= 0` or `> 200` (invalid/outlier fares)
- Removed rows with `distance_km <= 0` or `> 100` (invalid coordinates)
- Dropped non-predictive columns (`key`, raw `pickup_datetime`)

## Models Compared

- **Linear Regression** — baseline
- **Random Forest Regressor**
- **XGBoost Regressor** (tuned: `n_estimators=500`, `max_depth=8`, `learning_rate=0.01`, `subsample=0.9`, `colsample_bytree=0.9`)

Models are evaluated on RMSE, MAE, and R², with a train-vs-test RMSE check to confirm the best model isn't overfitting.

## Setup

```bash
pip install pandas numpy scikit-learn xgboost opendatasets
```

The notebook downloads the dataset automatically via `opendatasets` (requires a Kaggle account — you'll be prompted for your Kaggle username and API key on first run).

## Usage

Run `NYtaxifareProject.ipynb` top to bottom. It will:
1. Download and load the dataset
2. Engineer features
3. Train and compare all three models
4. Report RMSE/MAE/R² for each
5. Check the best model for overfitting
6. Generate `submission.csv` in Kaggle's expected format

## Results

| Model | RMSE |
|---|---|
| Linear Regression | ~4.6 |
| Random Forest | ~3.7 |
| XGBoost (tuned) | ~3.5 |

*(Trained on a ~105k row subset of the full 55M-row dataset.)*

## Tech Stack

- Python, pandas, NumPy
- scikit-learn (Linear Regression, Random Forest, train/test split, metrics)
- XGBoost
