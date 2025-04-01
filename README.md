# SQL_Murder_Mystery
![image](https://github.com/user-attachments/assets/8b70f15b-a0e4-470c-a661-62bc61c044bf)
There's been a Murder in SQL City! The SQL Murder Mystery is designed to be both a self-directed lesson to learn SQL concepts and commands and a fun game for experienced SQL users to solve an intriguing crime.

To have a go visit https://mystery.knightlab.com/  

How I approached the challenge:
/* STEP 1 - Start by retrieving the corresponding crime scene report 
from the police department’s database. We know the crime was a ​murder​ that occurred 
sometime on ​Jan.15, 2018​ and that it took place in ​SQL City*/ 

SELECT 
  * 
FROM 
  crime_scene_report 
WHERE 
  date = 20180115 
  AND city = "SQL City" 
  AND type = 'murder'
