# Student Mental Health: International vs. Domestic Students in Japan

![Illustration of silhouetted heads](mentalhealth.jpg)

Does going to university in a different country affect your mental health? A Japanese international university surveyed its students in 2018 and published a study the following year that was approved by several ethical and regulatory boards.

The study found that international students have a higher risk of mental health difficulties than the general population, and that social connectedness (belonging to a social group) and acculturative stress (stress associated with joining a new culture) are predictive of depression.

This project explores the `students` data using **PostgreSQL** to find out whether a similar conclusion holds for international students, and whether length of stay is a contributing factor.

## Data Description

| Field Name      | Description                                        |
| --------------- | -------------------------------------------------- |
| `inter_dom`     | Types of students (international or domestic)      |
| `japanese_cate` | Japanese language proficiency                      |
| `english_cate`  | English language proficiency                       |
| `academic`      | Current academic level (undergraduate or graduate) |
| `age`           | Current age of student                             |
| `stay`          | Current length of stay in years                    |
| `todep`         | Total score of depression (PHQ-9 test)            |
| `tosc`          | Total score of social connectedness (SCS test)    |
| `toas`          | Total score of acculturative stress (ASISS test)  |

## Preview the Data

```sql
SELECT *
FROM students;
```

The table has 286 rows and 50 columns (including demographic fields, language proficiency, depression, social connectedness and acculturative stress scores, and help-seeking behaviors).

## Analysis: Mental Health Scores by Length of Stay (International Students)

```sql
SELECT
    stay,
    COUNT(*) AS count_int,
    ROUND(AVG(todep), 2) AS average_phq,
    ROUND(AVG(tosc), 2) AS average_scs,
    ROUND(AVG(toas), 2) AS average_as
FROM students
WHERE inter_dom = 'Inter'
GROUP BY stay
ORDER BY stay DESC;
```

### Results

| stay | count_int | average_phq | average_scs | average_as |
| ---: | --------: | ----------: | ----------: | ---------: |
|   10 |         1 |       13.00 |       32.00 |      50.00 |
|    8 |         1 |       10.00 |       44.00 |      65.00 |
|    7 |         1 |        4.00 |       48.00 |      45.00 |
|    6 |         3 |        6.00 |       38.00 |      58.67 |
|    5 |         1 |        0.00 |       34.00 |      91.00 |
|    4 |        14 |        8.57 |       33.93 |      87.71 |
|    3 |        46 |        9.09 |       37.13 |      78.00 |
|    2 |        39 |        8.28 |       37.08 |      77.67 |
|    1 |        95 |        7.48 |       38.11 |      72.80 |

## Key Observations

- Most international students in the sample have stayed only 1–3 years (180 of 201 with a recorded stay), so results for longer stays (5+ years) rest on very few students and should be interpreted cautiously.
- Average depression scores (PHQ-9) are highest for stays of 3 years (9.09) and lowest for 1 year (7.48) among groups with reasonable sample sizes, suggesting a slight rise in depression scores after the first year.
- Average acculturative stress (ASISS) peaks at 4 years (87.71) and is lowest for the 1-year group (72.80) among larger groups.
- Average social connectedness (SCS) is fairly flat across the larger groups (about 34–38).

## Tools

- PostgreSQL
- Jupyter Notebook (DataCamp Workspace)
