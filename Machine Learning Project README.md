# Predicting Concrete Compressive Strength

A machine learning regression project that predicts concrete compressive strength from concrete mix composition and curing age.

The project was completed during the Ironhack Data Analytics Bootcamp and focuses on the full supervised machine learning workflow: data cleaning, exploratory data analysis, feature engineering, baseline modeling, ensemble methods, hyperparameter tuning, and final evaluation.

## Business Problem

Concrete compressive strength is normally confirmed through physical testing after a curing period. These tests are reliable, but waiting for final results can slow mixture development and increase the number of laboratory trials required.

This project explores whether machine learning can provide a preliminary strength estimate from the mixture design and curing age.

The model is intended as a decision-support and screening tool, not as a replacement for physical testing.

## Project Objective

Predict concrete compressive strength, measured in megapascals (MPa), using:

- Cement
- Blast furnace slag
- Fly ash
- Water
- Superplasticizer
- Coarse aggregate
- Fine aggregate
- Curing age

## Dataset

The project uses the Concrete Compressive Strength dataset from the UCI Machine Learning Repository.

After cleaning, the modeling dataset contained:

- **1,005 observations**
- **8 original predictors**
- **4 engineered predictors**
- **12 final predictors**
- **1 regression target:** concrete compressive strength in MPa

## Data Preparation

The preparation workflow included:

- Standardizing column names
- Checking data types
- Removing exact duplicate rows
- Confirming that no missing values remained
- Retaining meaningful zero values for ingredients that were not used in some mixtures
- Separating the predictors from the target
- Splitting the data into training and test sets before preprocessing

## Exploratory Data Analysis

Exploratory analysis was used to examine:

- Predictor distributions
- Relationships between ingredients and compressive strength
- Correlations between original and derived predictors
- Potential multicollinearity
- The influence of curing age and mixture proportions

The strongest signals in the final predictor set included:

- Water-to-binder ratio
- Total binder
- Cement
- Curing age

## Feature Engineering

Four domain-informed predictors were created from the original mixture variables:

- `binder_total`  
  Cement + blast furnace slag + fly ash

- `aggregate_total`  
  Coarse aggregate + fine aggregate

- `water_binder_ratio`  
  Water divided by total binder

- `aggregate_binder_ratio`  
  Total aggregate divided by total binder

These features were created only from the original predictors. The target variable was not used during feature engineering.

## Modeling Workflow

The general workflow was:

1. Split the data into training and test sets
2. Fit `MinMaxScaler` using only the training predictors
3. Transform the training and test predictors
4. Train regression models
5. Compare models using mean absolute error and R²
6. Tune selected ensemble models with `GridSearchCV`
7. Evaluate the final selected model on the held-out test set

MinMax scaling was included to follow a consistent preprocessing workflow. The final tree-based ensemble models are generally insensitive to feature scaling.

## Models Evaluated

### Baseline Models

- Linear Regression
- Decision Tree Regressor

The Decision Tree captured nonlinear relationships more effectively than Linear Regression.

### Ensemble Models

- Bagging Regressor
- Pasting
- Random Patches
- Random Forest Regressor
- AdaBoost Regressor
- Gradient Boosting Regressor

Pasting achieved the strongest initial held-out test performance and was selected for tuning alongside Gradient Boosting.

## Hyperparameter Tuning

`GridSearchCV` with five-fold cross-validation was used to tune:

- Pasting
- Gradient Boosting

Gradient Boosting achieved the lower mean cross-validation MAE and was selected as the final model.

## Final Model Performance

The tuned Gradient Boosting model achieved the following results on the held-out test set:

| Metric | Result |
|---|---:|
| Test MAE | **2.66 MPa** |
| Test RMSE | **4.21 MPa** |
| Test R² | **0.941** |

The MAE means that the model's predictions were approximately **2.66 MPa away from the measured strength on average**.

## Feature Importance

The most influential predictors in the final Gradient Boosting model were:

1. Curing age
2. Water-to-binder ratio
3. Cement
4. Total binder

These results indicate that both curing time and the balance between water and cementitious material were important to the model's predictions.

## Repository Structure

```text
Predicting-Concrete-Compressive-Strength-from-Mix-Composition-and-Curing-Age/
│
├── 01_data_cleaning_and_exploration.ipynb
├── 02_feature_engineering_and_model_preparation.ipynb
├── 03_initial_model_development_and_tuning.ipynb
├── 04_advanced_ensemble_modeling_and_final_evaluation.ipynb
│
├── Processed_Data/
│   ├── concrete_cleaned.csv
│   └── concrete_engineered.csv
│
├── Plots/
│   └── project visualizations
│
├── Models/
│   └── saved model files
│
├── src/
│   └── reusable project code
│
├── requirements.txt
├── .gitignore
└── README.md
```

## How to Run the Project

### 1. Clone the repository

```bash
git clone <repository-url>
cd Predicting-Concrete-Compressive-Strength-from-Mix-Composition-and-Curing-Age
```

### 2. Create and activate a virtual environment

```bash
python -m venv .venv
```

Windows:

```bash
.venv\Scripts\activate
```

macOS or Linux:

```bash
source .venv/bin/activate
```

### 3. Install the required packages

```bash
pip install -r requirements.txt
```

### 4. Run the notebooks in order

1. `01_data_cleaning_and_exploration.ipynb`
2. `02_feature_engineering_and_model_preparation.ipynb`
3. `03_initial_model_development_and_tuning.ipynb`
4. `04_advanced_ensemble_modeling_and_final_evaluation.ipynb`

## Evaluation Metrics

### Mean Absolute Error

MAE measures the average absolute difference between the predicted and measured strength values.

Lower values are better, and the result remains in MPa, making it easy to interpret.

### Root Mean Squared Error

RMSE gives more weight to larger prediction errors.

Lower values are better.

### R²

R² measures the proportion of variation in compressive strength captured by the model.

Values closer to 1 indicate stronger predictive performance.

## Limitations

- The dataset contains approximately 1,000 observations, which limits the variety of mixtures available for training.
- The data may not fully represent all real-world production conditions.
- The dataset does not include variables such as temperature, humidity, curing method, admixture chemistry, or production variability.
- The model should not replace required laboratory testing or engineering validation.

## Future Improvements

Future work could include:

- Training on a larger and more varied dataset
- Adding environmental and curing-condition variables
- Comparing additional boosting algorithms
- Testing model performance across concrete strength ranges
- Building a Streamlit interface for preliminary mix screening
- Adding prediction intervals or uncertainty estimates
- Validating the model using external production data

## Key Takeaway

Machine learning can estimate concrete compressive strength with strong predictive performance, but model quality depends on the data, feature design, validation strategy, and tuning process.

The final model is best viewed as a screening and decision-support tool that can help prioritize testing and reduce trial-and-error during mixture development.

## Author

**Kyle Haustein**  
Ironhack Data Analytics Bootcamp  
Machine Learning Regression Project
