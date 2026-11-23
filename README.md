# Experiment No. 1: Data Cleaning and Preprocessing

## Aim

To perform data cleaning and preprocessing on a business dataset using Python libraries for better data quality and analysis readiness.

## Dataset

The dataset used for this experiment is `heartdisease.csv`. It contains
medical and demographic information related to heart disease patients.

The dataset is opened and analyzed using Jupyter Notebook to study its
data structure, identify data types, and perform basic statistical
analysis for data-cleaning and preprocessing purposes.

## Algorithm

1.  Import essential Python libraries.
2.  Load the dataset using Pandas.
3.  View the dataset structure, data types, and memory usage.
4.  Check for missing values and duplicates.
5.  Perform data summary statistics using `describe()`.
6.  View initial and final records using `head()` and `tail()`.
7.  Sort and group the data based on key attributes.
8.  Rename columns or modify data where necessary.
9.  Save the cleaned dataset for further analysis.

## Functions and Methods Used in the Experiment

### 1. Data Loading and Basic Exploration

  Function / Method      Description  
  ---------------------- ------------------------------------------------------\
  `pd.read_csv()`        Reads a CSV file into a Pandas DataFrame.\
  `df.info()`            Displays column names, data types, and memory usage.\
  `df.dtypes`            Returns the data types of all columns.\
  `df['column'].dtype`   Returns the data type of a specific column.\
  `df.describe()`        Provides summary statistics for numerical columns.\
  `df.head()`            Displays the first 5 rows of the DataFrame.\
  `df.tail()`            Displays the last 5 rows of the DataFrame.\

### 2. Sorting and Grouping

  Function / Method    Description  
  -------------------- ---------------------------------------------  
  `df.sort_values()`   Sorts the DataFrame by one or more columns.  
  `df.groupby()`       Groups data based on one or more columns.  
  `groupby.sum()`      Returns the sum for each group.  
  `groupby.mean()`     Returns the mean for each group.  
  `groupby.median()`   Returns the median for each group.  
  `groupby.max()`      Returns the maximum value in each group.  
  `groupby.min()`      Returns the minimum value in each group.  

### 3. Data Summary and Manipulation  

  Function / Method   Description  
  ------------------- ----------------------------------------------  
  `df.mean()`         Calculates the mean for all numeric columns.  
  `df.rename()`       Renames columns in the DataFrame.  

### 4. Optional Additions  

  Function / Method         Description  
  ------------------------- ----------------------------------------------  
  `df.isnull().sum()`       Checks for missing values in each column.  
  `df.duplicated().sum()`   Counts duplicate rows.  
  `df.dropna()`             Removes rows containing missing values.  
  `df.fillna()`             Fills missing values with a specified value.  
  `df.drop_duplicates()`    Removes duplicate rows.  
  `df.shape`                Returns the number of rows and columns.  
  `df.columns`              Lists column names in the DataFrame.  

## Program & Output

# Step 1: Import Essential Libraries
import pandas as pd
import numpy as np

# Step 2: Load the Dataset
df = pd.read_csv('heartdisease.csv')

print("HEART DISEASE DATASET")
display(df)

# Step 3: View Dataset Structure and Information
print("\nDATASET INFORMATION")
df.info()

print("\nDataset Shape:", df.shape)
print("\nColumn Names:")
print(df.columns)

print("\nData Types:")
print(df.dtypes)

# Step 4: Display First and Last Five Records
print("\nFIRST FIVE RECORDS")
display(df.head())

print("\nLAST FIVE RECORDS")
display(df.tail())

# Step 5: Check Missing Values
print("\nMISSING VALUES")
print(df.isnull().sum())

print("\nTotal Missing Values:", df.isnull().sum().sum())

# Step 6: Check and Remove Duplicate Records
print("\nDUPLICATE RECORDS:", df.duplicated().sum())

df = df.drop_duplicates()

print("Shape After Removing Duplicates:", df.shape)

# Step 7: Statistical Analysis
print("\nSTATISTICAL SUMMARY")
display(df.describe())

print("\nMEAN VALUES")
display(df.mean(numeric_only=True))

print("\nMEDIAN VALUES")
display(df.median(numeric_only=True))

# Step 8: Handle Missing Values
numeric_columns = df.select_dtypes(include=np.number).columns

for col in numeric_columns:
    if df[col].isnull().any():
        df[col] = df[col].fillna(df[col].median())

categorical_columns = df.select_dtypes(exclude=np.number).columns

for col in categorical_columns:
    if df[col].isnull().any():
        df[col] = df[col].fillna(df[col].mode()[0])

print("\nMISSING VALUES AFTER CLEANING")
print(df.isnull().sum())

# Step 9: Sort the Dataset
if 'age' in df.columns:
    sorted_df = df.sort_values(by='age', ascending=True)
    print("\nDATASET SORTED BY AGE")
    display(sorted_df.head(10))

# Step 10: Group the Dataset
if 'sex' in df.columns:
    print("\nMEAN VALUES GROUPED BY GENDER")
    display(df.groupby('sex').mean(numeric_only=True))

  print("\nMAXIMUM VALUES GROUPED BY GENDER")
    display(df.groupby('sex').max(numeric_only=True))

  print("\nMINIMUM VALUES GROUPED BY GENDER")
    display(df.groupby('sex').min(numeric_only=True))

# Step 11: Rename Columns
rename_columns = {}

if 'cp' in df.columns:
    rename_columns['cp'] = 'chest_pain_type'

if 'thalach' in df.columns:
    rename_columns['thalach'] = 'maximum_heart_rate'

df = df.rename(columns=rename_columns)

print("\nUPDATED COLUMN NAMES")
print(df.columns)

# Step 12: Final Dataset Verification
print("\nFINAL DATASET INFORMATION")
df.info()

print("\nFINAL DATASET SHAPE")
print(df.shape)

print("\nREMAINING MISSING VALUES")
print(df.isnull().sum().sum())

print("\nREMAINING DUPLICATE RECORDS")
print(df.duplicated().sum())

print("\nCLEANED DATASET")
display(df.head())

# Step 13: Save the Cleaned Dataset
df.to_csv('cleaned_heartdisease.csv', index=False)

print("\nCleaned dataset successfully saved as cleaned_heartdisease.csv")

# Output

<img width="1920" height="5129" alt="image" src="https://github.com/user-attachments/assets/9ee462bc-80ed-4eb0-ab69-07816259695d" />

## Result

The data cleaning and preprocessing experiment was successfully performed using Python and Pandas. The dataset was analysed, cleaned, sorted, grouped, and saved as a cleaned CSV file for further analysis.
