# Module 7 - Exercise 1: Bringing it all together
Locating and Installing your Data

- Name: Oluwafemi Salawu
- Course: Database for Analytics
- Module: 6
- Database Used: Movies_db
- Tools Used: PostgreSQL

---

## Overview

I used a Jupyter Notebook in VS Code with Pandas and SQLAlchemy to load the IMDb TSV file into PostgreSQL. Pandas was used to safely read the file using Windows-1252 encoding and convert IMDb’s \N values to nulls. SQLAlchemy then handled the database connection, and the data was inserted in chunks to efficiently load the large dataset without encoding or permission issues.

## Why this approach works so well (important insight)

- Pandas handles broken encodings gracefully
- Python ignores illegal bytes instead of crashing
- PostgreSQL receives clean Unicode strings
- This is how ETL pipelines are often built in practice

--











---

## Information courtesy of IMDb

(https://www.imdb.com).

Used with permission.

---