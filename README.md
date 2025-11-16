# Risk Management and Backtesting: Estimating VaR for MBB Stock

## Overview

This project provides an evaluation of **Value at Risk (VaR)** for the **MBB stock**, focusing on risk quantification and model validation through backtesting. VaR is a crucial risk management tool used to quantify the potential loss in the value of an asset or portfolio over a given time horizon at a specified confidence level.

The analysis estimates VaR using three distinct models applied to historical log returns of MBB stock, followed by rigorous backtesting to assess their accuracy and reliability in predicting market risk.

| Detail | Information |
| :--- | :--- |
| **Topic** | Risk Management and Backtesting: Estimating VaR for MBB Stock |
| **Institution** | National Economics University, Faculty of Mathematical Economics |
| **Author** | Nguyễn Hoài An (Student’s ID: 11220032) |
| **Time Horizon** | 1-day Value at Risk (VaR) |
| **Confidence Level** | 99% confidence level |

## Data and Scope

The analysis utilizes daily closing prices of the stock symbol **MBB**, retrieved using Excel's `STOCKHISTORY` function.

| Dataset Period | Purpose | Dates |
| :--- | :--- | :--- |
| **Full Dataset Range** | Complete scope of analysis | January 1, 2023, to April 29, 2025 |
| **Estimation Data** | Used to estimate VaR models | January 1, 2023, to January 1, 2024 |
| **Backtesting Data** | Used for out-of-sample model evaluation | January 2, 2024, to April 29, 2025 |

The input for risk estimation is the **return series**, calculated using **log returns**.

## VaR Calculation Methods

The 1-day VaR at the 99% confidence level was estimated using three approaches based on the MBB stock's log return series:

1.  **Parametric VaR (Normal Distribution):** This method assumes that returns are **normally distributed**. VaR is calculated using the mean and standard deviation of returns along with the inverse of the cumulative distribution function (CDF) of the normal distribution.
2.  **Parametric VaR (Student’s t-Distribution):** This approach accounts for potential **heavy tails** in the return distribution by assuming a Student’s t-distribution. The parameters are estimated via maximum likelihood, and VaR is computed using the inverse CDF of the t-distribution.
3.  **Historical Simulation (Non-Parametric VaR):** This method is non-parametric, meaning it **does not rely on any distributional assumptions**. VaR is calculated directly from the empirical distribution of historical returns by finding the $\alpha$-quantile.

### VaR Estimates (99% Confidence, 1-Day Loss)

The calculated results represent the estimated potential one-day loss as a percentage of portfolio value:

| VaR Method | Estimated Loss | Conservative Measure |
| :--- | :--- | :--- |
| **Normal Distribution** | **−3.55%** | Less robust in tail-risk estimation |
| **Student’s t-distribution** | **−4.12%** | **Most conservative**, capturing more tail risk |
| **Historical Simulation** | **−3.41%** | Better predictive precision for loss magnitude |

## Backtesting and Evaluation

Backtesting was conducted using the out-of-sample data (January 2, 2024 to April 29, 2025) to assess model accuracy. Key metrics and statistical tests utilized include:

*   **Violation Ratio (VR):** The proportion of days where actual losses exceeded the predicted VaR.
*   **Root Mean Squared Error (RMSE):** Measures the average magnitude of forecast errors.
*   **Mean Absolute Percentage Error (MAPE):** Provides an average percentage error relative to the predicted VaR.
*   **Kupiec Test (LR Statistic):** A likelihood ratio test assessing whether the observed violation frequency matches the expected 1% frequency.
*   **Conditional Coverage Test (LR):** Jointly assesses both the correct frequency and the independence of violations.

### Summary of Backtesting Results

**The Parametric t-distribution model demonstrates the best statistical backtesting performance**.

*   Its violation ratio (1.52%) is **closest to the expected 1%**.
*   It achieved the lowest LR values for both the Kupiec and Conditional Coverage tests, indicating accurate coverage and independent breaches.
*   However, it records the **highest RMSE**, meaning it has larger average errors in magnitude prediction.

**The Historical Simulation model offers the best predictive precision for loss magnitude**.

*   It has the **lowest RMSE and MAPE**.
*   However, it slightly **overestimates VaR breaches** (VR of 1.83%), exceeding the 1% threshold. (The Parametric Normal model yielded identical VR, LR Kupiec, and LR Conditional values to Historical Simulation.)

## Conclusion and Recommendations

The choice of the optimal model depends on the risk management objective:

| Objective | Recommended Model | Rationale (as per source) |
| :--- | :--- | :--- |
| **Regulatory Compliance** | **Parametric t-distribution model** | Most reliable in terms of matching the expected violation rate and statistical accuracy. |
| **Accurate Loss Forecasting** | **Historical Simulation model** | Offers the best precision in predicting the magnitude of loss sizes (lowest RMSE/MAPE). |

The **parametric normal model** is generally considered **less suitable for critical risk management needs** as it underperforms in capturing extreme risks (tail-risk estimation) and correctly predicting violation frequency.
