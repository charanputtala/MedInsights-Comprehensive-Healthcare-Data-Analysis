# MedInsights: Comprehensive Healthcare Data Analysis
![SQL](https://img.shields.io/badge/Language-%20SQL-yellow/Workbench)
![SQL](https://img.shields.io/badge/Workbench-%20MySQL-green)

## Project Overview

"HealthCare Data Insights" is a comprehensive analysis project that leverages SQL to extract valuable insights from a healthcare dataset. The dataset includes patient demographics, medical conditions, treatments, financial aspects, and hospital performances. This project aims to facilitate data-driven decision-making in healthcare management and analysis.



## Introduction

The project utilizes a fictional healthcare dataset to perform various SQL queries that help uncover insights into patient demographics, medical conditions, treatments, billing, and hospital performances. The goal is to provide a thorough understanding of the dataset and highlight key aspects that can inform healthcare management strategies.

### 1. **Data Overview & Basic Statistics**
      - The dataset was explored to gather a comprehensive view of patient information and healthcare records. Queries included counting total records, finding the maximum and average ages of hospitalized patients, and analyzing patient demographics based on age.

### 2. **Medical Conditions & Medications**
      - Detailed insights were derived regarding prevalent medical conditions, medications prescribed for specific conditions, and the frequency of their occurrence. This information assists in understanding the distribution and treatment of various health issues within the dataset.

### 3. **Insurance Providers & Hospitals**
     - The project delved into patient preferences for insurance providers and hospitals based on frequency. This data aids in resource allocation, understanding coverage preferences, and evaluating the prominence of healthcare services across different facilities.

### 4. **Financial Analysis & Duration of Hospitalization**
     - Financial aspects were scrutinized by examining average billing amounts associated with different medical conditions and calculating the total billing amount and duration of hospital stays for patients across various hospitals. This helps in understanding costs, hospital efficiency, and patient care duration.

### 5. **Blood Type Analysis & Donation Matching**
     - The distribution of blood types among patients was explored, highlighting potential correlations between age groups and blood type occurrences. Additionally, a stored procedure, 'Blood_Matcher,' was created to identify potential donors and recipients based on specific criteria of blood types, age, and hospital affiliation or non-affiliation.

### 6. **Yearly Admissions & Insurance Analysis**
     - The analysis extended to identifying hospitals with patient admissions in specific years (2024 and 2025) and understanding billing patterns across different insurance providers. This aids in understanding patient inflow trends and disparities in billing practices among insurance companies.

### 7. **Patient Risk Categorization**
     - A column was created to categorize patients into high, medium, or low-risk categories based on their medical conditions and test results. This categorization allows for a quick assessment of patient status and required follow-up actions.


### Conclusion
This project demonstrates the power of SQL in analyzing healthcare data, providing crucial insights into patient demographics, medical conditions, treatments, billing, and hospital performances. The findings can significantly aid in healthcare management and decision-making processes.


### Dataset Structure
- id (INT): Unique identifier for each record.
- Name (VARCHAR): Name of the patient.
- Age (INT): Age of the patient.
- Gender (VARCHAR): Gender of the patient.
- Blood_Type (VARCHAR): Blood type of the patient.
- Medical_Condition (VARCHAR): Medical condition of the patient.
- Date_of_Admission (DATE): Date when the patient was admitted.
- Doctor (VARCHAR): Doctor attending the patient.
- Hospital (VARCHAR): Hospital where the patient is admitted.
- Insurance_Provider (VARCHAR): Insurance provider for the patient.
- Billing_Amount (DECIMAL): Billing amount for the patient's treatment.
- Room_Number (INT): Room number where the patient is admitted.
- Admission_Type (VARCHAR): Type of admission (e.g., emergency, routine).
- Discharge_Date (DATE): Date when the patient was discharged.
- Medication (VARCHAR): Medication prescribed to the patient.
- Test_Results (VARCHAR): Test results for the patient.

## Procedure

### Create a Procedure to Find Blood Donor/Receiver
```sql
DELIMITER $$

CREATE PROCEDURE Blood_Matcher(IN Name_of_patient VARCHAR(200))
BEGIN 
SELECT D.Name AS Donor_name, D.Age AS Donor_Age, D.Blood_Type AS Donors_Blood_type, D.Hospital AS Donors_Hospital, 
R.Name AS Receiver_name, R.Age AS Receiver_Age, R.Blood_Type AS Receivers_Blood_type, R.Hospital AS Receivers_hospital
FROM healthcare D 
INNER JOIN healthcare R ON (D.Blood_type = 'O-' AND R.Blood_type = 'AB+') 
AND ((D.Hospital = R.Hospital) OR (D.Hospital != R.Hospital))
WHERE (R.Name REGEXP Name_of_patient) AND (D.AGE BETWEEN 20 AND 40);
END $$

DELIMITER ;

CALL Blood_Matcher('Matthew Cruz'); 
