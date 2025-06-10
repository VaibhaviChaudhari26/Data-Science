# A2 - Data Wrangling-2

✅ Tested and working as intended.

---

## Pre-requisites

- Install required libraries: `pandas` & `numpy`

```shell
pip install pandas numpy
```

- Dataset generated, not imported.

---

## Code blocks

1. Import libraries:

```python3
import pandas as pd
# import pandas as shriniwas
import numpy as np
```

2. Generate random data:

```python3
# Generate data
np.random.seed(50)    #for consistency

data = {
    'Student_id': range(1, 51),
    'Name': ['Student_' + str(i) for i in range(1, 51)],
    'Age': np.random.randint(18, 25, size=50),
    'Gender': np.random.choice(['Male', 'Female'], size=50),
    'Scores': [np.random.randint(50, 100, size=3).tolist() for _ in range(50)],
    'Attendance': np.random.randint(20,100,size=50),
    'Grade': np.random.choice(['A', 'B', 'C', 'D', 'F'], size=50)
}
```

> [!NOTE]
> If you wish to enter data manually, here's an example of how to do so:

```python3
data = {
    'Student_id': [1,2,3,4,5,6,7,8,9,10],
    'Name': ['Ayan', 'Priya', 'Sahil', 'Riya', 'Kunal', 'Tanya', 'Rahul', 'Anjali', 'Raj', 'Neha'],
    'Age': [18, 20, 21, 22, 25, 18, 18, 19, 23, 24],
    'Gender': ['Female', 'Male', 'Female', 'Female', 'Male', 'Male', 'Female', 'Male', 'Male', 'Female'],
    'Scores': [[64, 54, 72], [93, 69, 82], [87, 90, 80], [94, 93, 85], [88, 77, 78], [81, 90, 65], [55, 97, 54], [54, 68, 97], [92, 67, 76],
 [58, 96, 61]],
    'Attendance': [92, 95, 85, 88, 96, 80, 97, 78, 93, 89],
    'Grade': ['B', 'C', 'F', 'C', 'F', 'D', 'D', 'C', 'C', 'A']
}
```

3. Import data into DataFrame:

```python3
df = pd.DataFrame(data)
df.head() # Print first 5 rows
```

4. Assign grades:

```python3
def assign_grade(scores):
    avg_score = np.mean(scores)

    if avg_score > 90:
        return 'A'
    elif avg_score > 80:
        return 'B'
    elif avg_score > 70:
        return 'C'
    elif avg_score > 60:
        return 'D'
    else:
        return 'F'

df['Grade'] = df['Scores'].apply(assign_grade)
```

5. Introduce missing + invalid values and inconsistencies:

```python3
df = pd.DataFrame(data)
df.loc[8, 'Age'] = np.nan
df.loc[29, 'Age'] = np.nan
df.loc[35, 'Age'] = np.nan
df.loc[11, 'Scores'] = None
df.loc[19, 'Scores'] = None
df.loc[9, 'Attendance'] = 105   # invalid percentage
df.loc[15, 'Grade'] = 'Z'   # invalid grade
df.head(20) # Print first 20 rows
```

6. Locating & printing missing/invalid values:

```python3
missing_values = df.isnull().sum()    #check missing values
invalid_attendance = df[(df['Attendance'] < 0) | (df['Attendance'] > 100)]
invalid_grades = df[~df['Grade'].isin(['A', 'B', 'C', 'D', 'F'])]

print("Missing values:\n", missing_values)
print("Invalid attendance:\n", invalid_attendance)
print("Invalid grades:\n", invalid_grades)
```

7. Handling missing/invalid values:

```python3
df['Age'] = df['Age'].fillna(df['Age'].median())    #fill by median
df['Attendance'] = df['Attendance'].apply(lambda x: 100 if x > 100 else (0 if x < 0 else x))

def handle_invalid_scores(scores):
    if scores is None:
        return [0, 0, 0]

    return [max(0, min(100, score)) for score in scores]

df['Scores'] = df['Scores'].apply(handle_invalid_scores)
df['Grade'] = df['Scores'].apply(assign_grade)
df['Grade'] = df['Grade'].apply(lambda x: x if x in ['A', 'B', 'C', 'D', 'F'] else 'F')
df.head(20) # Print first 20 rows
```

8. Adding outiers:

```python3
df.loc[5, 'Age'] = 35
df.loc[5, 'Age'] = 50
df.loc[5, 'Age'] = 65
df.loc[10, 'Attendance'] = 200
df.loc[12, 'Attendance'] = 175
df.loc[12, 'Attendance'] = 166

print("DataFrame with Outliers:")
print(df.iloc[5:20])
```

9. Handling outliers:

```python3
def handle_outliers_iqr(df, column):
    Q1 = df[column].quantile(0.25)
    Q3 = df[column].quantile(0.75)

    IQR = Q3 - Q1

    lower_bound = Q1 - 1.5 * IQR
    upper_bound = Q3 + 1.5 * IQR

    df[column] = df[column].apply(lambda x: upper_bound if x > upper_bound else (lower_bound if x < lower_bound else x))

handle_outliers_iqr(df, 'Age')
handle_outliers_iqr(df, 'Attendance')

print(df.iloc[5:20])
```

10. Data transformation using min-max scaling:

```python3
df['Scaled_Attendance'] = (df['Attendance'] - df['Attendance'].min()) / (df['Attendance'].max() - df['Attendance'].min())

print("DataFrame with Min-Max Scaling on 'Attendance':")
print(df[['Attendance', 'Scaled_Attendance']].head(20))
```

---
