# Josh Ho - SQL Project | QA Process

What are your risk areas? Identify and describe them.
1. One risk is the amount of rows imported into the Postgres database not matching up with the number of rows form the original file, when it should. For example when opening the analytics.csv file using Excel, the application has a cut off how much data to show, as to not crash the application. This results in only 1048576 rows being shown, when in fact the file has 4301122 total rows. Thus, in order to not have any confusion, it is best to count the rows and confirm the total amount by comparing them.

QA Process and SQL Query:
```SQL
SELECT
	COUNT(*) AS row_count
FROM
	analytics a;
```

To validate the row count and successful loading of the data, I counted the number of rows in the raw unloaded data, then used the query above to count the rows of the loaded data. Comparing them to ensure they were equal, representing a successful load of the data into the Postgres database.

![](images/qa1.png "matching row count!")

***
2. Another risk area is having a row(s) of data with a NULL value when the column is a primary key, or has pertinent information and should be filled. An example of this is in the country column from the all_sessions table. It is important have this column filled with a complete set of data, as alot of querying is done with this column, and we will be deriving a lot of info based on where the customer is located.
```SQL
SELECT
	fullvisitorid,
	country,
	city 
FROM all_sessions as2
WHERE country IS NULL;
```

To validate this, we will be using a query to ensure there are no NULL values. The query will return rows that have a NULL value as well as their corresponding visitor id's and city (if any). Otherwise, it will be empty, meaning there are no rows will NULL values to return. In the chance that there are rows returned, we can address it with a CASE statement to fill in the row based on related information. (ex. if country = NULL, but city = Taipei, then we can interpolate that country = Taiwan). However, in this case we have identified that there are no NULL values in this column, which is great.

![](images/qa2.png "no null values!")
