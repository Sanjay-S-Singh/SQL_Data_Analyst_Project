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
 
# Analysis & Insights

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

### 4. What are the top skills based on salary?

The SQL code extracts the top skills based on salary for Data Analyst roles offering remote work options. It computes the average salary for each skill, filtering for positions with non-null average salaries and remote work availability. The results are then grouped by skills and sorted in descending order by average salary, presenting the top 10 skills with the highest average salaries among remote Data Analyst jobs.

```sql
SELECT
        skills,
        ROUND(AVG(salary_year_avg),0) AS avg_salary
FROM job_postings_fact
INNER JOIN skills_job_dim ON job_postings_fact.job_id = skills_job_dim.job_id
INNER JOIN skills_dim ON skills_job_dim.skill_id = skills_dim.skill_id
WHERE
    job_title_short = 'Data Analyst' AND
    salary_year_avg IS NOT NULL AND
    job_work_from_home = TRUE
GROUP BY 
    skills
ORDER BY
    avg_salary DESC
LIMIT 10;
```
An analysis of the top-paying skills for Data Analysts:

- **High Demand for Big Data & ML Skills:** Analysts proficient in big data technologies (such as PySpark and Couchbase), machine learning tools (like DataRobot and Jupyter), and Python libraries (including Pandas and NumPy) command top salaries. This reflects the industry's high valuation of data processing and predictive modeling capabilities.

- **Software Development & Deployment Proficiency:** Proficiency in development and deployment tools such as GitLab, Kubernetes, and Airflow indicates a lucrative overlap between data analysis and engineering. Skills facilitating automation and efficient data pipeline management are highly valued, contributing to competitive salaries in this domain.

- **Cloud Computing Expertise:** Expertise in cloud and data engineering tools like Elasticsearch, Databricks, and GCP highlights the growing significance of cloud-based analytics environments. Cloud proficiency significantly enhances earning potential in data analytics, emphasizing the importance of adapting to cloud technologies for data professionals.

![image](https://github.com/Sanjay-S-Singh/SQL_Data_Analyst_Project/assets/157696369/7fcb9671-5548-4574-9a2e-9b8e15dffb58)

Table of the average salary for the top 10 paying skills for data analysts.

### 5. What are the most optimal skills to learn (have high demand and a high-paying)?

Combining insights from demand and salary data, this query aimed to pinpoint skills that are both in high demand and have high salaries, offering a strategic focus for skill development.

```sql
WITH skills_demand AS(
SELECT
    skills_dim.skill_id,
    skills_dim.skills,
    count(skills_job_dim.job_id) AS demand_count
FROM job_postings_fact
INNER JOIN skills_job_dim ON job_postings_fact.job_id = skills_job_dim.job_id
INNER JOIN skills_dim ON skills_job_dim.skill_id = skills_dim.skill_id
WHERE
    job_title_short = 'Data Analyst' AND
    salary_year_avg IS NOT NULL AND
    job_work_from_home = TRUE
GROUP BY 
    skills_dim.skill_id

), average_salary AS(

SELECT
    skills_job_dim.skill_id,
    ROUND(AVG(job_postings_fact.salary_year_avg),0) AS avg_salary
FROM job_postings_fact
INNER JOIN skills_job_dim ON job_postings_fact.job_id = skills_job_dim.job_id
INNER JOIN skills_dim ON skills_job_dim.skill_id = skills_dim.skill_id
WHERE
    job_title_short = 'Data Analyst' AND
    salary_year_avg IS NOT NULL AND
    job_work_from_home = TRUE
GROUP BY 
    skills_job_dim.skill_id
)

SELECT
    skills_demand.skill_id,
    skills_demand.skills,
    demand_count,
    avg_salary
FROM
    skills_demand
INNER JOIN average_salary ON skills_demand.skill_id = average_salary.skill_id
WHERE demand_count > 20
ORDER BY
    demand_count DESC,
    avg_salary DESC
LIMIT 25;
```
Breakdown of Optimal Skills for Data Analysts in 2023:

- **High-Demand Programming Languages:** Python and R exhibit significant demand, with counts of 236 and 148 respectively. Despite their popularity, average salaries for Python ($101,397) and R ($100,499) suggest widespread proficiency.

- **Cloud Technologies:** Snowflake, Azure, AWS, and BigQuery skills are highly sought after, boasting considerable demand and relatively high average salaries. This underscores the increasing importance of cloud platforms and big data technologies in data analysis.

- **Business Intelligence Tools:** Tableau and Looker, with demand counts of 230 and 49 respectively, offer average salaries of around $99,288 and $103,795. Their prominence highlights the crucial role of data visualization and business intelligence in extracting actionable insights.

- Database Expertise: Skills in both traditional and NoSQL databases (Oracle, SQL Server, NoSQL) remain in demand, with average salaries ranging from $97,786 to $104,534. This emphasizes the enduring need for expertise in data storage, retrieval, and management.

![image](https://github.com/Sanjay-S-Singh/SQL_Data_Analyst_Project/assets/157696369/3085a653-7b63-48ce-af5c-9974e5914737)

Table of the most optimal skills for data analyst sorted by salary.
#

# What I Learned

Throughout this journey, I've honed my SQL skills to a razor-sharp edge, empowering myself with advanced techniques and strategic maneuvers:

- **Complex Query Crafting:** I've delved deep into the intricacies of SQL, mastering the art of crafting complex queries. From seamlessly merging tables to executing ninja-like maneuvers with WITH clauses, I've become adept at navigating through intricate data structures with precision and finesse.

- **Data Aggregation Mastery:** I've become intimately familiar with the power of data aggregation techniques. Whether it's harnessing the capabilities of GROUP BY to segment and summarize data or wielding aggregate functions like COUNT() and AVG() to derive meaningful insights, I've transformed these tools into invaluable assets in my analytical arsenal.

- **Analytical Wizardry:** Armed with a keen analytical mindset, I've transformed real-world challenges into opportunities for data-driven solutions. Through the strategic formulation of SQL queries, I've unlocked actionable insights and unearthed hidden patterns within complex datasets, enabling informed decision-making and driving business success.

- **ETL (Extract, Transform, Load) Proficiency:** I worked on data integration through ETL processes, seamlessly extracting data from disparate sources, transforming it into a consistent format, and loading it into target systems. Whether it's cleaning messy data, restructuring datasets, or performing complex transformations, I've become a maestro of ETL operations. 

# Conclusion

Insights from the analysis reveal key findings:

- Top-Paying Data Analyst Jobs: Remote positions offer a wide salary range, with the highest reaching $650,000.
- Skills for Top-Paying Jobs: Proficiency in SQL is critical for securing high-paying data analyst roles.
- Most In-Demand Skills: SQL emerges as the most sought-after skill in the data analyst job market.
- Skills with Higher Salaries: Specialized skills like SVN and Solidity command the highest average salaries.
- Optimal Skills for Job Market Value: SQL stands out for both demand and high average salary, making it an optimal skill for maximizing market value.

In conclusion, this project has not only enhanced my SQL skills but also provided valuable insights into the data analyst job market. By prioritizing high-demand, high-salary skills, aspiring data analysts can better position themselves in a competitive job market. This underscores the importance of continuous learning and adapting to emerging trends in data analytics.

# About Me!

**Hi!** 👋 

I am Sanjay S Singh – a versatile professional poised at the intersection of performance marketing and data analytics. With over five years of prolific experience in sculpting and refining digital campaigns, I am now charting a course towards a dynamic role as a Data Analyst. 📊💻

As an engineering graduate specializing in computer engineering, I am currently pursuing a Master's degree in Digital Marketing and Data Science, aligning my academic journey with the dynamic landscape of technology and analytics. 🎓🔍

My proficiency spans a versatile spectrum of technical tools and skills, including SQL, Python, Excel, PowerPoint, Power BI, Tableau, Data Analysis, and Data Visualization. These competencies equip me to navigate the complexities of data-driven decision-making and contribute effectively to strategic initiatives. 🛠️📊

Beyond the confines of academia, I actively engage in community endeavors as a dedicated member of the Mumbai Cycling Group. Through this involvement, I embrace opportunities to foster connections and contribute positively to communal initiatives, reflecting my commitment to social engagement and collective growth. 🚴‍♂️🤝

Outside professional commitments, my passions encompass the culinary arts 🍳, cycling adventures 🚴‍♂️, exploring new things 🌍, and growth and problem-solving mindset. Driven by a growth-oriented mindset and a penchant for problem-solving, I continuously seek avenues for personal and professional development, embracing challenges with enthusiasm and resilience. 🌱🚀
