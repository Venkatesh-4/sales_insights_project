# Sales Insights Project

Learning Power BI with fictitious sales data from a MySQL server. The YouTube series followed can be found here: [YouTube Playlist](https://youtube.com/playlist?list=PLeo1K3hjS3uva8pk1FI3iK9kCOKQdz1I9&si=SmLgTp2Bqn19i7cx).

## Objective

To learn Power BI using fictitious sales data from a MySQL server. The goal is to create a dashboard that can be easily used by anyone to analyze the sales data.

## Steps

1. Load data into MySQL and perform some initial analysis of the data (EDA).
2. Load the data into Power BI to create the dashboard.

## Dashboard Images

1. Key Insights page
  ![key_insights](https://github.com/Venkatesh-4/sales_insights_project/assets/46065241/30a9ee0c-f027-43a3-914b-5d9b2513ba2d)

3. Profit Analysis page
  ![profit_analysis](https://github.com/Venkatesh-4/sales_insights_project/assets/46065241/b277e5ea-8c3f-4f27-a183-0979619f414f)

5. Performance Insights page
  ![perfomance_insights](https://github.com/Venkatesh-4/sales_insights_project/assets/46065241/04a3f9ea-d30e-4a0e-8336-966e8741a89a)

### MySQL

Some of the queries used were:

1. Show the total number of customers:
   ```sql
   SELECT count(*) FROM customers;
   ```

2. Show transactions for the Chennai market (market code for Chennai is Mark001):
   ```sql
   SELECT * FROM transactions WHERE market_code='Mark001';
   ```

3. Show distinct product codes that were sold in Chennai:
   ```sql
   SELECT DISTINCT product_code FROM transactions WHERE market_code='Mark001';
   ```

4. Show transactions where the currency is US dollars:
   ```sql
   SELECT * FROM transactions WHERE currency='USD';
   ```

5. Show transactions in 2020 joined by the date table:
   ```sql
   SELECT transactions.*, date.* 
   FROM transactions 
   INNER JOIN date ON transactions.order_date=date.date 
   WHERE date.year=2020;
   ```

6. Identify the frequency of sales quantities to check which quantity size is most preferred:
   ```sql
   SELECT sales_qty, count(*) 
   FROM transactions 
   GROUP BY sales_qty 
   ORDER BY count(*) DESC;
   ```

### Power BI

1. Established relationships between tables and transformed the markets table.
   - Sales in the USA and Paris were one-off events, so they were excluded from the sales analysis as the primary market for the company is in India.

2. Transformed the transactions table:
   - Removed transactions with sales quantities less than or equal to 0.
   - Normalized currency to INR and adjusted the data for two different USD values.

3. Removed duplicate rows in the transactions table:
   - USD and INR repeat. **Attempted to use a spot conversion table to convert the USD values to INR**.

4. Created the base_measures table and started dashboard development:
   - Created two base measures: revenue and sales quantity.
   - Displayed both measures along with a horizontal bar chart displaying revenue by customer.

5. Visualized per customer quantity and revenue per year and month:
   - Altered the `cy_date` column format to make it more understandable and concise.

6. Changed the classification base to Region:
   - Changed revenue and sales quantity to be based on the region as opposed to the customer.

7. Added Top 5 customers and products:
   - Resized elements, changed bar colors, altered certain titles, and changed the canvas background to aid with element positioning.

8. Added Revenue trend:
   - Added a line chart depicting the revenue trend and rearranged the elements to make it more understandable.

9. Visualized revenue by customer and product type along with sales frequency:
   - Added bar charts depicting the customer and product type with the highest revenue.
   - Added a bar chart to represent the most frequent sales quantities purchased by customers to see the type/size of customers availing the service.

10. Changed Visual Options:
    - Changed the default visual interaction from cross-highlighting to cross-filtering to avoid highlighting data with zero values after filtering.

11. Updated Database, New Measures Added Along with New Report Page:
    - Updated the database: The transactions table now includes three new columns: profit margin, percentage, and cost_price. Removed norm_sales and the USD filter. Altered the revenue base measure formula.
    - Added new measures: Profit margin and profit margin percentage. Displayed region-wise profit margin percentage.

12. New Measure Added and Visualized:
    - Created a new measure for profit margin contribution percentage to identify individual contributions to the total margin.

13. Created New Measure:
    - Created a measure called Revenue Contribution Percentage and visualized the results.

14. Multi-Dimensional Table View:
    - Generated a Customers table displaying Revenue, Revenue Contribution Percentage, Profit Margin Contribution Percentage, and Profit Margin Percentage.

15. Added Dimension to Revenue Contribution Graph:
    - Added the customer type dimension to the revenue contribution percentage by region table. Renamed the different pages to better reflect their purpose and intent.

16. Performance Insights Page Created:
    - Created a graph with profit margin percentage with respect to region and zone. Developed a measure called Target Difference, which the graph's color function uses to highlight data based on a slider.

17. Graph Axis Element Change, Extra Dimension Added:
    - Moved the zone dimension above the region to better reflect the hierarchy of the drill-down action. Added the customer name dimension to the graph. Created a measure to obtain the previous year's revenue, given the current year as input.

18. Chart Title Measure Added:
    - Added a measure to dynamically change the chart's title based on the drill-down action. When attempting to go to the next hierarchy level (clicking the double arrow key on the chart), nothing changes.

19. Revenue Trend Double Bar Chart Added:
    - Converted the line chart into a line and clustered column chart. Plotted revenue and LY (last year) revenue side by side. Added a profit margin percentage line.
