# Linear Regression Multiple Variables

## Project Overview

This project builds a multivariable linear regression model to predict a Telco customer's monthly charge based on the services they subscribe to.

The main goal is to answer this question:

> Given which add-on services a customer subscribes to, what monthly charge should we expect them to pay?

The model uses the required 10 service indicator variables as predictors and `target` as the monthly charge target variable.

## Dataset

The dataset used in this project is a cleaned/prepared Telco dataset saved locally as:

```text
telco.csv
```

The notebook loads the dataset directly using:

```python
csv_file = "telco.csv"
df = pd.read_csv(csv_file)
```

The original data source is the Telco Customer Churn dataset from Kaggle:

```text
blastchar/telco-customer-churn
```

To reproduce the project locally, place `telco.csv` in the same folder as the notebook before running the cells.

## Target Variable

The target variable is:

```text
target
```

This column represents the customer's monthly charge. It is a continuous numeric variable, so linear regression is appropriate.

## Predictor Variables

The multivariable model uses the following 10 service indicators:

```text
PhoneService
MultipleLines
OnlineSecurity
OnlineBackup
DeviceProtection
TechSupport
StreamingTV
StreamingMovies
InternetService_Fiber optic
InternetService_No
```

Each predictor is encoded as a clean 0/1 indicator.

## Cleaning and Preparation Steps

The notebook performs the following steps:

1. Loads the prepared Telco dataset from `telco.csv`.
2. Inspects the data using `head`, `shape`, `describe`, `info`, and missing-value checks.
3. Confirms that `target` is the monthly charge target variable.
4. Selects the required 10 service indicator predictors.
5. Verifies that the final predictor columns are clean 0/1 indicators with no missing values.

## Model

The main model is a multivariable linear regression model:

```text
MonthlyCharges = intercept + coefficient_1 * service_1 + ... + coefficient_10 * service_10
```

The model is trained using:

```python
LinearRegression()
```

The data is split into training and testing sets using an 80/20 split with `random_state=42`.

## Results

The multivariable model achieved:

```text
R2:   0.9988
MAE:  0.7886
RMSE: 1.0504
```

The single-variable baseline model using only `num_addons` achieved:

```text
R2:   0.7009
MAE:  14.2369
RMSE: 16.4551
```

The multivariable model performs much better than the baseline because it knows exactly which services the customer has, rather than only knowing the number of services.

## Key Findings

- The estimated base monthly plan cost is about **$24.97**.
- `InternetService_Fiber optic` has the highest positive contribution, about **$24.95**.
- `PhoneService` contributes about **$20.04**.
- Streaming services contribute about **$10** each.
- Smaller add-ons such as `OnlineBackup`, `DeviceProtection`, `MultipleLines`, `TechSupport`, and `OnlineSecurity` contribute about **$5** each.
- `InternetService_No` has a negative coefficient because customers with no internet service pay less.
- A customer with phone service, multiple lines, and tech support is predicted to pay about **$55.05** per month.

## Charts Included

The notebook includes three charts:

1. Estimated contribution of each service.
2. Prediction error comparison between the baseline and multivariable model.
3. R2 score comparison between the baseline and multivariable model.

## How to Run

1. Make sure `telco.csv` is in the same folder as the notebook.
2. Open `Linear_Regression_Multiple_Variable.ipynb` in Jupyter Notebook, VS Code, or Google Colab.
3. Install the required libraries listed in `requirements.txt`.
4. Run all cells from top to bottom.

## Required Libraries

```text
numpy
pandas
matplotlib
scikit-learn
```

## Files

```text
Linear_Regression_Multiple_Variable.ipynb
README.md
requirements.txt
telco.csv
```

## Author

Omar Gomaa
