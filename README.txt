# XGBoost Hail Probability Models

Pre-trained XGBoost models that predict hail probability from ERA5-derived
environmental predictors.

## Input data

Predictors must be provided as a 4D array `preds_4d` with shape
`[variable, time, lat, lon]`. The variables **must be in this order**:

1. `CAPEmax`
2. `VS03`
3. `FLH`
4. `CINmax`
5. `VS06`
6. `DewT`
7. `RH850`

To extract these predictors from ERA5, see
[XGBoost_hail_proxy_extraction](https://github.com/borusseee/XGBoost_hail_proxy_extraction/tree/main).

## Making predictions

```python
import numpy as np
import xgboost as xgb

# Load the trained model
model = xgb.Booster()
model.load_model("path/to/model.json")  # <- replace with your model file

# Flatten [variable, time, lat, lon] -> [samples, variable]
n_var, n_time, n_lat, n_lon = preds_4d.shape
preds_2d = preds_4d.reshape(n_var, -1).T

# Predict
dmatrix = xgb.DMatrix(preds_2d)
probs = model.predict(dmatrix)

# Restore the spatial and temporal dimensions
probs = probs.reshape(n_time, n_lat, n_lon)
```

## Output

`probs` has shape `[time, lat, lon]` and contains hail probability
values between 0 and 1.