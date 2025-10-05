# 🚲 Ford GoBike / Bay Wheels Trip Data Analysis (Feb 2019)  
**by Abdullah Altamimi**

This repository contains two Jupyter notebooks that explore **183,412 bike trips** from the San Francisco Bay Area bike-share system (February 2019).  
- **Part I — Dataset Exploration:** end-to-end wrangling and univariate/bivariate/multivariate EDA.  
- **Part II — Focused Investigation:** concise analysis around rider demographics, time, and duration patterns.

---

## 📑 Table of Contents
1. [Data & Scope](#data--scope)  
2. [Part I — Dataset Exploration](#part-i--dataset-exploration)  
3. [Part II — Focused Investigation](#part-ii--focused-investigation)  
4. [Cleaning & Feature Engineering](#cleaning--feature-engineering)  
5. [Key Visuals](#key-visuals)  
6. [Notes & Next Steps](#notes--next-steps)  
7. [Summary](#summary)

---

## Data & Scope
**File:** `201902-fordgobike-tripdata.csv`  
**Rows:** 183,412 **Columns:** 16

**Core variables**
- `duration_sec` (trip duration, seconds)
- `start_time`, `end_time` (timestamps)  
- Station IDs, names, and coordinates (start/end)
- `bike_id`, `user_type` (Customer/Subscriber)
- `member_birth_year`, `member_gender`
- **Derived:** `start_day`, `start_month`, `start_hr`, `end_day`, `end_month`, `end_hr`

---

## Part I — Dataset Exploration
**Notebook:** `part1_exploration.ipynb`

**Goals**
- Inspect structure, types, and missingness.
- Clean and transform time and ID fields.
- Explore **who rides**, **when they ride**, and **how long** they ride.
- Analyze relationships across **gender**, **birth year (age)**, **weekday**, and **duration**.

**Highlights**
- **Gender mix:** ~**74.6% male**, ~23.3% female (others minimal).  
- **Weekday usage:** **Thursday highest**, **Saturday lowest** (commute-leaning behavior).  
- **Age band:** majority born **1980–1997** (≈ ages 27–44 in 2019).  
- **Duration vs. age:** younger riders take **longer trips** on average.  
- **Outliers:** long duration outliers across genders → prefer robust stats (median/IQR) or transforms.

---

## Part II — Focused Investigation
**Notebook:** `part2_investigation.ipynb`

**Questions**
1. **Distribution of rides by gender** (counts + percentages).  
2. **Relationship between rider birth year and ride duration** (scatter).  
3. **Average ride duration by gender across weekdays** (FacetGrid bar plots).

**Findings**
- **Gender distribution:** males represent **~74.6%** of riders.  
- **Birth year vs. duration:** **inverse relation** (younger → longer durations).  
- **By weekday & gender:** higher male averages on **Thu/Sat**; female averages peak on **Mon/Sun**; “Other” varies mid-week.

---

## Cleaning & Feature Engineering
- **Null handling:** rows with nulls in key fields dropped for a consistent analysis base.  
- **Type corrections:**  
  - `start_time`, `end_time` → `datetime`
  - `start_station_id`, `end_station_id`, `member_birth_year` → numeric  
- **Derived temporal features:** `start_day`, `start_month`, `start_hr`, `end_day`, `end_month`, `end_hr`.

> Tip: assign with `.loc` to avoid `SettingWithCopyWarning`, e.g.  
> `df_clean.loc[:, "start_time"] = pd.to_datetime(df_clean["start_time"])`

---

## Key Visuals
You can include visuals in the README (optional):

- **Gender share of rides**  
  <img width="720" height="542" alt="image" src="https://github.com/user-attachments/assets/459ba8a6-2d33-4cfc-868a-41122b40fae3" />

- **Rides by weekday (ordered Mon→Sun)**  
  <img width="585" height="425" alt="image" src="https://github.com/user-attachments/assets/008e9e26-ac7e-4c88-a2fe-61bb3c893c76" />

- **Birth year histogram**  
 <img width="568" height="410" alt="image" src="https://github.com/user-attachments/assets/e98a0bb4-9141-4d61-bcaa-2118d39e6cc9" />

- **Duration by gender (boxplot)**  
  <img width="575" height="433" alt="image" src="https://github.com/user-attachments/assets/24353ba9-9a11-424d-a30f-825d02bdbd90" />


- **Start hour vs duration (heatmap)**  
  <img width="587" height="430" alt="image" src="https://github.com/user-attachments/assets/a985da9e-8029-498c-b059-2d3c9e65e04d" />

- **Birth year vs duration (scatter)**  
  <img width="587" height="431" alt="image" src="https://github.com/user-attachments/assets/e7a6c4d4-5e5b-435d-a3a0-e105ba08e0ce" />

- **FacetGrid: avg duration by weekday & gender**  
  <img width="905" height="236" alt="image" src="https://github.com/user-attachments/assets/02375f32-7be7-4aff-9664-f82992352d78" />


---

## Notes & Next Steps
- **Bias from dropping nulls:** demographics could be under/over-represented; consider imputation or sensitivity analysis.  
- **Outliers:** cap/extreme filtering or log transform `duration_sec` for modeling.  
- **Suggested extensions:**
  - Compare **Subscribers vs Customers** by time of day & duration.  
  - **Spatial** flows and hotspot mapping (station pairs, kernel density).  
  - **Seasonality** beyond February (if additional months available).  
  - Predictive models for **duration** or **ride probability** by attributes.

---

## Summary
Across both notebooks, the Ford GoBike/Bay Wheels data show a **weekday-centric** usage pattern, dominated by **male riders (~74.6%)**, with the **largest cohort aged 27–44**. **Younger riders** tend to record **longer durations**, and duration density is highest **between ~10:00 and 17:00**. Gender-weekday interactions reveal **different average duration peaks** (e.g., males on Thu/Sat; females on Mon/Sun). These insights can guide **operational planning** (bike rebalancing, staffing), **product decisions** (membership incentives), and future **spatiotemporal analyses**.
