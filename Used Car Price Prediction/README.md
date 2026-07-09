# Used Car Price Prediction

## Project Overview

This project builds a machine learning regression model to predict the fair market price of used cars for WheelsBazaar, an online used-car marketplace. The goal is to help identify reasonable car prices based on vehicle attributes such as make, model, age, kilometers driven, fuel type, transmission, ownership history, engine specifications, and physical dimensions.

## Business Problem

WheelsBazaar currently relies on sellers to set their own prices and uses manual review to identify listings that appear overpriced or underpriced. This process does not scale well as the marketplace grows. An automated price prediction model can help:

- Reduce overpriced listings that remain unsold for too long
- Reduce underpriced listings that cause sellers to lose money
- Support pricing review for a larger number of listings
- Provide a first-pass estimate for future instant-buy pricing decisions

## Dataset

The dataset used is `car details v4.csv`.

It contains used-car listing information, including:

- Make and model
- Price
- Year
- Kilometers driven
- Fuel type
- Transmission
- Location
- Ownership history
- Seller type
- Engine, power, and torque specifications
- Vehicle dimensions and seating capacity

The target variable is:

```text
Price
```

## Model Used

This notebook uses a **Linear Regression** model.

Linear Regression was selected because the assignment requires building a machine learning model to predict a continuous numeric value: used-car price. It is also simple, interpretable, and appropriate as a baseline regression model.

To improve the model, the target variable was log-transformed before training. This helped handle the skewed price distribution and reduced unrealistic prediction behavior caused by very expensive outlier cars.

## Main Steps

1. Loaded the dataset
2. Inspected column types, summary statistics, and missing values
3. Checked numeric columns for invalid zero or negative values
4. Extracted useful numeric values from text columns such as engine size, power, and torque
5. Selected relevant features for price prediction
6. Filled missing numeric values using the median
7. Filled missing categorical values using the most frequent value
8. One-hot encoded categorical variables
9. Split the data into training and testing sets
10. Trained a Linear Regression model
11. Evaluated the model using MAE, RMSE, and R²
12. Compared actual prices against predicted prices using a scatter plot

## Results

The final log-transformed Linear Regression model achieved:

```text
Mean Absolute Error: 413,967.97
Root Mean Squared Error: 903,435.17
R² Score: 0.883
```

The R² score shows that the model explains about 88.3% of the variation in used-car prices. This means the model performs strongly overall, especially for lower and mid-range vehicles. However, predictions are less reliable for very expensive cars, where prices vary more widely.

## Conclusion

The model provides a strong first-pass estimate of used-car prices and can help WheelsBazaar reduce the amount of manual pricing review required. However, because only part of the predictions fall within a strict pricing tolerance, the model should be used as a decision-support tool rather than a fully automated pricing system. Human review would still be useful for high-value cars and listings where the prediction differs significantly from the seller's asking price.

## Files

```text
Used_Car_Price_Prediction.ipynb
car details v4.csv
README.md
```

## Requirements

The notebook uses the following Python libraries:

```text
pandas
numpy
matplotlib
scikit-learn
```

## How to Run

1. Open `Used_Car_Price_Prediction.ipynb`
2. Make sure `car details v4.csv` is in the same folder
3. Run the notebook cells from top to bottom
4. Review the model evaluation results and actual vs predicted price graph
