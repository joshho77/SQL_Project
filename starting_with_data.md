# Josh Ho - SQL Project | Starting with Data

**Question 1: What is the distribution (minimum and maximum) between products ordered for each country and their city?**

SQL Queries: 
```SQL
SELECT DISTINCT 
	a.country,
	a.city, 
	min(s.totalordered) OVER w AS smallest_order,
	max(s.totalordered) OVER w AS largest_order
FROM all_sessions a
JOIN sales_report s
ON a.productsku = s.productsku
WINDOW w AS (PARTITION BY a.country 
	ORDER BY a.city)
ORDER BY a.country, a.city;
```
Answer: 

First 10 Columns

![](https://raw.githubusercontent.com/joshho77/SQL_Project/main/Images/q2.1.png "The first 10 columns of query")

Columns - country, city, smallest_order, largest_order

Rows - 366
***
\
\
**Question 2: How much web traffic (page views) was generated by each country, and what were the search engine methods used?**

SQL Queries:
```SQL
SELECT 
	country, 
	CASE
		WHEN as2.channelgrouping IS NULL THEN 'Total Views'
		ELSE as2.channelgrouping
	END AS search_method,
	sum(pageviews) AS page_views
FROM all_sessions as2 
GROUP BY ROLLUP (country, channelgrouping)
ORDER BY country, channelgrouping;
```
Answer:

![](https://raw.githubusercontent.com/joshho77/SQL_Project/main/Images/q2.2.png "The first 10 columns of query")

Columns - country, search_method, page_views

Rows - 500
***
\
\
**Question 3: Which product had the highest average sentiment score and sentiment magnitude?**

SQL Queries:
```SQL
SELECT
	name,
	AVG(sentimentscore) AS avg_sentiment_score,
	AVG(sentimentmagnitude) AS avg_sentiment_magnitude
FROM sales_report sr 
GROUP BY "name"
ORDER BY avg_sentiment_score DESC, avg_sentiment_magnitude DESC;
```
Answer:

![](https://raw.githubusercontent.com/joshho77/SQL_Project/main/Images/q2.3.png "The first 10 columns of query")

Columns - name, avg_sentiment_score, avg_sentiment_magnitude

Rows - 237



