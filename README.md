# SQL Data Analysis and Transformation Assignment

## Overview

This repository contains solutions to an SQL data analysis and transformation assignment. The exercises focus on leveraging SQL to manipulate, aggregate, and analyze data from a fictional dataset related to countries and their various attributes, such as region, income category, and country codes. The tasks range from simple data retrieval to more complex aggregations, transformations, and calculations, aimed at reinforcing SQL proficiency for real-world data analysis.


## Objective

The goal of this assignment is to improve SQL competency, particularly in the areas of:

- **Data Retrieval**: Using `SELECT`, `WHERE`, and `JOIN` statements to fetch and filter relevant data.
- **Aggregation**: Using aggregate functions like `COUNT()`, `SUM()`, `AVG()`, and grouping data with `GROUP BY`.
- **Data Transformation**: Using `CASE` statements, subqueries, and complex queries to manipulate data.
- **Data Analysis**: Analyzing complex datasets through multiple steps, ensuring accurate results and insights.

## Skills Utilized

- **Basic SQL Queries**: `SELECT`, `WHERE`, `ORDER BY`
- **Aggregation**: `COUNT()`, `SUM()`, `GROUP BY`
- **Subqueries**: For more complex data retrieval.
- **Joins**: Combining data from multiple tables.
- **`CASE` Statements**: Conditional logic for handling missing or custom data.
- **Data Transformation**: Pivot tables, percentage calculations, and data reshaping.

## Tasks and Solutions

### Task 1: List all unique values of regions in the `wdi_country` table.
- **Objective**: Identify the distinct values for regions in the dataset.
- **SQL Approach**: Use `SELECT DISTINCT` on the region field.

### Task 2: Count the number of countries in each region.
- **Objective**: Aggregate the number of countries within each region using `GROUP BY` and `COUNT()`.

### Task 3: Identify countries in North America.
- **Objective**: List country full names and regions for countries in North America, filtering the data based on region.

### Task 4: Investigate the income category field.
- **Objective**: Group countries by income category and count how many belong to each category.

### Task 5: Analyze country abbreviations (`country_abbr` and `country_wb_abbr`).
- **Objective**: Identify countries with mismatched abbreviations across the two fields.

### Task 6: Display the region and income group pairings, including missing values.
- **Objective**: Use `CASE` and aggregation to display each region and income group combination, showing missing values in the dataset.

### Task 7: Calculate the percentage of countries in each income category.
- **Objective**: Calculate percentages of countries in each income category relative to the total.

### Task 8: Find regions with the highest number of low-income countries.
- **Objective**: Aggregate low-income countries by region and display the region with the highest number.

### Task 9: Look at the Marshall Islands' region and income category.
- **Objective**: Query for countries with the same region and income category as the Marshall Islands.

### Task 10: Create pivot tables displaying the number of countries in each region-income pair.
- **Objective**: Use `CASE` statements to create pivot tables and display the percentage of total countries per income category in each region.

## SQL Queries

Here are some of the queries used in the assignment:

```sql
-- Query to list unique regions
SELECT DISTINCT region FROM wdi_country;

-- Query to count the number of countries in each region
SELECT region, COUNT(*) AS num_countries FROM wdi_country GROUP BY region;

-- Query to list countries in North America
SELECT country_full_name, region FROM wdi_country WHERE region = 'North America' ORDER BY country_full_name;

-- Query to count countries by income category
SELECT income_category, COUNT(*) AS num_countries FROM wdi_country GROUP BY income_category ORDER BY num_countries DESC;

-- Query to identify mismatched abbreviations
SELECT country_code, country_short_name, country_abbr, country_wb_abbr, region 
FROM wdi_country 
WHERE country_abbr != country_wb_abbr;

-- Query to calculate percentages of countries by income category
SELECT region, income_category, COUNT(*) AS num_countries,
       SUM(COUNT(*)) OVER (PARTITION BY region) AS region_total,
       SUM(COUNT(*)) OVER (PARTITION BY income_category) AS income_total,
       COUNT(*) / SUM(COUNT(*) OVER ()) * 100 AS percentage_of_total
FROM wdi_country
GROUP BY region, income_category
ORDER BY region, income_category;
