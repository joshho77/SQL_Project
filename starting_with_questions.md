# Josh Ho - SQL Project | Starting with Questions

Answer the following questions and provide the SQL queries used to find the answer.

**Question 1: Which cities and countries have the highest level of transaction revenues on the site?**


SQL Queries:
```SQL
SELECT 
	country, 
	city, 
	sum(totaltransactionrevenue) AS total_transaction_revenue
FROM all_sessions as2 
WHERE totaltransactionrevenue IS NOT NULL 
GROUP BY country, city 
ORDER BY total_transaction_revenue DESC;
```


Answer:

First 10 Columns

![](https://raw.githubusercontent.com/joshho77/SQL_Project/main/Images/q1.1.png "The first 10 columns of query")

Columns - country, city, total_transaction_revenue

Rows - 22

Highest Revenue - United States, City not specified, $6829680000
\
\
\
**Question 2: What is the average number of products ordered from visitors in each city and country?**


SQL Queries:
```SQL
SELECT 
	a.country,
	a.city,
	ROUND(AVG(s.totalordered),2) AS total_ordered
FROM all_sessions a
JOIN sales_report s 
ON a.productsku = s.productsku 
GROUP BY a.country, a.city 
ORDER BY a.country; 
```

Answer:

![](https://raw.githubusercontent.com/joshho77/SQL_Project/main/Images/q1.2.png "The first 10 columns of query")

Columns - country, city, total_ordered

Rows - 336
\
\
\
**Question 3: Is there any pattern in the types (product categories) of products ordered from visitors in each city and country?**


SQL Queries:
```SQL
SELECT 
	country,
	city,
	v2productcategory AS product_category  
FROM all_sessions a
ORDER BY country, city;
```

Answer:

![](https://raw.githubusercontent.com/joshho77/SQL_Project/main/Images/q1.3.png "The first 10 columns of query")

Columns - country, city, product_category

Rows - 15134

Insight - Each city seems to purchase different products from a variety of product categories - therefore one pattern is the fact that each city purchases things in varying categories.
\
\
\
**Question 4: What is the top-selling product from each city/country? Can we find any pattern worthy of noting in the products sold?**


SQL Queries:
```SQL
SELECT 
	country,
	city,
	v2productname AS product, 
	COUNT(v2productname) AS total_orders
FROM all_sessions 
GROUP BY country, city, product
ORDER BY total_orders DESC;
```

Answer:

![](https://raw.githubusercontent.com/joshho77/SQL_Project/main/Images/q1.4.png "The first 10 columns of query")

Columns - country, city, product, total_orders

Rows - 7628

Insight - Companies owned by Alphabet (Google, Youtube) are the most sold products amongs all cities, with their branded products having the highest order numbers.
\
\
\
**Question 5: Can we summarize the impact of revenue generated from each city/country?**

SQL Queries:
```SQL
SELECT 
	a.country, 
	a.city, 
    (s.totalordered * (a.productprice/1000000)) AS revenue
FROM all_sessions a
JOIN sales_report s 
ON a.productsku = s.productsku 
WHERE s.totalordered > 1
ORDER BY a.country, a.city; 
```

Answer:

![](https://raw.githubusercontent.com/joshho77/SQL_Project/main/Images/q1.5.png "The first 10 columns of query")

Columns - country, city, revenue

Rows - 6807






