# Gold Price Direction Prediction - Case Study

## Project Overview
This project is a comprehensive data science case study focused on predicting the **daily direction of gold price changes** (UP or DOWN) using historical market and macroeconomic data from 2010 to 2024. The analysis frames the problem as a **supervised binary classification task**, comparing a baseline rule-based model with a more complex ensemble machine learning algorithm.

**Author:** Andrii Khomenko  
**Field of Study:** Data Science (IAD), 3rd Year

## Research Objective
The primary goal is to determine if external financial indicators—such as the S&P 500 index, oil prices, palladium prices, and macroeconomic factors (inflation, interest rates)—can provide reliable signals for predicting whether gold prices will rise or fall on a given day.

## Data Source & Features
The study utilizes the `financial_regression.csv` dataset, which integrates data of varying frequencies:
- **Daily Market Data:** OHLCV (Open, High, Low, Close, Volume) for Gold, S&P 500, NASDAQ, Silver, Oil, Platinum, and Palladium.
- **Currency Pairs:** USD/CHF and EUR/USD exchange rates.
- **Macroeconomic Indicators:** US Interest Rates (monthly), Consumer Price Index (CPI - monthly), and Gross Domestic Product (GDP - quarterly).

## Methodology
The project follows a rigorous analytical pipeline implemented in **R**:
1. **Data Preparation:** - Synchronized mixed-frequency data to a daily timeline using the **forward-fill** method.
    - Handled missing values (approx. 4.47% of the dataset) by removing incomplete rows after imputation.
    - Performed **Exploratory Data Analysis (EDA)** to identify outliers and analyze volatility.
2. **Feature Engineering:** - Created the binary target variable `gold_direction` (UP if price increased, DOWN otherwise).
    - Removed highly correlated features (>0.95) to prevent redundancy and data leakage.
3. **Model Training:**
    - Split data chronologically (80% training, 20% validation) to respect the time-series nature of financial markets.
    - Compared two models: **OneR** (baseline) and **Random Forest** (advanced).

## Results & Comparison
| Metric | OneR (Baseline) | Random Forest |
| :--- | :--- | :--- |
| **Accuracy** | ~0.49 | **~0.51** |
| **Recall (UP)**| 0.67 | **0.91** |
| **F1-Score** | 0.58 | **0.66** |

- **OneR:** Served as a simple benchmark, selecting a single rule that best separated classes but failed to capture non-linear market complexities.
- **Random Forest:** Demonstrated superior performance by effectively identifying growth days (high recall) and balancing precision, though overall accuracy reflects the high inherent randomness of financial markets.

## Project Files
- `Case_Study.Rmd`: The primary R Markdown source code for data processing, EDA, and modeling.
- `Case_Study.pdf`: The rendered report including code execution and visualizations.
- `Finalny Raport Case Study.pdf`: A detailed formal report (in Polish) covering the business understanding, data interpretation, and final conclusions.

## Requirements
To reproduce the analysis, ensure you have **R** installed along with the following libraries:
`tidyverse`, `naniar`, `zoo`, `reshape2`, `caret`, `OneR`, `randomForest`, `lubridate`.
