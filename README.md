# ETL Pipeline & BI Dashboard for Lok Sabha Attendance Analysis

## Architecture
![image](https://github.com/user-attachments/assets/c3b73d18-b114-44db-8fd9-5d74ac91266f)

_https://whimsical.com/lok-sabha-attendance-data-pipeline-architecture-Eudq74Pk2bM1WTFHcUUuWe_

The data for the report is sourced from the following REST API URLs.
| Description                        | API Endpoint |
|------------------------------------|-------------|
| Attendance per day (Example: Lok Sabha = 15, Session = 12, Date = 2012/11/23) | https://sansad.in/api_ls/member/getMemberAttendanceDateWise?loksabha=15&session=12&dateOfAttendance=2012/11/23 |
| All Lok Sabha Session Dates        | https://sansad.in/api_ls/business/AllLoksabhaAndSessionDates |
| All Lok Sabha Members Info         | https://sansad.in/api_ls/member |

The attendance data starts from **_Lok Sabha 14, Session 10, Feb 2007_** onwards.


## Step 1: Data Ingestion
ADF pipeline **PL_LoadFileToADLS** ingests the ministers’ data and session dates from REST API to ADLS. Then, it iterates through each date to load that day’s file in CSV format in ADLS.
_Run frequency: Once._
![image](https://github.com/user-attachments/assets/141302a3-3d63-433b-988f-c29d91a9b08d)
![image](https://github.com/user-attachments/assets/fd7d0997-224e-48f0-a15a-fb90c95f72fe)
![image](https://github.com/user-attachments/assets/4b39c1a1-a691-4eb6-8513-250852eaecd3)



## Step 2: Data Transformation
Databricks notebook **DBNotebook_Attendance consolidation.ipynb** reads all the files from the ADLS path and consolidates the 1700 CSV files into a single parquet file in the following schema.
![image](https://github.com/user-attachments/assets/a2a7ba33-0ced-41b5-9e65-132ff1d7b5b2)
This file has a total of 5,96,100 records.

## Step 3: Reporting
A report with 4 pages is made in Power BI.

### Page 1: Overview
![image](https://github.com/user-attachments/assets/592ce48c-a4bd-44c8-b7ab-722f809104ad)
This page gives an overview of the attendance in the Lok Sabha of the biggest parties, over each session. And it also mentions the yearly trend, and the MPs that have 100% attendance. You can click on the MPs names to drill through their profiles (page 4).

### Page 2: State and Constituency Insights
![image](https://github.com/user-attachments/assets/94fb1ad5-8a48-4249-a17b-e96637bfbbaa)
This page gives a state-wise and constituency-wise analysis of the attendance of the Lok Sabha MPs. You can select each state to filter the data and drill through the MPs profiles (page 4).

### Page 3: Insights
![image](https://github.com/user-attachments/assets/7b6bc26a-52d5-4c5e-b244-c4e2a297993b)
This page gives extra insights (or fun facts) about the analysis. We can see that Atal Bihari Vajpayee and Somnath Chatterjee have served the most terms in the Lok Sabha. We can also see the age distribution and the gender distribution in the Lok Sabha, and the qualification by the MPs.

### Page 4: MP Profiles
![image](https://github.com/user-attachments/assets/a0da7b62-5c64-4be0-84e3-c44beb601512)
This is the profile page of the MPs in the Lok Sabha, sitting or former. We can filter using the parties and select the names of the MPs for their information. This page also functions as a drill through page from the other pages whenever an MPs name is clicked.

## Future
Currently, this project has data only till Dec 2024. In the future, another pipeline can be added in this project to keep this well updated.
### PL_DailyAttendance
Pipeline to load a particular day’s attendance if there was a Lok Sabha Session on that day.
Run frequency: Daily when sessions are happening.

