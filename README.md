# NYC Taxi trip duration

## README

```markdown
# NYC Taxi Trip Duration

A regression model for predicting NYC taxi trip durations.
Built on the [Kaggle NYC Taxi Trip Duration](https://www.kaggle.com/c/nyc-taxi-trip-duration)
competition dataset (~1.45M trips from 2016).

## Results

| Model                                | Test RMSLE |
| ------------------------------------ | ---------- |
| Linear Regression (baseline)         | 0.5394     |
| XGBoost (default + early stopping)   | 0.3302     |
| **XGBoost (tuned + early stopping)** | **0.3240** |

## Methodology

- **64/16/20 train/val/test split** — test set is only used for final evaluation
- **Data quality filtering on the full dataset**: only physically impossible rows
  (trips > 6 hours, speed > 200 km/h)
- **Modeling outlier filter on the train set only** (60s ≤ trip ≤ 9000s,
  1 km/h ≤ speed ≤ 100 km/h) to avoid target leakage
- **Feature engineering**: Haversine distance, cyclic (sin/cos) encoding for time features
- **Target log-transform** (log1p) due to the heavy-tailed distribution
- **Early stopping on the validation set** (NOT on test) during XGBoost training
- **RandomizedSearchCV** for hyperparameter tuning

## File structure

├── 01_eda.ipynb # Exploratory analysis, feature engineering, cleaning
├── 02_modeling.ipynb # Linear regression + XGBoost models
├── data/ # Raw and cleaned data (gitignored)
├── requirement.txt # Python dependencies
└── README.md

## Run the notebooks in order:

01_eda.ipynb — produces data/dataset_clean.csv
02_modeling.ipynb — trains and evaluates the models
```
