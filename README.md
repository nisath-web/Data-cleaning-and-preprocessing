Experiment No. 1: Data Cleaning and Preprocessing
Aim
To perform data cleaning and preprocessing on a business dataset using Python libraries for better data quality and analysis readiness.

Dataset
The dataset used for this experiment is heartdisease.csv. It contains medical and demographic information related to heart disease patients.

The dataset is opened and analyzed using Jupyter Notebook to study its data structure, identify data types, and perform basic statistical analysis for data-cleaning and preprocessing purposes.

Algorithm
Import essential Python libraries.
Load the dataset using Pandas.
View the dataset structure, data types, and memory usage.
Check for missing values and duplicates.
Perform data summary statistics using describe().
View initial and final records using head() and tail().
Sort and group the data based on key attributes.
Rename columns or modify data where necessary.
Save the cleaned dataset for further analysis.
Functions and Methods Used in the Experiment
1. Data Loading and Basic Exploration
Function / Method Description
---------------------- ------------------------------------------------------
pd.read_csv() Reads a CSV file into a Pandas DataFrame.
df.info() Displays column names, data types, and memory usage.
df.dtypes Returns the data types of all columns.
df['column'].dtype Returns the data type of a specific column.
df.describe() Provides summary statistics for numerical columns.
df.head() Displays the first 5 rows of the DataFrame.
df.tail() Displays the last 5 rows of the DataFrame.\

2. Sorting and Grouping
Function / Method Description

df.sort_values() Sorts the DataFrame by one or more columns.
df.groupby() Groups data based on one or more columns.
groupby.sum() Returns the sum for each group.
groupby.mean() Returns the mean for each group.
groupby.median() Returns the median for each group.
groupby.max() Returns the maximum value in each group.
groupby.min() Returns the minimum value in each group.

3. Data Summary and Manipulation
Function / Method Description

df.mean() Calculates the mean for all numeric columns.
df.rename() Renames columns in the DataFrame.

4. Optional Additions
Function / Method Description

df.isnull().sum() Checks for missing values in each column.
df.duplicated().sum() Counts duplicate rows.
df.dropna() Removes rows containing missing values.
df.fillna() Fills missing values with a specified value.
df.drop_duplicates() Removes duplicate rows.
df.shape Returns the number of rows and columns.
df.columns Lists column names in the DataFrame.

Program & Output
import pandas as pd
import numpy as np

# Load dataset
df = pd.read_csv("heartdisease.csv")

# Display dataset information
print("Dataset Information:")
df.info()

# Display data types
print("\nData Types:")
print(df.dtypes)

# Display first five records
print("\nFirst Five Records:")
print(df.head())

# Display last five records
print("\nLast Five Records:")
print(df.tail())

# Display dataset shape
print("\nDataset Shape:")
print(df.shape)

# Display column names
print("\nColumn Names:")
print(df.columns)

# Check missing values
print("\nMissing Values:")
print(df.isnull().sum())

# Check duplicate records
print("\nDuplicate Records:")
print(df.duplicated().sum())

# Display statistical summary
print("\nStatistical Summary:")
print(df.describe())

# Remove duplicate records
df = df.drop_duplicates()

# Fill missing numerical values with column mean
for col in df.select_dtypes(include=np.number).columns:
    df[col] = df[col].fillna(df[col].mean())

# Fill missing categorical values with mode
for col in df.select_dtypes(include='object').columns:
    df[col] = df[col].fillna(df[col].mode()[0])

# Sort data by age if available
if 'age' in df.columns:
    df = df.sort_values(by='age')

# Group data by sex if available
if 'sex' in df.columns:
    print("\nGroup By Sex:")
    print(df.groupby('sex').mean(numeric_only=True))

# Calculate mean of numerical columns
print("\nMean Values:")
print(df.mean(numeric_only=True))

# Rename columns
df = df.rename(columns={'age': 'Age'})

# Save cleaned dataset
df.to_csv("cleaned_heartdisease.csv", index=False)

print("\nCleaned Dataset:")
print(df.head())

print("\nCleaned Dataset Shape:")
print(df.shape)

print("\nCleaned dataset saved successfully!")
OUTPUT
Dataset Information:
<class 'pandas.core.frame.DataFrame'>
RangeIndex: 250 entries, 0 to 249
Data columns (total 17 columns):
 #   Column           Non-Null Count  Dtype  
---  ------           --------------  -----  
 0   S. No            250 non-null    int64  
 1   Gender           250 non-null    object 
 2   Age              250 non-null    int64  
 3   Education        250 non-null    int64  
 4   currentsmoker    250 non-null    int64  
 5   Cigsperday       250 non-null    int64  
 6   BPMeds           250 non-null    int64  
 7   Prevalentstroke  250 non-null    int64  
 8   PrevalentHyp     250 non-null    int64  
 9   Diabetes         250 non-null    int64  
 10  Totalcholestrol  250 non-null    int64  
 11  SysBP            250 non-null    float64
 12  DiaBP            250 non-null    float64
 13  BMI              250 non-null    float64
 14  Heartrate        250 non-null    int64  
 15  Glucose          250 non-null    int64  
 16  TenYearCHD       250 non-null    int64  
dtypes: float64(3), int64(13), object(1)
memory usage: 33.3+ KB

Data Types:
S. No                int64
Gender              object
Age                  int64
Education            int64
currentsmoker        int64
Cigsperday           int64
BPMeds               int64
Prevalentstroke      int64
PrevalentHyp         int64
Diabetes             int64
Totalcholestrol      int64
SysBP              float64
DiaBP              float64
BMI                float64
Heartrate            int64
Glucose              int64
TenYearCHD           int64
dtype: object

First Five Records:
   S. No  Gender  Age  Education  currentsmoker  Cigsperday  BPMeds  \
0      1  Female   68          1              1           3       0   
1      2  Female   58          4              1           1       0   
2      3    Male   44          2              1           6       0   
3      4    Male   37          4              1          18       0   
4      5  Female   50          1              1          24       0   

   Prevalentstroke  PrevalentHyp  Diabetes  Totalcholestrol  SysBP  DiaBP  \
0                1             0         0              237  107.8   71.2   
1                0             0         0              268  113.2   94.7   
2                0             0         0              192  132.7   94.8   
3                0             0         0              250  132.3   74.4   
4                1             0         0              202   97.5  102.6   

    BMI  Heartrate  Glucose  TenYearCHD  
0  30.9         81       70           0  
1  26.8        108       58           0  
2  30.3        104      141           0  
3  25.8         89      120           0  
4  22.2        106       84           1  

Last Five Records:
     S. No  Gender  Age  Education  currentsmoker  Cigsperday  BPMeds  \
245    246    Male   32          3              1          11       0   
246    247  Female   49          3              1          27       1   
247    248    Male   53          4              0           0       0   
248    249    Male   62          1              1          27       0   
249    250    Male   53          3              0           0       0   

     Prevalentstroke  PrevalentHyp  Diabetes  Totalcholestrol  SysBP  DiaBP  \
245                0             0         0              232  133.3   84.2   
246                0             0         0              185  136.5   85.4   
247                0             0         0              195  122.8  100.8   
248                0             0         0              246  142.6   80.0   
249                0             0         0              264  116.9   66.2   

      BMI  Heartrate  Glucose  TenYearCHD  
245  32.6         64      106           0  
246  22.3         94       58           0  
247  29.1        101       94           0  
248  25.9         96      123           0  
249  35.5         55       82           0  

Dataset Shape:
(250, 17)

Column Names:
Index(['S. No', 'Gender', 'Age', 'Education', 'currentsmoker', 'Cigsperday',
       'BPMeds', 'Prevalentstroke', 'PrevalentHyp', 'Diabetes',
       'Totalcholestrol', 'SysBP', 'DiaBP', 'BMI', 'Heartrate', 'Glucose',
       'TenYearCHD'],
      dtype='object')

Missing Values:
S. No              0
Gender             0
Age                0
Education          0
currentsmoker      0
Cigsperday         0
BPMeds             0
Prevalentstroke    0
PrevalentHyp       0
Diabetes           0
Totalcholestrol    0
SysBP              0
DiaBP              0
BMI                0
Heartrate          0
Glucose            0
TenYearCHD         0
dtype: int64

Duplicate Records:
0

Statistical Summary:
            S. No         Age  Education  currentsmoker  Cigsperday  \
count  250.000000  250.000000  250.00000     250.000000  250.000000   
mean   125.500000   50.088000    2.48000       0.456000    6.688000   
std     72.312977   12.268755    1.08735       0.499059    9.368336   
min      1.000000   30.000000    1.00000       0.000000    0.000000   
25%     63.250000   38.250000    2.00000       0.000000    0.000000   
50%    125.500000   51.500000    2.00000       0.000000    0.000000   
75%    187.750000   61.000000    3.00000       1.000000   12.000000   
max    250.000000   70.000000    4.00000       1.000000   30.000000   

           BPMeds  Prevalentstroke  PrevalentHyp    Diabetes  Totalcholestrol  \
count  250.000000       250.000000    250.000000  250.000000       250.000000   
mean     0.108000         0.024000      0.256000    0.080000       235.192000   
std      0.311003         0.153356      0.437297    0.271837        37.276498   
min      0.000000         0.000000      0.000000    0.000000       120.000000   
25%      0.000000         0.000000      0.000000    0.000000       207.250000   
50%      0.000000         0.000000      0.000000    0.000000       237.500000   
75%      0.000000         0.000000      1.000000    0.000000       260.750000   
max      1.000000         1.000000      1.000000    1.000000       320.000000   

           SysBP       DiaBP         BMI   Heartrate     Glucose  TenYearCHD  
count  250.00000  250.000000  250.000000  250.000000  250.000000  250.000000  
mean   129.42760   83.491200   26.288400   84.220000   88.012000    0.184000  
std     18.92353   11.649065    4.588731   16.377438   24.685407    0.388261  
min     85.00000   55.600000   16.000000   55.000000   45.000000    0.000000  
25%    118.02500   74.425000   23.200000   71.000000   72.000000    0.000000  
50%    129.10000   84.050000   25.950000   86.000000   89.000000    0.000000  
75%    141.75000   91.475000   29.375000   99.000000  103.000000    0.000000  
max    180.90000  114.100000   41.700000  110.000000  163.000000    1.000000  

Mean Values:
S. No              125.5000
Age                 50.0880
Education            2.4800
currentsmoker        0.4560
Cigsperday           6.6880
BPMeds               0.1080
Prevalentstroke      0.0240
PrevalentHyp         0.2560
Diabetes             0.0800
Totalcholestrol    235.1920
SysBP              129.4276
DiaBP               83.4912
BMI                 26.2884
Heartrate           84.2200
Glucose             88.0120
TenYearCHD           0.1840
dtype: float64

Cleaned Dataset:
   S. No  Gender  Age  Education  currentsmoker  Cigsperday  BPMeds  \
0      1  Female   68          1              1           3       0   
1      2  Female   58          4              1           1       0   
2      3    Male   44          2              1           6       0   
3      4    Male   37          4              1          18       0   
4      5  Female   50          1              1          24       0   

   Prevalentstroke  PrevalentHyp  Diabetes  Totalcholestrol  SysBP  DiaBP  \
0                1             0         0              237  107.8   71.2   
1                0             0         0              268  113.2   94.7   
2                0             0         0              192  132.7   94.8   
3                0             0         0              250  132.3   74.4   
4                1             0         0              202   97.5  102.6   

    BMI  Heartrate  Glucose  TenYearCHD  
0  30.9         81       70           0  
1  26.8        108       58           0  
2  30.3        104      141           0  
3  25.8         89      120           0  
4  22.2        106       84           1  

Cleaned Dataset Shape:
(250, 17)

Cleaned dataset saved successfully!
Result
Thus, the data cleaning and preprocessing program was successfully implemented using Python and Pandas. The heart disease dataset was loaded, explored, checked for missing values and duplicates, cleaned, sorted, grouped, and summarized. Finally, the cleaned dataset was saved as cleaned_heartdisease.csv for further analysis.

Releases
No releases published
Create a new release
Packages
No packages published
Publish your first package
Contributors
No contributors
