# Attrition Dashboard

## Aim
The purpose of the Attrition Dashboard is to analyse employee turnover trends across years, departments, designations, and business units.  
It provides insights into:

- Overall attrition trends (voluntary and involuntary)
- Early attrition analysis (0–12 months)
- Department and designation-wise attrition distribution
- Gender and manager-wise attrition breakdown
- Comparison of employees joining vs. leaving

---

## Data Overview

| Source | File Name | Description |
|---------|------------|-------------|
| HR Employee Data | EmployeeMaster_31-Oct-25.csv | Contains employee details such as Employee ID, Designation, Department, Date of Joining, Date of Exit, Separation Reason, Manager, Gender, and Business Unit |
| Calendar Table | Derived in Power BI | Used to create year-based filtering and time intelligence calculations |

---

## Key KPIs, DAX & Mathematical Logic

| KPI | Mathematical Logic | DAX Formula (Simplified) | Description |
|------|--------------------|---------------------------|--------------|
| **Active Employees Count** | Employees whose Date of Joining ≤ Today and (Date of Exit is blank OR Date of Exit > Today) | ```DAX Active Employees = CALCULATE( COUNTROWS('AttritionDashboard'), FILTER('AttritionDashboard', 'AttritionDashboard'[Date Of Joining] <= TODAY() && (ISBLANK('AttritionDashboard'[Date Of Exit])``` | Displays total number of currently active employees in the organization. |
| **Employees Left (Attrition Count)** | Employees having a non-blank Date of Exit | ```DAX Employees Left = CALCULATE( COUNTROWS('AttritionDashboard'), FILTER('AttritionDashboard', NOT(ISBLANK('AttritionDashboard'[Date Of Exit]))) )``` | Total number of employees who exited the company. |
| **Overall Attrition %** | Attrition % = (Employees Left / Average Headcount) × 100  <br>Where Average Headcount = (Active Employees + Employees Left) / 2 | ```DAX Attrition % = DIVIDE( [Employees Left], ( [Active Employees] + [Employees Left] ) / 2 ) * 100``` | Represents the % of employees who left compared to average workforce in a period. |
| **Voluntary Attrition %** | Voluntary % = (Voluntary Exits / Total Exits) × 100 | ```DAX Voluntary % = DIVIDE( [Voluntary Count], [Employees Left] ) * 100``` | Shows % of attrition due to voluntary resignation reasons. |
| **Involuntary Attrition %** | Involuntary % = (Involuntary Exits / Total Exits) × 100 | ```DAX Involuntary % = DIVIDE( [Involuntary Count], [Employees Left] ) * 100``` | Represents % of exits due to layoffs, performance, or policy issues. |
| **Early Attrition %** | Early Attrition % = (Employees Leaving within 12 Months / Total Exits) × 100 | ```DAX Early Attrition % = VAR Diff = DATEDIFF('AttritionDashboard'[Date Of Joining], 'AttritionDashboard'[Date Of Exit], MONTH) RETURN IF(Diff <= 12, "Early", "Later")``` | Indicates % of employees leaving within their first year. |

---

## Visuals Overview

### KPI Cards
- Active Employees Count (968) → total current workforce  
- Employees Leaving (1653) → all employees who exited  
- Average Tenure (5.15 Years) → average length of service  
- Overall Attrition % (18.95%) → overall turnover rate  
- Involuntary Attrition % (1.63%) → exits due to company-initiated actions  

---

### Pie Chart: Attrition by Tenure
Displays attrition ranges:

| Tenure Range | % of Attrition |
|---------------|----------------|
| 0–3 Months | 11.86% |
| 3–6 Months | 7.86% |
| 6–12 Months | 12.73% |
| 1–2 Years | 17.91% |
| 2+ Years | 49.73% |

**Insight:** Nearly 68% of employees leave within their first year.

---

### Line Chart: Joiners vs. Leavers by Year
- Shows how many employees joined vs. left each year.  
- Used to analyze overall workforce growth trends.

---

### Department / Designation Attrition
- Bar and Tree Maps showing which areas have higher attrition.  
- Top departments:  
  - Production → 343  
  - General Trade → 284  
  - Sales Frontline → 232

---

### Manager-wise and Gender-wise Analysis
- Highlights diversity and managerial influence on attrition patterns.

---

## Summary Insights
- Early attrition (0–6 months) is high, suggesting onboarding improvement needed.  
- Voluntary exits dominate overall attrition (~98%).  
- Production and Sales teams show the highest turnover.  
- Average employee tenure = 5.15 years, indicating moderate retention.  
- Active headcount (968) reflects stable staffing.

---

## Tools Used
- Power BI Desktop  
- Power Query (ETL)  
- DAX Calculations  
- Calendar Table for time-based filtering  
- Visuals: Cards, Line Chart, Tree Map, Donut Chart, Clustered Bar Chart

---

## Conclusion
The Attrition Dashboard provides a comprehensive view of employee retention and exit trends.  
It helps HR and management identify high-risk areas and make data-driven decisions to improve workforce stability.