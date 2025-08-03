# FINAL_EXAM_PROJECT-agricultural-and-rural-development-rwanda

## Project Title: Agricultural and Rural Development Analysis - Rwanda
## Prepared by: Uwase Anitha
## ID: 26945

### Project description
This project analyzes Rwanda’s agricultural and rural development indicators using data from the World Bank. The data is cleaned, enriched, and visualized to identify key trends, seasonal patterns, and insights to support sustainable development policies.

Dataset
Dataset used: Agricultural and Rural Development - Rwanda

Source: https://data.humdata.org/dataset/world-bank-agriculture-and-rural-development-indicators-for-rwanda

File location: C:/Users/HP/Desktop/agriculture_features_final.csv

## Data Processing
Loaded dataset into Jupyter Notebook
code
```
 STEP 1: Import libraries
import pandas as pd
import numpy as np
import os

# STEP 2: Define correct file path
file_path = "C:/Users/HP/Downloads/agriculture-and-rural-development_rwa.csv"

# STEP 3: Load the dataset
df = pd.read_csv(file_path)
print("✅ Loaded successfully! Shape:", df.shape)
df.head()
```
### screensshot of data loading
<img width="816" height="347" alt="load data" src="https://github.com/user-attachments/assets/c6514878-d34f-4dda-a7b5-3db8b76d7d0f" />


### Cleaned missing values and handled duplicates
codes
```
  Check missing values
print("Missing values per column:")
print(df.isnull().sum())


df = df.dropna(thresh=len(df.columns) - 2)
df = df.dropna()
print("✅ Shape after removing missing data:", df.shape)
df.head()
```
### screenshot that remove missing values
<img width="869" height="280" alt="shape  after removing missing data" src="https://github.com/user-attachments/assets/eb637681-417c-4d30-a7e9-a59c0cab47d3" />

### Transformed and pivoted data for analysis
codes
```
 Convert 'Value' to numeric to fix pivot error
df['Value'] = pd.to_numeric(df['Value'], errors='coerce')

# Pivot: years as rows, indicators as columns
df_pivot = df.pivot_table(index='Year', columns='Indicator Name', values='Value')

# Drop columns with too much missing data
df_pivot = df_pivot.dropna(thresh=5, axis=1)

# Fill missing values (optional)
df_pivot = df_pivot.fillna(method='ffill').fillna(method='bfill')

# Reset index so 'Year' becomes a column
df_pivot.reset_index(inplace=True)

print("✅ Pivoted successfully. Shape:", df_pivot.shape)
df_pivot.head()


```
## screenshoot

<img width="862" height="323" alt="pivot successfully" src="https://github.com/user-attachments/assets/26251295-4fa9-4ff3-b769-985fcbaab7c9" />

### Exported cleaned and enriched dataset as CSV
## codes
```
export_path = "C:/Users/HP/Desktop/agriculture_features_final.csv"
df_final.to_csv(export_path, index=False)
print("✅ Exported cleaned and enriched dataset to:", export_path)
```
### screenshoot of exported cleaned datasets 
<img width="885" height="148" alt="Exported  cleaned and enriched dataset power BI" src="https://github.com/user-attachments/assets/ea5cc831-661c-4870-a22b-7d03d8f3380c" />

### Power BI Report Instructions 

Visualizations to Include: 

 Custom Visual Plan for Your Dataset
 
🟢 1. Indicator Distribution
Visual: Column chart or histogram
Axis: Indicator Name
Values: Value

Insight: See how values vary across different indicators (like Agriculture land %, Employment in agri, etc.)

🟢 2. Indicator Value vs Year
Visual: Line chart
X-Axis: Year
Y-Axis: Value
Legend: Indicator Name

Insight: Analyze how key indicators changed over time.

🟢 3. Compare Two Indicators
Visual: Scatter chart
X-Axis: Value of one indicator
Y-Axis: Value of another (you may need to filter data for two specific indicators only)

Insight: Example — Does a rise in Agricultural employment correlate with an increase in Agriculture land %?

🟢 4. Monthly Trend (if month was extracted)
Visual: Line chart
X-Axis: Month
Y-Axis: Average or Total Value
Legend: Indicator Name (optional)

Insight: Discover seasonality in agriculture (if applicable).

🟢 5. Indicator Importance (by average value)
Visual: Bar chart
Axis: Indicator Name
Values: Average Value

Insight: Identify which indicators consistently report higher or lower values.

🟢 6. Region or Category-Based Analysis (Optional if you have more categorical columns)
Visual: Pie chart or stacked bar
Legend: Category (e.g., Indicator type if grouped)
Values: Count of entries or average Value

🟢 7. Map Visualization (If geolocation is available in future)
Visual: Filled map
Location: Country or region
Values: Value of selected indicator

## Contact
For questions or clarifications,
please contact Uwase Anitha.

Email: uwaseanitha1010@gmail.com
