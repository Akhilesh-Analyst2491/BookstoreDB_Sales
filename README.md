# Bookstore Analysis Using SQL

## Project Overview
This project focuses on analyzing a bookstore database using SQL. The dataset includes information about books, customers, and orders, allowing us to derive insights related to book sales, stock management, and customer purchases. The queries help in understanding revenue generation, stock availability, and customer ordering behavior.

## Data Sources
The analysis is based on structured data stored in MySQL, which includes:
- **Customers**: Details of registered customers (e.g., name, email, city, country).
- **Books**: Information about books available for sale (e.g., title, author, price, stock levels).
- **Orders**: Customer transactions, including order dates, quantities, and total amounts.

## Project Overview
1. Created MySQL tables to store bookstore data.
2. Imported data from CSV files into MySQL.
3. Executed analytical SQL queries to extract insights.

# SQL Queries for Bookstore Database

Here are the SQL queries for various tasks related to a bookstore database.

---

### 1. **Orders in November 2023**: Retrieve all orders placed within this month. 
```sql
SELECT * 
FROM Orders 
WHERE order_date BETWEEN '2023-11-01' AND '2023-11-30';
```
### 2. **Total Stock**: Calculate the total number of books available in stock.
```sql
SELECT SUM(Stock) AS Total_Stock 
FROM Books;
```

### 3. **Most Expensive Book**: Identify the most expensive book in the collection.
```sql
SELECT * 
FROM Books 
ORDER BY Price DESC 
LIMIT 1;
```
### 4. **Customers Who Ordered More Than One Item**: Find customers who purchased multiple books.
```sql
SELECT * 
FROM Orders 
WHERE Quantity > 1;
```
### 5. **High-Value Orders**: Retrieve all orders where the total amount exceeds 20.
```sql
SELECT * 
FROM Orders 
WHERE Total_Amount > 20;
```
### 6. **List of Available Genres**: Display all unique book genres in the database.
```sql
SELECT DISTINCT Genre 
FROM Books;
```
### 7. **Lowest Stock Book**: Identify the book with the least stock remaining.
```sql
SELECT * 
FROM Books 
ORDER BY Stock ASC 
LIMIT 1;
```
### 8. **Total Revenue Calculation**: Compute the total revenue generated from all sales.
```sql
SELECT SUM(Total_Amount) AS Total_Revenue 
FROM Orders;
```
#### 9. **Stock Remaining After Orders**: Calculate the stock left after fulfilling all orders.
```sql
SELECT b.Book_ID, 
       b.Title, 
       b.Stock AS Initial_Stock, 
       COALESCE(SUM(o.Quantity), 0) AS Total_Sold, 
       (b.Stock - COALESCE(SUM(o.Quantity), 0)) AS Remaining_Stock
FROM Books b
LEFT JOIN Orders o ON b.Book_ID = o.Book_ID
GROUP BY b.Book_ID, b.Title, b.Stock;
```


## Limitations and Challenges
- **Incomplete Data Handling**: Missing customer details may affect order analysis.
- **Stock Limitations**: The analysis assumes real-time stock updates, but delays might exist.
- **Revenue Calculation Complexity**: Discounts and promotions (if any) are not considered in total revenue.

## Results and Insights
- Identified high-selling books and their respective genres.
- Determined peak order periods and customer purchasing behaviors.
- Analyzed stock levels to optimize inventory management.
- Estimated total revenue and order trends.

## Conclusion
This analysis provides valuable insights into the bookstore's sales, stock levels, and customer preferences. By leveraging SQL queries, bookstore managers can optimize inventory, boost sales, and improve customer satisfaction.

## Additional Insights
- **Top Customers by Spending**: Identifying the customers who generate the highest revenue.
- **Best-Selling Book Categories**: Analyzing the most popular genres based on sales data.
- **Order Frequency by Customer**: Determining which customers make repeat purchases.
- **City-Wise Sales Performance**: Understanding regional differences in book demand.


## Future Work
- Incorporate discounts and promotions into revenue calculations.
- Analyze seasonal sales trends for better stock planning.
- Implement machine learning models for sales forecasting.

## How to Use
1. **Run `create_tables.sql`** to set up the database structure.
2. **Execute `import_data.sql`** to load data into MySQL.
3. **Run queries from `queries.sql`** to analyze the bookstore data.

## Requirements
- MySQL 8.0+
- MySQL Workbench

