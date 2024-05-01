# 📊 HR Data Analysis Assessment

Datasets:
1. general_data
2. employee_survey_data
3. manager_survey_data
4. in_time
5. out_time

***
## MS Excel
Open the `general_data` & `employee_survey_data` datasets in a single Excel workbook and make them into tables.

***

1. Using Excel, how would you filter the dataset to only show employees aged 30 and above?

`general_data` -> Click on the filter button of the 'Age' column -> Number Filters -> Greater than or equal to -> 30

![image](https://github.com/khushi-sabarad/psyliq_data_analyst_internship/assets/71957748/047da60b-dfbd-4d08-bf26-bbea6caabb1b)

***

2. Create a pivot table to summarize the average Monthly Income by Job Role.

- Select general_data table -> Insert tab -> PivotTable -> Ok
- Pivot Table -> Values: MonthlyIncome (Average) -> Rows: JobRole

![image](https://github.com/khushi-sabarad/psyliq_data_analyst_internship/assets/71957748/6e1b2baf-a778-4a31-ad91-fc2fc06230b5)

***

3. Apply conditional formatting to highlight employees with Monthly Income above the company's average income.

- Select MonthlyIncome column -> Home tab -> Conditional Formatting -> Top/Bottom rules -> Above Average (I chose Green colour)

![image](https://github.com/khushi-sabarad/psyliq_data_analyst_internship/assets/71957748/9667ab14-c804-45be-b548-c07171ab76b1)

***

4. Create a bar chart in Excel to visualize the distribution of employee ages.

- PivotTable -> Rows: Age -> Values: EmployeeID (Count)
- Insert Tab -> Bar chart
  
![image](https://github.com/khushi-sabarad/psyliq_data_analyst_internship/assets/71957748/8807d35e-0462-49d6-a550-6d22b42278f9)

***

5. Identify and clean any missing or inconsistent data in the "Department" column.

- The Department Column is already clean

![image](https://github.com/khushi-sabarad/psyliq_data_analyst_internship/assets/71957748/6f00b6d3-52ab-4d22-a05a-62248db712a3)

***

6. Using Excel, create a pivot table that displays the count of employees in each Marital Status category, segmented by Department.

- PivotTable: Columns: Department -> Rows: Marital Status -> Values: EmployeeCount (Sum)
  
![image](https://github.com/khushi-sabarad/psyliq_data_analyst_internship/assets/71957748/d686e2ba-76d7-44af-a99a-1e313aa766ab)

***

7. Apply conditional formatting to highlight employees with both above-average Monthly Income and above-average Job Satisfaction.

- Add a column 'JobSatisfaction' from `employee_survey_data` by using the formula:
  = VLOOKUP([@EmployeeID],Table2,3,FALSE)
- Select JobSatisfaction column -> Home tab -> Conditional Formatting -> Top/Bottom rules -> Above Average (I chose Green colour)

![image](https://github.com/khushi-sabarad/psyliq_data_analyst_internship/assets/71957748/9a9cacb1-3a56-4ce0-b89b-0ee1ecc46bcc)

***

8. In Excel, calculate the total Monthly Income for each Department, considering only the employees with a Job Level greater than or equal to 3.

- PivotTable -> Columns: JobLevel -> Rows: Department -> Values: MonthlyIncome (Sum)
- JobLevel Filter button -> unselect 1 & 2.
  
![image](https://github.com/khushi-sabarad/psyliq_data_analyst_internship/assets/71957748/ebfc5b15-950a-448c-9447-3a7e75c840ee)

***
9. Explain how to perform a What-If analysis in Excel to understand the impact of a 10% increase in Percent Salary Hike on Monthly Income.

- In a new sheet, Add a new column MonthlyIncomeWithHike with the formula: = Table1[@MonthlyIncome] * (1 + Table1[@PercentSalaryHike])
- Write 0.1 in a column (10% in PercentSalaryHike)
- Another column: MonthlyIncomeWithIncreasedHike with formula,
= Table1[@MonthlyIncome] * (1+Table1[@PercentSalaryHike] + general_data!$AA$3)
- Select the range -> Data Tab -> What-If Analysis -> Data Table

![image](https://github.com/khushi-sabarad/psyliq_data_analyst_internship/assets/71957748/55f65978-3ed5-45f4-ac09-3ac54523b0eb)

***

## Power BI Desktop

Home Tab -> Get Data -> Text/CSV -> {Chose file} -> Load 
Datasets loaded: `general_data`, `in_time`, `out_time`
These are seen in the 'Data' field on the left side panel.

***

10. In Power BI, establish a relationship between the "EmployeeID" in the employee data and the "EmployeeID" in the time tracking data.

- Model View (on the left side panel) -> All 3 tables are unrelated. To establish a relationship, drag the 'EmployeeID' of the general_data table, into 'Column1' of the in_time & out_time.

![image](https://github.com/khushi-sabarad/psyliq_data_analyst_internship/assets/71957748/7913d70d-b827-4a52-a2b5-99a02acebf4a)

***

11. Using DAX, create a calculated column that calculates the average years an employee has spent with their current manager.

- 'Data' right-sidebar -> right-click on general_data -> New Column
- Formula bar at the top -> enter this formula:
  AvgYearWithCurrManager = AVERAGE(general_data[YearsWithCurrManager])
- Click on Table View from the left-sidebar
  
![image](https://github.com/khushi-sabarad/psyliq_data_analyst_internship/assets/71957748/dce69b7b-27aa-4524-9a24-5c8efd447d79)

***

12. In Power BI, create a line chart that visualizes the trend of Employee Attrition over the years.

- Report view (left sidebar) -> Visualizations (right sidebar) -> X-axis: YearsAtCompany -> Y-axis: EmployeeID -> Line Chart -> Format Your Visual

![image](https://github.com/khushi-sabarad/psyliq_data_analyst_internship/assets/71957748/3ac4cd9a-c409-4ae9-900c-de5929c5b72a)

***

13. Using DAX, calculate the rolling 3-month average of Monthly Income for each employee.

- TableView -> Data (right sidebar) -> right click on general_data -> New column -> Formula bar: 3MonthsIncome = 3*general_data[MonthlyIncome]

![image](https://github.com/khushi-sabarad/psyliq_data_analyst_internship/assets/71957748/9569b2cc-b710-4044-8efa-ef12af08f0c0)

***

14. Create a hierarchy in Power BI that allows users to drill down from Department to Job Role to further narrow their analysis.

- ReportView -> Visualizations -> Matrix -> Rows: Department & JobRole -> Values: EmployeeID
  
![image](https://github.com/khushi-sabarad/psyliq_data_analyst_internship/assets/71957748/8c07e7e6-0e1f-4fc4-9349-0430ad854371)

***
15. Describe how you would create a star schema for this dataset, explaining the benefits of doing so.

- Load the other datasets (manager_survey_data, employee_survey_data) too 
- Fact table: general_data
- Dimension tables: employee_survey_data , manager_survey_data, in_time, out_time
- Establish Relationships
  
  ![image](https://github.com/khushi-sabarad/psyliq_data_analyst_internship/assets/71957748/48d6a759-6b10-43d9-b96e-1861063498d1)

Benefits:
- Simplified Queries & Improved Performance: query complexity is simplified by reducing the number of joins needed, leading to faster query performance
- Enhanced readability: database schema is easy to understand
- Optimized for Analytics: Supports analytical queries, making it ideal for data warehousing
- Scalable & Easier Mainenance
  
***
16. How can you set up parameterized queries in Power BI to allow users to filter data based on the Distance from Home column?

- Create a Parameter:
 Home tab -> Manage Parameters -> New Parameter (name it DistanceFromHomeParameter)
- Modify the Query:
  Select general_data -> Edit the query to include a filter: 
     FilteredRows = Table.SelectRows(general_data, each [DistanceFromHome] <= DistanceFromHomeParameter) -> Apply the Filter
- Add a slicer visualization (Choose DistanceFromHomeParameter as slicer) -> adjust slicer to filter data

***

17. Verify if the data adheres to a predefined schema. What actions would you take if you found inconsistencies?

- the data adheres to a predefined schema.
- Actions to take if inconsistencies are found:
   - Determine the type and amount of inconsistencies found, like missing data
  - check the source of the data
  - keep a copy of the original data before performing data cleaning
  - data cleaning: remove duplicates, fill in missing values, correct datatypes, address outliers, remove unwanted data
    
   
***
Let's connect on [LinkedIn!](https://www.linkedin.com/in/khushi-sabarad/)🤝
