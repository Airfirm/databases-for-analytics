# Exercise 02: World Database – Joins, Grouping, and Data Quality

- Name:
- Course: Database for Analytics
- Module: 2
- Database Used: World Database (PostgreSQL)

---

## Instructions

- Answer each question below using SQL executed against the **World database**.
- All SQL commands **must be run by you**.
- For each SQL-based question:
  - Include the SQL command in a fenced code block
  - Include a **screenshot** showing the command and its results
- Store screenshots in the `screenshots/` folder and embed them below each answer.

---

## Question 1

When importing records from `worldPGSQL.sql`, **how many cities were imported**?

### Answer
_CityCount = 4079._

### Screenshot
_Show evidence of how you determined this (for example, a COUNT query)._

```sql
SELECT COUNT(*) AS CityCount
FROM city;
```

![Q1 Screenshot](image-Q1.png)

---

## Question 2

Using the World database, write the SQL command to **display each country name along with the name of each language spoken in that country**.

### SQL

```sql
SELECT c.Name AS CountryName,
       cl.Language AS LanguageName
FROM country AS c
JOIN countrylanguage AS cl
  ON c.Code = cl.CountryCode
ORDER BY c.Name, cl.Language;
```

### Screenshot

![Q2 Screenshot](image-Q2.png)

---

## Question 3

Using the World database, write the SQL command to **display each country name along with the name of each official language spoken in that country**.

### SQL

```sql
SELECT c.Name AS CountryName,
       cl.Language AS OfficialLanguage
FROM country AS c
JOIN countrylanguage AS cl
  ON c.Code = cl.CountryCode
WHERE cl.IsOfficial = 'T'
ORDER BY c.Name, cl.Language;
```

### Screenshot

![Q3 Screenshot](image-Q3.png)

---

## Question 4

Consider the following two SQL statements:

```sql
SELECT *
FROM country, countrylanguage
WHERE country.code = countrylanguage.countrycode;
```

```sql
SELECT *
FROM country
LEFT OUTER JOIN countrylanguage
ON country.code = countrylanguage.countrycode;
```

**In your own words**, describe what data the **second query returns that the first query does not**.

### Answer
_The first query behaves like an INNER JOIN because it only returns rows where a country has at least one matching row in countrylanguage (countries without languages are excluded)._

_The second query is a LEFT OUTER JOIN, so it returns all countries, including countries that do not have any matching rows in countrylanguage. For those unmatched countries, the countrylanguage columns will show NULL. (This is the key difference: it keeps “unmatched” countries.)._

---

## Question 5

Using the World database, write the SQL command to **list all different forms of government** found in the data.
Do **not** repeat any form of government more than once.

### SQL

```sql
SELECT DISTINCT GovernmentForm
FROM country
ORDER BY GovernmentForm;
```

### Screenshot

![Q5 Screenshot](image-Q5.png)

---

## Question 6

Using the World database, write the SQL command to **list all names of cities and countries in one column**.
Label the column **"City or Country Name"**.

### SQL

```sql
SELECT Name AS `City or Country Name`
FROM city
UNION
SELECT Name AS `City or Country Name`
FROM country;
```

### Screenshot

![Q6 Screenshot](image-Q6.png)

---

## Question 7

Using the World database, write the SQL command to **list all countries by name**, along with the **number of languages spoken in each country**.
Be sure to **sort by country name**.

### SQL

```sql
SELECT c.Name AS CountryName,
       COUNT(cl.Language) AS LanguageCount
FROM country AS c
LEFT JOIN countrylanguage AS cl
  ON c.Code = cl.CountryCode
GROUP BY c.Code, c.Name
ORDER BY c.Name;
```

### Screenshot

![Q7 Screenshot](image-Q7.png)

---

## Question 8

Using the World database, write the SQL command to **list all languages**, along with the **number of countries where each language is spoken**.
Be sure to **sort by language name**.

### SQL

```sql
SELECT cl.Language AS LanguageName,
       COUNT(DISTINCT cl.CountryCode) AS CountriesSpokenIn
FROM countrylanguage AS cl
GROUP BY cl.Language
ORDER BY cl.Language;
```

### Screenshot

![Q8 Screenshot](image-Q8.png)

---

## Question 9

Using the World database, write the SQL command to **list countries that have more than two official languages**, along with the **number of official languages spoken**.

*Hint: There are 8 such countries in this dataset.*

### SQL

```sql
SELECT c.Name AS CountryName,
       COUNT(*) AS OfficialLanguageCount
FROM country AS c
JOIN countrylanguage AS cl
  ON c.Code = cl.CountryCode
WHERE cl.IsOfficial = 'T'
GROUP BY c.Code, c.Name
HAVING COUNT(*) > 2
ORDER BY OfficialLanguageCount DESC, c.Name;
```

### Screenshot

![Q9 Screenshot](image-Q9.png)

---

## Question 10

Using the World database, write the SQL command to **find cities where the district value is missing**.

*Hint: Use `LIKE` and the dash (`-`) since some rows use that instead of actual data.*

### SQL

```sql
SELECT ID, Name, CountryCode, District
FROM city
WHERE District IS NULL
   OR District = ''
   OR District LIKE '-%';
```

### Screenshot

![Q10 Screenshot](image-Q10.png)

---

## Question 11

Using the World database, write the SQL command to **calculate the percentage of cities with missing district values**.

*Hint: The result should be approximately 0.4%.*

### SQL

```sql
SELECT
  ROUND(
    100.0 * COUNT(*) / (SELECT COUNT(*) FROM city),
    2
  ) AS PercentCitiesMissingDistrict
FROM city
WHERE District = '';
```

### Screenshot

![Q11 Screenshot](image-Q11.png)
