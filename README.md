# Raymond Priestley Centre — Reviews Analysis

A data analytics project analysing participant feedback for the **Raymond Priestley Centre (RPC)**, an outdoor education and leadership development facility at the University of Birmingham. The project applies NLP-based sentiment analysis and time-series forecasting to surface actionable insights from review data.

---

## Project Overview

The Raymond Priestley Centre runs a range of residential and day programmes — leadership retreats, team-building residentials, and skills courses — primarily for University of Birmingham students and external groups. This project analyses structured review data collected from participants to:

- Understand overall satisfaction across key dimensions (education, delivery, facilities, equipment, food)
- Identify sentiment patterns in open-text comments
- Forecast future attendance trends to support operational planning

---

## Repository Structure

```
├── Reviews_RPC_Cleaned.xlsx                    # Cleaned and structured review dataset
├── Reviews_sentimentanalysis.ipynb             # Sentiment analysis notebook
├── Timeseries__Hybrid_STL___SARIMA_.ipynb      # Time-series forecasting notebook
├── img/                                        # Chart outputs
│   ├── img_attendance_original.png
│   ├── img_trend_component.png
│   ├── img_stationary_residual.png
│   ├── img_acf_pacf.png
│   ├── img_sarima_forecast.png
│   ├── img_wordcloud_recommendation.png
│   ├── img_avg_sentiment_bar.png
│   ├── img_sentiment_distribution_pie.png
│   ├── img_sentiment_heatmap.png
│   └── img_top20_words.png
└── README.md
```

> **Note:** Store all chart images in an `img/` folder at the repo root. Update the paths in this README if you use a different folder name.

---

## Dataset

**File:** `Reviews_RPC_Cleaned.xlsx`

The workbook contains five sheets:

| Sheet | Description |
|---|---|
| `Feedback_Raw` | Raw, unprocessed survey responses from multiple cohorts |
| `Feedback_Cleaned` | Cleaned and standardised feedback with dates, course names, and ratings |
| `Ratings` | Numerical ratings only (1–10 scale) across six dimensions |
| `Comments` | Open-text explanations accompanying each rating |
| `Bednights` | Aggregate visit data including group sizes and bednight counts |

**Rating dimensions collected:**
- Likelihood to recommend the RPC
- Educational value
- Educational delivery and instruction
- Facilities
- Equipment
- Food and drink

**Courses/programmes included:** MRC IMPACT, SC3, SC4, and other University of Birmingham residential programmes.

---

## Notebooks

### 1. Sentiment Analysis — `Reviews_sentimentanalysis.ipynb`

Analyses open-text review comments to classify sentiment and identify key themes.

**Key steps:**
- Text preprocessing: tokenisation, stop-word removal (including custom stop words)
- Sentiment scoring using **VADER** (`SentimentIntensityAnalyzer` from NLTK), producing a compound score per review
- Classification of reviews as **Positive**, **Neutral**, or **Negative**
- Visualisations: word clouds, bar charts, pie chart, heatmap, and word frequency histogram

**Libraries used:** `pandas`, `numpy`, `matplotlib`, `seaborn`, `nltk` (VADER, stopwords, punkt), `wordcloud`

---

### 2. Time-Series Forecasting — `Timeseries__Hybrid_STL___SARIMA_.ipynb`

Forecasts future attendance at the Raymond Priestley Centre using a hybrid decomposition-plus-ARIMA approach.

**Methodology — Hybrid STL + SARIMA:**

1. **STL Decomposition** — Decomposes the attendance time series into Trend, Seasonal, and Residual components (seasonal period = 12 months)
2. **Residual Stationarisation** — Applies a **Yeo-Johnson transformation** followed by first-order differencing
3. **ACF / PACF Analysis** — Used to determine optimal ARIMA lag order
4. **SARIMA on Residuals** — Fits a `SARIMA(10,1,10)(1,1,1,12)` model on the transformed residuals
5. **Forecast Recombination** — Combines SARIMA residual forecasts with trend and seasonal components
6. **Evaluation metrics:** MAE, MSE, RMSE on a held-out 20% test set
7. **Future forecasting:** Extended projections generated through to January 2025

**Libraries used:** `pandas`, `numpy`, `scipy` (yeojohnson), `statsmodels` (STL, ARIMA), `sklearn` (MAE, MSE), `matplotlib`, `plotly`

---

## Visualisations

### Time-Series Analysis

**Original Attendance Data**
Monthly attendance at the RPC from early 2021 to mid-2024, showing strong growth and increasing volatility in 2023–2024.

![Original Attendance Data](img/img_attendance_original.png)

---

**STL Trend Component**
The long-term upward trend extracted from the time series via STL decomposition, showing accelerating growth from 2023 onwards.

![Trend Component](img/img_trend_component.png)

---

**Stationary Residual Component**
The residual series after Yeo-Johnson transformation and first-order differencing, confirming stationarity prior to ARIMA modelling.

![Stationary Residual Component](img/img_stationary_residual.png)

---

**ACF and PACF Plots**
Autocorrelation and Partial Autocorrelation plots used to identify the lag structure for the SARIMA model.

![ACF and PACF](img/img_acf_pacf.png)

---

**Hybrid STL + SARIMA Forecast (Till January 2025)**
Final combined forecast showing training data, test set actuals, in-sample forecasts, and future projections through to January 2025.

![Hybrid STL + SARIMA Forecast](img/img_sarima_forecast.png)

---

### Sentiment Analysis

**Word Cloud — Likelihood of Recommendation**
The most frequently used words in recommendation-related comments. Dominant terms like *activities*, *experience*, *great*, *staff*, and *amazing* reflect overwhelmingly positive participant sentiment.

![Word Cloud - Likelihood of Recommendation](img/img_wordcloud_recommendation.png)

---

**Average Sentiment Scores by Category**
VADER compound sentiment scores averaged across each review category. *Likelihood of recommendation* (0.65) and *Educational delivery and instructions* (0.54) score highest; *Improvement ideas* (0.25) and *Interested for further opportunities* (0.13) are lower by nature of their content.

![Average Sentiment Scores by Category](img/img_avg_sentiment_bar.png)

---

**Overall Sentiment Distribution**
Across all open-text comments, **75.7%** are classified as Positive, **19.1%** as Neutral, and only **5.2%** as Negative — indicating a highly satisfied participant base.

![Overall Sentiment Distribution](img/img_sentiment_distribution_pie.png)

---

**Heatmap of Average Sentiment Scores Across Categories**
A colour-coded summary of VADER scores per category. *Likelihood of recommendation* (0.66) and *Educational delivery and instructions* (0.54) are the strongest; *Interested for further opportunities* (0.13) is the lowest, consistent with that category capturing more tentative or conditional responses.

![Sentiment Heatmap](img/img_sentiment_heatmap.png)

---

**Top 20 Most Frequent Words (Excluding Common Words)**
The most commonly used words across all review comments. *Activities* and *good* lead at ~275 occurrences each, followed by *food*, *great*, *fun*, and *time* — reinforcing the themes visible in the word cloud.

![Top 20 Most Frequent Words](img/img_top20_words.png)

---

## Getting Started

### Prerequisites

```bash
pip install pandas numpy matplotlib seaborn nltk wordcloud statsmodels scipy scikit-learn plotly openpyxl
```

Download required NLTK data (run once):

```python
import nltk
nltk.download('vader_lexicon')
nltk.download('stopwords')
nltk.download('punkt')
```

### Running the Notebooks

1. Clone this repository
2. Place `Reviews_RPC_Cleaned.xlsx` in the same directory as the notebooks (or update the file path in the notebook cells)
3. Open and run the notebooks in Jupyter:

```bash
jupyter notebook
```

> **Note:** The notebooks currently reference absolute local file paths. Update the `pd.read_excel(...)` call in each notebook to point to your local copy of the dataset before running.

---

## Key Findings

- Participant reviews are overwhelmingly **positive** — 75.7% of all comments classify as positive sentiment
- **Educational delivery and instruction** (0.54) and **likelihood of recommendation** (0.66) achieve the highest sentiment scores across all categories
- **Improvement ideas** comments — while lower in sentiment score — focus constructively on facilities (shower-to-bed ratio, door noise) and transport (need for additional vehicles)
- The most frequent words across all reviews — *activities*, *good*, *food*, *great*, *fun* — closely align with what participants value most
- Attendance shows a clear **upward trend** with strong seasonal variation, picking up sharply from mid-2023 onwards
- The Hybrid STL + SARIMA model captures both the seasonal structure and the accelerating growth trend, producing reliable short-term attendance projections through to January 2025

---

## Acknowledgements

Data collected from participants of programmes run at the **Raymond Priestley Centre**, University of Birmingham. Analysis conducted as part of an MSc Business Analytics Capstone Project.
