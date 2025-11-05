# 🪙 Gold Price Forecasting (2013–2023)
*A Comparative Study of Statistical, Machine Learning, and Deep Learning Models*

---

## 📘 Overview
This repository contains the complete workflow, analysis, and report for a decade-long **gold price forecasting study** conducted on daily price data from **2013–2023**.  
The goal of the project is to evaluate the predictive performance of **classical time-series models (AR, MA, ARMA, ARIMA, GARCH)**, a **machine-learning regression model (CART)**, and a **deep learning model (LSTM)** under a **unified preprocessing and evaluation framework**.

All results, figures, and metrics are reproducible using the Jupyter Notebook provided in this repository.

---

## 🧾 Dataset
**Source:** [Kaggle – Gold Price (2013–2023)](https://www.kaggle.com/datasets)  
**Records:** 3,634 daily observations  
**Fields:**
- `Date`: Timestamp of observation  
- `Price`: Daily gold price in USD  

### Data Characteristics
- Period covered: **January 2013 – December 2023**  
- Frequency: **Daily** (resampled to continuous daily intervals)  
- Missing values handled via **time-based interpolation**  
- Non-stationarity confirmed via **ADF test** (p-value = 0.74 at level)  
- Achieved stationarity after **first differencing (p-value < 0.001)**  

Key transformations:
- Conversion of numeric strings with currency symbols  
- Duplicate removal and chronological sorting  
- Resampling and interpolation for continuity  
- Scaling via **Min–Max normalization [0,1]** for ML/DL models  

---

## 🧪 Methodology

### Preprocessing
1. Cleaned and standardized data format  
2. Conducted **Augmented Dickey–Fuller (ADF)** test  
3. Examined **ACF and PACF** plots for lag behavior  
4. Differenced the data to enforce stationarity  
5. Normalized series for neural network training  

### Models Implemented
| Model | Description | Key Feature |
|--------|--------------|--------------|
| **AR(p)** | Linear dependence on past values | Stationary-only |
| **MA(q)** | Linear dependence on past errors | White-noise driven |
| **ARMA(p,q)** | Combines AR & MA | Stationary series |
| **ARIMA(p,d,q)** | Adds differencing for trend removal | Handles non-stationary data |
| **GARCH(1,1)** | Captures volatility clustering | Conditional variance modeling |
| **CART** | Regression tree with lag and SMA features | Non-parametric, interpretable |
| **LSTM** | Long Short-Term Memory network | Sequential pattern learning |

---

## ⚙️ Experimental Setup

- **Environment:** Kaggle Notebook (Python 3.10, 16GB RAM, Tesla T4 GPU)
- **Libraries:** `statsmodels`, `arch`, `pmdarima`, `scikit-learn`, `tensorflow`, `pandas`, `matplotlib`
- **Data Split:** 80% training (2013–2021), 20% testing (2022–2023)
- **Forecast Type:** One-step-ahead rolling predictions
- **Metrics:**  
  - RMSE – Root Mean Squared Error  
  - MAE – Mean Absolute Error  
  - MAPE – Mean Absolute Percentage Error  

All random seeds were fixed (`seed = 42`) to ensure reproducibility.

---

## 📊 Results and Analysis

### Quantitative Results
| Model | RMSE | MAE | MAPE (%) |
|--------|------|------|-----------|
| **ARIMA (5,2,0)** | **14.46** | **9.88** | **0.55** |
| **CART (lags + SMA)** | 15.31 | 11.22 | 0.62 |
| **LSTM (simple)** | 26.91 | 23.01 | 1.27 |
| AR (p=20) | 84.51 | 66.64 | 3.66 |
| ARMA (5,4) | 90.03 | 70.02 | 3.83 |
| GARCH (1,1) | 140.81 | 122.35 | 6.95 |
| MA (q=17) | 454.94 | 447.64 | 24.72 |

**Best Performing Model:**  
> 📈 **ARIMA(5,2,0)** – lowest RMSE and MAPE among all candidates.

### Visualization Summary
- **Trend Plot:** Gold price exhibited long-term upward trend with mild volatility spikes.  
- **ACF–PACF Analysis:** Confirmed strong autocorrelation and necessity for differencing.  
- **Residual Diagnostics:** ARIMA residuals passed normality and independence tests.  
- **Forecast Comparison:** ARIMA tracked actual gold prices most closely (2022–2023).  
- **Error Distribution:** ARIMA produced near-zero mean residuals with minimal autocorrelation.

---

## 🧩 Discussion

1. **ARIMA’s Dominance:** Once differenced, the gold series behaved as a stationary stochastic process, making ARIMA’s linear framework highly effective.  
2. **CART’s Competitiveness:** Captured short-term regime shifts but lacked temporal continuity.  
3. **LSTM’s Limitation:** Underperformed due to small data volume and lack of exogenous inputs.  
4. **GARCH’s Utility:** Accurately modeled variance but not mean dynamics.  

The findings collectively demonstrate that **classical models remain highly competitive** in financial forecasting when rigorous preprocessing is performed.  

---

## ⚠️ Limitations
- Only **univariate** modeling (no macroeconomic features like USDX, CPI, oil prices).  
- **Static parameters**—no adaptive or time-varying coefficients used.  
- **Short forecast horizon** (1-day ahead rolling forecasts).  
- LSTM model **not deeply tuned** (basic 1-layer configuration).  

These factors limit generalization but establish a strong baseline for future hybrid and multivariate research.

---

## 🔭 Future Scope
- Introduce **exogenous macroeconomic indicators** (ARIMAX, GARCH-X, VAR).  
- Develop **hybrid ARIMA–LSTM** or **GARCH–LSTM** models for joint trend–volatility learning.  
- Explore **Transformer-based** models (Temporal Fusion Transformer, Informer).  
- Generate **probabilistic forecasts** with confidence intervals.  
- Extend analysis to **other commodities** (silver, crude oil, copper).

---


---

## 🧠 Key Insights
- Gold prices exhibit **persistent trend and autocorrelation** rather than random walk behavior.  
- Statistical differencing and model validation are **critical preprocessing stages**.  
- Deep learning does not guarantee superiority without **sufficient data scale**.  
- Interpretability and stability of ARIMA make it **preferable for practical forecasting** in stable market conditions.

---

## 🧩 Citation
If you use this work or parts of it in your research, please cite as:
Roy, S. (2025). Gold Price Forecasting (2013–2023):
A Comparative Study of Statistical, Machine Learning, and Deep Learning Models.
Department of Data Science and Analytics, Central University of Rajasthan.


---

## 🧑‍💻 Author
**Suha Roy**  
Department of Data Science and Analytics  
Central University of Rajasthan, India  

For questions or collaboration: [suha.academics@gmail.com]



---

*This repository accompanies the full academic report and provides the computational foundation for all results and figures presented therein.*




