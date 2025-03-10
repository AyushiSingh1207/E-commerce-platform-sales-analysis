# E-commerce Sales Analysis: Data-Driven Insights

## Project Overview
   This project analyzessales of an E-commerce platform to uncover key insights into customer behavior, product performance, and business 
   trends. The dataset consists of 8 CSV files, each containing crucial sales-related data, such as customer demographics, 
   orders, payments, and product details.

   By integrating Python, Pandas, SQL, and visualization libraries (Matplotlib & Seaborn), we perform data cleaning, 
   transformation, and exploratory analysis to extract valuable business insights.

   <img width="428" alt="image" src="https://github.com/user-attachments/assets/4e453bc0-722c-4fd1-a702-1d222fd9af88" />


## Project Workflow
### 1. Data Preprocessing & Cleaning
    
    Merging multiple datasets to form a complete view of sales.
    Handling missing values, duplicates, and inconsistent data.
    Converting timestamps and numerical columns for better analysis.

### 2. Exploratory Data Analysis (EDA)
 
    Understanding sales trends across different time periods.
    Identifying top-selling products & categories.
    Analyzing customer purchasing behavior and payment preferences.
    Evaluating seller performance & order fulfillment rates.

### 3. Business Insights & Visualizations

    Revenue Trends: Analyzing total sales per month/year.
    Product Performance: Finding best-selling products & categories.
    Customer Analysis: Studying repeat customers & location-wise sales.
    Payment Methods: Checking preferred payment types among customers.

  ### 4.Technologies Used
     
     Python (Pandas, NumPy, Matplotlib, Seaborn, SQLAlchemy)
     SQL for Data Extraction & Analysis
     Jupyter Notebook for Data Exploration

## Data Cleaning Steps in Python (Using Pandas)
Before storing the data in SQL, we need to clean and preprocess it.

  ## Step 1: Load the Data

import pandas as pd

### Load all CSV files
   
     customers = pd.read_csv("customers.csv")
     sellers = pd.read_csv("sellers.csv")
     order_items = pd.read_csv("order_items.csv")
     geolocation = pd.read_csv("geolocation.csv")
     payments = pd.read_csv("payments.csv")
     orders = pd.read_csv("orders.csv")
     products = pd.read_csv("products.csv")

### Step 2: Handle Missing Values

#### Check for missing values
print(customers.isnull().sum())

#### Fill missing values (if applicable) or drop them

    orders.dropna(subset=['order_status'], inplace=True)  
    geolocation.fillna(method='ffill', inplace=True)  
    
## Step 3: Remove Duplicates

### Remove duplicates in the dataset
  
     customers.drop_duplicates(inplace=True)
     sellers.drop_duplicates(inplace=True)
     order_items.drop_duplicates(inplace=True)
## Step 4: Convert Data Types for Accuracy

### Convert date columns to datetime format

     orders["order_purchase_timestamp"] = pd.to_datetime(orders["order_purchase_timestamp"])
     payments["payment_value"] = payments["payment_value"].astype(float)  # Convert prices to float
## Step 5: Merge Data for a Complete View
     We need to merge the datasets to create a single, structured dataset.


### Merge order details with customers and payments
     merged_data = orders.merge(customers, on="customer_id", how="left") \
                    .merge(order_items, on="order_id", how="left") \
                    .merge(products, on="product_id", how="left") \
                    .merge(payments, on="order_id", how="left")
                    
## Connecting to SQL Database (Using SQLAlchemy)
    After cleaning the data, we store it in MySQL/PostgreSQL for analysis.

## Step 6: Install Required Libraries

     pip install sqlalchemy,mysql-connector-python
## Step 7: Connect Python to SQL

    from sqlalchemy import create_engine

## MySQL database connection (Replace with your credentials)
   
      db_user = "root"
      db_password = "your_password"
      db_host = "localhost"
      db_name = "walmart_sales"

### Create a database connection
     engine = create_engine(f"mysql+mysqlconnector://{db_user}:{db_password}@{db_host}/{db_name}")

### Save data to MySQL tables
    merged_data.to_sql("walmart_sales", con=engine, if_exists="replace", index=False)
    print("Data successfully stored in SQL database!")
     Query Data from SQL for Analysis
Once the data is stored in SQL, we can use SQL queries to analyze it.

###  Visualizing the Data
Once we retrieve SQL data, we can visualize it using Matplotlib and Seaborn.

## Final Summary
    Loaded and cleaned the dataset.
    Removed missing values, duplicates, and fixed data types.
    Merged datasets for a structured view.
    Stored the cleaned data in MySQL using SQLAlchemy.
    Queried the SQL database to analyze E-commerce sales trends.
    Visualized the results using Matplotlib and Seaborn.
  
  
  
  
  
  
 
