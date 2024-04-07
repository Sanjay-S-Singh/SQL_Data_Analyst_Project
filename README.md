# Introduction
* Explore the Data Job Market: Delve into lucrative data analyst roles, uncovering 💰 top-paying positions, in-demand skills, and 📈 the intersection of high demand and high salary in data analytics.
#


# About Project

Motivated by a quest to find more about "Data Analyst" like what skills are needed, top-paying jobs, and most in-demand skills for a data analyst role, this project was born from a drive to identify top-paying roles and in-demand skills, simplifying the process for others seeking optimal career paths.

Data was sourced from my SQL Course, providing insights into job titles, salaries, locations, and crucial skills.

Key questions I aimed to address through my SQL queries include:

1. What are the top-paying data analyst jobs?
2. What skills are required for these top-paying jobs?
3. What skills are most in demand for data analysts?
4. Which skills are associated with higher salaries?
5. What are the most optimal skills to learn?
#


# Tools Used

In my comprehensive exploration of the data analyst job market, I leveraged the capabilities of several essential tools:

- SQL: The backbone of my analysis, SQL enabled me to effectively query the database and extract crucial insights.
- PostgreSQL: As the selected database management system, PostgreSQL proved instrumental in managing the vast job posting data efficiently.
- Visual Studio Code: This versatile platform served as my primary tool for database management tasks and executing SQL queries with ease.
- Git & GitHub: Vital for version control, Git, and GitHub facilitated seamless collaboration and provided a structured platform for sharing my SQL scripts and analysis, fostering teamwork and project transparency.
-  Microsoft Excel: Visualizing SQL query results, providing a user-friendly interface for data analysis and presentation.
#

# Analysis

### 1. What are the high-paying jobs of Data Analyst?


The SQL query retrieves the top-paying Data Analyst jobs, selecting job ID, company name, title, location, schedule type, average yearly salary, and posted date. It filters for Data Analyst roles with a specified location and non-null salary, sorting results by salary and limiting to the top 10 highest-paying positions.

```sql
SELECT
    job_id,
    name AS company_name,
    job_title,
    job_location,
    job_schedule_type,
    salary_year_avg,
    job_posted_date :: DATE
FROM
    job_postings_fact
LEFT JOIN company_dim
ON job_postings_fact.company_id = company_dim.company_id
WHERE
    job_title_short = 'Data Analyst' AND 
    job_location = 'Anywhere' AND
    salary_year_avg IS NOT NULL
ORDER BY salary_year_avg DESC
LIMIT 10;
```

Breakdown of the top data analyst jobs in 2023:

- Wide Salary Range: Top 10 paying data analyst roles span from $184,000 to $650,000, indicating significant salary potential in the field.
- Diverse Employers: Companies like SmartAsset, Meta, and AT&T are among those offering high salaries, showing a broad interest across different industries.
- Job Title Variety: There's a high diversity in job titles, from Data Analyst to Director of Analytics, reflecting varied roles and specializations within data analytics.

<img width="919" alt="image" src="https://github.com/Sanjay-S-Singh/SQL_Data_Analyst_Project/assets/157696369/42223c18-19bf-4044-869d-9baf8c831445">

Bar graph visualizing the salary for the top 10 salaries for data analysts; generated this graph using Excel from my SQL query results.

### 2. What are the skills required for high-paying data analyst jobs?


This SQL script fetches top-paying data analyst jobs and their required skills. It creates a CTE called "top_paying_jobs" to select job ID, company name, job title, average yearly salary, and posted date for the top 10 highest-paying data analyst positions. These are filtered based on specific criteria and sorted by salary. The main query then selects these job details along with associated skills from related tables.

```sql
WITH top_paying_jobs AS(
SELECT
    job_id,
    name AS company_name,
    job_title,
    salary_year_avg,
    job_posted_date :: DATE
FROM
    job_postings_fact
LEFT JOIN company_dim
ON job_postings_fact.company_id = company_dim.company_id
WHERE
    job_title_short = 'Data Analyst' AND 
    job_location = 'Anywhere' AND
    salary_year_avg IS NOT NULL
ORDER BY salary_year_avg DESC
LIMIT 10
)

SELECT 
    top_paying_jobs.*,
    skills
FROM top_paying_jobs
INNER JOIN skills_job_dim ON top_paying_jobs.job_id = skills_job_dim.job_id
INNER JOIN skills_dim ON skills_job_dim.skill_id = skills_dim.skill_id
ORDER BY
    salary_year_avg DESC;
```
Here's the breakdown of the most demanded skills for the top 10 highest-paying data analyst jobs in 2023:

- SQL is leading with a bold count of 8 out of 10.
- Python follows closely with a bold count of 7.
- Tableau is also highly sought after, with a bold count of 6. Other skills like R, Snowflake, Pandas, and Excel show varying degrees of demand.

<img width="961" alt="image" src="https://github.com/Sanjay-S-Singh/SQL_Data_Analyst_Project/assets/157696369/0030dc82-5e77-4632-81d6-506f6dc59d9f">

Bar graph visualizing the count of skills for the top 10 paying jobs for data analysts; generated this graph using Excel from my SQL query results.

### 3. What are the most in-demand skills for data analysts?


This SQL query identifies the most in-demand skills for data analysts. It counts the occurrences of each skill associated with data analyst positions, focusing on those with the job title 'Data Analyst'. The results are grouped by skills and ordered by demand count in descending order, limited to the top 5 most in-demand skills.

```sql
SELECT
    skills,
    count(skills_job_dim.job_id) AS demand_count
FROM job_postings_fact
INNER JOIN skills_job_dim ON job_postings_fact.job_id = skills_job_dim.job_id
INNER JOIN skills_dim ON skills_job_dim.skill_id = skills_dim.skill_id
WHERE
    job_title_short = 'Data Analyst'
GROUP BY skills
ORDER BY demand_count DESC
LIMIT 5;
```
Here's the breakdown of the most demanded skills for data analysts in 2023

SQL and Excel remain fundamental, emphasizing the need for strong foundational skills in data processing and spreadsheet manipulation.
Programming and Visualization Tools like Python, Tableau, and Power BI are essential, pointing towards the increasing importance of technical skills in data storytelling and decision support.

<img width="927" alt="image" src="https://github.com/Sanjay-S-Singh/SQL_Data_Analyst_Project/assets/157696369/01859c70-f751-4f4e-bcb2-12dce4c5598a">

The graph shows the demand for the top 5 skills in data analyst job postings.



# Insights
# What I Learned
# Conclusion
# About Me!


 
