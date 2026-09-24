# Delhivery Business Case Study — Feature Engineering & Delivery Analytics

## 📌 Project Overview

This project analyzes **Delhivery delivery and logistics data** to clean and transform raw operational data into meaningful features that support forecasting and business decision-making.

**Workflow:** Raw Data → Data Cleaning → EDA → Feature Engineering → Statistical Analysis → Business Insights → Recommendations

The project focuses on delivery performance, trip-level behavior, route characteristics, actual vs estimated performance, and geographic patterns.

## 🎯 Business Objective

The objective is to:
- Clean and sanitize the raw delivery dataset.
- Understand data quality and operational patterns.
- Engineer meaningful segment-level and trip-level features.
- Analyze delivery time and distance behavior.
- Compare actual performance with OSRM-based estimates.
- Identify important routes, locations, and route types.
- Validate key differences using statistical testing.
- Translate findings into actionable business recommendations.

## 📊 Dataset

The original dataset contains **144,867 rows and 24 columns** representing delivery trip and segment-level operational information.

Key variable groups include:

| Category | Examples |
|---|---|
| Trip identifiers | `trip_uuid`, `route_type` |
| Location | `source_center`, `destination_center`, `source_name`, `destination_name` |
| Time | `start_scan_to_end_scan`, `actual_time`, `osrm_time`, `segment_actual_time`, `segment_osrm_time` |
| Distance | `actual_distance_to_destination`, `osrm_distance`, `segment_osrm_distance` |

The analysis transforms segment-level information into a more useful **trip-level analytical dataset**.

## 🧹 Data Cleaning

The workflow includes:
- Data shape, datatype, missing-value and duplicate checks.
- Datetime conversion.
- Categorical-type conversion.
- Removal of undefined/unused operational fields.
- Missing-location handling.
- Location-name standardization.
- Extraction of state, city, place and code.
- Creation of date and time features.

### Data Quality Summary

- **Raw records:** 144,867
- **Raw columns:** 24
- **Cleaned records:** 144,316
- **Cleaned columns:** 19

## ⚙️ Feature Engineering

### Segment-Level Features

A segment is identified using:

`trip_uuid + source_center + destination_center`

Cumulative features are created for:
- `segment_actual_time`
- `segment_osrm_time`
- `segment_osrm_distance`

### Trip-Level Aggregation

Segment information is aggregated to the **trip level** using appropriate sum, first and last operations.

Additional features include:
- Source state/city/place
- Destination state/city/place
- Year, month and day
- Trip time difference
- Aggregated time and distance measures

## 🔎 Exploratory Data Analysis

The analysis covers:

### Univariate Analysis
- Delivery-time distributions
- Actual and estimated distances
- Segment-level metrics
- Route-type frequencies
- Source and destination locations

### Bivariate Analysis
Relationships between:
- Actual distance and actual time
- Actual distance and OSRM distance
- Actual time and OSRM time
- Segment OSRM time and segment OSRM distance
- Route type and delivery performance
- Geographic locations and operational metrics

## 📈 Correlation Analysis

Strong relationships are observed among several operational measures, particularly:
- Actual distance ↔ Actual time
- Actual distance ↔ OSRM distance
- Actual time ↔ OSRM time
- Segment OSRM time ↔ Segment OSRM distance

These relationships help identify useful variables for forecasting and potential feature redundancy.

## 🚨 Outlier Analysis

Outliers are identified across important time and distance variables.

Raw segment-level outliers are **not blindly removed**, because extreme observations may represent genuine operational behavior.

Instead, the workflow aggregates data to the trip level first and applies outlier treatment at the **trip level**, where observations are more meaningful for business analysis.

## 🗺️ Geographic & Route Analysis

The project analyzes:
- Source states
- Destination states
- Source cities
- Destination cities
- Source/destination corridors
- Route types

The **Bhiwandi–Mumbai corridor** receives focused analysis of delivery time and distance behavior.

## 🚚 Route Type Analysis

The dataset contains:
- **FTL — Full Truck Load**
- **Carting**

The analysis distinguishes between **row-level** and **trip-level** route distributions because multiple raw segment records can belong to one trip.

## 🧪 Statistical Hypothesis Testing

Non-parametric testing is used because the operational variables are not assumed to follow a normal distribution.

**Significance level: α = 0.10**

| # | Comparison | Test | Result |
|---|---|---|---|
| 1 | Actual Time vs OSRM Time | Mann–Whitney U | Statistically different at α = 0.10 |
| 2 | Actual Time vs Segment Actual Time | Mann–Whitney U | No statistically significant difference at α = 0.10 |
| 3 | OSRM Distance vs Segment OSRM Distance | Mann–Whitney U | Statistically different at α = 0.10 |
| 4 | OSRM Time vs Segment OSRM Time | Mann–Whitney U | No statistically significant difference at α = 0.10 |

A paired **Wilcoxon signed-rank test** is also included as a robustness check.

> **Note:** The OSRM-distance comparison has a p-value around 0.0575. It is significant at the project's 10% threshold, but not at the conventional 5% threshold.

## 💡 Key Business Insights

### 1. Route Mix
Carting is the most common route type at the trip level after the relevant aggregation and cleaning.

### 2. Geographic Concentration
Major source and destination activity is concentrated in:
- Maharashtra
- Karnataka
- Haryana

Prominent cities include:
- Bengaluru
- Mumbai
- Gurgaon

### 3. High-Activity Corridors
The analysis identifies important delivery corridors, including the **Bhiwandi–Mumbai corridor**.

### 4. Actual vs Estimated Delivery Time
Actual delivery time and OSRM-estimated time are statistically different at the selected 10% significance level, indicating that standard route-based estimates do not fully capture observed operational delivery time.

### 5. Segment-Level Time Consistency
Actual trip time and aggregated segment actual time do not show a statistically significant difference under the selected test. OSRM time and segment OSRM time likewise do not show a statistically significant difference.

## 💼 Business Recommendations

### 1. Improve ETA Prediction
Enhance ETA models by incorporating factors beyond route distance and standard travel-time estimates, such as historical route performance, traffic, delivery-center congestion, time of day and route type.

### 2. Focus on High-Volume Locations
Prioritize operational monitoring and service-quality initiatives in major locations such as Bengaluru, Mumbai and Gurgaon.

### 3. Monitor High-Activity Corridors
Track corridors such as Bhiwandi–Mumbai for recurring delays, time-distance patterns, ETA gaps and segment-level bottlenecks.

### 4. Use Trip-Level Features for Forecasting
Trip-level aggregation provides a cleaner business representation and can support future delivery-time prediction, ETA forecasting, route optimization and operational monitoring.

## 🛠️ Tools & Technologies

- Python
- Pandas
- NumPy
- Matplotlib
- Seaborn
- SciPy
- Google Colab
- GitHub

## 📓 Notebook

Complete analysis:

**`Delhivery_Business_Case_Study_Final.ipynb`**

The notebook covers raw-data inspection, cleaning, EDA, feature engineering, statistical testing, business insights and recommendations.

## 📁 Repository Structure

```text
Delhivery-Business-Case-Study/
│
├── Delhivery_Business_Case_Study_Final.ipynb
└── README.md
```

## 👩‍💻 Author

**Janhavi Shukla**

Data Analyst | Business Analytics | Python | SQL | Statistics | AI/ML

This project demonstrates an end-to-end approach to transforming raw logistics data into actionable business insights using data analysis, statistical methods and feature engineering.

## ⭐ Project Takeaway

This case study demonstrates how:

**Data Cleaning → Feature Engineering → Statistical Validation → Business Interpretation**

can transform operational logistics data into insights supporting **ETA prediction, route analysis, operational monitoring and data-driven decision-making**.
