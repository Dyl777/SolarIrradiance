Got it ✅ — you want the LaTeX paper rewritten in **Markdown format** (so it’s easier to read, edit, and adapt into blogs, GitHub docs, or Overleaf later) while also **expanding the technical discussion about AMMC**.

Here’s the rewritten **Markdown research paper** version with an extended AMMC discussion:

---

# Solar Irradiance Forecasting in Cameroon Using Statistical, Deep Learning, and Hybrid Time Series Models

**Authors:**
 Dyl Padaran Ambe

---

## Abstract

Accurate solar irradiance forecasting is vital for renewable energy integration in sub-Saharan Africa, where solar resources are abundant but underutilized. This study evaluates statistical (ARIMA, SARIMAX), deep learning (LSTM, GRU, CNN-LSTM), and hybrid frameworks (Prophet, AMMC) using multi-location meteorological data from Cameroon (2005–2020). The models were trained and tested on irradiance, temperature, humidity, and wind speed across four towns. Results show that AMMC consistently outperformed baselines, reducing underfitting and improving generalization across volatile tropical weather. The findings provide insights for solar grid integration and renewable energy planning in Africa. AMMC required just 30-40s to train on a Colab CPU over 108k data samples (15s on a T4 GPU) as opposed to ARIMA took 1-2mins to train while SARIMAX took 2-3mins to train on even Google Colab 8-core CPU and 15-30secs, 40-50secs on a single T4 Google Colab GPU respectively. We performed gridsearch for hyperparameter tuning but it didn’t significantly improve the quality of the models, which took around 1hr24mins on a single Google Colab 8-core CPU, 30-50mins for CNN, LSTMs

---

## 1. Introduction

Cameroon possesses abundant solar resources, yet the integration of photovoltaic (PV) energy remains challenged by the stochastic variability of solar irradiance. Accurate forecasting is crucial for grid stability, energy dispatch, and optimizing storage systems. Existing research primarily focuses on developed countries with temperate climates, creating a gap in methodologies tailored for tropical sub-Saharan Africa. This study addresses this gap by leveraging high-frequency (24 readings per day) meteorological data from four towns in Cameroon.

---

## 2. Related Work

* **Statistical models (ARIMA, SARIMAX):** capture linear and seasonal dependencies but fail under strong nonlinear fluctuations.
* **Deep learning (LSTM, GRU):** handle nonlinear temporal dependencies but tend to underfit in volatile, noisy tropical environments.
* **Hybrid models (Prophet, CNN-LSTM, AMMC):** combine interpretability with flexibility. Ensembles and adaptive hybrids often outperform single models in literature.

---

## 3. Methodology

### 3.1 Data Sources

Meteorological datasets (2005–2020) from Bambili, Bamenda, Bafoussam, and Yaoundé were used. Features included irradiance (W/m²), temperature (°C), humidity (%), and wind speed (m/s), with 24 readings per day.

### 3.2 Data Preprocessing

* **Column Normalization:** corrected inconsistent names (`humidity` vs. `humudity`).
* **Missing Values:** none found; no imputation needed.
* **Feature Engineering:** extracted year, month, day; future work could use rolling statistics and lagged features.
* **Normalization:** Min–Max scaling applied:

$$
X_{\text{scaled}} = \frac{X - X_{\min}}{X_{\max} - X_{\min}}
$$

### 3.3 Implemented Functions

* **`clean_by_date_mean`** – aggregated values by day, corrected labels, added location tags.
* **`_plot_series`** – generated irradiance time series plots.

*📌 Figure Placeholder: Data cleaning and preprocessing pipeline*

---

### 3.4 Forecasting Models

#### Statistical Models

* **ARIMA(p,d,q):** univariate, captured seasonality but failed on volatility.
* **SARIMAX:** extended ARIMA with exogenous inputs (temperature, humidity, wind speed).

#### Deep Learning Models

* **LSTM:** long-term sequence learning, smoothed predictions.
* **GRU:** lighter variant of LSTM, generalized slightly better.
* **CNN-LSTM:** used convolutional filters to detect local temporal features before passing into LSTMs.

#### Hybrid Models

* **Prophet:** decomposed time series into trend + seasonality + holiday components, but severely underfit.
* **AMMC (Adaptive Multi-Modal Core):**

  * **RevIN (Reversible Instance Normalization):** dynamically normalizes input distributions, stabilizing training across diverse stations.
  * **Adaptive Variate Selection (AVS):** selects the most relevant meteorological features (e.g., humidity, temperature) for each forecast horizon.
  * **Enhanced Series-Core Fusion (ESCF):** fuses global trends with local fluctuations to capture both high-level seasonality and short-term anomalies.
  * **Multi-Modal Context Fusion (MMCF):** integrates heterogeneous data streams (irradiance + weather) into a unified representation.

**Why AMMC Outperforms:**
Unlike LSTM/GRU, which sequentially encode a single trajectory, AMMC adaptively switches between relevant features and dynamically rescales inputs. This makes it robust to:

* High-frequency tropical noise (sudden cloud cover, microclimate changes).
* Cross-location heterogeneity (Bambili vs. Yaoundé).
* Both **short-term peaks** (daily irradiance spikes) and **long-term trends** (seasonal cycles).

*📌 Figure Placeholder: AMMC architecture overview*

---

## 4. Results and Analysis

### 4.1 Descriptive Statistics

* Humidity: 85–95%
* Temperature: 18–20 °C
* Irradiance: peaks at 600–800 W/m²

*📌 Figure Placeholder: Time series of irradiance in Bamenda (2005–2020)*

### 4.2 Model Comparisons

| Location  | RMSE   | MAE   | MAPE (%) |
| --------- | ------ | ----- | -------- |
| Bambili   | 121.36 | 93.26 | 23.6     |
| Bamenda   | 102.99 | 82.67 | 19.9     |
| Bafoussam | 67.42  | 56.53 | 10.8     |
| Yaoundé   | 60.67  | 50.34 | 10.3     |

### 4.3 Discussion

* **ARIMA/SARIMAX:** captured seasonality but weak under volatility.
* **LSTM/GRU:** smoothed outputs but underfit sharp fluctuations.
* **CNN-LSTM:** extracted features but failed to fully capture volatility.
* **Prophet:** underfit, approximated constant average.
* **AMMC:** outperformed across all metrics, captured **sharp peaks and troughs**, robust to noise, and generalized well across locations.


## 5. Conclusion and Future Work

This research demonstrates the importance of adaptive hybrid frameworks in forecasting solar irradiance in tropical climates. AMMC consistently outperformed statistical and deep learning baselines, making it suitable for practical energy planning in Cameroon and beyond.

**Future work:**

* Integration of satellite imagery and weather forecasts.
* Deployment of real-time AMMC on IoT-enabled solar farms.
* Transfer learning for cross-regional generalization across Africa.

---

## Acknowledgments

We thank Dr. Sop Lionel for his guidance and the University of Buea for resources.

---


Would you like me to also **add a new section on “Reasoning Trees and RL-based Interpretability”** (like we discussed earlier), so the paper not only covers forecasting but also ties into your reinforcement learning research direction?
