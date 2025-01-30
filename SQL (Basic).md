# Basic Select
## Revising the Select Query 1
Query all columns for all American cities in the CITY table with populations larger than 100000. The CountryCode for America is USA.

The CITY table is described as follows:

![CITY TABLE 1](https://s3.amazonaws.com/hr-challenge-images/8137/1449729804-f21d187d0f-CITY.jpg)

```sql
SELECT *                                              --- select all columns (*)
FROM CITY                                             --- from the table "CITY"
WHERE COUNTRYCODE = "USA" and POPULATION > 100000     --- where the country (COUNTRYCODE) is "USA" and the population is greater than 100000
```

---
## Revising the Select Query 2
Query the NAME field for all American cities in the CITY table with populations larger than 120000. The CountryCode for America is USA.


```sql
SELECT NAME                                        --- select all columns (*)
FROM CITY                                          --- from the table "CITY"
WHERE COUNTRYCODE = "USA" and POPULATION > 120000  --- where the country (COUNTRYCODE) is "USA" and the population is greater than 120000
```

---
## Select All
Query all columns (attributes) for every row in the CITY table.


```sql
SELECT *                             --- select all columns (*)
FROM CITY                            --- from the table "CITY"
```

---
## Select By ID
Query all columns for a city in CITY with the ID 1661.


```sql
SELECT *                             --- select all columns (*)
FROM CITY                            --- from the table "CITY"
WHERE ID = 1661                      --- where the ID column = "1661
```

---
## Japanese Cities' Attributes
Query all attributes of every Japanese city in the CITY table. The COUNTRYCODE for Japan is JPN.


```sql
SELECT *                             --- select all columns (*)
FROM CITY                            --- from the table "CITY"
WHERE COUNTRYCODE = "JPN"            --- where the country (COUNTRYCODE) is Japan (JPN)
```

---
## Japanese Cities' Names
Query the names of all the Japanese cities in the CITY table. The COUNTRYCODE for Japan is JPN.

```sql
SELECT NAME                          --- select the "NAME" column
FROM CITY                            --- from the table "CITY"
WHERE COUNTRYCODE = "JPN"            --- where the country (COUNTRYCODE) is Japan (JPN)
```

---
## Weather Observation Station 1
Query a list of CITY and STATE from the STATION table.

The STATION table is described as follows:

![STATION TABLE 1](![image](https://github.com/user-attachments/assets/68fff274-6b64-4671-b9c6-d529e4b22d7e))

```sql
SELECT CITY, STATE                  --- select the "CITY" and "STATE" column
FROM STATION                        --- from the "STATION" 
```

---
## 
