#  Student Performance Analysis Dashboard

An end-to-end data analysis project using **Microsoft Excel and Power BI** to clean, analyze, and visualize student performance data.

---

##  Project Overview

This project analyzes student performance data and presents the results through an interactive **Power BI dashboard**.

The project follows a complete data analyst workflow:

**Raw Data → Data Cleaning in Excel → Data Preparation → Power BI Analysis → DAX Measures → Dashboard → Insights**

The dataset contains information about students' gender, race/ethnicity, parental education, lunch type, test preparation, and scores in mathematics, reading, and writing.

The main objective is to identify patterns and relationships associated with student performance.

---

##  Project Objectives

The analysis aims to answer the following questions:

- How is student performance distributed?
- Is completing a test preparation course associated with better performance?
- How does good-performance rate vary by parental education level?
- How does good-performance rate vary by lunch type?
- How do average subject scores differ by gender?
- How do average subject scores differ across race/ethnicity groups?
- How strongly are mathematics, reading, and writing scores correlated?

---

#  Dataset

The original dataset contains:

- **1,005 records**
- **8 main columns**

### Main Variables

| Column | Description |
|---|---|
| `gender` | Student gender |
| `race/ethnicity` | Race/ethnicity group |
| `parental level of education` | Highest parental education level |
| `lunch` | Lunch category |
| `test preparation course` | Whether the student completed the preparation course |
| `math score` | Mathematics score |
| `reading score` | Reading score |
| `writing score` | Writing score |

After the cleaning process, the final dataset contains **1,000 records**.

---

#  Data Cleaning in Excel

The raw dataset was first cleaned and prepared using **Microsoft Excel** before being imported into Power BI.

The purpose of the cleaning process was to improve data quality while preserving genuine missing information.

## 1. Data Quality Inspection

The raw data was inspected to identify:

- Missing values
- Duplicate records
- Inconsistent capitalization
- Leading and trailing spaces
- Typographical errors
- Invalid or impossible score values

---

## 2. Standardizing Categorical Data

Inconsistent categorical values were standardized so that identical categories would not be treated as separate groups during analysis.

Examples included:

| Original value | Cleaned value |
|---|---|
| `Female` / `female` | `female` |
| `Male` / `male` | `male` |
| `STANDARD` / `standard` | `standard` |
| `FREE/REDUCED` / `free/reduced` | `free/reduced` |
| `goup B` | `group B` |

Unnecessary leading and trailing spaces were also removed from categorical values.

---

## 3. Handling Invalid Scores

The `math score` column contained values outside the expected score range.

These invalid values were identified and converted to blank values rather than being treated as legitimate scores.

This prevents invalid observations from affecting:

- Average scores
- Performance classification
- Dashboard calculations

---

## 4. Handling Missing Values

Missing values were **not artificially filled** when no reliable information was available.

For example:

- Missing gender values were retained as missing.
- Missing subject scores were retained as missing.

No assumptions were made to invent missing information.

Students with insufficient score information were instead classified as:

**`insufficient data`**

This approach preserves the integrity of the original data.

---

## 5. Removing Duplicate Records

Duplicate records were identified and removed during the cleaning process.

The raw dataset contained:

**1,005 records**

After removing:

**5 duplicate records**

the cleaned dataset contained:

**1,000 records**

---

## 6. Creating the Performance Classification

A new `performance` column was created in Excel to categorize students according to their available subject scores.

The classification contains three categories:

- **Good Performance**
- **At Risk**
- **Insufficient Data**

Students with incomplete score information were not assigned an arbitrary performance level.

Instead, they were classified as **Insufficient Data**.

---

## 7. Final Data Preparation

After completing the cleaning process in Excel, the cleaned dataset was imported into **Power BI** for further analysis and visualization.

---

# 📊 Power BI Dashboard

The final dashboard provides an overview of student performance and explores several factors associated with it.

![Student Performance Dashboard](<img width="1117" height="736" alt="Student_Analysis_Dashboard" src="https://github.com/user-attachments/assets/5d681f7e-b6b0-474a-8d80-2f90aa0f41cd" />
)

---

##  Dashboard Components

### 1. Student Performance Distribution

Shows the percentage of students classified as:

- Good Performance
- At Risk


The dashboard shows that approximately **79% of students are classified as good performers**.

---

### 2. Number of Students

A KPI card displays the total number of students included in the cleaned dataset:

**1,000 students**

---

### 3. Good Performance Rate

A KPI card displays the proportion of students classified as good performers:

**79%**

---

### 4. Good Performance Rate by Test Preparation

This visual compares the proportion of good performers between students who:

- Completed the test preparation course
- Did not complete the course

The analysis shows a higher good-performance rate among students who completed the preparation course.

Approximately:

- **88%** among students who completed the course
- **74%** among students who did not

This indicates an **association** between test preparation and student performance.

It does **not** establish that the preparation course directly caused the difference.

---

### 5. Good Performance Rate by Parent Education

This visual compares the proportion of good performers across different parental education levels.

The analysis suggests that good-performance rates tend to be higher among students whose parents have higher levels of education.


---

### 6. Good Performance Rate by Lunch

This visual compares good-performance rates between the two lunch categories.

The dashboard shows a higher good-performance rate among students in the `standard` lunch category compared with students in the `free/reduced` category.

---

### 7. Average Subject Scores by Gender

The dashboard compares average:

- Mathematics score
- Reading score
- Writing score

between male and female students.

The analysis shows an interesting pattern:

- Male students have a higher average **math score**
- Female students have higher average **reading and writing scores**

---

### 8. Average Subject Scores by Race/Ethnicity

This visual compares average mathematics, reading, and writing scores across the different race/ethnicity groups.

It allows differences in subject performance between groups to be explored.

---

### 9. Correlation Between Subjects

The project also examines the relationships between the three subject scores.


The strongest relationship is between **reading and writing**, with a correlation of approximately **0.95**.

This indicates a very strong positive relationship between the two scores.

---

#  Key Insights

Several patterns can be observed from the analysis.

### Overall Performance

Approximately **79% of students** are classified as good performers, while approximately **20%** are classified as at risk.

### Test Preparation

Students who completed the test preparation course have a higher good-performance rate than students who did not complete it.

### Gender

Performance differs depending on the subject:

- Math performance is higher among male students.
- Reading and writing performance is higher among female students.

### Reading & Writing

Reading and writing scores have a particularly strong positive correlation:

**r = 0.95**

Students who perform well in reading also tend to perform well in writing.

### Parent Education

Higher parental education levels are generally associated with higher good-performance rates.

### Lunch

Students in the standard lunch category have a higher good-performance rate than students in the free/reduced category.

---

#  DAX

Several DAX measures were created in Power BI to support the dashboard.

For example, the **Good Performance Rate** was calculated using:

```DAX
Good Performers % =
DIVIDE(
    CALCULATE(
        COUNTROWS(StudentsPerformance_messy),
        StudentsPerformance_messy[performance] = "good performance"
    ),
    COUNTROWS(StudentsPerformance_messy),
    0
)
