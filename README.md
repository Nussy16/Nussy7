# Let's consider a dataset containing information about customer purchases from an e-commerce platform. We'll go through the steps of loading the data, cleaning it, and preparing it for analysis, documenting each step along the way.

import pandas as pd

# Step 1: Loading the Data
df = pd.read_csv('ecommerce_data.csv')

# Step 2: Exploratory Data Analysis (EDA)
print(df.head())
print(df.describe())
print(df.isnull().sum())
print(df.dtypes)

# Step 3: Data Cleaning
df['product_category'].fillna('Unknown', inplace=True)
df['purchase_date'] = pd.to_datetime(df['purchase_date'])
df = df[df['quantity'] > 0]

# Step 4: Feature Engineering
df['purchase_year'] = df['purchase_date'].dt.year
df['purchase_month'] = df['purchase_date'].dt.month

# Step 5: Data Transformation
df = pd.get_dummies(df, columns=['product_category'])

# Step 6: Data Aggregation
customer_purchase = df.groupby('customer_id')['purchase_amount'].sum().reset_index()

# Step 7: Data Integration
customer_data = pd.merge(customer_data, customer_purchase, on='customer_id', how='left')

# Step 8: Data Validation
print(df.isnull().sum())

# Step 9: Data Export
df.to_csv('cleaned_ecommerce_data.csv', index=False)

#This script includes all the steps from loading the data to exporting the cleaned dataset into one Python file
