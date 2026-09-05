# ✈️ Hamad International Airport — Flight Delay Prediction & Analytics Dashboard

An end-to-end data analytics project combining **Python (Machine Learning)** and **Power BI** to predict and analyze flight delays at Hamad International Airport (HIA), Doha, Qatar.

---

## 📌 Project Overview

Flight delays are costly for airlines, airports, and passengers alike. This project builds a complete analytics pipeline that:

1. **Predicts** whether a flight will be delayed using a machine learning model (Python / Scikit-learn)
2. **Analyzes** delay patterns across airlines, destinations, weather conditions, and scheduling by hour/season
3. **Visualizes** everything in an interactive, multi-page Power BI dashboard styled as a dark aviation-themed report

> **Note:** The dataset is synthetically generated (see [Data](#-data) below) to simulate realistic HIA flight operations, since real operational flight data is not publicly available for scraping/download. All patterns (weather seasonality, peak-hour congestion, delay distributions) are modeled to reflect real-world airport behavior.

---

## 🎯 Business Questions Answered

- What percentage of flights are delayed, and by how much on average?
- Which airlines and destinations have the highest delay rates?
- What time of day / month sees the most delays?
- How much does weather (fog, sandstorms, thunderstorms) contribute to delays?
- Can we predict a delay *before* it happens, using scheduling and weather data?

---

## 🧠 Machine Learning Model

| Detail | Value |
|---|---|
| Model | Random Forest Classifier (Scikit-learn) |
| Target | `Is_Delayed` (binary — delay ≥ 15 minutes) |
| Features | Airline, Flight Type, Destination, Scheduled Hour, Day of Week, Month, Weather Condition, Flight Duration |
| Accuracy | 70.1% |
| Precision | 47.1% |
| Recall | 67.0% |
| F1 Score | 55.3% |

**Top predictive feature:** Weather Condition (46.7% importance) — confirming that weather is the single largest driver of flight delays at HIA, followed by scheduled hour (13.1%) and airline (9.0%).

The model was deliberately tuned with `class_weight="balanced"` to prioritize **recall** — catching as many real delays as possible is more operationally valuable than avoiding false alarms in an airport context.

---

## 📊 Power BI Dashboard

A 5-page interactive report:

| Page | Contents |
|---|---|
| **Overview** | KPI cards (Total Flights, Delayed Flights, Delay Rate, Avg Delay), monthly trend, On-Time vs Delayed breakdown |
| **Delay Analysis** | Delay heatmap (Month × Hour), top airlines/destinations by delay |
| **Weather Impact** | Delay rate by weather condition, avg delay by weather × airline, severe weather share |
| **Prediction Results** | Feature importance chart, model accuracy metrics, predicted vs. actual comparison |
| **Flight Details** | Filterable flight-level table |

Styled with a custom **dark aviation theme** (navy background, bright-blue accents) matching a custom HTML landing/cover page with animated flight-route graphics.

---

## 🗂️ Data

| File | Description | Rows |
|---|---|---|
| `hia_flights.csv` | Core flight schedule data (Sept 2025 – Feb 2026) | ~8,000 |
| `model_predictions.csv` | Row-level test-set predictions from the ML model | ~1,600 |
| `feature_importance.csv` | Feature importance scores from the trained model | 8 |

Key columns: `Flight_ID`, `Airline`, `Flight_Type`, `Destination_City`, `Scheduled_DateTime`, `Weather_Condition`, `Delay_Minutes`, `Is_Delayed`.

---

## 🛠️ Tech Stack

- **Python** — pandas, scikit-learn (data generation, model training/evaluation)
- **Power BI** — Power Query (data modeling), DAX (measures), custom HTML visuals (landing page, KPI cards)
- **Design** — custom dark theme, SVG/HTML illustrations

---

## 📁 Repository Structure

```
├── data/
│   ├── hia_flights.csv
│   ├── model_predictions.csv
│   └── feature_importance.csv
├── model/
│   └── flight_delay_model.py
├── powerbi/
│   ├── HIA_Flight_Dashboard.pbix
│   └── Hamad_Airport_Theme.json
└── README.md
```

---

## 🚀 How to Reproduce

1. Clone this repo
2. Run the model: `python model/flight_delay_model.py` (requires `pandas`, `scikit-learn`)
3. Open `powerbi/HIA_Flight_Dashboard.pbix` in Power BI Desktop
4. Import the Power BI theme: `View → Themes → Browse for themes → Hamad_Airport_Theme.json`

---

## 📈 Key Insights

- Overall delay rate: **~27.6%**, consistent with major international airport benchmarks
- **Weather is the dominant delay driver** — thunderstorms and sandstorms show the highest delay rates
- Peak congestion hours (early morning and evening banks) correlate with elevated delay risk
- Long-haul flights (6+ hours) show slightly higher delay rates than regional routes
