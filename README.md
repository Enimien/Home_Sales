# Home_Sales
Import all dependencies
Import packages
Create a spark session
Read in the Aws S3 bucket into a dataframe and display the data frame
Create a temporary view of the DataFrame.
Determine the average sale price of four-bedroom houses for each year, rounded to two decimal places. This metric helps in understanding the market trends and price fluctuations over time for specific property types.
SELECT YEAR(date) AS YEAR,extracts the year from the date column and labels it as YEAR,ROUND(AVG(price), 2) AS AVERAGE_PRICE,calculates the average price of the houses and rounds it to two decimal places, labeling the result as AVERAGE_PRICE FROM home_sales,indicates that the data is being queried from the home_sales temporary view.WHERE bedrooms = 4 Filters the data to include only records where the number of bedrooms is four.
GROUP BY YEAR Groups the data by the extracted year to calculate the average price per year.
ORDER BY YEAR DESC Orders the results in descending order based on the year, displaying the most recent year first.

Determine the average sale price of homes that have 3 bedrooms and 3 bathrooms for each year they were built. This analysis helps in understanding how property prices for specific home configurations have evolved over time.
SELECT Clause YEAR(date_built) AS YEAR: Extracts the year from the date_built column and labels it as YEAR.
ROUND(AVG(price), 2) AS AVERAGE_PRICE: Calculates the average price of the homes and rounds it to two decimal places, labeling the result as AVERAGE_PRICE.
FROM Clause FROM home_sales: Specifies the temporary view home_sales as the data source.
WHERE Clause WHERE bedrooms = 3 AND bathrooms = 3: Filters the data to include only those homes that have exactly 3 bedrooms and 3 bathrooms.
GROUP BY Clause GROUP BY YEAR(date_built): Groups the data by the year the home was built to calculate the average price per year.
ORDER BY Clause ORDER BY YEAR DESC: Orders the results in descending order based on the year, showing the most recent year first.

Determine the average sale price of homes that meet the following criteria for each year they were built:

3 bedrooms
3 bathrooms
Two floors
Living area ≥ 2,000 square feet
SELECT Clause:

YEAR(date_built) AS YEAR_BUILT: Extracts the year from the date_built column and labels it as YEAR_BUILT.
ROUND(AVG(price), 2) AS AVERAGE_PRICE: Calculates the average price of the homes meeting the criteria and rounds it to two decimal places, labeling the result as AVERAGE_PRICE.
FROM Clause:

FROM home_sales: Specifies the temporary view home_sales as the data source.
WHERE Clause:

WHERE bedrooms = 3 AND bathrooms = 3 AND sqft_living >= 2000 AND floors = 2: Filters the data to include only those homes that have exactly 3 bedrooms, 3 bathrooms, two floors, and a living area of at least 2,000 square feet.
GROUP BY Clause:

GROUP BY YEAR_BUILT: Groups the data by the year the home was built to calculate the average price per year.
ORDER BY Clause:

ORDER BY YEAR_BUILT DESC: Orders the results in descending order based on the year, showing the most recent year first.

Determine the average sale price of homes for each "view" rating, considering only those with an average price greater than or equal to $350,000. Additionally, measure the runtime of this query to evaluate its performance, even though the dataset is small.

SELECT Clause view: Retrieves the "view" rating of the home.
ROUND(AVG(price), 2) AS AVERAGE_PRICE: Calculates the average price of homes for each view rating, rounded to two decimal places, and labels it as AVERAGE_PRICE.
FROM  home_sales: Specifies the temporary view home_sales as the data source.
GROUP BY view: Groups the data by the "view" rating to calculate the average price for each category.
HAVING AVG(price) >= 350000: Filters the groups to include only those with an average price of $350,000 or higher.
ORDER BY view DESC: Orders the results in descending order based on the "view" rating.
Runtime Measurement time.time() Captures the current time before and after the query execution to calculate the total runtime.

Primary Goal: Calculate the average price of homes per "view" rating, rounded to two decimal places, for homes with an average price ≥ $350,000, and determine the runtime of this query.
Secondary Goal: Compare the runtime of the query executed on uncached data versus cached data to assess the performance benefits of caching in Spark.

The view column represents the quality or type of view from the home.
The AVG(price) function computes the mean price of homes for each view rating, rounded to two decimal places for precision.
Filtering: The HAVING clause ensures that only those view ratings with an average price of $350,000 or higher are included in the results.
Ordering: The results are ordered in descending order based on the view rating to prioritize higher-rated views.

caching provides measurable performance benefits, which become more significant with larger datasets or more complex queries.

Optimize the storage and query performance of your home sales data by partitioning the Parquet files based on the date_built field. Partitioning organizes data into distinct directories based on the unique values of the partition column, enabling more efficient data retrieval and management and  Read the parquet formatted data.

Create a temporary table for the parquet data.

Using the parquet DataFrame, run the last query above, that calculates the average price of a home per "view" rating, rounded to two decimal places,having an average home price greater than or equal to $350,000.

Caching the dataset significantly reduces query execution time, especially for repeated queries. This project demonstrates the performance benefits of caching in Spark and highlights the flexibility of working with Parquet files for large-scale data analysis.
Determine the runtime and compare it to the cached runtime.

 Uncache the home_sales temporary table.
 Check if the home_sales is no longer cached