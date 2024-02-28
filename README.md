# HR-Data-Analytics #Dataset from FP20 Analytics Challenge

Happy to share the outcome of my recent data analysis journey. Despite the completion of the FP20 Analytics Challenge, I couldn't resist diving deeper into the dataset available on their official website. Utilizing DAX in Power BI, I've distilled some key insights.

Key Metrics:
1. Attrition Rate: How many employees we're losing.
Attrition Rate = 
   100 * COUNTROWS(FILTER('HR_Gender Diversity & Equality', 'HR_Gender Diversity & Equality'[Status] = "Resignation" || 'HR_Gender Diversity & Equality'[Status] = "HR Termination")) / COUNTROWS('HR_Gender Diversity & Equality')
   
2. Retention Rate: How good we are at keeping our awesome team.
Retention Rate = 100 - [Attrition Rate]

3. Turnover Rate: The overall churn in our workforce.
Turnover Rate = 
    DIVIDE(
        COUNTROWS(FILTER('HR_Gender Diversity & Equality', NOT(ISBLANK('HR_Gender Diversity & Equality'[Leave Date])))),
        COUNTROWS('HR_Gender Diversity & Equality'))

4. Sameperiod_LY_salary = 
    CALCULATE(
        SUM('HR_Gender Diversity & Equality'[Annual Salary ($)]),
        SAMEPERIODLASTYEAR('HR_Gender Diversity & Equality'[Hire Date].[Date]))

5. YoY Salary Change: The percentage change in salaries from year to year.
YoY_Annual_Salary_Percentage_Change = 
VAR CurrentYearSalary = SUM('HR_Gender Diversity & Equality'[Annual Salary])
VAR PreviousYearSalary = CALCULATE(
    SUM('HR_Gender Diversity & Equality'[Annual Salary ($)]),
    SAMEPERIODLASTYEAR('HR_Gender Diversity & Equality'[Hire Date].[Date]))
VAR PercentageChange = 
    IF( ISBLANK(CurrentYearSalary) || ISBLANK(PreviousYearSalary) || PreviousYearSalary = 0,
        BLANK(),
        DIVIDE(CurrentYearSalary - PreviousYearSalary, PreviousYearSalary))
RETURN
    FORMAT(PercentageChange, "0.00%")

7. Active Employees Count = 
    COUNTROWS(FILTER('HR_Gender Diversity & Equality', 'HR_Gender Diversity & Equality'[Status] = "Active"))

Report: 
1. Employee Insights I: Explored the organizational landscape, unveiling gender distribution, job roles, and branch-wise representation. Delving into diversity and workforce distribution offers valuable insights into the fabric of the company.
2. Employee Insights II: Navigated the financial and employee satisfaction terrain. This page provides a comprehensive view of total compensation, annual salary insights, and a breakdown of leave reasons. A holistic perspective on employee well-being and financial aspects.
3. Employee Insights III: Uncovered managerial impact and performance metrics. Charts on turnover rates, year-over-year changes, and salary comparison from 2014 to 2019 offer a strategic view of employee performance and financial trends.

Key Insights:
* Predominantly a workforce in their 60s.
* 55% males, 45% females.
* Most hires in 2014; 85.3% still active.
* 36 left due to performance issues, 25 due to salary expectations.
* Satisfaction closely tied to performance, with only 3 individuals receiving low scores post-Performance Improvement Plans.
* To mitigate departures to higher-paying jobs, it's recommended to re-evaluate compensation based on performance. A strategic move to retain talent and foster employee satisfaction.
* Employee satisfaction tends to rise with higher annual salaries and total compensation but surprisingly decreases with higher bonus amounts. Balancing these factors is crucial for maintaining a satisfied workforce.
