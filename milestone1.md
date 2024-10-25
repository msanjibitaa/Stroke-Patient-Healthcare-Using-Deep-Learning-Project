# Import required library
# We import the pandas library to leverage its powerful data manipulation and analysis capabilities.
import pandas as pd
<br>
<br>
# Load dataset
# This line loads the dataset into a pandas DataFrame. The dataset is assumed to be in cvs format.
df = pd.read_csv('dataset/data.csv')
<br><br>
# Data Exploration

## 1.Basic Exploration
### Basic statistical description of numerical data:
# We generate descriptive statistics for numerical columns to understand the data's distribution, central tendencies, and variability.
print(df.describe())
print("Basic statistical description of numerical data:")
<br><br>
### Dataset information (columns, types, and non-null counts):
# This provides an overview of the DataFrame's structure, including the data types and the number of non-null entries, which helps identify potential data issues.
print("\nDataset information (columns, types, and non-null counts):")
print(df.info())
<br><br>
### Shape of the dataset (rows, columns):
# Knowing the dimensions of the dataset is crucial for understanding its size and the complexity of any analyses we plan to perform.
print("\nShape of the dataset (rows, columns):")
print(df.shape)
<br><br>
### Basic statistical description of categorical data:
# This step gives insight into categorical variables, revealing the number of unique entries and their frequency, which aids in understanding the dataset's categorical distribution.
print("\nBasic statistical description of categorical data:")
print(df.describe(include="object'))
<br><br>
## 2. Unique Value and Null Value Analysis

### Unique values in 'gender' column:
# Identifying unique values in categorical columns like 'gender' is important for understanding the diversity of the dataset and ensuring the data is clean.
print("\nUnique values in 'gender' column:")
gender_unique = df['gender].unique()
<br><br>
### Unique values in 'smoking_status' column:
# Similarly, checking for unique values in 'smoking_status' helps us ensure that the data is properly categorized and identify any potential outliers or errors.
print("\nUnique values in 'smoking_status' column:")
smoking_status_unique = df['smoking_status'].unique()
<br><br>
### Check for null values in the dataset:
# Understanding the presence of null values is criticaal because missing data can skew analysis and lead to misleading coclusion.
null_values = df.isnull().sum()
print("\nNull values in each column:")
print(null_values)
<br><br>
### Percentage of null values in each column:
# Calculating the percentage of nulls helps prioritize which columns need attention based on the extent of missing data.
null_percentage = df.isnull().mean() * 100
print("\nPercentage of null values in each column:")
print(null_percentage)
<br><br>
##  3. Observations

### Observation 1: Dataset dimensions
# Reporting the dimensions helps contextualize the size of the dataset for analysis.
print(f'1. The dataset contains {df.shape[0]} rows and {df.shape[1]} columns.")
<br><br>
### Observation 2: Missing values in 'bmi' column
# Reporting missing values specifically for 'bmi' highlights potential issues in this critical health metric.
missing_bmi_count = null_values['bmi']
if missing_bmi_count > 0:
print(f'2. The 'bmi' column originally contained {missing_bmi_count} missing values.")
else:
print("2. The 'bmi' column contains no missing values.")
<br><br>
### Observation 3: Unique values in 'gender' column
# This observation confirms the diversity of gender representation in the dataset.
print(f"3. The 'gender' column contains the following unique values: {gender_unique}")
<br><br>
### Observation 4: Unique values in 'smoking_status' column
# Undersatanding the unique smoking statuses can be crucial for health-related analysis.
print(f'4. The 'smoking_status' column contains the following unique values: {smoking_status_unique}")
<br><br>
### Observation 5: Missing data analysis
# This highlights columns needing imputation or cleaning, ensuring a more robust analysis.
print(f"5. The dataset contains missing data in the following columns (with percentages):")
print(null_percentage[null_percebtage > 0])
<br><br>
## 4. Handling Missing Values in 'bmi' Column

### Option 1: Dropping rows with missing 'bmi' values
# This option can simplify analysis but may result in loss of potentially valuable data.
df_dropped = df.dropna(subset+['bmi"])
print(f"6. After dropping rows with missing 'bmi' values, the dataset contains {df_dropped.shape[0]} rows.")
<br><br>
### Option 2: Imputing missing 'bmi' values with the mean
# Imputing with the mean retains all data points, which is often preferred, especially if missingness is minimal.
mean_bmi = df['bmi'].mean()
df['bmi'].fillna(mean_bmi, inplace=True)
print("f\nImputing missing 'bmi' values with mean value: {mean_bmi}")
<br><br>
### Check null values after imputation
#Confirming the success of imputation is crucial to ensure that our data is now complete.
null_values_after = df.isnull().sum()
print("\nNull values after imputing missing 'bmi' values:")
print(null_values_after)
<br><br>
### Observation 7: No missing values in 'bmi' column after imputation
# This final confirmation ensures we can proceed confidently with analysis.
if null_values_after['bmi'] == 0:
print("7. After imputing, the 'bmi' column has no missing values.")
<br><br>
## 5. Duplicate Rows Check
### Identify duplicate rows in the dataset:
# Identifying duplicates is vital for data integrity; duplicates can distort analysis results.
duplicates = df.duplicated().sum()
print(f"\nNumber of duplicate rows: {duplicates}")
<br><br>
## 6. Stroke Rate Analysis

### Stroke rate by gender:
#Analyzing stroke rates by gender helps uncover potential health disparities and informs targeted health interventions.
print("\nStroke rate by gender:")
print(df.groupby('gender')['stroke'].mean())
<br><br>
# Observation of stroke rate by gender:
# gender 
# Female       0.047094
# Male         0.051064
# Other        0.000000
<br><br>
### Stroke percentage by gender (relative to all stroke cases):
total = df['stroke'].sum()
strokes_gender = df[df['stroke'] == 1].groupby('gender')['stroke'].count()
stroke_per = (strokes_gender / total) * 100
print("\nStroke percentage by gender (relative to all stroke cases:"))
print(stroke_per) # Understanding the proportion of strokes by gender is essential for evaluating the impact of gender on stroke incident.
<br><br>
# Output of stroke percentage:
# gender
# Female    56.626506
# Male      43.373494
