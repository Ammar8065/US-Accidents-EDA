# US Accidents EDA

## Project Overview
This project performs an Exploratory Data Analysis (EDA) on a US accidents dataset spanning 2013 to 2023. The dataset contains over 7.7 million records of accidents, with features including location, time, weather conditions, road features, and severity (rated 1 to 4, with 4 being the most severe). The goal of the EDA was to understand the patterns, distributions, and relationships in the data to inform potential modeling efforts and identify key factors contributing to accident frequency and severity.

### Dataset
- **Source**: US Accidents dataset (2013–2023)
- **Size**: ~7.7 million records
- **Key Features**:
  - `Severity`: Accident severity (1–4, with 4 being the most severe)
  - `Start_Lat`, `Start_Lng`: Geographic coordinates of the accident
  - `Start_Time`: Timestamp of the accident
  - `Weather_Condition`: Weather at the time of the accident
  - `Sunrise_Sunset`: Day or Night indicator
  - `City`, `State`: Location details
  - Road features (e.g., `Junction`, `Traffic_Signal`): Boolean indicators of road conditions
- **Class Imbalance**: Severity 2 dominates (~80%), with Severity 1 and 4 being rare (<2.6% each).

### EDA Objectives
1. Analyze the distribution of accident severity.
2. Identify temporal patterns (e.g., by hour, day of week, day/night).
3. Explore the impact of weather conditions on accident frequency and severity.
4. Investigate geospatial patterns and accident hotspots.
5. Assess the role of road features and regional differences.

### Key Findings

#### 1. Severity Distribution
- **Imbalance**: The dataset is heavily imbalanced, with ~80% of accidents being Severity 2, ~16% Severity 3, and <2.6% each for Severity 1 and 4 (see `Distribution of Accident Severity` histogram).
- **Implication**: This severe imbalance poses challenges for predictive modeling, as minority classes (Severity 1 and 4) are underrepresented.

#### 2. Temporal Patterns
- **Day of Week** (`Accidents by Day of Week` bar plot):
  - Fridays have the highest number of accidents (~1.4M), likely due to end-of-week travel or fatigue.
  - Weekends (Saturday and Sunday) have fewer accidents (~0.6M each), reflecting reduced commuting.
  - Weekdays (Monday–Thursday) show consistent accident counts (~1.2M–1.3M).
- **Hour of Day** (`Accidents by Hour of Day` bar plot):
  - Peaks during rush hours: 7–9 AM (~500K each) and 4–6 PM (~550K each), corresponding to commuting times.
  - Lowest at night (0–5 AM, ~50K–100K), due to lower traffic volume.
  - Midday (10 AM–3 PM) shows moderate accidents (~300K–400K).
- **Day vs. Night** (`Severity Distribution by Day vs. Night` stacked bar plot):
  - Daytime accidents (~4.5M) far outnumber nighttime (~1.5M), reflecting higher traffic volume.
  - Severity proportions are similar between Day and Night, suggesting time of day impacts frequency more than severity.

#### 3. Weather Conditions
- **Top Weather Conditions** (`Accidents by Weather Condition (Top 10)` bar plot):
  - Fair weather dominates (~2.73M), followed by Mostly Cloudy (~1.01M), Cloudy (~817K), and Clear (~808K).
  - Adverse conditions like Light Rain (~332K), Light Snow (~204K), and Fog (~129K) are less frequent but may pose higher risks per mile driven.
- **Severity by Weather** (`Severity Distribution by Top Weather Conditions` stacked bar plot):
  - Severity distribution is similar across weather types, with Severity 2 dominating in all conditions.
  - No strong correlation between weather and severity in raw counts, but normalization for exposure (e.g., accidents per mile driven) is needed for true risk assessment.
- **Day/Night and Weather** (`Heatmap of Accidents by Day/Night and Weather Condition`):
  - Daytime Fair weather (1.82M) and Cloudy (783K) lead, reflecting high traffic in good conditions.
  - Nighttime Fair (913K) and Cloudy (233K) also dominate, but counts are lower.
  - Adverse conditions (e.g., Fog, Light Snow) have fewer accidents but may be riskier when normalized.

#### 4. Geospatial Patterns
- **Accident Locations** (`Accident Locations by Severity (Sample)` scatter plot):
  - A 10,000-row sample shows accidents concentrated along major highways and urban areas (e.g., California, Texas, Florida, Northeast I-95 corridor).
  - High-severity accidents (Severity 3–4) are scattered, not clustered, suggesting they depend on conditions rather than location.
- **Top Cities in California** (`Top Cities with Most Accidents in California` bar plot):
  - Los Angeles (~1.5M), Sacramento (~600K), San Diego (~500K), and San Jose (~300K) are hotspots, reflecting population and traffic density.

### Visualizations
1. **Scatter Plot**: `Accident Locations by Severity (Sample)` – Geospatial distribution of accidents.
2. **Bar Plots**:
   - `Accidents by Day of Week` – Accident frequency by day.
   - `Accidents by Hour of Day` – Accident frequency by hour.
   - `Accidents by Weather Condition (Top 10)` – Frequency by weather.
   - `Top Cities with Most Accidents in California` – City-level analysis.
3. **Stacked Bar Plots**:
   - `Severity Distribution by Top Weather Conditions` – Severity breakdown by weather.
   - `Severity Distribution by Day vs. Night` – Severity by time of day.
   - `Accidents by Day/Night and Weather Condition` – Combined effect of time and weather.
4. **Heatmap**: `Heatmap of Accidents by Day/Night and Weather Condition` – Interaction between time and weather.
5. **Histogram**: `Distribution of Accident Severity` – Severity imbalance.

### Insights for Future Work
- **Temporal Features**: `Hour`, `Is_Rush_Hour` (7–9 AM, 4–6 PM), `Is_Weekend`, and `Sunrise_Sunset` are key predictors due to clear temporal patterns.
- **Weather**: Fair and Cloudy conditions dominate, but adverse conditions (Fog, Light Snow) may pose higher risks when normalized for exposure. Simplified weather categories (`Weather_Simple`) are useful.
- **Geospatial**: Urban areas (e.g., Los Angeles, Houston) are hotspots. Clustering on `Start_Lat` and `Start_Lng` could enhance modeling.
- **Severity Imbalance**: The dominance of Severity 2 (~80%) suggests a binary target (Severe [4] vs. Non-Severe [1–3]) or oversampling techniques for modeling.
- **Normalization**: Future analysis should normalize accident counts by traffic volume to assess true risk (e.g., accidents per mile driven in Fog vs. Fair weather).

### Repository Structure
- `eda_notebook.ipynb`: Jupyter Notebook containing the EDA code and visualizations.
- `visualizations/`: Folder with saved plots (e.g., `severity_distribution.png`, `accidents_by_hour.png`).
- `README.md`: This file.

### How to Run
1. Clone the repository:
   ```bash
   git clone <repository-url>
