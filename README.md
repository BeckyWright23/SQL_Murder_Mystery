# SQL_Murder_Mystery
![image](https://github.com/user-attachments/assets/8b70f15b-a0e4-470c-a661-62bc61c044bf)
There's been a Murder in SQL City! The SQL Murder Mystery is designed to be both a self-directed lesson to learn SQL concepts and commands and a fun game for experienced SQL users to solve an intriguing crime.

To have a go visit https://mystery.knightlab.com/  

__<ins>How I approached the challenge:</ins>__ <br />
Started out by reading the challenge info, going through the available tables and inspecting the schema as below. I use Exclaidraw to gather pictures or text as it can help to have all in one place and make notes.
![image](https://github.com/user-attachments/assets/f01dfffa-887c-41bd-ab5e-7750fbf7e5db)

* STEP 1 - Start by retrieving the corresponding crime scene report 
from the police department’s database. We know the crime was a ​murder​ that occurred 
sometime on ​Jan.15, 2018​ and that it took place in ​SQL City

```
SELECT 
  * 
FROM 
  crime_scene_report 
WHERE 
  date = 20180115 
  AND city = "SQL City" 
  AND type = 'murder'
```

* STEP 2 - Find the 2 witnesses described from the crime scene report
One lives in the last house on "Northwestern Dr" & the 2nd named Annabel, 
lives somewhere on "Franklin Ave"

```
SELECT 
id
,address_number
, name
FROM person
WHERE address_street_name = "Northwestern Dr"
ORDER BY address_number DESC
LIMIT 1;

SELECT  
id
,address_number
, name
FROM 
  person 
WHERE 
  address_street_name = "Franklin Ave" 
  AND name like 'Annabel%'
```

* STEP 3 - Having found the witnesses' IDs. Now find the witness interviews using the person ID
```
SELECT transcript
FROM interview
WHERE person_id in("14887","16371")
```

* STEP 4 - Find the murderer. From the 2 witness transcripts, there is the start of a get fit now gym 
gold membership number '48Z', part of a license plate 'H42W', and the date the murderer
was scene at the gym 09/01/2015
```
SELECT p.name
FROM get_fit_now_check_in
    INNER JOIN get_fit_now_member as gfnm
        ON get_fit_now_check_in.membership_id = gfnm.id
    INNER JOIN person as p
        ON p.id = gfnm.person_id
    INNER JOIN drivers_license as dl
        ON p.license_id=dl.id
WHERE check_in_date = 20180109
AND membership_id like "48Z%"
```
__Success! Found the murderer. Now to query the interview transcript of the murderer to find the real villain behind this crime__

* STEP 5 - Using the person ID, find the murder's interview transcript
```
SELECT transcript
FROM interview
WHERE person_id = "67318"
```


* Step 6 - Find the mastermind. Based on the murderer's transcript, he was hired by a woman with red hair
and around 65" or 67" who drives a Tesla Model S. She attended a SQL Symphony Concernt 3 times in Dec 2017
```
SELECT 
  distinct name, 
  p.id, 
  license_id 
FROM 
  person as p 
  INNER JOIN drivers_license as dl ON p.license_id = dl.id 
  INNER JOIN facebook_event_checkin as fb ON p.id = fb.person_id 
WHERE 
  hair_color = 'red' 
    AND gender = "female" 
    AND height in (65, 66, 67) 
    AND car_model like "Model S" 
    AND fb.event_name = "SQL Symphony Concert"
```

__<ins>What I learnt:</ins>__ <br />
This is the 2nd time I've completed the SQL Murder Mystery, however the first time was in my first days of properly learning SQL and I only used separate queries. This time round I've learnt you can use multiple joins, I've limited my select statements to fields I need, rather than all, and I've used aliases. This is also my debut repository and I look forward to many more! 
