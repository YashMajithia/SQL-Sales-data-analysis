# SQL-Sales-data-analysis

## Project Overview

This project analyzes a simulated sales dataset to gain insights into product performance and customer behavior. It utilizes SQL to query the data and extract meaningful information.

## Database Schema

The database consists of three tables:

* **Products:**
    * `ProductID` (INTEGER, PRIMARY KEY)
    * `ProductName` (TEXT)
    * `Category` (TEXT)
    * `Price` (REAL)
* **Customers:**
    * `CustomerID` (INTEGER, PRIMARY KEY)
    * `CustomerName` (TEXT)
    * `City` (TEXT)
* **Sales:**
    * `SaleID` (INTEGER, PRIMARY KEY)
    * `ProductID` (INTEGER, FOREIGN KEY)
    * `CustomerID` (INTEGER, FOREIGN KEY)
    * `SaleDate` (DATE)
    * `Quantity` (INTEGER)

## Setup Instructions

1.  **Install SQLite (or your chosen DBMS):** Download and install SQLite from [SQLite website](https://www.sqlite.org/download.html) or use your chosen DBMS.
2.  **Create the Database:** Use the SQL scripts provided in the `scripts` folder (or inline in this file) to create the tables.
3.  **Populate the Tables:** Use the provided `INSERT` statements to add sample data.
4.  **Run the Queries:** Execute the SQL queries in the `queries.sql` file to analyze the data.

## SQL Queries and Analysis

The following queries were used to analyze the data:

* **Total sales per product:**
    ```sql
    SELECT p.ProductName, SUM(s.Quantity) AS TotalSales
    FROM Sales s
    JOIN Products p ON s.ProductID = p.ProductID
    GROUP BY p.ProductName;
    ```
    * *Analysis:* This query calculates the total quantity of each product sold.

* **Top-selling product:**
    ```sql
    SELECT p.ProductName, SUM(s.Quantity) AS TotalSales
    FROM Sales s
    JOIN Products p ON s.ProductID = p.ProductID
    GROUP BY p.ProductName
    ORDER BY TotalSales DESC
    LIMIT 1;
    ```
    * *Analysis:* This query identifies the product with the highest total sales quantity.

* **Total Revenue:**
    ```sql
    SELECT SUM(p.Price * s.Quantity) AS TotalRevenue
    FROM Sales s
    JOIN Products p ON s.ProductID = p.ProductID;
    ```
    * *Analysis:* This query calculates the total revenue from all sales.

* **Customer purchase amounts:**
    ```sql
    SELECT c.CustomerName, SUM(p.Price * s.Quantity) AS TotalSpent
    FROM Sales s
    JOIN Products p ON s.ProductID = p.ProductID
    JOIN Customers c on s.CustomerID = c.CustomerID
    GROUP BY c.CustomerName;
    ```
    * *Analysis:* This query shows how much each customer has spent.

## Key Findings
1. Top-selling products: Mice and Books were the top-selling products in terms of quantity.
2. Revenue: The business generated a total revenue of $12,560.00 from the sales.
3. Customer Insights: Henry Martinez was the highest-spending customer, followed by Alice Smith.
