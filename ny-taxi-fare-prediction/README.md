# New York Taxi Fare Prediction

A machine-learning project that predicts New York City taxi fares from trip location and time features.

## Project contents

- `NYtaxifareProject.ipynb`: data download, preprocessing, feature engineering, model training, and evaluation.

## Data

The notebook downloads the Kaggle New York City Taxi Fare Prediction dataset with `opendatasets`. A Kaggle account and API credentials may be required.

## Models

- Linear Regression
- XGBoost Regressor

The feature engineering includes trip distance, pickup and dropoff time features, weekend indicators, and proximity to New York-area airports.

## Result

The saved local validation result for XGBoost is an RMSE of `3.565`. Kaggle also evaluates this competition with RMSE, where lower is better. This is a local train/test split result, not an official Kaggle leaderboard score, because the notebook does not create or submit predictions for Kaggle's hidden test set.

For comparison, the completed Kaggle leaderboard's visible top-50 cutoff is approximately `2.879`, so this result would fall outside the top 50 if it transferred directly to the competition test set. An exact rank cannot be assigned without an official Kaggle submission.

## Setup

```bash
pip install -r requirements.txt
```

Open `NYtaxifareProject.ipynb` in Jupyter or VS Code and run the cells in order.