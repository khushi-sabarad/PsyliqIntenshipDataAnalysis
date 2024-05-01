# DIABETES PREDICATION ASSESSMENT

Dataset: Diabetes_prediction (`Excel Worksheet`)
- create a new column 'DOBcorrected' by using the formula: `= IFERROR(TEXT(DATE(RIGHT(D2, 4), LEFT(D2, FIND("/", D2) - 1), MID(D2, FIND("/", D2) + 1, FIND("/", D2, FIND("/", D2) + 1) - FIND("/", D2) - 1)), "dd-mm-yyyy"), D2)`

- Create a new column 'age' by using the formula: `=DATEDIF(E2, TODAY(), "y")`. Here, the E column is the DOBcorrected column created in the previous step 
- Save as -> file type: CSV UTF-8 (Comma delimited)
- `MySQL Workbench` -> connect to MYSQL database -> Create Schema:
  ```sql
  CREATE SCHEMA `diabetes_pred`;
  ```
- Navigate to `diabetes_pred` under SCHEMAS on the left side, right-click 'Tables' and click on Table Data Import Wizard -> browse and import the CSV data {importing a large dataset, 100000 rows in this case, will take some time}

```sql
show databases;
use diabetes_pred;
show tables;

SELECT * FROM diabetes_prediction_csv;

ALTER TABLE diabetes_prediction_csv
RENAME COLUMN ï»¿EmployeeName TO EmployeeName;

SELECT * FROM diabetes_prediction_csv;
```

```sql
-- 1. Retrieve the Patient_id and ages of all patients.
select Patient_id, age from diabetes_prediction_csv;

-- 2. Select all female patients who are older than 30.
select * from diabetes_prediction_csv
where gender = 'Female' and age > 30;

-- 3. Calculate the average BMI of patients.
select AVG(bmi) from diabetes_prediction_csv;

-- 4. List patients in descending order of blood glucose levels.
select * from diabetes_prediction_csv
order by blood_glucose_level desc;

-- 5. Find patients who have hypertension and diabetes.
select * from diabetes_prediction_csv
where hypertension = 1 and diabetes = 1;

-- 6. Determine the number of patients with heart disease.
select count(*) as heart_disease_patients from diabetes_prediction_csv
where heart_disease = 1;

-- 7. Group patients by smoking history and count how many smokers and nonsmokers there are.
select smoking_history,count(*) from diabetes_prediction_csv
group by smoking_history;

-- 8. Retrieve the Patient_ids of patients who have a BMI greater than the average BMI.
-- from Q3, AVG(bmi) is 27.32076709999422
select Patient_id, bmi from diabetes_prediction_csv
where bmi > (select AVG(bmi) from diabetes_prediction_csv);

-- 9. Find the patient with the highest HbA1c level and the patient with the lowest HbA1clevel.
select Patient_id, HbA1c_level as HbA1c_level_Max_Min
from diabetes_prediction_csv
where HbA1c_level = (select MAX(HbA1c_level) from diabetes_prediction_csv)
   or HbA1c_level = (select MIN(HbA1c_level) from diabetes_prediction_csv);

-- 10. Calculate the age of patients in years (assuming the current date as of now).
-- calculated this in Excel before importing the dataset

-- 11. Rank patients by blood glucose level within each gender group.
SELECT 
    Patient_id, 
    gender, 
    blood_glucose_level,
    RANK() OVER (PARTITION BY gender ORDER BY blood_glucose_level) AS glucose_level_rank
FROM diabetes_prediction_csv
ORDER BY gender, blood_glucose_level;

-- 12. Update the smoking history of patients who are older than 30 to "Ex-smoker."
UPDATE diabetes_prediction_csv
SET smoking_history = 'Ex-smoker'
WHERE age > 30;

-- 13. Insert a new patient into the database with sample data.
INSERT INTO diabetes_prediction_csv
VALUES ('Khushi', 'PT100', 'Female', '01-09-2002', '01-09-2002', 21, 0, 0, 'never', 24, 4, 110, 0);

select * from diabetes_prediction_csv
where EmployeeName = 'Khushi';

-- 14. Delete all patients with heart disease from the database.
/*
I had to disable the safe update option for the delete statement to work
SET SQL_SAFE_UPDATES = 0;
*/
DELETE FROM diabetes_prediction_csv WHERE heart_disease = 1;

-- 15. Find patients who have hypertension but not diabetes using the EXCEPT operator.
-- Patients with hypertension
SELECT Patient_id
FROM diabetes_prediction_csv
WHERE hypertension = 1

EXCEPT

-- Patients with both hypertension and diabetes
SELECT Patient_id
FROM diabetes_prediction_csv
WHERE hypertension = 1 AND diabetes = 1;


-- 16. Define a unique constraint on the "patient_id" column to ensure its values are unique.

ALTER TABLE diabetes_prediction_csv
CHANGE COLUMN Patient_id Patient_id VARCHAR(10),
ADD CONSTRAINT patient_id_unique UNIQUE (Patient_id);


-- 17. Create a view that displays the Patient_ids, ages, and BMI of patients.
/*
A view in a database is a virtual table that is based on the result set of a SELECT query. 
Unlike a physical table, which stores data permanently, a view does not store data itself. 
Instead, it is a saved query that dynamically retrieves data from one or more tables whenever it is referenced.
*/

create view patient_info_view as
select Patient_id, age, bmi from diabetes_prediction_csv;

SELECT * FROM patient_info_view;

```
***

18. Suggest improvements in the database schema to reduce data redundancy and improve data integrity.
To improve the database schema for reducing data redundancy and enhancing data integrity, consider the following suggestions:

- Normalization: Normalize the database schema to reduce redundancy and dependency issues. This involves breaking down the dataset into smaller, related tables to minimize data duplication and ensure each piece of information is stored only once
- Use of Foreign Keys: Implement foreign key constraints to enforce referential integrity between related tables. For example, if there are tables for employees and patients separately, you can use the patient ID as a foreign key in other tables where patient information is referenced
- After adding a "DOBcorrected" column in Excel to rectify incorrect dates, delete the original "D.O.B" column before importing the dataset into SQLWorkbench, ensuring to work with a copy of the original dataset to avoid data loss.
- Enum: For columns like "gender" and "smoking_history," consider using enumerated types. This approach reduces data redundancy and ensures consistency in values
- Consistent Data Types: Store hypertension, heart disease, and diabetes as boolean values (0 or 1), to maintain consistency throughout the schema
- Documentation: Document the database schema thoroughly to provide clear guidelines for developers and ensure understanding of the database structure and relationships

  
***

19. Explain how you can optimize the performance of SQL queries on this dataset.

- Indexing: Identify columns frequently used in WHERE clauses or JOIN conditions and create appropriate indexes. This helps speed up data retrieval by allowing the database engine to locate rows based on indexed columns quickly.
- Avoid using SELECT *, instead, specify only the columns you need. Use WHERE clauses to filter data early in the query execution process.
- Normalization and Denormalization: Normalize the database schema to reduce redundancy and improve data integrity. Denormalize tables if performance becomes a concern, especially for frequently accessed data.
- Use of Joins: Optimize JOIN operations by selecting appropriate join algorithms (e.g., nested loop, hash join, merge join) based on the size of the tables and available indexes. Consider using INNER JOIN instead of OUTER JOIN if you don't need to retrieve unmatched rows.
- Query Caching: Implement query caching mechanisms to store the results of frequently executed queries in memory. This reduces the need to recompute results for identical queries, improving overall query performance.
- Partitioning: Partition large tables based on certain criteria (e.g., date ranges) to distribute data across multiple physical storage devices. This can improve query performance by reducing the amount of data that needs to be scanned.

   
***
Let's connect on [LinkedIn!](https://www.linkedin.com/in/khushi-sabarad/)🤝
