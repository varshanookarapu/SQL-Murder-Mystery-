# SQL Murder Mystery

Haha this was fun.  https://mystery.knightlab.com/

Run the following squence of queries to piece the clues together to find the murderer.

```sql

SELECT * FROM crime_scene_report WHERE type='murder' AND  date = 20180115 AND city = 'SQL City' ;


-- First Witness Details

SELECT * FROM person WHERE address_street_name = 'Northwestern Dr' ORDER BY address_number DESC

-- Second Witness Details

SELECT * FROM person WHERE name LIKE 'Anna%' AND address_street_name = 'Franklin Ave'
ORDER BY name
    
-- Drivers licenses of the two witnesses

SELECT * FROM drivers_license WHERE id = 118009 OR id = 490173

-- event name : The Funky Grooves Tour -20180115

SELECT * FROM facebook_event_checkin WHERE person_id = 14887 OR person_id = 16371	

-- Interview

SELECT * FROM interview  WHERE person_id = 14887 OR person_id = 16371

--Details from Interview
--Get Fit Now Gym Bag
-- membership started with 48Z - gold member
-- car plate H42W
-- Jan 9th 

---id	person_id	name	membership_start_date	membership_status
---48Z7A	28819	Joe Germuska	20160305	    gold
---48Z55	67318	Jeremy Bowers	20160101	    gold

 SELECT * FROM get_fit_now_member WHERE membership_status = 'gold' AND id LIKE '48Z%'

--membership_id	check_in_date	check_in_time	check_out_time
--48Z7A	20180109	1600	1730
--48Z55	20180109	1530	1700

SELECT * FROM get_fit_now_check_in WHERE membership_id LIKE '48Z%' AND check_in_date = 20180109

-- need to run this again for person id
SELECT * FROM drivers_license WHERE  plate_number LIKE  '%H42W%' 


--id	name	      license_id	address_number	address_street_name	ssn
--28819	Joe Germuska	173289	  111	Fisk Rd	                    138909730
--67318	Jeremy Bowers	423327	  530	Washington Pl, Apt 3A	    871539279

SELECT * FROM person WHERE id = 28819 OR id = 67318

SELECT  * FROM income WHERE ssn= 138909730 OR ssn =871539279
-- noticed that there are no details for ssn 138909730

SELECT * FROM person WHERE name = 'Jeremy Bowers'
SELECT * FROM drivers_license WHERE id = 423327
```
**Jeremy Bowers** is our guy !!! 
