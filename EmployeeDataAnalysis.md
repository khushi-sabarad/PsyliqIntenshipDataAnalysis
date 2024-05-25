# 📊 Employee Data Analysis Assessment 

Datasets:
1. Employee_data
2. Employee_engagement_survey_data
3. Recruitment_Data
4. Training_and_Development_data

***

1. Can you create a pivot table to summarize the total number of employees in each department?

Select the `Employee_data` table: Ctrl + Shift + right arrow key + down arrow key > Insert Tab > Pivot table > Rows field:  DepartmentType > Values field: Employee_ID (Summarize value field by Count).

![image](https://github.com/khushi-sabarad/psyliq_data_analyst_internship/assets/71957748/7b9be33d-40c6-4357-8562-0435a32c6c16)

***
2. Apply conditional formatting to highlight employees with a "Performance Score" below 3 in red.

- Create a column EmployeeName =CONCAT(B2," ",C2)
- Select Current Employee Rating column > home tab > Conditional Formatting > Highlight Cells Rules > Less than > type 3 and Click OK.

![image](https://github.com/khushi-sabarad/psyliq_data_analyst_internship/assets/71957748/9e45610a-50e9-4397-97bf-d31cf9170b37)

***
3. Calculate the average "Satisfaction Score" for male and female employees separately using a pivot table.

- Drag-drop the `employee_engagement_survey_data` into a new sheet in the `employee_data` workbook.
- Convert the data into tables
- add a column 'Satisfaction Score' in Employee_data table with this formula: =VLOOKUP(Table1[Employee ID], employee_engagement_survey_data!A2:E3001, 4, FALSE). 
- Select the range > Insert Tab > Pivot Table >  From table/range > New Worksheet
- Drag GenderCode from Table1 in the Rows field > Satisfaction Score in the values field > value field settings > choose Average

![image](https://github.com/khushi-sabarad/psyliq_data_analyst_internship/assets/71957748/80d69395-c03c-4021-b7d7-0ac26189f677)


***
4. Create a chart to visualize the distribution of the "Work-Life Balance Score" for different job functions.

- add a column 'Work-Life Balance Score' in the Employee_data table with this formula:
  = VLOOKUP(Table1[Employee ID],Table2,5,FALSE)
-  Pivot Table -> Rows: JobFunctions -> Values: Work-Life Balance Score\
-  Select pivot table -> Insert Tab -> Recommended Charts
  
![image](https://github.com/khushi-sabarad/psyliq_data_analyst_internship/assets/71957748/fe18c10b-884c-4536-8e57-a4564ba78bbd)

***
5. Filter the data to display only terminated employees and find out the most common "Termination Type."

- Pivot Table -> Rows: Termination Type -> Values: Termination type (Count)
- The most common Termination Type is 'Unk'
  
![image](https://github.com/khushi-sabarad/psyliq_data_analyst_internship/assets/71957748/dfca9b2b-8683-40dd-8b46-e55636283ed1)

  
***
6. Calculate the average "Engagement Score" for each department using a pivot table.

- From the `employee_engagement_survey_data` bring the column to the `Employee_data` sheet by this formula:
  = VLOOKUP(Table1[Employee ID],Table2,3,FALSE)
- Pivot Table -> Rows: DepartmentType -> Values: Engagement Score (Average)
![image](https://github.com/khushi-sabarad/psyliq_data_analyst_internship/assets/71957748/7d0c6173-4483-4d56-8df6-78d1ea93cebb)

***
7. Use VLOOKUP to find the supervisor's email address for a specific employee.

- The supervisor's ID is in the recruitment_data sheet, add it to this workplace and make it into a table. 
- Use this formula in the Employee_data sheet:
 = VLOOKUP(Table1[Employee ID],Table3,8,FALSE)

![image](https://github.com/khushi-sabarad/psyliq_data_analyst_internship/assets/71957748/51bc1cb4-a47b-4f1f-b1f3-fa713b7bb9df)

***
8. Can you identify the department with the highest average "Employee Rating?"

- Pivot Table -> Rows: DepartmentType -> Values: Current Employee Rating (Average)
- The Department with the highest average 'Employee Rating' is the Admin Offices.

![image](https://github.com/khushi-sabarad/psyliq_data_analyst_internship/assets/71957748/609859ad-37f6-4f75-9037-d0b3ee5cf3d1)

***
9. Create a scatter plot to explore the relationship between "Training Duration (Days)" and "Training Cost."

- add the `training_and_development_data` sheet to the workplace, and make it into a table.
- Pivot Table -> Rows: Training Duration (days) -> Values: Training Cost (Average)
- Copy the values of the pivot table and paste it next to it. Select it -> Insert tab -> Scatter Chart

![image](https://github.com/khushi-sabarad/psyliq_data_analyst_internship/assets/71957748/78c7cbc2-e3f4-455f-be7d-37f1472e6f8a)

***
10. Build a pivot table that shows the count of employees by "RaceDesc" and "GenderCode."

- Pivot Table -> Rows: GenderCode & RaceDesc -> Values:EmployeeID (Count)
  
![image](https://github.com/khushi-sabarad/psyliq_data_analyst_internship/assets/71957748/df208823-2687-4dad-b8dc-7f1964ea995d)

***
11. Use INDEX and MATCH functions to find the "Training Program Name" for an employee with a specific ID.

- Write a few IDs as lookup values.
- In a column next to it, use this formula to lookup the Training Program Name for that employee:
  = INDEX(Table6,MATCH(K2,Table6[Employee ID],0),3)
  
![image](https://github.com/khushi-sabarad/psyliq_data_analyst_internship/assets/71957748/1925fb6d-8c50-4ade-b041-5c533000e669)

***
12. Create a multi-level pivot table to analyze the "Performance Score" by "BusinessUnit"
and "JobFunctionDescription."

- Pivot Table -> Rows: BusinessUnit & JobFunctionDescription -> Values : Performance Score (Count)
  ![image](https://github.com/khushi-sabarad/psyliq_data_analyst_internship/assets/71957748/f89e0692-a48b-4829-8e22-b0fe8a062e10)
  
![image](https://github.com/khushi-sabarad/psyliq_data_analyst_internship/assets/71957748/079193e4-c962-42a3-9539-e3da47a8f935)

***
13. Design a dynamic chart that allows users to select and visualize the performance of any employee over time.

- Create a Year column with formula: =YEAR([@StartDate])
- Pivot Table -> Rows: Year -> Columns: Performace Score -> Filters: Employee ID -> Values: Performance Score (Count)
- Click on any cell in the pivot table -> PivotTableAnalyze Tab -> Insert Slicer (select employee ID from drop-down).
- click on any cell in the pivot table -> Insert Tab -> Charts

![image](https://github.com/khushi-sabarad/psyliq_data_analyst_internship/assets/71957748/64a5a024-926a-43ca-90d4-67a1a647fd9b)

***
14. Calculate the total training cost for each "Training Program Name" and display it in a bar chart.

- Pivot Table -> Rows: Training Program Name -> Values: Training Cost (Sum)
- click on the pivot table -> Insert tab -> Bar Chart
  
![image](https://github.com/khushi-sabarad/psyliq_data_analyst_internship/assets/71957748/45116c71-da7b-4d70-a0b8-4cc4fd955d60)

***
15. Apply advanced conditional formatting to highlight the top 10% and bottom 10% of employees based on "Current Employee Rating."

- Select the Current Employee Rating column -> Home Tab -> Conditional Formatting -> Top/Bottom Rules -> Top 10 % (Green) -> Bottom 10% (Red)

![image](https://github.com/khushi-sabarad/psyliq_data_analyst_internship/assets/71957748/c5966135-19c9-4ef2-b501-7ec0a2c80622)

***
16. Use a calculated field in a pivot table to determine the average "Engagement Score" per year.

- Pivot Table -> Rows: Year -> Values: Engagement Score (Average)
  
![image](https://github.com/khushi-sabarad/psyliq_data_analyst_internship/assets/71957748/32ec77fd-fe9d-4be2-8f24-1e0c04becc9f)

***
17. Can you build a macro that automates the process of updating and refreshing all pivot tables in the workbook?

- Enable Developer Tab: File -> Options -> Customize Ribbon -> Developer
- Developer Tab -> Record Macro -> Click on any cell within a pivot table -> PivotTable Analyze -> Refresh All -> Developer Tab -> Stop Recording.
- Developer Tab -> Insert Button -> Name the button -> Assign Macro 


![image](https://github.com/khushi-sabarad/psyliq_data_analyst_internship/assets/71957748/04b5b99b-bb2c-4976-be87-eebe372b4ccb)

***
18. Create a histogram to understand the distribution of "ExitDate" for terminated employees.

- Pivot table -> Columns: Years (ExitDate) -> Rows: TerminationType -> Values: Employee ID (Count)

![image](https://github.com/khushi-sabarad/psyliq_data_analyst_internship/assets/71957748/9a9a0879-1d5b-4fb6-a6ff-ec17ade1a8ec)

- Filtered out 'Unk' while creating a graph
  
![image](https://github.com/khushi-sabarad/psyliq_data_analyst_internship/assets/71957748/1e11c4ec-5ba1-4631-9553-44e15faa27b6)

*** 
19. Utilize the SUMPRODUCT function to calculate the total training cost for employees in a specific location.

- Using the formula to calculate the total training cost of Erinfort.
- Formula: = SUMPRODUCT((Table6[Location]="Erinfort")*(Table6[Training Cost]))

![image](https://github.com/khushi-sabarad/psyliq_data_analyst_internship/assets/71957748/ef7f8cc5-8608-405e-a0dc-d3fe8c4f0b65)

***
20. Develop a dashboard that provides an overview of key HR metrics, including headcount, performance, and training costs, using charts and pivot tables.

![image](https://github.com/khushi-sabarad/BigDataAnalysis/assets/71957748/00a071ec-212d-457c-9b31-4fe84d6e25af)



***
Let's connect on [LinkedIn!](https://www.linkedin.com/in/khushi-sabarad/)🤝
