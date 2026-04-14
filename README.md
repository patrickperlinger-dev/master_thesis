# Reducing Supermarket Food Waste through Sales Forecasting

This repository contains the code and methodology developed for my **Master’s Thesis in Information Management (Specialization in Business Intelligence)** at NOVA Information Management School.

## Research Overview
Food waste is a critical global challenge, with more than one billion tons of food wasted annually. This research investigates the optimization of retail sales forecasting for highly perishable goods, specifically strawberries, within a single Austrian supermarket to support data-driven waste reduction.

### Research Question
> *Which machine learning algorithm and which combination of features result in the highest prediction accuracy for the sales of perishable goods of a specific Austrian supermarket?*

---

## Technical Stack
The project is implemented in Python using the following core libraries:
* **Darts:** Used for time-series forecasting supporting statistical and machine learning methods.
* **Pandas & NumPy:** For data manipulation and feature engineering.
* **Matplotlib & Seaborn:** For exploratory data analysis and error visualization.

---

## Data Description
The empirical analysis is based on a joined dataset covering the timeframe from 2021 to 2025:
* **Sales Data:** Internal supermarket transaction records at a granular daily level.
* **Weather Data:** 27 meteorological features (temperature, precipitation, wind speed, etc.) sourced from the Open-Meteo API.
* **Calendric Data:** Engineered features including public holidays and cyclical encoding (sine/cosine) for weekdays and months.

> **Note:** Data files are not shared due to a non-disclosure agreement with the supermarket.

---

## Experimental Pipeline
The project follows a systematic modeling pipeline:
1. **Data Preparation:** Data consolidation, stockout imputation, feature engineering and cyclical encoding.
2. **Train-Validation-Test:** A chronological 60-20-20 split (Train: 2021-2023, Val: 2024, Test: 2025).
3. **Feature Subsets:** Systematic evaluation of four versions: Sales Only (V1), Sales + Weather (V2), Sales + Calendric (V3), and Full Set (V4).
4. **Training of Algorithms:** ARIMAX, LightGBM, XGBoost, LSTM and TFT are benchmarked against a naive baseline
5. **Hyperparameter Tuning:** Optimized through Grid Search, Random Search and business logic.
6. **Ensemble Construction:** A hybrid stacking ensemble utilizing a meta-learner to integrate base architectures.

---

## Key Findings
The models were evaluated using **WAPE** (Weighted Absolute Percentage Error) as the main evaluation metric on the 2025 test set.

| Model | Test WAPE (%) | Rank |
| :--- | :--- | :--- |
| Stacking Ensemble | 43.00% | 1 |
| XGBoost (Tuned) | 44.22% | 2 |
| ARIMAX (Tuned) | 47.55% | 3 |
| LSTM (Tuned) | 54.54% | 4 |
| LightGBM (Tuned) | 55.34% | 5 |
| Temporal Fusion Transformer | 56.34% | 6 |
| *Naive Seasonal Baseline* | *59.90%* | *-* |

### Research Insights
* **Ensemble Superiority:** The stacking ensemble achieved the highest accuracy, confirming that hybrid models yield more robust forecasts.
* **Feature Impact:** Calendric data was identified as the most significant exogenous feature set for improving accuracy.
* **Complexity vs. Performance:** Simpler tree-based models and statistical baselines outperformed complex deep learning architectures (LSTM, TFT) in this store-level environment.

---

## Author & Supervision
* **Author:** Patrick Perlinger
* **Supervisor:** Professor Fernando José Ferreira Lucas Bação
* **Institution:** NOVA Information Management School

*Vienna, April 2026*
