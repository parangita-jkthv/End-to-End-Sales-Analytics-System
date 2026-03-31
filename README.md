# End-to-End-Sales-Analytics-System
Building a complete data pipeline from data generation to business dashboard.


PROJECT: Python → Excel → SQL → Power BI → Dashboard

--------------------------------------------------
STEP 1: PYTHON DATA GENERATION (ENHANCED)
--------------------------------------------------

Install:
pip install pandas openpyxl faker

Code:

import pandas as pd
import random
from faker import Faker

fake = Faker()

products = ["Laptop", "Mobile", "Tablet", "Headphones", "Monitor"]
cities = ["Delhi", "Mumbai", "Hyderabad", "Chennai", "Bangalore"]
categories = ["Electronics", "Accessories"]

data = []

for i in range(1, 501):
    quantity = random.randint(1, 5)
    price = random.randint(1000, 50000)

    record = {
        "OrderID": i,
        "CustomerName": fake.name(),
        "Product": random.choice(products),
        "Category": random.choice(categories),
        "City": random.choice(cities),
        "OrderDate": fake.date_between(start_date='-1y', end_date='today'),
        "Quantity": quantity,
        "Price": price,
        "Total": quantity * price
    }
    data.append(record)

df = pd.DataFrame(data)
df.to_excel("advanced_sales_data.xlsx", index=False)

--------------------------------------------------
STEP 2: EXCEL DATA CLEANING
--------------------------------------------------

Tasks:
- Remove duplicates
- Format date column
- Add new column:
  Profit = Total * 0.2

--------------------------------------------------
STEP 3: SQL INTEGRATION (OPTIONAL)
--------------------------------------------------

CREATE TABLE sales_data (
    OrderID INT,
    CustomerName VARCHAR(100),
    Product VARCHAR(50),
    Category VARCHAR(50),
    City VARCHAR(50),
    OrderDate DATE,
    Quantity INT,
    Price INT,
    Total INT
);

Import Excel data into SQL

Sample Queries:

1. Total Sales:
SELECT SUM(Total) FROM sales_data;

2. Sales by City:
SELECT City, SUM(Total) FROM sales_data GROUP BY City;

3. Top Products:
SELECT Product, SUM(Total) as Sales
FROM sales_data
GROUP BY Product
ORDER BY Sales DESC;

--------------------------------------------------
STEP 4: POWER BI DASHBOARD
--------------------------------------------------

Load Data:
Home → Get Data → Excel → Load

Create Visuals:

1. KPI Cards:
- Total Sales
- Total Orders
- Total Quantity

2. Charts:
- Bar Chart → Product vs Sales
- Pie Chart → City vs Sales
- Line Chart → Sales over Time

3. Slicers:
- City
- Product
- Category

--------------------------------------------------
STEP 5: ADVANCED DAX
--------------------------------------------------

Total Sales = SUM(sales_data[Total])

Average Sales = AVERAGE(sales_data[Total])

Profit = SUM(sales_data[Total]) * 0.2

--------------------------------------------------
STEP 7: FINAL OUTPUT
--------------------------------------------------

- Automated data generation system
- Clean dataset
- SQL queries
- Interactive dashboard

--------------------------------------------------
LEARNING OUTCOMES
--------------------------------------------------

- Python for data generation
- Excel for preprocessing
- SQL for querying
- Power BI for visualization
