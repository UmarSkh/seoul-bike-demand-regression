# Seoul Bike Demand Prediction Using Multiple Linear Regression

## Project Overview

This project develops and evaluates a multiple linear regression model for predicting hourly bicycle rental demand in Seoul.

The analysis examines how rental demand is associated with time, weather, season, holiday status, day of the week, and whether the bike-sharing system was functioning.

The project includes:

- Data cleaning and preprocessing
- Exploratory data analysis
- Multiple linear regression
- Chronological train-test evaluation
- Statistical significance testing using p-values
- Coefficient and confidence-interval interpretation
- Regression diagnostics
- A complete written report

---

## Research Question

> To what extent can weather, time, seasonal, holiday, and operational variables explain hourly bike rental demand in Seoul?

---

## Dataset

The project uses the **Seoul Bike Sharing Demand** dataset from the UCI Machine Learning Repository.

The dataset contains **8,760 hourly observations** with information about:

- Rented bike count
- Hour of the day
- Temperature
- Humidity
- Wind speed
- Visibility
- Dew-point temperature
- Solar radiation
- Rainfall
- Snowfall
- Season
- Holiday status
- Functioning-day status

### Target Variable

The regression target is:

```text
Rented Bike Count
```

### Dataset Source

UCI Machine Learning Repository:

https://archive.ics.uci.edu/dataset/560/seoul+bike+sharing+demand

---

## Project Structure

```text
seoul-bike-demand-regression/
│
├── README.md
├── LICENSE
├── requirements.txt
├── .gitignore
│
├── data/
│   ├── raw/
│   │   └── SeoulBikeData.csv
│   └── processed/
│       ├── seoul_bike_analysis.csv
│       └── seoul_bike_cleaned.csv
│
├── notebooks/
│   └── seoul_bike_regression.ipynb
│
├── reports/
│   └── seoul_bike_regression_report.docx
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

The project follows these main steps:

1. Load and inspect the original dataset.
2. Standardize column names.
3. Convert the date variable to a datetime format.
4. Check missing values, duplicates, and invalid values.
5. Extract day-of-week information.
6. Encode categorical variables using dummy variables.
7. Sort observations by date and hour.
8. Divide the dataset chronologically into training and testing sets.
9. Train a multiple linear regression model.
10. Evaluate predictive performance using R-squared, MAE, and RMSE.
11. Fit an Ordinary Least Squares model to obtain coefficients, p-values, and confidence intervals.
12. Examine residual behavior and regression limitations.

### Why a Chronological Split Was Used

The dataset contains hourly observations ordered over time. A random train-test split could place nearby observations in both sets and produce an overly optimistic performance estimate.

The first 80% of the observations were therefore used for training, while the final 20% were used for testing.

---

## Model Performance

| Metric | Result |
|---|---:|
| Training observations | 7,008 |
| Testing observations | 1,752 |
| Training R-squared | 0.5535 |
| Testing R-squared | 0.5511 |
| Adjusted R-squared | 0.5522 |
| Test MAE | 309.67 |
| Test RMSE | 410.92 |
| F-statistic | 433.1127 |
| Overall model p-value | < 0.001 |
| Durbin-Watson statistic | 0.4923 |

The test R-squared of **0.5511** indicates that approximately **55.1% of the variation in bike rental demand in the chronological test period was explained by the predictors included in the model**.

The difference between training and test R-squared was only approximately 0.0024. This indicates stable performance on the later test observations and provides no obvious evidence of conventional overfitting.

The test MAE of 309.67 means that the predictions differed from the actual hourly rental counts by approximately 310 bikes on average, without considering the direction of the error.

---

## Exploratory Data Analysis

### Distribution of Bike Rental Demand

figures/demand_distribution.png

The rented-bike-count distribution is right-skewed. Lower and moderate demand levels occur more frequently than very high rental counts.

---

### Average Demand by Hour

![Average bike rental demand by hour](figures changes substantially throughout the day. The hourly pattern indicates that demand cannot be fully explained by weather variables alone.

A single linear hour coefficient provides a simplified representation of this pattern. Future versions could model hour as a categorical or cyclical variable.

---

### Correlation Matrix

figures/correlation_heatmap.png

The correlation matrix shows the pairwise relationships among numerical variables. Temperature, humidity, dew-point temperature, and solar radiation contain related weather information.

Correlation does not establish causation and does not account for the effects of other predictors included in the regression model.

---

### Seasonal Demand

figures/seasonal_demand.png

Bike rental demand varies across seasons. The fitted model found statistically significant differences for winter, spring, and summer relative to the omitted reference season.

---

## Regression Results

### Selected Statistically Significant Variables

| Variable | Coefficient | P-value | Interpretation |
|---|---:|---:|---|
| Functioning day: Yes | 912.11 | < 0.001 | Operational periods had substantially higher expected demand than non-functioning periods. |
| Hour | 27.88 | < 0.001 | A one-hour increase was associated with approximately 27.9 additional rentals under the linear specification. |
| Rainfall | -58.81 | < 0.001 | An additional millimetre of rainfall was associated with approximately 58.8 fewer rentals. |
| Winter | -400.19 | < 0.001 | Winter had lower expected demand than the reference season. |
| Solar radiation | -83.56 | < 0.001 | Solar radiation had a negative conditional coefficient after controlling for the other predictors. |
| Humidity | -9.69 | < 0.001 | A one-percentage-point increase in humidity was associated with approximately 9.7 fewer rentals. |
| Sunday | -163.73 | < 0.001 | Sunday had lower expected demand than the reference weekday. |
| Temperature | 19.53 | < 0.001 | A one-degree Celsius increase was associated with approximately 19.5 additional rentals. |
| No Holiday | 114.64 | < 0.001 | Non-holidays had higher expected demand than holidays. |
| Wind speed | 22.52 | < 0.001 | Wind speed had a positive conditional coefficient in the fitted model. |
| Snowfall | 52.45 | < 0.001 | Snowfall had a positive conditional coefficient after controlling for other variables. |

The coefficients represent conditional associations while holding the other variables constant. They should not be interpreted as causal effects.

Raw coefficient magnitudes should also not be directly compared as measures of importance because the predictors use different units.

The complete coefficient results, including standard errors, t-statistics, p-values, and 95% confidence intervals, are available in:

```text
results/coefficient_results.csv
```

---

## Actual vs Predicted Demand

![Actualactual_vs_predicted.png

Points close to the diagonal line represent accurate predictions. Larger deviations from the line represent larger prediction errors.

The linear model captures a meaningful portion of demand variation, but it may have difficulty representing extreme or nonlinear demand patterns.

---

## Residual Analysis

figures/residual_plot.png

The residual plot can be used to identify:

- Nonlinear patterns
- Unequal residual variance
- Groups or clusters
- Extreme prediction errors
- Systematic underprediction or overprediction

The Durbin-Watson statistic was **0.4923**, which indicates substantial positive autocorrelation in the residuals.

This means that prediction errors from nearby hourly observations are related. The independence assumption of ordinary least squares is therefore not fully satisfied.

Consequently, the OLS p-values should be treated as baseline inferential results rather than definitive time-series inference.

---

## Key Findings

- The regression model explained approximately 55.1% of the variation in chronological test-period demand.
- Training and test performance were nearly identical.
- Functioning-day status had the largest raw coefficient.
- Rainfall, humidity, and winter were associated with lower expected demand.
- Temperature and hour were associated with higher expected demand.
- The overall regression was statistically significant.
- The residuals showed substantial positive autocorrelation.
- The fitted model is useful as an interpretable baseline but does not fully capture the temporal and nonlinear structure of hourly bike demand.

---

## Limitations

1. **Residual autocorrelation**

   Hourly observations are temporally related, and the low Durbin-Watson statistic shows that the independence assumption is not fully satisfied.

2. **Linear treatment of hour**

   Bike demand often contains morning and evening peaks. A single linear hour coefficient cannot completely represent this pattern.

3. **Correlated weather variables**

   Temperature, humidity, dew point, and solar radiation may contain overlapping information, influencing coefficient size and direction.

4. **Operational-status effect**

   Functioning-day status distinguishes system closures from normal customer demand and therefore has a very large coefficient.

5. **Omitted variables**

   The dataset does not include station-level bike availability, public events, transit disruptions, or detailed customer information.

6. **Association, not causation**

   The coefficients describe conditional statistical relationships and should not be interpreted as causal effects.

---

## How to Run the Project

### 1. Clone the repository

```bash
git clone https://github.com/YOUR-USERNAME/seoul-bike-demand-regression.git
```

### 2. Open the project directory

```bash
cd seoul-bike-demand-regression
```

### 3. Create a virtual environment

```bash
python -m venv .venv
```

### 4. Activate the virtual environment

#### Windows Command Prompt

```bat
.venv\Scripts\activate
```

#### Windows PowerShell

```powershell
.\.venv\Scripts\Activate.ps1
```

#### Linux or macOS

```bash
source .venv/bin/activate
```

### 5. Install dependencies

```bash
python -m pip install -r requirements.txt
```

### 6. Open the notebook

Open the following notebook in VS Code or Jupyter:

```text
notebooks/seoul_bike_regression.ipynb
```

Run the notebook from top to bottom.

---

## Technologies Used

- Python
- pandas
- NumPy
- Matplotlib
- Seaborn
- scikit-learn
- statsmodels
- Jupyter Notebook
- Microsoft Word

---

## Repository Outputs

The main outputs are:

- Complete Jupyter notebook
- Cleaned datasets
- Exploratory-analysis figures
- Regression coefficient table
- Predictive evaluation metrics
- Microsoft Word report

---

## Future Improvements

Future versions of the project could:

- Treat hour as a categorical variable
- Create cyclical sine and cosine hour features
- Add lagged-demand variables
- Add rolling averages
- Use time-series cross-validation
- Calculate heteroscedasticity and autocorrelation-consistent standard errors
- Compare linear regression with Ridge and Lasso regression
- Compare performance with Random Forest, Gradient Boosting, or XGBoost
- Build a Streamlit dashboard for interactive predictions
- Separate normal operating demand from system-closure periods
- Add standardized coefficients or permutation importance

---

## Author

**Mohammad Umar Shaikh Mohd Abdul Sattar**

Graduate Engineer Trainee with interests in data science, machine learning, artificial intelligence, and enterprise technology.

---

## License

This project is intended for educational and portfolio purposes.

See the `LICENSE` file for reuse conditions.

---

## Acknowledgements

The dataset was obtained from the UCI Machine Learning Repository. Credit belongs to the original dataset creators and contributors.

---

## Dataset Citation

UCI Machine Learning Repository. (2020).

Seoul Bike Sharing Demand Data Set.

Available at:
https://archive.ics.uci.edu/dataset/560/seoul+bike+sharing+demand