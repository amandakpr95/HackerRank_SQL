<img Logo src="https://wizardsourcer.com/wp-content/uploads/2021/10/HackerRank-logo.png" width="100"> <img src="https://1000logos.net/wp-content/uploads/2020/08/MySQL-Logo.png" width="100"> <img src="https://github.com/user-attachments/assets/85aa484a-7f87-4edd-81d3-a771dd03f27d" width ="50">


# HackerRank's Basic Select in SQL
Hello! These are all my answers (with detailed comments explaining the code) for [HackerRank's Prepare SQL Basic Select](https://www.hackerrank.com/domains/sql?filters%5Bsubdomains%5D%5B%5D=select) Questions!
Here you will learn the very basics of SQL, like:
- SELECT
- FROM
- WHERE
- COUNT
- DISTINCT
- LENGTH
- UNION
- ORDER BY
- LIMIT
- LIKE
- OPERATORS

This is a great place to start your SQL journey! I highly recommend creating your own notebook (here I used Jupyter Notebooks), to take your own notes and personalize your code. 
This is how I solved these queries, but it is absolutely not the only way to solve! Get creative!

## Revising the Select Query 1
Query all columns for all American cities in the CITY table with populations larger than 100000. The CountryCode for America is USA.

The CITY table is described as follows:

![CITY TABLE 1](https://s3.amazonaws.com/hr-challenge-images/8137/1449729804-f21d187d0f-CITY.jpg)

```sql
SELECT *                                              --- select all columns (*)
FROM CITY                                             --- from the table "CITY"
WHERE COUNTRYCODE = "USA" and POPULATION > 100000     --- where the COUNTRYCODE column = "USA" and the POPULATION column is greater than 100000
```

---
## Revising the Select Query 2
Query the NAME field for all American cities in the CITY table with populations larger than 120000. The CountryCode for America is USA.

```sql
SELECT NAME                                        --- select all columns (*)
FROM CITY                                          --- from the table "CITY"
WHERE COUNTRYCODE = "USA" and POPULATION > 120000; --- where the country (COUNTRYCODE) is "USA" and the population is greater than 120000
```

---
## Select All
Query all columns (attributes) for every row in the CITY table.

```sql
SELECT *                             --- select all columns (*)
FROM CITY;                           --- from the table "CITY"
```

---
## Select By ID
Query all columns for a city in CITY with the ID 1661.

```sql
SELECT *                             --- select all columns (*)
FROM CITY                            --- from the table "CITY"
WHERE ID = 1661;                     --- where the ID column = "1661
```

---
## Japanese Cities' Attributes
Query all attributes of every Japanese city in the CITY table. The COUNTRYCODE for Japan is JPN.

```sql
SELECT *                             --- select all columns (*)
FROM CITY                            --- from the table "CITY"
WHERE COUNTRYCODE = "JPN";           --- where the country (COUNTRYCODE) is Japan (JPN)
```

---
## Japanese Cities' Names
Query the names of all the Japanese cities in the CITY table. The COUNTRYCODE for Japan is JPN.

```sql
SELECT NAME                          --- select all the names ("NAME")
FROM CITY                            --- from the table "CITY"
WHERE COUNTRYCODE = "JPN";           --- where the country (COUNTRYCODE) is Japan (JPN)
```

---
## Weather Observation Station 1
Query a list of CITY and STATE from the STATION table.

The STATION table is described as follows:

![STATION TABLE 1](https://s3.amazonaws.com/hr-challenge-images/9336/1449345840-5f0a551030-Station.jpg)

```sql
SELECT CITY, STATE                  --- select the cities ("CITY") and states ("STATE")
FROM STATION;                       --- from the "STATION" table
```

---
## Weather Observation Station 3
Query a list of CITY names from STATION for cities that have an even ID number. Print the results in any order, but exclude duplicates from the answer.

```sql
SELECT DISTINCT CITY               --- select all of the unique (DISTINCT) cities ("CITY")
FROM STATION                       --- from the "STATION" table
WHERE ID % 2 = 0;                  --- where the ID is an even number ("% 2 = 0", i.e. when divided by 2 there is no remainder)
```

---
## Weather Observation Station 4
Find the difference between the total number of CITY entries in the table and the number of distinct CITY entries in the table.

```sql
SELECT                                    --- select 
    COUNT(CITY) - COUNT(DISTINCT CITY)    --- the amount of cities ("COUNT(CITY)") minus the amount of unique cities ("- COUNT(DISTINCT CITY)")
FROM STATION;                             --- from the "STATION" table
```

---
## Weather Observation Station 5
Query the two cities in STATION with the shortest and longest CITY names, as well as their respective lengths (i.e.: number of characters in the name). If there is more than one smallest or largest city, choose the one that comes first when ordered alphabetically.

```sql
(SELECT CITY, LENGTH(CITY)               --- select the cities ("CITY") and the length of each city string ("LENGTH(CITY)")
 FROM STATION                            --- from the "STATION" table
 ORDER BY LENGTH(CITY) DESC, CITY ASC    --- organize the results first by the length of each city string ("LENGTH(CITY)"), lowest to highest, then by city alphabetically ("CITY ASC")
 LIMIT 1)                                --- limit the results to 1
UNION ALL                                --- join the results with the following
(SELECT CITY, LENGTH(CITY)               --- select the cities ("CITY") and the length of each city string ("LENGTH(CITY)")
 FROM STATION                            --- from the "STATION" table
 ORDER BY LENGTH(CITY) ASC, CITY ASC     --- organize the results first by the length of each city string ("LENGTH(CITY)"), highest to lowest, then by city alphabetically ("CITY ASC")
 LIMIT 1);                               --- limit the results to 1
```

---
## Weather Observation Station 6
Query the list of CITY names starting with vowels (i.e., a, e, i, o, or u) from STATION. Your result cannot contain duplicates.

```sql
SELECT DISTINCT CITY        --- select all the unique cities
FROM STATION                --- from the table "STATION"
WHERE CITY LIKE 'A%'        --- where the city starts with "A" and there can be anything behind it ("%")
   OR CITY LIKE 'E%'        --- or where the city starts with "E" and there can be anything behind it ("%")
   OR CITY LIKE 'I%'        --- or where the city starts with "I" and there can be anything behind it ("%")
   OR CITY LIKE 'O%'        --- or where the city starts with "O" and there can be anything behind it ("%")
   OR CITY LIKE 'U%';       --- or where the city starts with "U" and there can be anything behind it ("%")
```

---
##  Weather Observation Station 7
Query the list of CITY names ending with vowels (a, e, i, o, u) from STATION. Your result cannot contain duplicates.

```sql
SELECT DISTINCT CITY        --- select all the unique cities
FROM STATION                --- from the table "STATION"
WHERE CITY LIKE '%A'        --- where the city ends with "A" and there can be anything in front of it ("%")
   OR CITY LIKE '%E'        --- where the city ends with "E" and there can be anything in front of it ("%")
   OR CITY LIKE '%I'        --- where the city ends with "I" and there can be anything in front of it ("%")
   OR CITY LIKE '%O'        --- where the city ends with "O" and there can be anything in front of it ("%")
   OR CITY LIKE '%U'        --- where the city ends with "U" and there can be anything in front of it ("%")
ORDER BY CITY;              --- order the results by city alphabetically
```

---
##  Weather Observation Station 8
Query the list of CITY names from STATION which have vowels (i.e., a, e, i, o, and u) as both their first and last characters. Your result cannot contain duplicates.

```sql
SELECT DISTINCT CITY        --- select all the unique cities
FROM STATION                --- from the table "STATION"
WHERE CITY LIKE 'A%'        --- where the city starts with "A" and there can be anything behind it ("%")
   OR CITY LIKE 'E%'        --- or where the city starts with "E" and there can be anything behind it ("%")
   OR CITY LIKE 'I%'        --- or where the city starts with "I" and there can be anything behind it ("%")
   OR CITY LIKE 'O%'        --- or where the city starts with "O" and there can be anything behind it ("%")
   OR CITY LIKE 'U%';       --- or where the city starts with "U" and there can be anything behind it ("%")
WHERE CITY LIKE '%A'        --- where the city ends with "A" and there can be anything in front of it ("%")
   OR CITY LIKE '%E'        --- where the city ends with "E" and there can be anything in front of it ("%")
   OR CITY LIKE '%I'        --- where the city ends with "I" and there can be anything in front of it ("%")
   OR CITY LIKE '%O'        --- where the city ends with "O" and there can be anything in front of it ("%")
   OR CITY LIKE '%U'        --- where the city ends with "U" and there can be anything in front of it ("%")
ORDER BY CITY;              --- order the results by city alphabetically
```

---
## Weather Observation Station 9
Query the list of CITY names from STATION that do not start with vowels. Your result cannot contain duplicates.

```sql
SELECT DISTINCT CITY          --- select all the unique cities
FROM STATION                  --- from the table "STATION"
WHERE CITY NOT LIKE 'A%'      --- where the city does not start with "A"
    AND CITY NOT LIKE 'E%'    --- and the city does not start with "E"
    AND CITY NOT LIKE 'I%'    --- and the city does not start with "I"
    AND CITY NOT LIKE 'O%'    --- and the city does not start with "O"
    AND CITY NOT LIKE 'U%'    --- and the city does not start with "U"
ORDER BY CITY;                --- order the results by city alphabetically
```

---
## Weather Observation Station 10

Query the list of CITY names from STATION that do not end with vowels. Your result cannot contain duplicates.

```sql
SELECT DISTINCT CITY          --- select all the unique cities
FROM STATION                  --- from the table "STATION"
WHERE CITY NOT LIKE '%A'      --- where the city does not end with "A"
    AND CITY NOT LIKE '%E'    --- and the city does not end with "E"
    AND CITY NOT LIKE '%I'    --- and the city does not end with "I"
    AND CITY NOT LIKE '%O'    --- and the city does not end with "O"
    AND CITY NOT LIKE '%U'    --- and the city does not end with "U"
ORDER BY CITY;                --- order the results by city alphabetically
```

---
## Weather Observation Station 11
Query the list of CITY names from STATION that either do not start with vowels or do not end with vowels. Your result cannot contain duplicates.

```sql
SELECT DISTINCT CITY          --- select all the unique cities
FROM STATION                  --- from the table "STATION"
WHERE CITY NOT LIKE 'A%'      --- where the city does not start with "A"
    AND CITY NOT LIKE 'E%'    --- and the city does not start with "E"
    AND CITY NOT LIKE 'I%'    --- and the city does not start with "I"
    AND CITY NOT LIKE 'O%'    --- and the city does not start with "O"
    AND CITY NOT LIKE 'U%'    --- and the city does not start with "U"
OR (CITY NOT LIKE '%A'        --- OR the city does not end with "A"
    AND CITY NOT LIKE '%E'    --- and the city does not end with "E"
    AND CITY NOT LIKE '%I'    --- and the city does not end with "I"
    AND CITY NOT LIKE '%O'    --- and the city does not end with "O"
    AND CITY NOT LIKE '%U')   --- and the city does not end with "U"
ORDER BY CITY;                --- order the results by city alphabetically
```
---
## Weather Observation Station 12
Query the list of CITY names from STATION that do not start with vowels and do not end with vowels. Your result cannot contain duplicates.

```sql
SELECT DISTINCT CITY          --- select all the unique cities
FROM STATION                  --- from the table "STATION"
WHERE CITY NOT LIKE 'A%'      --- where the city does not start with "A"
    AND CITY NOT LIKE 'E%'    --- and the city does not start with "E"
    AND CITY NOT LIKE 'I%'    --- and the city does not start with "I"
    AND CITY NOT LIKE 'O%'    --- and the city does not start with "O"
    AND CITY NOT LIKE 'U%'    --- and the city does not start with "U"
AND (CITY NOT LIKE '%A'       --- AMD the city does not end with "A"
    AND CITY NOT LIKE '%E'    --- and the city does not end with "E"
    AND CITY NOT LIKE '%I'    --- and the city does not end with "I"
    AND CITY NOT LIKE '%O'    --- and the city does not end with "O"
    AND CITY NOT LIKE '%U')   --- and the city does not end with "U"
ORDER BY CITY;                --- order the results by city alphabetically
```

---
## Higher Than 75 Marks
Query the Name of any student in STUDENTS who scored higher than  Marks. Order your output by the last three characters of each name. If two or more students both have names ending in the same last three characters (i.e.: Bobby, Robby, etc.), secondary sort them by ascending ID.
The STUDENTS table is described as follows:
![STUDENTS TABLE 1](https://s3.amazonaws.com/hr-challenge-images/12896/1443815243-94b941f556-1.png)
```sql
SELECT NAME                            --- select all the names ("NAME")
FROM STUDENTS                          --- from the table "STUDENTS"
WHERE MARKS > 75                       --- where the students grades ("MARKS") are greater than 75
ORDER BY RIGHT(NAME, 3) ASC, ID ASC;   --- order the results by the last 3 characters in the "NAME" string, alphabetically, then by ID, lowest to highest
```
---
## Employee Names
Write a query that prints a list of employee names (i.e.: the name attribute) from the Employee table in alphabetical order.

The Employee table containing employee data for a company is described as follows:

![EMPLOYEE TABLE 1](https://s3.amazonaws.com/hr-challenge-images/19629/1458557872-4396838885-ScreenShot2016-03-21at4.27.13PM.png)
```sql
SELECT NAME                            --- select all the names ("NAME")
FROM EMPLOYEE                          --- from the table "EMPLOYEE"
ORDER BY NAME ASC;                     --- order by "NAME" alphabetically
```

---
## Employee Salaries
Write a query that prints a list of employee names (i.e.: the name attribute) for employees in Employee having a salary greater than $2000 per month who have been employees for less than 10 months. Sort your result by ascending employee_id.

```sql
SELECT NAME                            --- select all the names ("NAME")
FROM EMPLOYEE                          --- from the table "EMPLOYEE"
WHERE SALARY > 2000 AND MONTHS < 10    --- where the salary is greater than 2000, and the months the employee have worked here is greater than 10
ORDER BY EMPLOYEE_ID ASC;              --- order by "EMPLOYEE_ID" from lowest to highest
WHERE COUNTRYCODE = "USA" and POPULATION > 100000     --- where the COUNTRYCODE column = "USA" and the POPULATION column is greater than 100000
```

---
