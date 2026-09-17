# New York Taxi Fare Prediction

A machine-learning project that predicts New York City taxi fares from trip location and time features.

## Project contents

- `NYtaxifareProject.ipynb`: data download, preprocessing, feature engineering, model training, and evaluation.

## Data

The notebook downloads the Kaggle New York City Taxi Fare Prediction dataset with `opendatasets`. A Kaggle account and API credentials may be required.

## Models

- Linear Regression
- XGBoost Regressor

## Feature engineering

The notebook transforms the raw trip records into features that describe when, where, and how far each ride travels:

- **Time features:** `pickup_datetime` is converted into pickup hour, day of week, month, and year. These capture commuting patterns, seasonal demand, and long-term fare changes.
- **Weekend indicator:** `is_weekend` is set to `1` for Saturday and Sunday and `0` for weekdays, allowing the model to learn different weekend travel behavior.
- **Trip distance:** Pickup and dropoff latitude/longitude are converted into `distance_km` using the Haversine formula. This approximates the straight-line distance between the two points and provides a strong signal for fare amount.
- **Airport proximity:** The notebook calculates the distance from each pickup and dropoff point to JFK, LaGuardia, and Newark airports. These distances are used to create `is_airport_trip`, which flags rides starting or ending within two kilometers of an airport.
- **Outlier filtering:** Records with non-positive or unusually high fares are removed, as are trips with zero or implausibly large distances. This reduces the effect of invalid coordinates and extreme records on model training.
- **Unused identifier:** The raw `key` column is removed because it identifies a record rather than describing the trip itself.

Together, these features give the models both continuous signals, such as distance, and categorical or time-based signals, such as weekend and airport-trip indicators.

## Result

The saved local validation result for XGBoost is an RMSE of `3.565`. Kaggle also evaluates this competition with RMSE, where lower is better. This is a local train/test split result, not an official Kaggle leaderboard score, because the notebook does not create or submit predictions for Kaggle's hidden test set.

For comparison, the completed Kaggle leaderboard's visible top-50 cutoff is approximately `2.879`, so this result would fall outside the top 50 if it transferred directly to the competition test set. An exact rank cannot be assigned without an official Kaggle submission.

## Setup

```bash
pip install -r requirements.txt
```

Open `NYtaxifareProject.ipynb` in Jupyter or VS Code and run the cells in order.