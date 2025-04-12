# Home_Sales
Big Data Module 22 Challenge (Week 22)
## Instructions

Import the necessary PySpark SQL functions for this assignment.
Read the home_sales_revised.csv from the provided AWS S3 bucket location into a PySpark DataFrame.
Create a temporary table called home_sales.

Answer the following questions using SparkSQL:
  - What is the average price for a four-bedroom house sold for each year? Round off your answer to two decimal places.
      query = """
        SELECT YEAR(date) AS year, ROUND(AVG(price), 2) AS avg_price
        FROM home_sales
        WHERE bedrooms = 4
        GROUP BY year
        ORDER BY year;
        """
      spark.sql(query).show()

  - What is the average price of a home for each year the home was built, that has three bedrooms and three bathrooms? Round off your answer to two decimal places.
      query = """
        SELECT date_built, ROUND(AVG(price), 2) AS avg_price
        FROM home_sales
        WHERE bedrooms = 3
        AND bathrooms = 3
        GROUP BY date_built
        ORDER BY date_built DESC;
        """

      spark.sql(query).show()

  - What is the average price of a home for each year the home was built, that has three bedrooms, three bathrooms, two floors, and is greater than or equal to 2,000 square feet? Round off your answer to two decimal places.
      query = """
        SELECT date_built, ROUND(AVG(price), 2) AS avg_price
        FROM home_sales
        WHERE bedrooms = 3
        AND bathrooms = 3
        AND floors = 2
        AND sqft_living >= 2000
        GROUP BY date_built
        ORDER BY date_built;
        """
    spark.sql(query).show()

  - What is the average price of a home per "view" rating having an average home price greater than or equal to $350,000? Determine the run time for this query, and round off your answer to two decimal places.
      start_time = time.time()
      query = """
        SELECT view, ROUND(AVG(price), 2) AS avg_price
        FROM home_sales
        GROUP BY view
        HAVING AVG(price) >= 350000
        ORDER BY view DESC;
        """
      spark.sql(query).show()
      print("--- %s seconds ---" % (time.time() - start_time))
      start_time = time.time()
      print("--- %s seconds ---" % (time.time() - start_time))

Cache your temporary table home_sales.

Check if your temporary table is cached.

Using the cached data, run the last query that calculates the average price of a home per "view" rating having an average home price greater than or equal to $350,000. Determine the runtime and compare it to uncached runtime.

Partition by the "date_built" field on the formatted parquet home sales data.

Create a temporary table for the parquet data.

Run the last query that calculates the average price of a home per "view" rating having an average home price greater than or equal to $350,000. Determine the runtime and compare it to uncached runtime.

Uncache the home_sales temporary table.

Verify that the home_sales temporary table is uncached using PySpark.

Download Home_Sales.ipynb file and upload it into "Home_Sales" GitHub repository.
