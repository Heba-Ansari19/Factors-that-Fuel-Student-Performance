# Factors-that-Fuel-Student-Performance
This project examines the factors that influence student performance using SQL. By analyzing study hours, extracurricular activities, teacher quality, and habits like sleep and attendance, it identifies key drivers of exam success and ranks students to provide actionable insights for educators and learners.
<br>
<br>

## PROJECT OVERVIEW

In today’s fast-paced educational landscape, understanding the elements that shape student success is crucial. Just as a transport system must adapt to serve the needs of a city, schools and educators must adapt to support their students. This project examines a dataset that includes variables such as study hours, extracurricular activities, sleep patterns, attendance, and tutoring sessions to identify the strongest drivers of exam performance.

The analysis focuses on identifying whether study habits and extracurricular activities directly influence performance, whether there is an optimal range of study hours for success, and how students compare to their peers through ranking. By drawing insights from this dataset, we aim to provide useful findings for students, teachers, and policymakers.
<br>
<br>

## OBJECTIVE / KEY QUESTIONS

* Do more study hours and extracurricular activities lead to better scores?
* Is there a sweet spot for study hours that maximizes exam performance?
* How can we rank students by performance without revealing exam scores?
<br>
<br>

## DATASET

* Source: Student performance dataset (synthetic educational data for analysis).
* Table: student_performance
* Structure:
  
| Column                      | Definition                                     | Data type |
| --------------------------- | ---------------------------------------------- | --------- |
| attendance                  | Percentage of classes attended                 | float     |
| extracurricular\_activities | Participation in extracurricular activities    | varchar   |
| sleep\_hours                | Average number of hours of sleep per night     | float     |
| tutoring\_sessions          | Number of tutoring sessions attended per month | integer   |
| teacher\_quality            | Quality of the teachers (Low/Medium/High)      | varchar   |
| exam\_score                 | Final exam score                               | float     |

* Sample Preview Query:
```
sql

SELECT *
FROM student_performance
LIMIT 10;
```
This query fetches the first 10 rows of the dataset to give us a quick preview of the data. It allows us to verify column values and ensure that the dataset is structured correctly before diving deeper.






























