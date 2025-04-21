# marketing_camp
converting a raw data file into the  clean file

## 🧹 Data Cleaning and Preparation using Python (Jupyter Notebook)

This project focuses on cleaning and preparing raw marketing campaign data using Python and pandas in a Jupyter Notebook environment.

### 📁 Dataset Used
- **File Name**: `marketing_campaign.csv`
- **Format**: Tab-separated values (`.tsv`)

---

### 🛠️ Steps Followed in the Cleaning Process

#### 1. Load the Dataset

We used pandas to read the `.csv` file with the correct delimiter:

```python
import pandas as pd

df = pd.read_csv("marketing_campaign.csv", delimiter="\t")
```

---

#### 2. Inspect the Data

We examined the structure and previewed the data:

```python
df.info()
df.head()
```

---

#### 3. Fix Column Names

Some column headers had trailing spaces, which were removed:

```python
df.columns = df.columns.str.strip()
```

---

#### 4. Handle Missing Values

All rows containing missing values (`NaN`) were removed:

```python
df = df.dropna()
```

---

#### 5. Remove Duplicate Rows

We eliminated any repeated rows in the dataset:

```python
df = df.drop_duplicates()
```

---

#### 6. Standardize Text Columns

Text fields were cleaned to ensure uniformity:

```python
df['Marital_Status'] = df['Marital_Status'].str.lower().str.strip()
df['Education'] = df['Education'].str.lower().str.strip()
```

---

#### 7. Convert Date Columns

Customer joining dates were converted to proper datetime format:

```python
df['Dt_Customer'] = pd.to_datetime(df['Dt_Customer'], dayfirst=True)
```

---

#### 8. Rename Columns (Consistent Format)

All column names were renamed to lowercase with underscores:

```python
df.columns = [col.lower().replace(" ", "_") for col in df.columns]
```

---

#### 9. Fix Data Types & Derive New Columns

We ensured numeric columns were in the correct format and added new derived columns:

```python
df['income'] = df['income'].astype(float)
df['age'] = pd.Timestamp.now().year - df['year_birth']
```

---

### ✅ Final Result

The cleaned dataset is:
- Free of missing and duplicate data
- Consistently formatted
- Ready for analysis, visualization, or modeling

---

### 💾 Optional: Save the Cleaned Dataset

```python
df.to_csv("marketing_campaign_cleaned.csv", index=False)
