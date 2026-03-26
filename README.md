# Raymond Priestley Centre Review Analysis
A data analytics project analysing participant feedback for the Raymond Priestley Centre (RPC), an outdoor education and leadership development facility at the University of Birmingham. The project applies NLP-based sentiment analysis and time-series forecasting to surface actionable insights from review data.

## 📌 Overview
The Raymond Priestley Centre runs a range of residential and day programmes — leadership retreats, team-building residentials, and skills courses — primarily for University of Birmingham students and external groups. This project analyses structured review data collected from participants to:

Understand overall satisfaction across key dimensions (education, delivery, facilities, equipment, food)
Identify sentiment patterns in open-text comments
Forecast future attendance trends to support operational planning

---

## 🎯 Objectives
- Analyze customer sentiment from review text
- Understand how sentiment changes over time
- Decompose time series into trend and seasonality
- Forecast future review trends using SARIMA

---

## 📊 Dataset
- File: `data/Reviews_RPC_Cleaned.xlsx`
- Contains customer reviews and timestamps
- Data was cleaned and preprocessed before analysis

---

## 🔍 Methodology

### 1. Sentiment Analysis
Notebook: Reviews_sentimentanalysis.ipynb
Analyses open-text review comments to classify sentiment and identify key themes.
Key steps:
- Text preprocessing: tokenisation, stop-word removal (including custom stop words)
- Sentiment scoring using VADER (SentimentIntensityAnalyzer from NLTK), producing a compound score per review
- Classification of reviews as Positive, Neutral, or Negative

Visualisations:
- Word clouds per review category
- Bar chart of average sentiment scores by category
- Pie chart of overall sentiment distribution
- Heatmap of average sentiment scores across categories
- Box plots of sentiment score distributions per category
- Top-20 most frequent words (after stop-word filtering)

Libraries used: pandas, numpy, matplotlib, seaborn, nltk (VADER, stopwords, punkt), wordcloud
---

### 2. Time Series Analysis
Notebook: Timeseries__Hybrid_STL___SARIMA_.ipynb
Forecasts future attendance at the Raymond Priestley Centre using a hybrid decomposition-plus-ARIMA approach.

#### Methodology — Hybrid STL + SARIMA:
#### STL Decomposition
1. STL Decomposition — Decomposes the attendance time series into Trend, Seasonal, and Residual components using statsmodels.tsa.seasonal.STL (seasonal period = 12 months)
2. Residual Stationarisation — Applies a Yeo-Johnson transformation followed by first-order differencing to make the residual component stationary
3. ACF / PACF Analysis — Used to determine ARIMA lag order
4. SARIMA on Residuals — Fits a SARIMA(10,1,10)(1,1,1,12) model on the transformed residuals
5. Forecast Recombination — Combines SARIMA residual forecasts with trend and seasonal components to produce the final attendance forecast
6. Evaluation metrics: MAE, MSE, RMSE on a held-out 20% test set
7. Future forecasting: Extended forecasts generated for the next 6 months and through to January 2025

Visualisations: Interactive Plotly charts for original data, decomposed components, in-sample forecasts, and future projections.
Libraries used: pandas, numpy, scipy (yeojohnson), statsmodels (STL, ARIMA), sklearn (MAE, MSE), matplotlib, plotly

---
## Getting Started
### Prerequisites
pip install pandas numpy matplotlib seaborn nltk wordcloud statsmodels scipy scikit-learn plotly openpyxl

Download required NLTK data (run once):
import nltk
nltk.download('vader_lexicon')
nltk.download('stopwords')
nltk.download('punkt')

### Running the Notebooks
1. Clone this repository
2. Place Reviews_RPC_Cleaned.xlsx in the same directory as the notebooks (or update the file path in the notebook cells)
3. Open and run the notebooks in Jupyter

Note: The notebooks currently reference local file paths (e.g. C:\Users\...). Update the file_path / pd.read_excel(...) call in each notebook to point to your local copy of the dataset.


## 📈 Key Findings
- Participant reviews are overwhelmingly positive, with educational delivery and food receiving particularly strong sentiment scores
- Facilities (especially shower-to-bed ratio and door noise) are the most common areas for constructive feedback
- Attendance shows a clear seasonal pattern, with peaks aligning with university term cycles
- The Hybrid STL + SARIMA model captures both the seasonal structure and longer-term trend effectively, providing reliable short-term attendance forecasts

# Acknowledgements
Data collected from participants of programmes run at the Raymond Priestley Centre, University of Birmingham. Analysis conducted as part of an MSc Business Analytics Capstone Project.

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
