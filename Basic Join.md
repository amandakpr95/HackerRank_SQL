<img Logo src="https://wizardsourcer.com/wp-content/uploads/2021/10/HackerRank-logo.png" width="100"> <img src="https://1000logos.net/wp-content/uploads/2020/08/MySQL-Logo.png" width="100"> <img src="https://github.com/user-attachments/assets/85aa484a-7f87-4edd-81d3-a771dd03f27d" width ="50">


# HackerRank's Basic Join in SQL
Hello! These are all my answers (with detailed comments explaining the code) for [HackerRank's Prepare SQL Aggregation](https://www.hackerrank.com/domains/sql?filters%5Bsubdomains%5D%5B%5D=join) Questions!
Here you will learn some more intermediate functions in SQL, like:
- ...

This is a great place to start your SQL journey! I highly recommend creating your own notebook (here I used Jupyter Notebooks), to take your own notes and personalize your code. 
This is how I solved these queries, but it is absolutely not the only way to solve! Get creative!

## Population Census
Given the CITY and COUNTRY tables, query the sum of the populations of all cities where the CONTINENT is 'Asia'.

Note: CITY.CountryCode and COUNTRY.Code are matching key columns.


The CITY and COUNTRY tables are described as follows:

<img src = https://s3.amazonaws.com/hr-challenge-images/8137/1449729804-f21d187d0f-CITY.jpg width = 300>
<img src = https://s3.amazonaws.com/hr-challenge-images/8342/1449769013-e54ce90480-Country.jpg width = 300>

```sql
SELECT SUM(CITY.POPULATION)  --- select the sum of the "POPULATION" column in the "CITY" table
FROM CITY   --- get the data from the "CITY" table
JOIN COUNTRY ON CITY.COUNTRYCODE = COUNTRY.code
--- join the data from the "COUNTRY" table to the "CITY" table
--- match the rows based on the common column (i.e. the "COUNTRYCODE" column in the "CITY" table and the "code" column in the "COUNTRY" table)
WHERE CONTINENT = 'Asia'  --- only use the data where the continent is "Asia"
```

---
## African Cities
Given the CITY and COUNTRY tables, query the names of all cities where the CONTINENT is 'Africa'.

Note: CITY.CountryCode and COUNTRY.Code are matching key columns.

```sql
SELECT CITY.Name  --- select the "Name" column in the "CITY" table
FROM CITY  --- get the data from the "CITY" table
JOIN COUNTRY ON CITY.CountryCode = Country.Code
--- join the data from the "COUNTRY" table to the "CITY" table
--- match the rows based on the common column (i.e. the "COUNTRYCODE" column in the "CITY" table and the "code" column in the "COUNTRY" table)
WHERE CONTINENT = 'Africa'  --- only use the data where the continent is "Africa"
```

---
## Average Population of Each Continent
Given the CITY and COUNTRY tables, query the names of all the continents (COUNTRY.Continent) and their respective average city populations (CITY.Population) rounded down to the nearest integer.

Note: CITY.CountryCode and COUNTRY.Code are matching key columns.

```sql
SELECT COUNTRY.Continent, FLOOR(AVG(CITY.Population)) AS AverageCityPopulation
--- select the "Continent" column from the "COUNTRY" table
--- also select the average of the "Population" column from the "CITY" table ("AVG(CITY.Population)")
--- round the result down to the nearest integer ("FLOOR(...)")
--- and call it "AverageCityPopulation"
FROM CITY  --- get the data from the "CITY" table
JOIN COUNTRY ON CITY.CountryCode = COUNTRY.Code
--- join the data from the "COUNTRY" table to the "CITY" table
--- match the rows based on the common column (i.e. the "COUNTRYCODE" column in the "CITY" table and the "code" column in the "COUNTRY" table)
GROUP BY COUNTRY.Continent;  --- group the result by "Continent"
```

---
## Top Competitors
Julia just finished conducting a coding contest, and she needs your help assembling the leaderboard! Write a query to print the respective hacker_id and name of hackers who achieved full scores for more than one challenge. Order your output in descending order by the total number of challenges in which the hacker earned a full score. If more than one hacker received full scores in same number of challenges, then sort them by ascending hacker_id.

The following tables contain contest data:

Hackers: The hacker_id is the id of the hacker, and name is the name of the hacker. 

<img src=https://s3.amazonaws.com/hr-challenge-images/19504/1458526776-67667350b4-ScreenShot2016-03-21at7.45.59AM.png width = 300>

Difficulty: The difficult_level is the level of difficulty of the challenge, and score is the maximum score that can be achieved for a challenge at that difficulty level. 

<img src=https://s3.amazonaws.com/hr-challenge-images/19504/1458526915-57eb75d9a2-ScreenShot2016-03-21at7.46.09AM.png width = 300>

Challenges: The challenge_id is the id of the challenge, the hacker_id is the id of the hacker who created the challenge, and difficulty_level is the level of difficulty of the challenge. 

<img src=https://s3.amazonaws.com/hr-challenge-images/19504/1458527032-f9ca650442-ScreenShot2016-03-21at7.46.17AM.png width = 300>

Submissions: The submission_id is the id of the submission, hacker_id is the id of the hacker who made the submission, challenge_id is the id of the challenge that the submission belongs to, and score is the score of the submission.

<img src=https://s3.amazonaws.com/hr-challenge-images/19504/1458527077-298f8e922a-ScreenShot2016-03-21at7.46.29AM.png width = 300>

```sql
SELECT h.hacker_id, h.name  --- select the "hacker_id" column and the "name" from the "Hackers" table
FROM Submissions s  --- get the data from the "Submissions" table and alias the table as "s"
JOIN Challenges c ON s.challenge_id = c.challenge_id
--- join the data from the "Challenges" table to the "Submissions" table
--- alias the "Challenges" table as "c"
--- match the rows based on the common column (i.e. the "challenge_id" column in both tables)
JOIN Difficulty d ON c.difficulty_level = d.difficulty_level
--- join the data from the "Difficulty" table to the "Challenges" table
--- alias the "Difficulty" table as "d"
--- match the rows based on the common column (i.e. the "difficulty_level" column in both tables)
JOIN Hackers h ON s.hacker_id = h.hacker_id
--- join the data from the "Hackers" table to the "Submissions" table
--- alias the "Hackers" table as "f"
--- match the rows based on the common column (i.e. the "hacker_id" column in both tables)
WHERE s.score = d.score
--- only use the data where the score from the submissions table (the score of the submission) is equal to the score from the difficulty table (the max score that can be achieved)
GROUP BY h.hacker_id, h.name  --- group the results by the "hacker_id" then the "name"
HAVING COUNT(s.challenge_id) > 1  --- only use data where the amount of challenges submitted is greater than 1
ORDER BY COUNT(s.challenge_id) DESC, s.hacker_id;  --- order by the amount of challenges submitted from highest to lowest, then by hacker id
```

---
## Olivander's Inventory
Harry Potter and his friends are at Ollivander's with Ron, finally replacing Charlie's old broken wand.

Hermione decides the best way to choose is by determining the minimum number of gold galleons needed to buy each non-evil wand of high power and age. Write a query to print the id, age, coins_needed, and power of the wands that Ron's interested in, sorted in order of descending power. If more than one wand has same power, sort the result in order of descending age.

The following tables contain data on the wands in Ollivander's inventory:

Wands: The id is the id of the wand, code is the code of the wand, coins_needed is the total number of gold galleons needed to buy the wand, and power denotes the quality of the wand (the higher the power, the better the wand is).

<img src=https://s3.amazonaws.com/hr-challenge-images/19502/1458538092-b2a8163a74-ScreenShot2016-03-08at12.13.39AM.png width = 300>

Wands_Property: The code is the code of the wand, age is the age of the wand, and is_evil denotes whether the wand is good for the dark arts. If the value of is_evil is 0, it means that the wand is not evil. The mapping between code and age is one-one.

<img src=https://s3.amazonaws.com/hr-challenge-images/19502/1458538221-18c4092b7d-ScreenShot2016-03-08at12.13.53AM.png width = 300>

```sql
SELECT W.id, Filtered_Wands.Max_Age, W.coins_needed, W.power
--- select the "id" column in the "Wands" table
--- select the "Max_Age" column in the "Filtered_Wands" table
--- select the "coins_needed" column in the "Wands" table
--- select the "power" column in the "Wands" table
FROM Wands W  --- get the data from the "Wands" table, and alias it as "w"
INNER JOIN (
    SELECT
      W1.code,  --- select the "code" column in the "Wands" table
      MIN(W1.coins_needed) AS Min_Coin, --- select the minimum value from the "coins_needed" column in the "Wands" table and alias it as "Min_Coin"
      MAX(WP.age) AS Max_Age,  --- select the maximum value from the "age" column in the "Wands_Property" table and alias it as "Max_Age"
      W1.Power  --- select the power column in the "Wands" table
    FROM Wands AS W1  --- get the data from the "Wands" table and alias it as "W1"
    INNER JOIN Wands_Property WP ON W1.code = WP.code
    --- join the data in the "Wands_Property" table to the "Wands" table by the common column "code"
    --- alias the "Wands_Property" table as WP
    WHERE WP.is_evil= 0  --- only use the data in the "Wands_Property" table that are not evil (i.e. = 0)
    GROUP BY WP.code, power)  --- group the result by code, then power 
    AS Filtered_Wands ON W.code = Filtered_Wands.code
    --- alias this subquery temporary table as "Filtered_Wands"
    --- join the "Filtered_Wands" table to the "Wands" table based on the common column "code"
WHERE W.coins_needed = Filtered_Wands.Min_Coin
--- only use the data where the "coins_needed" column from the "Wands" table is equal to the "Min_Coin" column from the "Filtered_Wands" table
ORDER BY W.power DESC, Filtered_Wands.Max_Age DESC  --- order the results by power from highest to lowerst, then age from highest to lowest
```

---
## Challenges
Julia asked her students to create some coding challenges. Write a query to print the hacker_id, name, and the total number of challenges created by each student. Sort your results by the total number of challenges in descending order. If more than one student created the same number of challenges, then sort the result by hacker_id. If more than one student created the same number of challenges and the count is less than the maximum number of challenges created, then exclude those students from the result.

The following tables contain challenge data:

Hackers: The hacker_id is the id of the hacker, and name is the name of the hacker. 

<img src = https://s3.amazonaws.com/hr-challenge-images/19506/1458521004-cb4c077dd3-ScreenShot2016-03-21at6.06.54AM.png width = 300>

Challenges: The challenge_id is the id of the challenge, and hacker_id is the id of the student who created the challenge.

<img src = https://s3.amazonaws.com/hr-challenge-images/19506/1458521079-549341d9ec-ScreenShot2016-03-21at6.07.03AM.png width = 300>

```sql
WITH ChallengeCounts AS (
    SELECT h.hacker_id, h.name, COUNT(*) AS total_challenges, COUNT(*) over (PARTITION BY COUNT(*)) AS duplicate, MAX(COUNT(*)) over() as max_count
    FROM Challenges c
    INNER JOIN Hackers h ON c.hacker_id = h.hacker_id
    GROUP BY h.hacker_id, h.name)
SELECT hacker_id, name, total_challenges
FROM ChallengeCounts
WHERE duplicate = 1 OR total_challenges = max_count
ORDER BY total_challenges DESC, hacker_id;
```

---
## Contest Leaderboard
You did such a great job helping Julia with her last coding contest challenge that she wants you to work on this one, too!

The total score of a hacker is the sum of their maximum scores for all of the challenges. Write a query to print the hacker_id, name, and total score of the hackers ordered by the descending score. If more than one hacker achieved the same total score, then sort the result by ascending hacker_id. Exclude all hackers with a total score of  from your result.

The following tables contain contest data:

Hackers: The hacker_id is the id of the hacker, and name is the name of the hacker. 

<img src = https://s3.amazonaws.com/hr-challenge-images/19503/1458522826-a9ddd28469-ScreenShot2016-03-21at6.40.27AM.png width = 300>

Submissions: The submission_id is the id of the submission, hacker_id is the id of the hacker who made the submission, challenge_id is the id of the challenge for which the submission belongs to, and score is the score of the submission.

<img src = https://s3.amazonaws.com/hr-challenge-images/19503/1458523022-771511df90-ScreenShot2016-03-21at6.40.37AM.png width = 300>

```sql
SELECT h.hacker_id, name, SUM(max_score) AS total_score
FROM Hackers h
LEFT JOIN (
    SELECT hacker_id, challenge_id, MAX(score) AS max_score 
    FROM Submissions 
    GROUP BY hacker_id, challenge_id) AS s
    ON h.hacker_id = s.hacker_id
GROUP BY h.hacker_id, name
HAVING sum(max_score) > 0 
ORDER BY total_score DESC, h.hacker_id;
```
