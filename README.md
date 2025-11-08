#  Retail Sales Forecasting with Weather-Aware LightGBM: A Comparative Study Including Prophet

##  Overview
Accurate sales forecasting is a crucial task in retailing as it ensures optimal goods allocation and helps reduce costly problems like **overstock** and **stockout**.  

This project extends traditional time series forecasting by integrating:
- **Advanced machine learning (LightGBM)**
- **External weather data**
- **Hybrid modeling with business rules**

The framework was applied to the **M5 Forecasting Competition (Walmart sales data)** and benchmarked against **Prophet** and **naive baselines**.

---

##  Project Highlights

###  Novel Contributions & Key Features
1. **Hybrid Forecasting with Domain Rules**  
   - Combined **LightGBM** predictions with business rules:  
     - +50% forecast for *holiday weekends*  
     - −20% during *heatwaves*  
     - −30% during *heavy snowfall*  
   - Captures extreme conditions that pure ML pipelines might miss.  

2. **Operationally Meaningful Evaluation**  
   - Evaluated not only with statistical metrics but also *business-focused* ones:  
     - **Overstock%**
     - **Stockout%**
     - **Cost Index (0.3 × Overstock + 0.7 × Stockout)**  

3. **Explainability at Multiple Levels**  
   - Used **SHAP analysis** globally and for single items to identify feature importance.  
   - Revealed that weather and holidays significantly affect forecasts at the item level.  

4. **Real-World Data Integration**  
   - Combined **M5 retail dataset (42,000 SKUs)** with **Open-Meteo weather data** and **calendar features** for realistic modeling.

---

##  Methodology Overview

Our sales forecasting pipeline integrates **statistical, machine learning,** and **rule-based** approaches.

###  LightGBM (Light Gradient Boosting Machine)
- Main model for its speed and scalability.  
- Key features:  
  - Lagged sales (`sales_lag7`),  
  - Rolling means (`sales_rolling7`),  
  - Temporal variables,  
  - Weather-based flags (`is_heatwave`, `is_heavy_snow`).  
- Trained using **time series cross-validation**.

###  Prophet (Additive Time Series Model)
- Used as a **statistical baseline** to capture trend and seasonality in daily sales.

###  Hybrid Model (LightGBM + Rules)
- Base predictions from LightGBM.  
- Applied deterministic **business rule adjustments** for operational robustness.

###  Data Source
- **M5 Forecasting Accuracy** dataset (Walmart – CA_1 store).  
- Weather data sourced from **Open-Meteo API**.

---

##  Results Summary

| Model | RMSE | MAE | R² | Overstock% | Stockout% | Cost_Index | MASE | RMSSE | WMAPE | Theil’s U |
|-------|------|------|----|-------------|------------|-------------|-------|--------|--------|-----------|
| **LightGBM** | **1.1033** | **0.7403** | **0.2303** | 67.00 | 36.64 | 47.35 | 0.7204 | 0.6454 | 94.23 | **0.4648** |
| **Hybrid** | 1.1115 | 0.7393 | 0.2190 | 66.53 | 37.11 | 47.94 | 0.7193 | 0.6502 | 94.09 | 0.4702 |
| **Prophet** | 1.2270 | 0.8454 | 0.0481 | 84.86 | 38.78 | 58.60 | 0.8226 | 0.7178 | 107.60 | 0.5317 |
| Naive (Mean) | 1.2546 | 0.9002 | 0.0048 | 164.34 | 39.10 | 128.67 | 0.8759 | 0.7339 | 114.58 | 0.5204 |
| Naive (Last Day) | 1.7097 | 1.0283 | −0.8478 | 46.22 | 28.85 | 22.06 | 1.0006 | 1.0001 | 130.88 | 0.5764 |

###  Key Findings
- **LightGBM** achieved the lowest **RMSE (1.10)** and **Theil’s U (0.46)**.  
- The **Hybrid model** improved inventory metrics with only a minor drop in RMSE.  
- **Prophet** lagged behind in both accuracy and business relevance.  
- Gradient boosting remains a robust baseline for retail demand forecasting.  

---

##  Evaluation Metrics

| Type | Metrics Used |
|------|---------------|
| **Statistical Accuracy** | RMSE, MAE, R², MASE, RMSSE |
| **Operational Performance** | Overstock%, Stockout%, Cost Index |
| **Relative Performance** | WMAPE, Theil’s U |

---

##  Visual Insights

- **Forecast Comparison:** LightGBM tracks demand variations more closely than Prophet.  
- **Error Distribution:** Near-symmetric spread confirms stable performance.  
- **SHAP (Global):** Lagged sales and rolling averages dominate.  
- **SHAP (Single Item):** `is_holiday` and `is_heatwave` gain importance — showing localized effects.  

---

##  Project Details

- **Author:** Akter Zaman  
- **Master's Project Defense:** ✅ Successfully Defended (2025)  
- **Code:** [`submission-code.ipynb`](submission-code.ipynb)   
- **GitHub Repository:** [https://github.com/AKTERZAMAN06](https://github.com/AKTERZAMAN06)  
- **LinkedIn:** [https://www.linkedin.com/in/akter-zaman-reyad/](https://www.linkedin.com/in/akter-zaman-reyad/)  
- **License:** MIT License  


