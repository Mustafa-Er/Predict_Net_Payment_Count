# 📈 Predict_Net_Payment_Count

## 🧾 Merchant Transaction Count Prediction

This project focuses on predicting **monthly merchant-based transaction counts** (`net_payment_count`) for the **last quarter of 2023** using historical data and machine learning.

---

## 📊 Project Objective

Predict the number of **net payment transactions** (i.e., `payment - cancel - refund`) per merchant for **October, November, and December 2023**, using data from **January 2020 to September 2023**.

---

## 📁 Dataset Description

The dataset consists of **categorical metadata** describing merchant attributes and their monthly transaction volumes.

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

> ℹ️ All columns, except `net_payment_count`, are **categorical**.

---

## 🔍 Exploratory Data Analysis (EDA)

- **Merchant Source**: Mostly from sources `1` and `2`; source `3` is rarely used.
- **Settlement Period**: Predominantly period `1`, followed by `3`. Period `2` is rarely used.
- **Working Type**: Types `5` and `6` dominate; types `1`, `3`, and `4` are nearly absent.
- **Merchant Segment**: Vast majority belong to segment `4`.

---

## 📊 Statistical Analysis

Since `net_payment_count` does **not follow a normal distribution**, **non-parametric tests** were used:

### 🧪 Kruskal-Wallis Test

Used to assess whether medians of different categorical groups differ significantly.  
✅ Result: Statistically significant differences were observed across several features.

### 🔍 Nemenyi Post-hoc Test

Performed after Kruskal-Wallis to determine **which group pairs** differ significantly.  
✅ Helped identify the impact of specific category values on transaction volume.

---

## 🤖 Models and Training

Two regression models were trained using **TimeSeriesSplit** cross-validation.

| **Model**             | **Run Time** | **Mean MAE** |
|-----------------------|--------------|---------------|
| ✅ XGBRegressor        | 6.13 seconds | **280.16**     |
| 🐈 CatBoostRegressor   | 230.36 seconds | **638.70**     |

> 🔍 **XGBRegressor** outperformed CatBoost in both speed and accuracy.

---

## 📌 Feature Importance

Top contributing features identified by the **XGBRegressor** model:

- `mcc_id`
- `merchant_segment`
- `working_type`

These features were found to have the most influence on `net_payment_count`.

---

## ✅ Conclusion

- **XGBRegressor** proved to be an efficient and effective model for forecasting merchant transaction counts.
- **Non-parametric statistical analysis** was critical due to the distribution of the target variable.
- Careful **feature engineering** and **EDA** revealed key categorical variables impacting transaction volume.



