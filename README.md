# 🎮 **Video Game Market Analysis**

## 📝 **Overview**
This project analyzes the video game market, focusing on release trends, sales by platform and genre, and regional user preferences. A thorough analysis was conducted, including data cleaning, preparation, exploratory analysis, and hypothesis testing. Insights were extracted to better understand market dynamics and growth opportunities.

---

## 📂 **Step-by-Step**

### 📥 **1. Opening and Initial Data Review**
Importing necessary libraries and loading the dataset:

```python
import pandas as pd

# Load the CSV file
df = pd.read_csv('/datasets/games.csv')

# Preview the first rows to understand the structure
print(df.head())

# Get general information about the dataset
print(df.info())
```

---

### 🛠️ **2. Data Preparation**

#### 🔄 Renaming Columns and Type Conversion
The dataset was cleaned and prepared for analysis:
```python
# Convert column names to lowercase
df.columns = df.columns.str.lower()

# Convert 'year_of_release' to numeric and 'user_score' to float
df['year_of_release'] = pd.to_numeric(df['year_of_release'], errors='coerce')
df['user_score'] = pd.to_numeric(df['user_score'], errors='coerce')
```

#### 🔧 Handling Missing Values
```python
# Replace 'TBD' with NaN in 'user_score'
df['user_score'] = df['user_score'].replace('tbd', pd.NA)

# Drop rows with missing 'year_of_release'
df_clean = df.dropna(subset=['year_of_release'])

# Check the cleaned dataset
print(df_clean.info())
```

---

### ✨ **3. Data Enrichment**

#### 📊 Adding Total Sales
A new column was added to calculate global sales:
```python
# Calculate total sales
df_clean['total_sales'] = df_clean[['na_sales', 'eu_sales', 'jp_sales', 'other_sales']].sum(axis=1)
```

---

### 📈 **4. Exploratory Data Analysis**

#### 📅 Number of Games Released Per Year
```python
# Convert years to integers
df_clean['year_of_release'] = df_clean['year_of_release'].astype(int)

# Count games released each year
release_counts = df_clean['year_of_release'].value_counts().sort_index()

# Visualize the distribution
release_counts.plot(kind='bar', title='Number of Games Released Per Year')
```

#### 💽 Sales by Platform
```python
# Aggregate sales by platform
platform_sales = df_clean.groupby('platform')['total_sales'].sum().sort_values(ascending=False)

# Visualize platform sales
platform_sales.plot(kind='bar', title='Total Sales by Platform')
```

---

### 🧪 **5. Hypothesis Testing**

#### 🎮 Comparing User Scores by Platform and Genre
```python
from scipy.stats import levene, ttest_ind

# Compare Xbox One vs. PC scores
levene_stat, levene_p = levene(xbox_one_scores, pc_scores)
equal_var = levene_p > 0.05

t_stat, p_val = ttest_ind(xbox_one_scores, pc_scores, equal_var=equal_var)
print(f"T-statistic: {t_stat}, p-value: {p_val}")
```

---

### 🏁 **6. Conclusion**

1. **Data Cleaning and Preparation:** Columns were standardized, missing values were handled, and total sales were calculated.
2. **Exploratory Analysis:** Trends in game releases, sales by platform, and genre popularity were identified.
3. **Regional Preferences:** Regional analysis revealed distinct platform and genre preferences.
4. **Hypothesis Testing:** User scores across platforms and genres were compared, providing additional insights into market dynamics.

**Recommendations:**
- Monitor emerging platform trends and prioritize popular genres in targeted regions.
- Continue evaluating user and critic scores, as they significantly impact game sales.

---

📅 **Date**: January 6, 2025  
**Author**: Francisco SLG

