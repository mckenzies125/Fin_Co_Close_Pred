# Equity Price Prediction

## Overview

This project investigates whether patterns learned from the historical stock data of several financial companies can generalize to a different company.

Using five years of market data, I trained regression models on JPMorgan Chase (JPM), PayPal (PYPL), MetLife (MET), and American International Group (AIG), then evaluated their ability to predict Goldman Sachs (GS) closing prices.

The project compares ordinary least squares (OLS) regression and support vector regression (SVR), with particular attention to both predictive performance and model diagnostics.

## Research Question

Can a model trained on the historical market behavior of several companies generalize to predict the closing price of another company?

Rather than training and testing a model on observations from the same stock, this project evaluates cross-company generalization by holding Goldman Sachs out of the training data entirely.

## Data

Five years of historical stock data were collected using the `yfinance` Python library for:

- JPMorgan Chase (`JPM`)
- PayPal (`PYPL`)
- MetLife (`MET`)
- American International Group (`AIG`)
- Goldman Sachs (`GS`)

The analysis uses daily market information including:

- Open price
- High price
- Low price
- Trading volume
- Closing price

To avoid using same-day information to predict the closing price, Open, High, Low, and Volume were lagged by one trading day. The resulting features therefore represent the previous day's market information.

## Methods

### Exploratory Analysis

Historical stock behavior was explored through:

- Daily, weekly, and monthly returns
- Return distributions
- Price and market trends
- Relationships among predictor variables

### Predictive Modeling

Two regression approaches were compared:

**Ordinary Least Squares (OLS)**  
A linear regression model was used as a baseline for estimating the relationship between lagged market features and closing price.

**Support Vector Regression (SVR)**  
A linear-kernel SVR model was fit using standardized predictors to provide an alternative regression approach.

Both models were trained using the combined JPM, PYPL, MET, and AIG observations and evaluated exclusively on GS observations.

## Results

| Model | Test R² | RMSE |
|---|---:|---:|
| OLS Regression | 0.9829 | 16.36 |
| Support Vector Regression | 0.9826 | 16.51 |

Both models produced similar predictive performance on the Goldman Sachs data, explaining approximately 98% of the observed variation in closing prices.

The OLS model achieved a slightly lower RMSE, although the difference between the two approaches was minimal.

## Model Diagnostics

High predictive performance did not imply that the models were appropriate for statistical inference.

Residual analysis revealed evidence of **heteroscedasticity**, with prediction errors displaying a non-constant variance pattern.

The predictor correlation matrix also showed extremely high correlations among Open, High, and Low prices, indicating substantial **multicollinearity**. While this does not necessarily prevent strong predictions, it can make individual regression coefficients unstable and difficult to interpret.

These findings illustrate the distinction between **predictive performance and inferential reliability**: a model can predict well while still violating assumptions that limit interpretation of its estimated parameters.

## Key Takeaways

- Models trained on multiple companies were able to achieve strong predictive performance when evaluated on a held-out company's stock data.
- OLS and linear SVR produced nearly identical performance in this analysis.
- Strong predictive metrics should not be interpreted as evidence that a model satisfies the assumptions required for reliable statistical inference.
- Residual diagnostics identified heteroscedasticity.
- Strong correlations among price-related predictors revealed substantial multicollinearity and potential coefficient instability.

## Technologies

- Python
- pandas
- NumPy
- scikit-learn
- Matplotlib
- yfinance
- Jupyter Notebook

## Repository Structure

`Skrastins_CaseStudy_1.ipynb` — Data collection, exploratory analysis, modeling, model evaluation, diagnostics, and conclusions.

## Limitations

This project is an exploratory academic analysis rather than a deployable financial forecasting system. Stock prices are time-dependent, and the models do not account for many factors that influence financial markets, including macroeconomic conditions, company-specific events, market sentiment, or broader temporal dynamics.

The high R² values should therefore be interpreted within the specific experimental design rather than as evidence that the models can reliably forecast future stock prices in real-world trading environments.

## Author

McKenzie Skrastins
