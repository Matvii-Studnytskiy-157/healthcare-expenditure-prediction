# Healthcare Expenditure Prediction

## Project Overview

This project investigates the problem of **predicting outpatient healthcare expenditure (`EXPENDOP`)** using demographic and healthcare utilization variables.

Healthcare cost data is typically **highly skewed**, with a small number of patients generating very large expenditures. This project explores whether classical regression techniques can capture the relationship between healthcare usage patterns and outpatient costs.

The analysis follows a structured machine learning workflow including:

* Exploratory Data Analysis (EDA)
* Baseline Linear Regression modeling
* Regularized regression (Ridge)
* Feature transformation experiments
* Feature selection analysis
* Model comparison and interpretation

The goal is not only to build a predictive model but also to **understand the drivers of healthcare expenditures**.

---

## Dataset

The dataset contains **1112 observations** and **28 variables** describing demographic characteristics and healthcare utilization.

For this project, the following predictors were used:

| Variable | Description                      |
| -------- | -------------------------------- |
| AGE      | Age of the individual            |
| famsize  | Family size                      |
| COUNTIP  | Number of inpatient visits       |
| COUNTOP  | Number of outpatient visits      |
| EXPENDIP | Inpatient healthcare expenditure |

Target variable:

```
EXPENDOP
```

Outpatient healthcare expenditure.

Healthcare expenditure variables exhibit **strong right-skewed distributions**, which is typical in medical cost datasets.

---

## Project Structure

```
healthcare-expenditure-prediction/
│
├── healthcare_expenditure_analysis.ipynb
├── HealthExpend.csv
├── README.md
```

The notebook contains the full modeling workflow and analysis.

---

## Exploratory Data Analysis

Key observations from the dataset:

* **COUNTOP** (outpatient visits) shows the strongest correlation with outpatient expenditure.
* **COUNTIP** and **EXPENDIP** also show moderate correlation with the target variable.
* Demographic variables such as **AGE** and **famsize** exhibit relatively weak predictive power.
* Healthcare expenditure variables are **highly right-skewed**, indicating the presence of extreme values.

These insights informed the modeling strategy used in later sections.

---

## Baseline Model: Linear Regression

A baseline Linear Regression model was trained using the selected predictors.

Performance:

| Metric    | Value   |
| --------- | ------- |
| Test RMSE | ≈ 2509  |
| Test R²   | ≈ 0.385 |

The model captures some predictive signal but struggles with extreme expenditure values due to the skewed distribution of healthcare costs.

---

## Ridge Regression

Ridge Regression was evaluated to determine whether **regularization improves model stability**.

The model was trained across a range of regularization strengths (α).

Result:

```
Optimal α ≈ 0.0001
```

This indicates that **regularization has little effect**, and Ridge Regression performs almost identically to the baseline Linear Regression model.

---

## Feature Transformation Experiments

Because several variables exhibit strong skewness, nonlinear transformations were tested.

Transformations evaluated:

```
Original predictors
log1p(X)
1 / (log1p(X) + 1)
```

Best result:

| Transformation | Test RMSE | Test R² |
| -------------- | --------- | ------- |
| log1p(X)       | ≈ 2372    | ≈ 0.451 |

Logarithmic transformation significantly improves model performance by reducing skewness and stabilizing extreme values.

---

## Feature Selection Experiments

Different feature subsets were evaluated to determine whether simpler models could maintain predictive performance.

Results show that **healthcare utilization variables carry most of the predictive signal**.

Key predictors:

```
COUNTIP
COUNTOP
EXPENDIP
```

Demographic variables provide only minor improvements to predictive accuracy.

---

## Best Performing Model

**Linear Regression with log-transformed predictors**

Performance:

```
Test RMSE ≈ 2372
Test R² ≈ 0.451
```

The improvement demonstrates that **handling skewed feature distributions is critical when modeling healthcare expenditures.**

---

## Key Insights

* Healthcare utilization variables are the strongest predictors of outpatient expenditure.
* Demographic variables contribute relatively little additional predictive power.
* Feature distribution shape (skewness) significantly affects model performance.
* Simple preprocessing techniques such as logarithmic transformations can improve regression models.

---

## Future Work

Potential improvements include:

* Incorporating additional predictors related to health conditions or insurance status
* Testing nonlinear models (Random Forest, Gradient Boosting)
* Applying robust regression techniques to handle extreme outliers
* Performing cross-validation for more robust model evaluation

---

## Technologies Used

* Python
* NumPy
* Pandas
* Scikit-learn
* Seaborn
* Matplotlib

---

## Author

**Matvii Studnytskiy**
