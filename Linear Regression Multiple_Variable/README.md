# Linear Regression Multiple Variables

## Project Overview

This project builds a multivariable linear regression model to predict a Telco customer's monthly charge based on the services they subscribe to.

The main goal is to answer this question:

> Given which add-on services a customer subscribes to, what monthly charge should we expect them to pay?

The model uses the required 10 service indicator variables as predictors and `MonthlyCharges` as the target variable.

## Dataset

The dataset used is the Telco Customer Churn dataset from Kaggle:

**Dataset:** `blastchar/telco-customer-churn`

The notebook downloads the dataset directly using `kagglehub`:

```python
path = kagglehub.dataset_download("blastchar/telco-customer-churn")
```

The original CSV file is:

```text
WA_Fn-UseC_-Telco-Customer-Churn.csv
```

## Target Variable

The target variable is:

```text
MonthlyCharges
```

In the notebook, it is renamed to:

```text
target
```

This is a continuous numeric variable, so linear regression is appropriate.

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

## Cleaning and Encoding Steps

The notebook performs the following cleaning steps:

1. Loads the Telco dataset.
2. Inspects the data using `head`, `shape`, `describe`, `info`, and missing-value checks.
3. Converts service values such as `No internet service` and `No phone service` into `No`.
4. Encodes Yes/No service columns as 1/0.
5. One-hot encodes `InternetService` to create:
   - `InternetService_Fiber optic`
   - `InternetService_No`
6. Renames `MonthlyCharges` to `target`.
7. Verifies that the final model predictors are clean 0/1 columns with no missing values.

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

The notebook includes two charts:

1. Estimated contribution of each service.
2. Actual monthly charge vs. predicted monthly charge.

## How to Run

1. Open the notebook in Google Colab or Jupyter Notebook.
2. Install the required libraries listed in `requirements.txt` if running locally.
3. Run all cells from top to bottom.
4. The notebook will download the dataset, clean it, train the model, evaluate performance, and display results.

## Required Libraries

```text
numpy
pandas
matplotlib
scikit-learn
kagglehub
```

## Files

```text
Linear_Regression_Multiple_Variable.ipynb
README.md
requirements.txt
```

## Author

Omar Gomaa
