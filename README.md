# Raymond Priestley Centre Review Analysis

## 📌 Overview
This project analyzes customer reviews of the Raymond Priestley Centre using:
- **Sentiment Analysis (NLP)**
- **Time Series Analysis (STL + SARIMA)**

The goal is to extract insights from textual reviews and identify temporal patterns in customer sentiment.

---

## 🎯 Objectives
- Analyze customer sentiment from review text
- Understand how sentiment changes over time
- Decompose time series into trend and seasonality
- Forecast future review trends using SARIMA

---

## 📂 Project Structure

---

## 📊 Dataset
- File: `data/Reviews_RPC_Cleaned.xlsx`
- Contains customer reviews and timestamps
- Data was cleaned and preprocessed before analysis

---

## 🔍 Methodology

### 1. Sentiment Analysis
- Text preprocessing (cleaning, tokenization)
- Sentiment scoring using NLP techniques
- Classification into positive, negative, neutral
- Visualization of sentiment distribution

---

### 2. Time Series Analysis

#### STL Decomposition
- Decomposed time series into:
  - Trend
  - Seasonality
  - Residual

#### SARIMA Model
- Built forecasting model using SARIMA
- Captured both trend and seasonal components
- Used for predicting future review patterns

---

## 📈 Results & Insights

### Sentiment Distribution
![Sentiment Distribution](images/sentiment_distribution.png)

- Majority of reviews are positive
- Negative reviews highlight specific issues

---

### Time Series Decomposition
![STL Decomposition](images/stl_decomposition.png)

- Clear seasonal patterns observed
- Trend shows variation in customer engagement over time

---

### Forecasting Results
![Forecast](images/forecast.png)

- SARIMA model successfully captured seasonality
- Useful for predicting future review trends

---

## 🛠️ Tech Stack
- Python
- Pandas, NumPy
- Matplotlib, Seaborn
- Statsmodels
- NLP libraries (NLTK / TextBlob)

---

## ▶️ How to Run

1. Clone the repository:
   ```bash
   git clone https://github.com/yourusername/raymond-priestley-review-analysis.git
