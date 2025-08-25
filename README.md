# Factors-That-Fuel-Student-Performance
This project examines the factors that influence student performance using SQL. By analyzing study hours, extracurricular activities, teacher quality, and habits like sleep and attendance, it identifies key drivers of exam success and ranks students to provide actionable insights for educators and learners.
<br>
<br>

## Project Overview

In today’s fast-paced educational landscape, understanding the elements that shape student success is crucial. Just as a transport system must adapt to serve the needs of a city, schools and educators must adapt to support their students. This project examines a dataset that includes variables such as study hours, extracurricular activities, sleep patterns, attendance, and tutoring sessions to identify the strongest drivers of exam performance.

The analysis focuses on identifying whether study habits and extracurricular activities directly influence performance, whether there is an optimal range of study hours for success, and how students compare to their peers through ranking. By drawing insights from this dataset, we aim to provide useful findings for students, teachers, and policymakers.
<br>
<br>

## Objective / Key Questions

* Do more study hours and extracurricular activities lead to better scores?
* Is there a sweet spot for study hours that maximizes exam performance?
* How can we rank students by performance without revealing exam scores?
<br>

## Dataset

* **Source**: Student performance dataset (synthetic educational data for analysis).
* **Table**: `student_performance`
* **Structure**:
  
| Column                      | Definition                                     | Data type |
| --------------------------- | ---------------------------------------------- | --------- |
| attendance                  | Percentage of classes attended                 | float     |
| extracurricular\_activities | Participation in extracurricular activities    | varchar   |
| sleep\_hours                | Average number of hours of sleep per night     | float     |
| tutoring\_sessions          | Number of tutoring sessions attended per month | integer   |
| teacher\_quality            | Quality of the teachers (Low/Medium/High)      | varchar   |
| exam\_score                 | Final exam score                               | float     |

* **Sample Preview Query**:
```
sql

SELECT *
FROM student_performance
LIMIT 10;
```
This query fetches the first 10 rows of the dataset to give us a quick preview of the data. It allows us to verify column values and ensure that the dataset is structured correctly before diving deeper.
<br>
<br>

## Tools & Skills Used

* **SQL (PostgreSQL) Concepts**: `SELECT, WHERE, AVG, SUM, GROUP BY, CASE WHEN, DENSE_RANK, ORDER BY`
* **Techniques Used**: Data exploration, Aggregation and summarization, Categorization of ranges, Ranking and comparative analysis, Insight extraction
<br>

## Analysis & Approach

### 1. Exploring the Table

```
sql

SELECT *
FROM student_performance;
```
This query retrieves all the rows and columns from the `student_performance table`. It is useful to view the dataset in its entirety, confirm data availability, and understand the distribution of values. This step ensures we are working with clean and complete data before starting the analysis.

<img width="1218" height="622" alt="image" src="https://github.com/user-attachments/assets/7a86b0af-0ae9-4ff5-8c65-fb94017c9558" />



### 2. Understanding Datatypes

```
sql

SELECT column_name, data_type
FROM information_schema.columns
WHERE table_name = 'student_performance';
```
This query checks the structure of the table by listing all column names along with their data types. It is important because knowing data types helps us choose the right SQL functions (e.g., AVG works only on numeric fields). This step validates that attributes like exam_score and hours_studied are stored correctly for analysis.

<img width="1212" height="286" alt="image" src="https://github.com/user-attachments/assets/3d8e625b-186e-4119-b860-b2643405ce0c" />



### 3. Do more study hours and extracurricular activities lead to better scores?

```
sql

SELECT 
    hours_studied,
    AVG(exam_score) AS avg_exam_score
FROM student_performance
WHERE hours_studied > 10 
  AND extracurricular_activities = 'Yes'
GROUP BY hours_studied
ORDER BY hours_studied DESC;
```
This query analyzes students who studied more than 10 hours per week and participated in extracurricular activities. It groups students by their actual hours studied and calculates the average exam score for each group. Ordering by study hours helps us observe whether increased study time with extracurricular involvement consistently results in higher performance.

<img width="1217" height="624" alt="image" src="https://github.com/user-attachments/assets/ef631be6-2319-48ae-b1a7-e4aae2e35d95" />



### 4. Is there a sweet spot for study hours?

```
sql

SELECT 
    CASE WHEN hours_studied <= 5 THEN '1-5 hours'
         WHEN hours_studied BETWEEN 6 AND 10 THEN '6-10 hours'
         WHEN hours_studied BETWEEN 11 AND 15 THEN '11-15 hours'
         WHEN hours_studied >= 16 THEN '16+ hours' END 
    AS hours_studied_range,
    AVG(exam_score) AS avg_exam_score
FROM student_performance
GROUP BY hours_studied_range
ORDER BY avg_exam_score DESC;
```
Here, study hours are categorized into ranges to determine whether there is an optimal level of study time. For each range, the average exam score is calculated, and the results are ordered by performance. This approach highlights whether studying excessively improves performance or if there’s a balanced “sweet spot” where students perform best.

<img width="1219" height="215" alt="image" src="https://github.com/user-attachments/assets/34521005-1a11-4043-b41f-e777a4a2dbd1" />



### 5. Ranking Students by Exam Performance

```
sql

SELECT 
    attendance,
    hours_studied,
    sleep_hours,
    tutoring_sessions,
    DENSE_RANK() OVER(ORDER BY exam_score DESC) AS exam_rank
FROM student_performance
ORDER BY exam_rank ASC
LIMIT 30;
```
This query assigns ranks to students based on their exam scores using `DENSE_RANK()`. The ranking is shown alongside attendance, hours studied, sleep, and tutoring sessions to give context to performance. Importantly, it allows a teacher to show students their relative position in the class without disclosing exact scores, protecting privacy while motivating learners.

<img width="1220" height="632" alt="image" src="https://github.com/user-attachments/assets/6471f4b1-48ef-4d38-8ade-a2dcf26cdc79" />
<br>
<br>

## Insights & Findings

* Students who study **more than 10 hours and participate in extracurricular activities** tend to have consistently **higher average exam scores**, highlighting the positive role of balanced engagement.
* When categorizing study hours, the **11–15 hour range often shows the highest average exam performance**, suggesting that excessive studying (16+ hours) does not necessarily guarantee better results.
* Attendance, sleep, and tutoring sessions also appear as supporting factors but do not overshadow study habits and extracurricular involvement as the strongest predictors.
* The ranking system provides teachers with a practical way to encourage healthy competition and self-awareness without compromising exam score confidentiality.
<br>

## Final Notes

This project demonstrates how SQL can uncover meaningful insights from educational datasets. By analyzing study patterns, extracurricular engagement, and lifestyle habits, we identified key drivers of student performance and ways to present rankings responsibly.

The findings emphasize the importance of a balanced approach—students benefit most not from overwork but from structured study habits combined with extracurricular activities. Educators and policymakers can use these insights to design strategies that foster sustainable academic success.
<br>
