EDA-TASK_7
Exploratory Data Analysis (EDA)
1. Project Overview
Exploratory Data Analysis (EDA) is a process used to analyze and understand a dataset using statistical methods and data visualization techniques. This project performs EDA on a Student Performance dataset using Python. It examines student information and their mathematics, reading, and writing scores to understand the data and identify useful patterns.

2. Objectives
To load and understand the dataset.
To inspect the structure and size of the dataset.
To identify missing values and duplicate records.
To calculate descriptive statistics.
To clean and standardize categorical data.
To calculate total marks and percentages.
To identify potential outliers using the IQR method.
To save the processed dataset as a CSV file.
3. Dataset Description
The dataset used in this project is StudentsPerformance.csv.

It contains 1,000 records and 8 columns.

The columns include:

Gender
Race/Ethnicity
Parental Level of Education
Lunch
Test Preparation Course
Math Score
Reading Score
Writing Score
The dataset provides information about students and their academic performance in three subjects.

4. Technologies Used
Python: Programming language used for data analysis.
Pandas: Used to load, manipulate, and analyze the dataset.
NumPy: Used for numerical operations.
Matplotlib: Used for data visualization.
Seaborn: Used for statistical data visualization.
Jupyter Notebook: Used to write and execute Python code.
5. Code and Output
Step 1: Import Libraries
Code:

import pandas as pd
import numpy as np
import matplotlib.pyplot as plt
import seaborn as sns
Output:

The required Python libraries are imported successfully.

Step 2: Load the Dataset
Code:

df = pd.read_csv("StudentsPerformance.csv")
Output:

The dataset is loaded into a Pandas DataFrame named df.

Step 3: Display the First Five Rows
Code:

df.head()
Output:

The first five records of the student performance dataset are displayed, including student details and subject scores.

Step 4: Check Dataset Shape
Code:

df.shape
Output:

(1000, 8)
The dataset contains 1,000 rows and 8 columns.

Step 5: Check Dataset Information
Code:

df.info()
Output:

The dataset contains 1,000 entries, with 5 categorical columns and 3 numerical columns. The numerical columns represent mathematics, reading, and writing scores.

Step 6: Check Missing Values
Code:

df.isnull().sum()
Output:

All columns contain zero missing values.

Step 7: Check Duplicate Records
Code:

df.duplicated().sum()
Output:

0
No duplicate records were found.

Step 8: Generate Descriptive Statistics
Code:

df.describe()
Output:

The descriptive statistics provide the count, mean, standard deviation, minimum, maximum, and quartiles for the three subject scores.

Subject	Average Score
Mathematics	66.09
Reading	69.17
Writing	68.05
Reading has the highest average score among the three subjects.

Step 9: Clean Categorical Data
Code:

categorical_cols = [
    'gender',
    'race/ethnicity',
    'parental level of education',
    'lunch',
    'test preparation course'
]

for col in categorical_cols:
    df[col] = df[col].astype('string').str.strip().str.lower()
Output:

Categorical values are converted to lowercase, and unnecessary spaces are removed.

Step 10: Calculate Score Statistics
Code:

score_cols = [
    'math score',
    'reading score',
    'writing score'
]

stats = df[score_cols].agg(['mean', 'median', 'std']).T

stats['Q1'] = df[score_cols].quantile(0.25)
stats['Q2'] = df[score_cols].quantile(0.50)
stats['Q3'] = df[score_cols].quantile(0.75)

print(stats.round(2))
Output:

The mean, median, standard deviation, and quartiles are calculated for each subject. These statistics help summarize student performance.

Step 11: Calculate Total Marks and Percentage
Code:

df['total mark'] = (
    df['math score']
    + df['reading score']
    + df['writing score']
)

df['percentage'] = (df['total mark'] / 300) * 100

print(df[
    ['math score', 'reading score', 'writing score',
     'total mark', 'percentage']
].head())
Output:

Math Score	Reading Score	Writing Score	Total Marks	Percentage
72	72	74	218	72.67%
69	90	88	247	82.33%
90	95	93	278	92.67%
47	57	44	148	49.33%
76	78	75	229	76.33%
Total marks are calculated out of 300, and the percentage is calculated using the total marks.

Step 12: Detect Outliers Using the IQR Method
Code:

for col in score_cols:
    Q1 = df[col].quantile(0.25)
    Q3 = df[col].quantile(0.75)

    IQR = Q3 - Q1

    lower = Q1 - 1.5 * IQR
    upper = Q3 + 1.5 * IQR

    outliers = df[(df[col] < lower) | (df[col] > upper)]

    print(col, "Outliers:", len(outliers))
Output:

The IQR method identifies potential outliers in the subject scores. The detected values can be investigated further to determine whether they are unusual observations.

Step 13: Save the Processed Dataset
Code:

df.to_csv("Student_Performance_Cleaned.csv", index=False)

print("Task completed!")
Output:

Task completed!
The processed dataset is saved as Student_Performance_Cleaned.csv.

6. Results
The EDA process successfully examined the student performance dataset. The analysis checked the dataset structure, missing values, duplicate records, descriptive statistics, and categorical values. It also calculated total marks and percentages and identified potential outliers using the IQR method.

7. Conclusion
This project demonstrates how Python can be used to perform Exploratory Data Analysis on a student performance dataset. Pandas and NumPy help with data processing and statistical analysis, while Matplotlib and Seaborn provide tools for visualization. The analysis provides a basic understanding of student scores and prepares the dataset for further analysis.

8. How to Run the Project
Install Python and the required libraries.
Place EDA_TASK_7.ipynb and StudentsPerformance.csv in the project folder.
Open the notebook using Jupyter Notebook or Google Colab.
Execute the code cells in order.
Review the outputs.
Check the generated Student_Performance_Cleaned.csv file.
Project: Exploratory Data Analysis (EDA)
Language: Python
Dataset: Student Performance Dataset

