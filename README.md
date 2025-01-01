# Loksabha-Attendance-Analysis


Architecture - Here is the architecture diagram of the project.

![image](https://github.com/user-attachments/assets/35b6afda-fc0d-40b9-b739-58a8618dc942)


Pipelines
•	PL_HistoryAndOthers: To load ministers’ data, Lok Sabha Sessions data and daily attendance based on Lok Sabha number and sessions till now from API to ADLS.
Run frequency: Once.
•	PL_DailyAttendance: To load today’s attendance if there was a Lok Sabha Session today.
Run frequency: Daily when sessions are happening.


Report Screenshots
Page 1: Overview
![image](https://github.com/user-attachments/assets/592ce48c-a4bd-44c8-b7ab-722f809104ad)


Page 2: State and Constituency Insights
![image](https://github.com/user-attachments/assets/94fb1ad5-8a48-4249-a17b-e96637bfbbaa)


Page 3: Insights
![image](https://github.com/user-attachments/assets/7b6bc26a-52d5-4c5e-b244-c4e2a297993b)


Page 4: MP Profiles
![image](https://github.com/user-attachments/assets/a0da7b62-5c64-4be0-84e3-c44beb601512)

