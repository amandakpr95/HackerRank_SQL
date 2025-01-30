<img Logo src="https://wizardsourcer.com/wp-content/uploads/2021/10/HackerRank-logo.png" width="100"> <img src="https://1000logos.net/wp-content/uploads/2020/08/MySQL-Logo.png" width="100"> <img src="https://github.com/user-attachments/assets/85aa484a-7f87-4edd-81d3-a771dd03f27d" width ="50">


# HackerRank's Aggregation in SQL
Hello! These are all my answers (with detailed comments explaining the code) for [HackerRank's Prepare SQL Aggregation](https://www.hackerrank.com/domains/sql?filters%5Bsubdomains%5D%5B%5D=aggregation) Questions!
Here you will learn some more intermediate functions in SQL, like:
- AVG
- SUM
- MAX
- MIN
- ABS
- POW
- SQRT
- Arithmetic operators
- CAST
- CEILING
- REPLACE
- ROUND
- TRUNCATE: removes all data from the table specified select statement, but does not delete the structure of the table
- subqueries

This is a great place to start your SQL journey! I highly recommend creating your own notebook (here I used Jupyter Notebooks), to take your own notes and personalize your code. 
This is how I solved these queries, but it is absolutely not the only way to solve! Get creative!

## Revising the Aggregations- The Count Function
Query a count of the number of cities in CITY having a Population larger than 100,000.

The CITY table is described as follows:

![CITY TABLE](https://s3.amazonaws.com/hr-challenge-images/8137/1449729804-f21d187d0f-CITY.jpg)

```sql
SELECT COUNT(*) AS CityCount  --- select the amount of cities and store it in a new column called "CityCount"
FROM CITY  --- get data from the CITY table
WHERE POPULATION > 100000  --- pull only the cities where the population is greater than 100000
```

---
## Revising Aggregations - The Sum Function
Query the total population of all cities in CITY where District is California.

```
SELECT SUM(POPULATION) AS CaliforniaPopulation  --- select the sum of the population and store it in a new column called "CaliforniaPopulation"
FROM CITY  --- get the data from the CITY table
WHERE DISTRICT = 'California';  --- sum only the populations where the district is california
```

---
## Revising Aggregations - Averages
Query the average population of all cities in CITY where District is California.

```sql
SELECT AVG(POPULATION) AS CalPopAvg  --- select the average of the populations and store it in a new column called "CalPopAvg"
FROM CITY  --- get the data from the CITY table
WHERE DISTRICT = 'California';  --- average only the populations where the district is california
```

---
## Average Population
Query the average population for all cities in CITY, rounded down to the nearest integer.

```sql
SELECT AVG(POPULATION) AS AvgPopulation  --- select the average of the populations and store it in a new column called "AvgPopulation"
FROM CITY;  --- get the data from the CITY table
```

---
## Japan Population
Query the sum of the populations for all Japanese cities in CITY. The COUNTRYCODE for Japan is JPN.

```sql
SELECT SUM(POPULATION) AS JapanPopulation  ---select the sum of the populations and store it in a new column called "JapanPopulation"
FROM CITY  --- get the data from the CITY table
WHERE COUNTRYCODE = 'JPN';  --- sum only the populations where the country is japan
```

---
## Population Density Difference
Query the difference between the maximum and minimum populations in CITY.

```sql
SELECT MAX(POPULATION) - MIN(POPULATION) AS PopDiff  --- select the highest population minus the lowest population and store it in a new column called "PopDiff"
FROM CITY;  --- get the data from the CITY table
```

---
## The Blunder
Samantha was tasked with calculating the average monthly salaries for all employees in the EMPLOYEES table, but did not realize her keyboard's 0 key was broken until after completing the calculation. She wants your help finding the difference between her miscalculation (using salaries with any zeros removed), and the actual average salary.

Write a query calculating the amount of error (i.e.: "actual - miscalculated" average monthly salaries), and round it up to the next integer.

The EMPLOYEES table is described as follows:

![EMPLOYEE Table](https://s3.amazonaws.com/hr-challenge-images/12893/1443817108-adc2235c81-1.png)

```sql
SELECT  --- select the following transformed data
  CAST(CEILING(AVG(CAST(Salary AS FLOAT)) - AVG(CAST(REPLACE(Salary, '0', '') AS FLOAT))) AS INT)
  --- convert the Salary data to a float ("CAST(Salary AS FLOAT)")
  --- replace the 0's in the Salary data with nothing ("REPLACE(Salary, '0', '')")
  --- average the salary data and subtract the average of the transformed (miscalculated) salary data
("AVG(...) - AVG(...)")
  --- round the difference to the nearest integer ("CEILING(...)")
  --- convert the result to an integer ("CAST(... AS INT)")
  AS SalaryError  --- store the result in a new column called "SalaryError"
FROM Employees;  --- get the data from the "Employees" table
```

---
## Top Earners
We define an employee's total earnings to be their monthly salary * months worked, and the maximum total earnings to be the maximum total earnings for any employee in the Employee table. 

Write a query to find the maximum total earnings for all employees as well as the total number of employees who have maximum total earnings. Then print these values as 2 space-separated integers.

![EMPLOYEE Table 2](https://s3.amazonaws.com/hr-challenge-images/19629/1458557872-4396838885-ScreenShot2016-03-21at4.27.13PM.png)

```sql
SELECT  --- select the transformed data
    MAX(salary * months) AS MaxTotalEarnings,
    --- multiply each salary months pair and get the max value, store that as "MaxTotalEarnings"
    COUNT(*) AS NumberOfEmployeesWithMaxEarnings
    --- count all of the instances of "MaxTotalEarnings" and store that as "NumberOfEmployeesWithMaxEarnings"
FROM Employee  --- get the data from the "Employee" table
WHERE salary * months = (SELECT MAX(salary * months) FROM Employee);
--- only use data where the product of salary and months is the max value
```

---
## Weather Observation 2
Query the following two values from the STATION table:

The sum of all values in LAT_N rounded to a scale of 2 decimal places.
The sum of all values in LONG_W rounded to a scale of 2 decimal places.

The STATION table is described as follows:

![STATION TABLE](https://s3.amazonaws.com/hr-challenge-images/9336/1449345840-5f0a551030-Station.jpg)

```sql
SELECT ROUND(SUM(LAT_N), 2), ROUND(SUM(LONG_W), 2)
--- select the sum of the latitudes column and the sum of the longitudes column ("SUM(...)")
--- round each result to 2 decimal places ("ROUND(..., 2)")
FROM STATION;  --- get the data from the "STATION" table
```

---
## Weather Observation 13
Query the sum of Northern Latitudes (LAT_N) from STATION having values greater than 38.7880 and less than 137.2345. Truncate your answer to 4 decimal places.

```sql
SELECT TRUNCATE(SUM(LAT_N), 4) AS SumOfLatitudes
--- select the sum of the latitudes column and remove all records from the latitudes column
--- store the result as "SumOfLatitudes"
FROM STATION  --- get the data from the "STATION" table
WHERE LAT_N > 38.7880 AND LAT_N < 137.2345;
--- only use the data where the latitude is between 38.7880 and 137.2345
```

---
## Weather Observation 14
Query the greatest value of the Northern Latitudes (LAT_N) from STATION that is less than 137.2345. Truncate your answer to 4 decimal places.

```sql
SELECT TRUNCATE(MAX(LAT_N), 4) AS MaxOfLatitudes
--- select the max of the latitudes column and remove all records from the latitudes column
--- store the result as "MaxOfLatitudes"
FROM STATION  --- get the data from the "STATION" table
WHERE LAT_N < 137.2345;
--- only use the data where the latitude is less than 137.2345
```

---
## Weather Observation 15
Query the Western Longitude (LONG_W) for the largest Northern Latitude (LAT_N) in STATION that is less than 137.2345. Round your answer to 4 decimal places.

```sql
SELECT ROUND(LONG_W, 4) AS Longitude
--- select the all of the values longitudes column and store the result as "Longitutde"
FROM STATION  --- get the data from the "STATION" table
WHERE LAT_N = (  --- only use the data where the latitude is
  SELECT MAX(LAT_N)  --- the max value
  FROM STATION  --- get the data from the "STATION" table
  WHERE LAT_N < 137.2345  --- only use the data where the latitudes are less than 137.2345
);
```

---
## Weather Observation 16
Query the smallest Northern Latitude (LAT_N) from STATION that is greater than 38.7880. Round your answer to 4 decimal places.

```sql
SELECT ROUND(MIN(LAT_N), 4) AS MinLat
--- select the minimum value in the latitudes column ("Min(...)"), round the result to 4 decimal places ("ROUND(..., 4)")
--- store the result as MinLat
FROM STATION  --- get the data from the "STATION" table
WHERE LAT_N > 38.7780  --- only use the data where the latitudes are greater than 38.7780
```

---
## Weather Observation 17
Query the Western Longitude (LONG_W) where the smallest Northern Latitude (LAT_N) in STATION is greater than 38.7780. Round your answer to 4 decimal places.

```sql
SELECT ROUND(LONG_W, 4)
--- select all the values in the longitudes column and round them to 4 decimal places
FROM STATION  --- get the data from the "STATION" table
WHERE LAT_N = (  --- only use the data where the latitudes
  SELECT MIN(LAT_N)  --- are the minimum value
  FROM STATION  --- get the data from the "STATION" table
  WHERE LAT_N > 38.7780);  --- only use the data where the latitudes are greater than 38.7780
```

---
## Weather Observation 18
Consider P1(a, b) and P2(c, d) to be two points on a 2D plane.
- a happens to equal the minimum value in Northern Latitude (LAT_N in STATION).
- b happens to equal the minimum value in Western Longitude (LONG_W in STATION).
- c happens to equal the maximum value in Northern Latitude (LAT_N in STATION).
- d happens to equal the maximum value in Western Longitude (LONG_W in STATION).

Query the Manhattan Distance between points P1 and P2 and round it to a scale of 4 decimal places.

For reference, here is the equation to solve for the Manhattan Distance

![Manhattan/Euclidean distance](https://miro.medium.com/v2/resize:fit:814/0*_9ljPf7RbVI5cVdG.png)


```sql
SELECT  --- select the transformed data
  ROUND(ABS(MIN(LAT_N) - MAX(LAT_N)) + ABS(MIN(LONG_W) - MAX(LONG_W)), 4)
  --- subtract the maximum latitude from minimum latitude and transform the result into an absolute value
  --- subtract the maximum longitutde from minimum longitude and transform the result into an absolute value
  --- add those two results together and round it to 4 decimal places
  AS ManhattanDistance  --- store the result as "ManhattanDistance"
FROM STATION;  --- get the data from the "STATION" table
```

---
## Weather Observation 19
Consider P1(a, b) and P2(c, d) to be two points on a 2D plane where (a, b) are the respective minimum and maximum values of Northern Latitude (LAT_N) and (c, d) are the respective minimum and maximum values of Western Longitude (LONG_W) in STATION.

Query the Euclidean Distance between points P1 and P2 and format your answer to display 4 decimal digits.

See the reference image above to get the equation to solve for the Euclidean Distance.

```sql
SELECT  --- select the transformed data
  ROUND(SQRT(POW(MAX(LAT_N) - MIN(LAT_N), 2) + POW(MAX(LONG_W) - MIN(LONG_W), 2)), 4)
  --- subtract the minimum latitude from the maximum latitude and square it ("POW(..., 2)")
  --- subtract the minimum longitude from the maximum longitude and square it ("POW(..., 2)")
  --- add those two results together and get the square root of the result ("SQRT(...+...)")
  --- round the result to 4 decimal places ("ROUND(..., 4)")
  AS EuclideanDistance
  --- store the result as "EuclideanDistance"
FROM STATION;  --- get the data from the "STATION" table
```

---
## Weather Observation 20
A median is defined as a number separating the higher half of a data set from the lower half. Query the median of the Northern Latitudes (LAT_N) from STATION and round your answer to 4 decimal places.

```sql
SELECT ROUND(LAT_N, 4) --- select the latitudes and round them to 4 decimal places
FROM (
    SELECT LAT_N,  --- select the latitudes
    ROW_NUMBER() OVER (ORDER BY LAT_N) AS row_num,
    --- for each latutide assign a row number ("ROWNUMBER()"), and order the row numbers by latitude ("ORDER BY LAT_N")
    --- store this information in a new column called "row_num"
    COUNT(*) OVER () AS total_count
    --- count all of the rows (i.e. latitudes) and store it as "total_count"
    FROM STATION  --- get the data from the "STATION" table
) temp --- store this subquery as a temporary table (called "temp") to use in the first query
WHERE row_num = (total_count + 1) / 2 OR row_num = (total_count / 2) + 1;
--- only use the data where the row_num is the middle row number (i.e. the median latitude)
```

---
