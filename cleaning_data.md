# Josh Ho - SQL Project | Cleaning Data
**What issues will you address by cleaning the data?**

1. Creating table and column names with effective and concise naming conventions, and selecting appropriate data types.
```SQL
CREATE TABLE products (
	id BIGSERIAL,
	SKU VARCHAR(50),
	name VARCHAR(100),
	orderedQuantity INT,
	stockLevel INT,
	restockingLeadTime INT,
	sentimentScore INT,
	sentimentMagnitude FLOAT,
	PRIMARY KEY(id));
)
```
\
2. Deleting irrelevant columns, especially those with only NULL values.
```SQL
ALTER TABLE all_sessions
DROP COLUMN productRefundAmount;
```
\
3. Modifying column data types to appropriate data types (ex. INT was originally casted as the data type, but then altered to FLOAT as the row values were decimals)
```SQL
ALTER TABLE products
ALTER COLUMN sentimentScore FLOAT;
```
\
4. Fill in missing values with logical possibilities (ratio is 0 for products with 0 orders, or when city has a value of "(not set)" then replace it with something more relatable).
```SQL
SELECT country,
CASE
    WHEN country = '(not set)' THEN 'Not specified'
    ELSE country 
FROM products
```
\
5. Formatting integer values into logical values (unit price in dollars, time into sec/min, numbers in dates).
```SQL
SELECT (productPrice/1000000) AS product_price
FROM products
```
\
8. Adding and setting logical primary key columns to each table.
```SQL 
CREATE TABLE products (
id BIGSERIAL,
PRIMARY KEY (id)) 
``` 





