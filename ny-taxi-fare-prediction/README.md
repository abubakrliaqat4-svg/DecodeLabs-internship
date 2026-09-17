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

## Setup

```bash
pip install -r requirements.txt
```

Open `NYtaxifareProject.ipynb` in Jupyter or VS Code and run the cells in order.