# Household Energy Forecasting with LSTM

This Google Colab project builds an LSTM-based forecasting pipeline that uses the previous 7 days of hourly household electricity data to predict the next 24 hours of `Global_active_power`.

## Dataset

The project uses the **Individual Household Electric Power Consumption** dataset from the UCI Machine Learning Repository.

Dataset page:  
https://archive.ics.uci.edu/dataset/235/individual+household+electric+power+consumption

The dataset contains approximately 2 million minute-level measurements collected from one household between December 2006 and November 2010.

The raw data file should be named:

```text
household_power_consumption.txt
```

The dataset is not included in this repository because of its size.

## Project Workflow

The notebook performs the following steps:

1. Loads and inspects the raw minute-level data.
2. Combines the date and time columns into a chronological `DatetimeIndex`.
3. Analyzes the approximately 1.25% missing sensor readings.
4. Resamples the data into hourly means.
5. Handles short gaps with time interpolation and longer gaps with training-set hour-of-week medians.
6. Splits the data chronologically into training, validation, and final six-month test sets.
7. Adds cyclical hour-of-day and day-of-week features.
8. Applies a `log1p` transformation to skewed non-negative power variables.
9. Fits MinMax scaling using the training set only.
10. Creates 168-hour input sequences and 24-hour prediction targets.
11. Trains a stacked LSTM using Huber loss, dropout, early stopping, and learning-rate reduction.
12. Evaluates forecasting accuracy, inference latency, and residual-based anomaly alerts.

## Model

The model receives input shaped as:

```text
(samples, 168 hours, 11 features)
```

It directly predicts:

```text
(samples, 24 future hours)
```

Architecture:

- LSTM with 128 units and sequence output
- Dropout
- LSTM with 64 units
- Dropout
- Dense layer with 64 ReLU units
- Dense output layer with 24 values

## Results

The final held-out test results were:

| Metric | Result |
|---|---:|
| MAE | 0.3916 kW |
| RMSE | 0.5623 kW |
| MAPE | 53.30% |
| Median inference latency | 69.66 ms |
| Mean inference latency | 79.24 ms |
| Estimated anomaly alert rate | 0.16% |

The model met the deployment latency requirement and the anomaly-alert-rate requirement.

MAPE remained high because many observations occur during low-consumption periods. A modest absolute error can become a large percentage error when the actual value is small. Individual appliance use also creates irregular spikes that are difficult to predict from historical power readings alone.

## Anomaly Alerting

Anomalies are detected using forecast residuals:

```text
residual = actual consumption - predicted consumption
```

The threshold is calculated from validation residuals using the mean plus or minus 3 standard deviations. An alert is raised only after the threshold is exceeded for at least 2 consecutive hours.

Because the dataset does not provide labeled anomaly ground truth, the percentage of flagged test hours is treated as an empirical false-alarm-rate estimate.

## Run in Google Colab

1. Download the notebook file from this repository.
2. Download `household_power_consumption.txt` from the UCI dataset page.
3. Open [Google Colab](https://colab.research.google.com/).
4. Select **File → Upload notebook** and upload `household_energy_forecasting.ipynb`.
5. Select **Runtime → Change runtime type**.
6. Set **Hardware accelerator** to **GPU**, then save.
7. In the Colab file panel, click **Upload to session storage** and upload `household_power_consumption.txt`.
8. Confirm that the data file appears in the same Colab working directory as the notebook.
9. Run the notebook from top to bottom using **Runtime → Run all**.

No local Python installation or `requirements.txt` file is needed. Google Colab already provides the required libraries, including TensorFlow, NumPy, pandas, Matplotlib, and scikit-learn.

## Important Colab Note

Files uploaded directly to Colab session storage are temporary. If the runtime disconnects or restarts, upload `household_power_consumption.txt` again before rerunning the notebook.

The notebook itself should be saved to Google Drive or downloaded after changes so progress is not lost.

## Files

```text
household_energy_forecasting.ipynb
README.md
household_power_consumption.txt   # downloaded and uploaded separately
```
