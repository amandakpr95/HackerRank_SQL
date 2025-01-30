# Basic Select
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
