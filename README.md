# Project 2: Retail Project

### Project Overview:
The primary goal of this project is to optimize inventory management and enhance sales forecasting for an online retail platform. By leveraging available data, the project aims to ensure that inventory levels align with customer demand, reducing excess stock and stockouts while improving customer satisfaction and profitability.

## 1. Finding and Analyzing Data

### Data Sources:
The following data sources from the dataset were utilized to achieve the business objective:

- **Sales Transactions**:
  - Customer Purchases: The `transaction_id`, `timestamp`, `customer_id`, `product_id`, `product_category`, `quantity`, `price`, `discount`, and `total_amount` columns provide insights into purchasing behavior, peak purchasing times, and popular product categories.

- **Customer Data**:
  - Demographics: The `customer_age`, `customer_gender`, and `customer_location` columns help in segmenting customers based on demographics, aiding in tailored marketing strategies and inventory decisions.

- **Product Data**:
  - Product Details: The `product_id`, `product_category`, `price`, and `discount` columns analyze product performance, pricing strategies, and the impact of discounts on sales volume.

### Success Metrics:
Success will be measured using the following metrics:

- **Reduced Stockouts**: Track the frequency and impact of stockouts on sales and customer satisfaction, aiming for a target reduction based on historical data.
- **Improved Forecast Accuracy**: Analyze sales forecast accuracy compared to actual sales, aiming for an accuracy improvement based on historical forecasting errors.
- **Optimized Ordering**: Measure the reduction in excess inventory costs by analyzing inventory turnover rates and aligning orders with forecasted demand.
- **Sales Growth**: Monitor overall sales growth by evaluating total revenue generated over specific periods compared to previous periods.
- **Customer Satisfaction**: Use feedback and return rates to measure satisfaction levels regarding product availability and order fulfillment.

### Dataset:
The dataset, sourced from Kaggle, consists of 100,000 rows and includes the following columns:

- `transaction_id` (IntegerType): Unique identifier for each transaction.
- `timestamp` (StringType): Date and time of the transaction.
- `customer_id` (IntegerType): Unique identifier for each customer.
- `product_id` (IntegerType): Unique identifier for each product.
- `product_category` (StringType): Category to which the product belongs.
- `quantity` (IntegerType): Number of units purchased.
- `price` (FloatType): Price per unit of the product.
- `discount` (FloatType): Discount applied to the transaction.
- `payment_method` (StringType): Method of payment.
- `customer_age` (IntegerType): Customer's age.
- `customer_gender` (StringType): Customer's gender.
- `customer_location` (StringType): Customer's geographical location.
- `total_amount` (FloatType): Total amount charged for the transaction.

---

## 2. Data Pipeline Creation

- **Data Ingestion**: 
  - Data was ingested from the on-premises SQL Server using **Azure Data Factory (ADF)** and a self-hosted integration runtime (IR) configured on my laptop.
  - The ingested data was copied to an **Azure Data Lake Storage (ADLS) Gen2** container, with an ADF pipeline trigger set to run weekly.

---

## 3. Transformation and Analytics

- **Secure Connection Setup**:
  - An **Azure service principal** stored in **Azure Key Vault** was used to connect **Azure Databricks** to **ADLS** for secure data access.

- **Data Cleaning & Transformation (PySpark)**:
  - Missing values in critical columns such as `customer_id`, `product_id`, and `total_amount` were removed.
  - Duplicate records based on customer transactions were dropped to ensure data accuracy and uniqueness.
  
- **New Columns**:
  - **age_group**: Created a new column to categorize customers into three groups:
    - `Young`: age ≤ 35
    - `Middle-aged`: 36 ≤ age ≤ 55
    - `Senior`: age > 55
  - **total_amount**: Calculated as the product of `quantity` and `price`.

- **Storage Format**:
  - The cleaned and transformed dataset was stored in **Parquet format** in ADLS due to its efficient storage, optimized performance, and compatibility.

- **SQL Queries in Azure Synapse Analytics**:
  - Created external tables in **Azure Synapse Analytics** and performed the following queries:
    - **Total Sales by Age Group**: Analyzed overall sales figures by age group.
    - **Average Quantity Sold per Product Category**: Determined the average quantity of products sold per category.
    - **Sales Distribution by Payment Method**: Analyzed sales distribution based on payment methods.
    - **Top 5 Products by Total Sales**: Identified top 5 products based on total sales.

---

## 4. Visualization (Power BI)

Connected **Azure Synapse Analytics** to **Power BI** to build interactive dashboards and reports. Key visualizations include:

1. **Total Sales by Age Group and Gender**:
   - A clustered bar chart displaying total sales categorized by age group (Young, Middle-aged, Senior) and gender (Male, Female, Other).
  
2. **Sales Distribution by Customer Location and Product Category**:
   - A map visualization showing sales across different customer locations and product categories, offering insights into geographical product demand.
  
3. **Top Customers by Total Sales**:
   - A pie chart representing the top customers driving the most revenue based on total sales.

4. **Total Sales and Discounts by Product Category and Gender**:
   - A scatter plot displaying the relationship between total sales and discounts, categorized by product category and gender.

5. **Overall Total Sales**:
   - A gauge chart showcasing overall sales performance against a set goal.

6. **Payment Method Distribution**:
   - A slicer for filtering sales data by payment method (Credit Card, Debit Card, PayPal, Gift Card).

7. **Filters for Interactive Insights**:
   - Slicers for customer location and age group allow dynamic filtering to gain insights into specific regions or demographics.

---

## 5. Conclusion:

This project demonstrates a comprehensive data engineering pipeline to enhance inventory management and sales forecasting for a retail company. Key highlights include:

- **Data Organization**: Following the Medallion Architecture, the data pipeline was structured for systematic ingestion, quality assurance, and transformation.
- **Actionable Insights**: SQL queries provided insights into customer behavior, inventory needs, and product trends, aiding decision-making in stock levels and marketing strategies.
- **Automation & Visualization**: The automated data pipeline using Azure services enables the company to adapt quickly to market trends, while the interactive Power BI dashboards facilitate data-driven decisions.

By leveraging Azure's cloud-based infrastructure and analytics tools, the retail company can improve operations, align inventory with demand, and enhance customer satisfaction.

