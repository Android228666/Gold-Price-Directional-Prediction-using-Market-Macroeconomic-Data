# Gold Price Direction Prediction - Case Study

## Project Overview
[cite_start]This project is a comprehensive data science case study focused on predicting the **daily direction of gold price changes** (UP or DOWN) using historical market and macroeconomic data from 2010 to 2024[cite: 17]. [cite_start]The analysis frames the problem as a **supervised binary classification task**, comparing a baseline rule-based model with a more complex ensemble machine learning algorithm[cite: 9, 74].

**Author:** Andrii Khomenko  
[cite_start]**Field of Study:** Data Science (IAD), 3rd Year [cite: 1]

## Research Objective
[cite_start]The primary goal is to determine if external financial indicators—such as the S&P 500 index, oil prices, palladium prices, and macroeconomic factors (inflation, interest rates)—can provide reliable signals for predicting whether gold prices will rise or fall on a given day[cite: 7, 137].

## Data Source & Features
[cite_start]The study utilizes the `financial_regression.csv` dataset, which integrates data of varying frequencies[cite: 17, 34]:
- [cite_start]**Daily Market Data:** OHLCV (Open, High, Low, Close, Volume) for Gold, S&P 500, NASDAQ, Silver, Oil, Platinum, and Palladium[cite: 19, 26].
- [cite_start]**Currency Pairs:** USD/CHF and EUR/USD exchange rates[cite: 31, 32].
- [cite_start]**Macroeconomic Indicators:** US Interest Rates (monthly), Consumer Price Index (CPI - monthly), and Gross Domestic Product (GDP - quarterly)[cite: 29, 30, 33].

## Methodology
The project follows a rigorous analytical pipeline implemented in **R**:
1.  [cite_start]**Data Preparation:** - Synchronized mixed-frequency data to a daily timeline using the **forward-fill** method[cite: 53, 54].
    - [cite_start]Handled missing values (approx. 4.47% of the dataset) by removing incomplete rows after imputation[cite: 57].
    - [cite_start]Performed **Exploratory Data Analysis (EDA)** to identify outliers and analyze volatility[cite: 36, 43].
2.  [cite_start]**Feature Engineering:** - Created the binary target variable `gold_direction` (UP if price increased, DOWN otherwise)[cite: 60, 62].
    - [cite_start]Removed highly correlated features (>0.95) to prevent redundancy and data leakage[cite: 67].
3.  **Model Training:**
    - [cite_start]Split data chronologically (80% training, 20% validation) to respect the time-series nature of financial markets[cite: 69, 71].
    - [cite_start]Compared two models: **OneR** (baseline) and **Random Forest** (advanced)[cite: 74].

## Results & Comparison
| Metric | OneR (Baseline) | Random Forest |
| :--- | :--- | :--- |
| **Accuracy** | [cite_start]~0.49 [cite: 101] | [cite_start]~0.51 [cite: 106] |
| **Recall (UP)**| [cite_start]0.67 [cite: 102] | [cite_start]**0.91** [cite: 107] |
| **F1-Score** | [cite_start]0.58 [cite: 103] | [cite_start]**0.66** [cite: 109] |

- [cite_start]**OneR:** Served as a simple benchmark, selecting a single rule that best separated classes but failed to capture non-linear market complexities[cite: 75, 103].
- [cite_start]**Random Forest:** Demonstrated superior performance by effectively identifying growth days (high recall) and balancing precision, though overall accuracy reflects the high inherent randomness of financial markets[cite: 107, 110].

## Project Files
- `Case_Study.Rmd`: The primary R Markdown source code for data processing, EDA, and modeling.
- `Case_Study.pdf`: The rendered report including code execution and visualizations.
- `Finalny Raport Case Study.pdf`: A detailed formal report (in Polish) covering the business understanding, data interpretation, and final conclusions.

## Requirements
To reproduce the analysis, ensure you have **R** installed along with the following libraries:
- `tidyverse`, `naniar`, `zoo`, `reshape2`, `caret`, `OneR`, `randomForest`, `lubridate`.
