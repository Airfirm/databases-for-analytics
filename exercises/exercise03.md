# Exercise 03: MongoDB – Document Queries and Analysis

- Name:
- Course: Database for Analytics
- Module: 3
- Database Used: MongoDB
- Dataset: `restaurants-json.json`

---

## Instructions

- Import the provided `restaurants-json.json` file into MongoDB.
- All commands must be **executed by you** in the MongoDB shell or MongoDB Compass.
- For each query:
  - Include the MongoDB command in a fenced code block
  - Include a **screenshot** showing the command and its result
- Store screenshots in the `screenshots/` folder and embed them below each answer.

---

## Question 1

When importing the documents from `restaurants-json.json`, **how many documents were imported into your collection**?

### Answer

_`25358` number of documents were imported._

### Screenshot
_Show evidence of how you determined this (for example, a count query)._

```javascript
db.restaurants.countDocuments()
```

![Q1 Screenshot](screenshots/q1_document_count.png)
![Q1 Screenshot](image-68.png)

---

## Question 2

Before writing queries on the data, **what command do you use to set the MongoDB shell to operate on the `44661` database**?

### MongoDB Command

```javascript
use 44661
```

### Screenshot

![Q2 Screenshot](screenshots/q2_use_database.png)
![Q2 Screenshot](image-67.png)

---

## Question 3

Using your `restaurants` collection in the `44661` database, write the MongoDB query needed to **locate all documents in the `"Queens"` borough**.

### MongoDB Query

```javascript
db.restaurants.find({ borough: "Queens" })
```

### Screenshot

![Q3 Screenshot](screenshots/q3_queens_restaurants.png)
![Q3 Screenshot](image-69.png)

---

## Question 4

Using your `restaurants` collection in the `44661` database, write the MongoDB query needed to **find the number of restaurants in the `"Queens"` borough**.

_Number of restaurants in the `"Queens"` borough is `5656`._

### MongoDB Query

```javascript
db.restaurants.countDocuments({ borough: "Queens" })
```

### Screenshot

![Q4 Screenshot](screenshots/q4_queens_count.png)
![Q4 Screenshot](image-70.png)

---

## Question 5

Using your `restaurants` collection in the `44661` database, write the MongoDB query needed to **find the number of restaurants in the `"Queens"` borough whose cuisine is `"Hamburgers"`**.

_Number of restaurants in the `"Queens"` borough whose cuisine is `"Hamburgers"` is `104`._

### MongoDB Query

```javascript
db.restaurants.countDocuments({ borough: "Queens", cuisine: "Hamburgers" })
```

### Screenshot

![Q5 Screenshot](screenshots/q5_queens_hamburgers.png)
![Q5 Screenshot](image-71.png)

---

## Question 6

Using your `restaurants` collection in the `44661` database, write the MongoDB query needed to **find the number of restaurants in Zipcode `10460`**.

_Number of restaurants in Zipcode `10460` is `68`._

*Hint: Look up how to query **embedded documents**.*

### MongoDB Query

```javascript
db.restaurants.countDocuments({ "address.zipcode": "10460" })
```

### Screenshot

![Q6 Screenshot](screenshots/q6_zipcode_count.png)
![Q6 Screenshot](image-72.png)

---

## Question 7

Using your `restaurants` collection in the `44661` database, write the MongoDB query needed to **display only the names of restaurants in Zipcode `10460`**.

*Hint: Look up how to **project fields** in MongoDB.*

Your output should resemble:

```
{ name: "Wild Asia" }
{ name: "Terrace Cafe" }
{ name: "African Terrace" }
{ name: "Cool Zone" }
{ name: "Beaver Pond" }
...
```

### MongoDB Query

```javascript
db.restaurants.find(
  { "address.zipcode": "10460" },
  { name: 1, _id: 0 }
)
```

### Screenshot

![Q7 Screenshot](screenshots/q7_zipcode_names.png)
![Q7 Screenshot](image-73.png)

---

## Question 8

Using your `restaurants` collection in the `44661` database, write the MongoDB query needed to **display only the names of restaurants whose name contains `"IHOP"`**, ignoring case.

Your results should include:
- `"Ihop"`
- `"Ihop Restaurant"`

### MongoDB Query

```javascript
db.restaurants.find(
  { name: { $regex: ".*IHOP.*", $options: "i" } },
  { name: 1, _id: 0 }
)
```

### Screenshot

![Q8 Screenshot](screenshots/q8_ihop_case_insensitive.png)
![Q8 Screenshot](image-74.png)
![Q8 Screenshot](image-75.png)
