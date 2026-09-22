# Seoul Bike Demand Prediction Using Multiple Linear Regression

## Overview

This project develops and evaluates a Multiple Linear Regression model to predict hourly bike rental demand in Seoul using weather, seasonal, temporal, and operational variables.

The analysis includes:

- Data cleaning and preprocessing
- Exploratory Data Analysis (EDA)
- Multiple Linear Regression
- Chronological train-test evaluation
- Statistical significance testing using p-values
- Model diagnostics and interpretation
- Business insights and recommendations

---

## Research Question

> To what extent can weather, time, seasonal, holiday, and operational variables explain hourly bike rental demand in Seoul?

---

## Dataset

The project uses the **Seoul Bike Sharing Demand** dataset from the UCI Machine Learning Repository.

**Dataset Characteristics**

- 8,760 hourly observations
- 13 predictor variables
- No missing values
- Regression problem

### Target Variable

```text
Rented Bike Count
```

### Dataset Source

https://archive.ics.uci.edu/dataset/560/seoul+bike+sharing+demand

---

## Project Structure

```text
seoul-bike-demand-prediction/
│
├── README.md
├── LICENSE
├── requirements.txt
├── .gitignore
│
├── data/
│   ├── raw/
│   └── processed/
│
├── notebooks/
│   └── seoul_bike_regression.ipynb
│
├── reports/
│   ├── seoul_bike_regression_report.docx
│   └── seoul_bike_regression_report.pdf
│
├── figures/
│   ├── demand_distribution.png
│   ├── hourly_demand.png
│   ├── correlation_heatmap.png
│   ├── seasonal_demand.png
│   ├── actual_vs_predicted.png
│   └── residual_plot.png
│
└── results/
    ├── coefficient_results.csv
    └── model_metrics.csv
```

---

## Methodology

The project follows these stages:

1. Data loading and inspection
2. Data cleaning and preprocessing
3. Feature engineering
4. Exploratory Data Analysis
5. Multiple Linear Regression
6. Statistical significance testing
7. Model evaluation
8. Residual diagnostics
9. Business interpretation

For evaluation, the first 80% of observations were used for training and the final 20% were used for testing, preserving the chronological structure of the data.

---

## Exploratory Analysis

### Average Bike Rental Demand by Hour

![Average Bike Rental Demand by Hour](figures changes substantially throughout the day. Demand typically peaks during commuting periods, illustrating the importance of temporal features in demand forecasting.

---

## Model Performance

| Metric | Value |
|----------|----------:|
| Training R² | 0.5535 |
| Testing R² | 0.5511 |
| Adjusted R² | 0.5522 |
| Test MAE | 309.67 |
| Test RMSE | 410.92 |
| F-statistic | 433.11 |
| Model p-value | < 0.001 |
| Durbin-Watson | 0.4923 |

### Interpretation

The model explains approximately **55.1% of the variation** observed in unseen hourly bike demand data.

Training and testing R² values are nearly identical, indicating stable predictive performance without obvious overfitting.

---

## Actual vs Predicted Demand

![Actual vs al_vs_predicted.png

The figure above compares actual bike rental demand against model predictions.

Observations close to the diagonal line indicate accurate predictions, while greater distances indicate larger model errors.

---

## Most Significant Variables

| Variable | Coefficient | P-value |
|----------|----------:|----------:|
| Functioning Day (Yes) | 912.11 | < 0.001 |
| Hour | 27.88 | < 0.001 |
| Rainfall | -58.81 | < 0.001 |
| Winter | -400.19 | < 0.001 |
| Solar Radiation | -83.56 | < 0.001 |
| Humidity | -9.69 | < 0.001 |
| Sunday | -163.73 | < 0.001 |
| Temperature | 19.53 | < 0.001 |
| No Holiday | 114.64 | < 0.001 |

### Key Insights

- Operational hours produce significantly higher demand.
- Demand increases with temperature.
- Rainfall reduces bike rentals.
- Winter shows lower demand than the reference season.
- Demand varies across days of the week.
- Holiday and operational status significantly affect usage patterns.

---

## Key Findings

- The model successfully predicts hourly bike demand using weather and temporal variables.
- Approximately 55% of demand variability is explained by the model.
- Functioning-day status is the strongest predictor.
- Rainfall and humidity negatively impact demand.
- Temperature positively impacts demand.
- The model performs consistently on unseen data.

---

## Limitations

- Residual autocorrelation exists (Durbin-Watson = 0.4923).
- Hourly demand patterns may be nonlinear.
- Some weather variables are correlated.
- External factors such as events and bike availability are not included.
- Model coefficients indicate associations rather than causation.

---

## Future Improvements

Potential future enhancements include:

- Ridge Regression
- Lasso Regression
- Time Series Cross Validation
- Lag Features
- Feature Scaling
- Random Forest Regression
- Gradient Boosting
- XGBoost
- Streamlit Deployment

---

## How to Run

```bash
git clone https://github.com/YOUR-USERNAME/seoul-bike-demand-prediction.git

cd seoul-bike-demand-prediction

python -m venv .venv

python -m pip install -r requirements.txt
```

Open:

```text
notebooks/seoul_bike_regression.ipynb
```

and run all cells.

---

## Technologies Used

- Python
- Pandas
- NumPy
- Matplotlib
- Seaborn
- Scikit-Learn
- Statsmodels
- Jupyter Notebook

---

## Dataset Citation

UCI Machine Learning Repository. (2020).

Seoul Bike Sharing Demand Dataset.

Available at:

https://archive.ics.uci.edu/dataset/560/seoul+bike+sharing+demand

---

## Author

**Mohammad Umar Shaikh Mohd Abdul Sattar**

Graduate Engineer Trainee | Data Science | Machine Learning | AI

---

## License

This project is licensed under the MIT License.

See the LICENSE file for details.