# Titanic Survival Prediction

This project builds a Decision Tree Classifier to predict whether a passenger survived the Titanic disaster using passenger information from the Titanic dataset.

## Project Overview

The goal of this notebook is to use machine learning to predict survival based on selected passenger features. The model uses a decision tree because it is easy to interpret and can show the rules used to make predictions.

## Dataset

The dataset used is `titanic.csv`. The target column is:

- `Survived`: whether the passenger survived
  - `0` = did not survive
  - `1` = survived

## Features Used

The model uses the following features:

- `Pclass` — passenger ticket class
- `Sex` — passenger sex
- `Age` — passenger age
- `SibSp` — number of siblings/spouses aboard
- `Parch` — number of parents/children aboard
- `Fare` — ticket fare
- `Embarked` — port of embarkation

Columns such as `Name`, `Ticket`, `Cabin`, and `PassengerId` were not used because they are either identifiers, text-based, or contain too many missing values.

## Steps Completed

1. Imported the required Python libraries.
2. Loaded and inspected the Titanic dataset.
3. Selected useful survival-related features.
4. Handled missing values:
   - Filled missing `Age` values with the median age.
   - Filled missing `Embarked` values with the most common port.
5. Converted categorical columns into numeric dummy variables.
6. Split the dataset into training and testing sets.
7. Built and trained a Decision Tree Classifier.
8. Evaluated the model using accuracy, classification report, and confusion matrix.
9. Visualized the decision tree and feature importance.
10. Compared training and testing accuracy.

## Model Used

The model used is a Decision Tree Classifier from scikit-learn:

```python
DecisionTreeClassifier(max_depth=4, random_state=42)
```

The maximum depth was limited to reduce overfitting and keep the model easier to interpret.

## Results

The model achieved:

- Training accuracy: approximately 84.1%
- Testing accuracy: approximately 78.8%

This shows that the model performed reasonably well on unseen data, with only slight overfitting.

## Conclusion

The decision tree model was able to predict Titanic survival with reasonable accuracy. It also provided interpretable rules that helped show which features influenced survival predictions.

## Requirements

To run this project, install the following Python libraries:

```bash
pip install pandas numpy matplotlib scikit-learn
```

## How to Run

1. Open `Titanic_Survival.ipynb` in Jupyter Notebook, JupyterLab, or Google Colab.
2. Make sure `titanic.csv` is in the same folder as the notebook.
3. Run the notebook cells from top to bottom.