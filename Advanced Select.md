<img Logo src="https://wizardsourcer.com/wp-content/uploads/2021/10/HackerRank-logo.png" width="100"> <img src="https://1000logos.net/wp-content/uploads/2020/08/MySQL-Logo.png" width="100"> <img src="https://github.com/user-attachments/assets/85aa484a-7f87-4edd-81d3-a771dd03f27d" width ="50">


# HackerRank's Advanced Select in SQL
Hello! These are all my answers (with detailed comments explaining the code) for [HackerRank's Prepare SQL Advanced Select](https://www.hackerrank.com/domains/sql?filters%5Bsubdomains%5D%5B%5D=advanced-select) Questions!
Here you will learn some more intermediate functions in SQL, like:
- CASE
    - WHEN
    - THEN
    - ELSE
- CONCAT
- SUBSTRING
- LOWER
- GROUP BY
- MAX
- ROWNUMBER
- JOIN
- subquieries

This is a great place to start your SQL journey! I highly recommend creating your own notebook (here I used Jupyter Notebooks), to take your own notes and personalize your code. 
This is how I solved these queries, but it is absolutely not the only way to solve! Get creative!

## Advanced Select
Write a query identifying the type of each record in the TRIANGLES table using its three side lengths. Output one of the following statements for each record in the table:
  - Equilateral: It's a triangle with 3 sides of equal length.
  - Isosceles: It's a triangle with 2 sides of equal length.
  - Scalene: It's a triangle with 3 sides of differing lengths.
  - Not A Triangle: The given values of A, B, and C don't form a triangle.

The TRIANGLES table is described as follows:

![TRIANGLES](https://s3.amazonaws.com/hr-challenge-images/12887/1443815629-ac2a843fb7-1.png)

```sql
SELECT  --- select the following transformed data
    CASE  --- only those where
        WHEN A + B > C AND A + C > B AND B + C > A THEN
        --- the sum of two sides of the triangle is larger than the third side (this is the triangle inequality theorem)
            CASE  --- and when
                WHEN A = B AND B = C THEN 'Equilateral'
                --- the three sides are equal, the triangle is called "Eqilateral"
                WHEN A = B OR A = C OR B = C THEN 'Isosceles'
                --- two of the three sides are equal, the triangle is called "Isosceles"
                ELSE 'Scalene'
                --- all other triangles (where all sides are unqiue) are calles "Scalene"
            END
        ELSE 'Not A Triangle'
        --- if sides do not satisfy the triangle inequality theorem (i.e. "ELSE"), than it is "Not A Triangle"
    END AS TriangleType
    --- store this information under a new column named "TriangleType"
FROM TRIANGLES;  --- get data from the table "TRIANGLES"
```

---

## The PADS
Generate the following two result sets:

  1. Query an alphabetically ordered list of all names in OCCUPATIONS, immediately followed by the first letter of each profession as a parenthetical (i.e.: enclosed in parentheses). For example: AnActorName(A), ADoctorName(D), AProfessorName(P), and ASingerName(S).
  2. Query the number of ocurrences of each occupation in OCCUPATIONS. Sort the occurrences in ascending order, and output them in the following format:
     ```sql
     There are a total of [occupation_count] [occupation]s.
     ```
where [occupation_count] is the number of occurrences of an occupation in OCCUPATIONS and [occupation] is the lowercase occupation name. If more than one Occupation has the same [occupation_count], they should be ordered alphabetically.

Note: There will be at least two entries in the table for each type of occupation.

The OCCUPATIONS table is described as follows:

![OCCUPATIONS TABLE](https://s3.amazonaws.com/hr-challenge-images/12889/1443816414-2a465532e7-1.png)

```sql
SELECT  --- select the following transformed data
  CONCAT(Name, '(', SUBSTRING(Occupation, 1, 1), ')') AS NameWithProfession
       --- Use CONCAT to combine:
       --- 1. The "Name" column
       --- 2. An open parenthesis "("
       --- 3. The first letter of the "Occupation" column (SUBSTRING(Occupation, 1, 1))
       ---     - The first "1" specifies the starting position (first character).
       ---     - The second "1" specifies the number of characters to extract (just one letter).
       --- 4. A closing parenthesis ")"
       --- Store the final result in a new column called "NameWithProfession"
FROM OCCUPATIONS  --- from the table "OCCUPATIONS"
ORDER BY Name;  --- order the "NameWithProfession" column by Name alphabetically

SELECT  --- select the following transformed data
    CONCAT('There are a total of ', COUNT(*), ' ', LOWER(Occupation), 's.') AS OccupationCount
     --- Use CONCAT to construct a sentence:
     --- 1. 'There are a total of ' (static text)
     --- 2. COUNT(*) - counts the number of occurrences for each occupation
     --- 3. ' ' (a space)
     --- 4. LOWER(Occupation) - converts the occupation name to lowercase
     --- 5. 's.' - Adds 's' for pluralization and a period at the end
     --- Store the final sentence in a new column called "OccupationCount"
FROM OCCUPATIONS  --- get data from the table "OCCUPATIONS"
GROUP BY Occupation  --- group the results by unique occupations
ORDER BY COUNT(*) ASC, Occupation ASC;  --- order the results by the amount of each occupation, from lowest to highest ("ASC"), then by occupation, alphbetically
```

---
## Occupations
Pivot the Occupation column in OCCUPATIONS so that each Name is sorted alphabetically and displayed underneath its corresponding Occupation. The output should consist of four columns (Doctor, Professor, Singer, and Actor) in that specific order, with their respective names listed alphabetically under each column.

Note: Print NULL when there are no more names corresponding to an occupation.

```sql
SELECT  --- select the following transformed data
    MAX(CASE WHEN Occupation = 'Doctor' THEN Name ELSE NULL END) AS Doctor,
    --- for each row pull one element or name ("MAX")
    --- pull the names ("THEN Name"), of the doctors ("CASE WHEN Occupation = 'Doctor'"),
    --- if there is no name then enter "NULL".
    --- Store in a new column called "Doctor"
    MAX(CASE WHEN Occupation = 'Professor' THEN Name ELSE NULL END) AS Professor,
    --- same logic as above, but for professors
    MAX(CASE WHEN Occupation = 'Singer' THEN Name ELSE NULL END) AS Singer,                       --- same logic as above, but for singers
    MAX(CASE WHEN Occupation = 'Actor' THEN Name ELSE NULL END) AS Actor                          --- same logic as above, but for actors
FROM (
    SELECT  --- select
      Name,  --- the name column
      Occupation,   --- and the occupation
      ROW_NUMBER() OVER (PARTITION BY Occupation ORDER BY Name) AS RowNumber
      --- assign a unique row number ("ROW_NUMBER()"), to each Name with the same occupation
      --- restart the numbering for each different occupation type ("PARTITION BY Occupation")
      --- order the names alphabetically ("ORDER BY Name")
      --- store as a new column called "RowNumber"
    FROM OCCUPATIONS  --- get data from the "OCCUPATIONS" table
) subquery  --- the above select statement is a temporary table (i.e. subquery) for the first select statement to pull data from
GROUP BY RowNumber  --- groups the rows by "RowNumber", which in the above subquery defined it as unique occupations
ORDER BY RowNumber;  --- order by "RowNumber" (i.e. unique occupations) alphabetically
```

---
## Binary Tree Nodes
You are given a table, BST, containing two columns: N and P, where N represents the value of a node in Binary Tree, and P is the parent of N.

![BINARY TREE EX](https://s3.amazonaws.com/hr-challenge-images/12888/1443773633-f9e6fd314e-simply_sql_bst.png)

![BST TABLE](https://s3.amazonaws.com/hr-challenge-images/12888/1443818507-5095ab9853-1.png)

Write a query to find the node type of Binary Tree ordered by the value of the node. Output one of the following for each node:
  - Root: If node is root node.
  - Leaf: If node is leaf node.
  - Inner: If node is neither root nor leaf node.

```sql
SELECT N,  --- select the nodes
CASE   --- and when
    WHEN P IS NULL THEN 'Root'  --- there is no parent to this node ("WHEN P IS NULL"), so this node is a 'Root'
    WHEN N IN (  --- the node value
        SELECT DISTINCT P --- is also a unique parent 
        FROM BST   --- in the table
        WHERE P IS NOT NULL) 
    THEN 'Inner'  --- then the node is a inner (i.e., it is also a parent)
    ELSE 'Leaf'  --- otherwise it is a leaf (i.e., not found in the parent column
END   --- end the case statement
FROM BST  --- get data from the "BST" table
ORDER BY N;  --- order the data by the nodes from lowest to highest.
```

---
## New Companies
Amber's conglomerate corporation just acquired some new companies. Each of the companies follows this hierarchy:

![Amber's conglomerate corporation](https://s3.amazonaws.com/hr-challenge-images/19505/1458531031-249df3ae87-ScreenShot2016-03-21at8.59.56AM.png)

Given the table schemas below, write a query to print the company_code, founder name, total number of lead managers, total number of senior managers, total number of managers, and total number of employees. Order your output by ascending company_code.

Note:The tables may contain duplicate records.

The company_code is string, so the sorting should not be numeric. For example, if the company_codes are C_1, C_2, and C_10, then the ascending company_codes will be C_1, C_10, and C_2.

Here is the schema of the tables:

Company Table:
![Company Table](https://s3.amazonaws.com/hr-challenge-images/19505/1458531125-deb0a57ae1-ScreenShot2016-03-21at8.50.04AM.png)

Lead Manager Table:
![LM Table](https://s3.amazonaws.com/hr-challenge-images/19505/1458534960-2c6d764e3c-ScreenShot2016-03-21at8.50.12AM.png)

Senior Manager Table:
![SM Table](https://s3.amazonaws.com/hr-challenge-images/19505/1458534973-6548194998-ScreenShot2016-03-21at8.50.21AM.png)

Manager Table:
![M Table](https://s3.amazonaws.com/hr-challenge-images/19505/1458534988-7fc0af46ce-ScreenShot2016-03-21at8.50.29AM.png)

Employee Table:
![E Table](https://s3.amazonaws.com/hr-challenge-images/19505/1458535002-d47f63cbb4-ScreenShot2016-03-21at8.50.41AM.png)

```sql
SELECT  --- select the following transformed data
    C.company_code,  --- the "company_code" from the Company table "C"
    C.founder,  --- the "founder" from the Company table "C"
    COUNT(distinct EM.lead_manager_code) AS total_LM,
    --- the amount of unique ("COUNT(distinct...") lead manager codes from the employee table "EM"
    --- store the result under a new column called "total_LM"
    COUNT(distinct EM.senior_manager_code) AS total_SM,
    --- same logic as above for senior manager codes
    COUNT(distinct EM.manager_code) AS total_M,
    --- same logic as above for manager codes
    COUNT(distinct EM.employee_code) AS total_employees
    --- same logic as above for employee codes
FROM Employee EM
--- get the data from the "Employee" table, and temporarily call (alias) the table "EM"
JOIN Company C on C.company_code = EM.company_code
--- join the EM table with the Company table on the column "company_code"
--- alias the Company table as "C"
GROUP BY C.company_code, C.founder  --- group the results first by company code, then by founder
```

---
