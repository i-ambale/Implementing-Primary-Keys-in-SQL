# 🌍 Geographic Location Table Creation using SQL
United Nations Database: Geographic Location Table

This project demonstrates how to normalize a database by extracting geographic location data from a larger dataset into a separate table with proper primary key constraints.

## 📘 Project Overview

The goal is to create a `Geographic_Location` table from the existing `Access_to_Basic_Services` table in a United Nations database, implementing proper database design principles:

- Table creation with appropriate data types
- Primary key constraints
- Handling of duplicate data during migration
- Establishing relationships between tables

## 📂 Database Schema

### Geographic_Location Table
| Column        | Type         | Description                |
|---------------|--------------|----------------------------|
| Country_name  | VARCHAR(37)  | Primary key (unique identifier) |
| Sub_region    | VARCHAR(25)  | Country's sub-region        |
| Region        | VARCHAR(32)  | Country's region           |
| Land_area     | NUMERIC(10,2)| Country's land area in km² |
---
📂 Tables Involved
1. `Access_to_Basic_Services`
The main dataset containing multiple records per country across years.

2. `Geographic_Location`
A new table created to store only geographic information:

- `Country_name (Primary Key)`

- `Sub_region`

- `Region`

- `Land_area`
---
## 🛠️ Key SQL Operations

1. **Table Creation**:
```sql
CREATE TABLE Geographic_Location (
  Country_name VARCHAR(37) PRIMARY KEY,
  Sub_region VARCHAR(25),
  Region VARCHAR(32),
  Land_area NUMERIC(10,2)
);
```
2. **Insert Cleaned Data**:
```sql
INSERT INTO united_nations.Geographic_Location (Country_name, Sub_region, Region, Land_area)
SELECT 
    Country_name,
    Sub_region,
    Region,
    AVG(Land_area) as Country_area
FROM united_nations.Access_to_Basic_Services
GROUP BY Country_name, Sub_region, Region;
```
---
⚠️ Notes
Country_name is not unique in the original dataset, as countries have multiple entries across years.

We use GROUP BY to aggregate and ensure one unique entry per country.

AVG(Land_area) helps standardize values in case of slight inconsistencies.

---
💻 Requirements
MySQL installed locally

pymysql and sqlalchemy installed in the Python environment

Jupyter Notebook
---
📎 Disclaimer
The notebook may not work on Google Colab because it requires a local MySQL server connection.

---
📌 Credits
Created as part of the ExploreAI Academy training on SQL and database normalization.

---
Adopted by: Ibrahim Ambale
