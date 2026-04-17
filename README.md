# 📊 Exploratory Data Analysis on Workforce Reductions

## 📌 Project Overview
This project focuses on performing **Exploratory Data Analysis (EDA)** on a real-world dataset of workforce reductions across companies. The goal was to uncover meaningful insights about **organizational trends, industry impact, and time-based patterns** using SQL.

The dataset contains information such as:
- Company names  
- Industry  
- Total employees affected  
- Percentage reduction  
- Funding raised  
- Company stage  
- Dates of workforce changes  

---

## 🎯 Objectives
- Analyze the **scale and severity** of workforce reductions  
- Identify **companies and industries most affected**  
- Examine **time trends (yearly and monthly)**  
- Understand the relationship between **funding and company survival**  
- Highlight **top companies contributing to workforce reductions each year**  

---

## 🛠️ Tools & Technologies
- **SQL (MySQL/PostgreSQL compatible)**  
- Data Cleaning & Transformation  
- Aggregations (`SUM`, `MAX`, `MIN`)  
- Window Functions (`DENSE_RANK`, `SUM() OVER`)  
- Common Table Expressions (CTEs)  

---

## 🔍 Key Analysis Performed

### 1. Data Exploration
- Reviewed dataset structure and variables  
- Identified key metrics like total affected employees and percentage reduction  

---

### 2. Maximum Impact Analysis
- Determined:
  - Highest number of employees affected in a single event  
  - Maximum percentage reduction (including **100% cases**)  

---

### 3. Complete Workforce Reductions
- Filtered cases where **100% of employees were affected**  
- Compared:
  - Size of reduction  
  - Funding raised  

📌 **Insight:**  
Even well-funded companies experienced complete shutdowns.

---

### 4. Company-Level Analysis
- Aggregated total workforce reductions by company  
- Identified **top companies contributing to overall reductions**  

---

### 5. Industry-Level Analysis
- Grouped data by industry  
- Ranked industries by total workforce reduction  

📌 **Insight:**  
Certain industries were significantly more impacted than others.

---

### 6. Time Series Analysis

#### 📅 Yearly Trends
- Analyzed workforce reductions by year  
- Identified **spikes during specific periods**  

#### 📆 Monthly Trends
- Grouped data by month  
- Observed short-term fluctuations  

---

### 7. Rolling (Cumulative) Analysis
- Computed cumulative workforce reductions over time using window functions  

📌 **Insight:**  
Workforce reductions showed a **steady upward trend**, indicating prolonged economic pressure.

---

### 8. Company Stage Analysis
- Compared reductions across:
  - Startups  
  - Growth-stage companies  
  - Mature organizations  

📌 **Insight:**  
All company stages were affected — not just early-stage startups.

---

### 9. Top Companies Per Year
- Used `DENSE_RANK()` to identify **Top 5 companies each year**  

📌 **Insight:**  
Top contributors changed yearly, showing **dynamic market conditions**.

---

## 📊 Key Insights
- Workforce reductions are **highly concentrated among top companies**  
- Some companies experienced **complete shutdowns (100%)**  
- **Funding does not guarantee stability or survival**  
- Trends follow **clear yearly and monthly patterns**  
- Certain industries are **more vulnerable to economic downturns**  
- Workforce reductions show a **consistent cumulative increase over time**  
- Market impact is **dynamic**, with different companies leading each year  

---


---

## 🚀 How to Use
1. Import the dataset into your SQL environment  
2. Run the queries in `exploratory_data_analysis.sql`  
3. Analyze outputs and replicate insights  
4. Modify queries for deeper exploration  

---

## 📌 Sample SQL Query
```sql
WITH company_year AS (
    SELECT company, YEAR(date) AS years, SUM(total_laid_off) AS total_laid_off
    FROM new_data2
    GROUP BY company, YEAR(date)
),
company_year_rank AS (
    SELECT *, 
    DENSE_RANK() OVER(PARTITION BY years ORDER BY total_laid_off DESC) AS ranking
    FROM company_year
)
SELECT *
FROM company_year_rank
WHERE ranking <= 5;
