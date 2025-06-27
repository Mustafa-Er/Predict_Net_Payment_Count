# Predict_Net_Payment_Count


🧾 Merchant Transaction Count Prediction
This project focuses on predicting monthly merchant-based transaction counts (net_payment_count) for the last quarter of 2023 using historical transaction data.

📊 Project Objective
Predict the number of net payment transactions (i.e., payment - cancel - refund) per merchant for October, November, and December 2023, using transaction data between January 2020 and September 2023.

📁 Dataset Description
The dataset consists of categorical metadata describing merchant attributes and their monthly transaction volumes.

### 📌 Features

| **Column**           | **Description**                                         |
|----------------------|---------------------------------------------------------|
| `merchant_id`        | Unique identifier for each merchant (masked)            |
| `month_id`           | Transaction month in `YYYYMM` format                    |
| `merchant_source`    | Source from which the merchant joined                   |
| `settlement_period`  | Frequency of payout to the merchant                     |
| `working_type`       | Type of workplace                                       |
| `mcc_id`             | Merchant category code                                  |
| `merchant_segment`   | Segment classification within the platform              |
| `net_payment_count`  | Target variable — net transactions for the given month  |


All columns, except net_payment_count, are categorical.

### 🔍 Exploratory Data Analysis (EDA)

- **Merchant Source**: Mostly from sources `1` and `2`; source `3` is rarely used.
- **Settlement Period**: Predominantly period `1`, followed by `3`. Period `2` is rarely used.
- **Working Type**: Types `5` and `6` dominate; types `1`, `3`, and `4` are nearly absent.
- **Merchant Segment**: Vast majority belong to segment `4`.


📊 Statistical Analysis
Since net_payment_count does not follow a normal distribution, non-parametric tests were applied:

🧪 Kruskal-Wallis Test
Used to assess whether medians of different categorical groups differ significantly.
Result: Revealed statistically significant differences in several features.

🔍 Nemenyi Post-hoc Test
Conducted after Kruskal-Wallis to identify which group pairs differ significantly.
Helped understand the impact of categorical values on transaction counts.

🤖 Models and Training
Two regression models were trained using TimeSeriesSplit cross-validation:

✅ XGBRegressor
Run Time: 6.13 seconds

Mean MAE: 280.16

🐈 CatBoostRegressor
Run Time: 230.36 seconds

Mean MAE: 638.70

🔍 XGBRegressor outperformed CatBoost in both speed and accuracy.

📌 Feature Importance
Below is a summary of the most important features based on XGBRegressor model:


mcc_id, merchant_segment, and working_type are the most impactful predictors.

📌 Conclusion
XGBRegressor provides a fast and accurate method for forecasting merchant transaction counts.

Non-parametric statistical tests are essential when the target variable is not normally distributed.

Feature engineering and category analysis helped to better understand which merchant attributes drive transaction volume.

