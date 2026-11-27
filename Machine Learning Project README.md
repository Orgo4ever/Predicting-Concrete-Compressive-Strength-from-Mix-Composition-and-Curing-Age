# Predicting Concrete Compressive Strength

Materials teams need preliminary strength estimates to prioritize candidate mix compositions and curing schedules before physical testing. I developed a regression model using the UCI Concrete Compressive Strength dataset.

## Results

The cleaned dataset contained 1,005 observations, eight original predictors and four engineered predictors. The tuned Gradient Boosting model achieved the following held-out test results:

| Metric | Result |
|---|---:|
| MAE | 2.66 MPa |
| RMSE | 4.21 MPa |
| R² | 0.941 |

Curing age, water-to-binder ratio, cement and total binder were the most influential predictors in the final model.

**Recommendation:** Use preliminary estimates to prioritize mixes for experimentation, not to approve structural materials or replace required laboratory tests.

## Approach

I prepared the dataset, explored relationships, engineered composition-based features, compared baseline and ensemble regression models, and used cross-validation and hyperparameter tuning before evaluating the selected model on held-out data.

The notebooks contain the analysis and modeling workflow. Install the dependencies from `requirements.txt` to reproduce them.

## Limitations

The dataset is relatively small and does not capture temperature, humidity, curing methods, admixture chemistry or production variability. The model requires further validation before application to new production conditions.
