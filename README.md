# Sales Performance Analysis for a Retail Store 
This project is tasked with analyzing the sales performance of a retail store by exploring the sales data to uncover key insights such as top-selling products, regional 
performance and monthly sales trends. The goal is to produce an interactive Power BI dashboard that highlights these findings.

[Overview](#overview)

[Data Sources](#data-sources)

[Tools Used](#tools-used)

[Data Cleaning and Preparation](#data-cleaning-and-preparation)

[Exploratory Data Analysis](#exploratory-data-analysis)

[Data Analysis](#data-analysis)

[Data Visualization](#data-visualization)

[Findings and Insights](#findings-and-Insights)

[Recommendations](#recommendations)

[Areas of Discussion](#areas-of-discussion)

[Conclusion](#conclusion)

### Overview
---
This Data Analysis project aims to generate insight into the sales performance of an E-commerce business over the period of two years. By analysing the various parameters in the dataset received, I seek to gather enough insight to make informed and reasonable decisions which will ultimately enable me tell  compelling stories around the data and to know the best performance from the dataset.
### Data Sources
The primary source of data used here is Sales Data.csv and this is an open source data that can be freely downloaded from an open source online such as Kaggle, FRED or any other data repository site.

### Tools Used
---
- Microsoft Excel [Download Here](https://www.microsoft.com)
   1. For Data Cleaning
   2. For Analysis
   3.  For Data Visualization.
- SQL
  Structured Query Language for Querying & Analysis.
- Power BI
  Report Creation and Advance Data Visualization.
- GitHub
  Portfolio Development and Version Control

 ### Data Cleaning and Preparation
 ---
  In the initial phase, I performed the following steps to ensure the dataset was ready for analysis: 

1. **Data Loading and Inspection**
   - Imported the dataset into Excel and checked for data integrity.
   - Reviewed column headers, data types, and overall structure.

2. **Handling Missing Values**
   - Identified and addressed missing values by using techniques such as:
     - Filling missing values with the mean/median where appropriate.
     - Removing records with excessive missing data.
     - Removing duplicates from dataset

3. **Data Cleaning and Formatting**
   - Standardized date formats and ensured consistency across entries.
   - Converted relevant columns into appropriate data types (e.g., currency, dates).

### Exploratory Data Analysis
---
EDA involved the process of exploring the dataset to answer some questions about the data such as;
- What is the overall sales trend?
- Which product are top sellers?
- What are the products on peak sales?

### Data Analysis
---
This is where I add some lines of code, queries and DAX expressions used during analysis;
#### Key Metrics Analyzed
- Total Sales over time
- Monthly sales trends
- Product performance analysis
- Customer demographics and purchasing behavior

#### SQL Queries
I used SQL to extract specific insights from the dataset, such as:
- Monthly sales totals
- Product category performance
- Customer retention rates

```SQL
SELECT * FROM [dbo].[Sales Data]

--------------To create Revenue column
ALTER TABLE[dbo].[Sales Data]
ADD Revenue int

UPDATE[dbo].[Sales Data]
SET Revenue = (Quantity*UnitPrice)

--------------To create Total Sales column
ALTER TABLE [dbo].[Sales Data]
ADD Total_Sales int

UPDATE[dbo].[Sales Data]
SET Total_Sales =(Quantity*UnitPrice)

ALTER TABLE[dbo].[Sales Data]
DROP column TotalSales

-----------------Retrieve the total sales for each product category.

SELECT Product, SUM(Total_Sales) as Sales_per_Product
FROM[dbo].[Sales Data]
GROUP by Product

-----------------Find the number of sales transactions in each region.

SELECT Region,SUM(Total_Sales) as Sales_per_Region
FROM[dbo].[Sales Data]
GROUP by Region

-----------------Find the highest-selling product by total sales value.

SELECT PRODUCT, SUM(Total_Sales) as top_selling_products
FROM[dbo].[Sales Data]
GROUP by PRODUCT
Order by top_selling_products desc

-----------------Calculate total revenue per product

SELECT Product,SUM(Quantity*UnitPrice) as Total_Revenue
FROM[dbo].[Sales Data]
GROUP BY Product

---------------To create OrderMonth column

ALTER TABLE[dbo].[Sales Data]
ADD OrderMonth nvarchar(50)

UPDATE[dbo].[Sales Data]
SET OrderMonth = DATENAME(MONTH, OrderDate)

Select * 
from [dbo].[Sales Data]

----------------To create orderYear column

ALTER TABLE[dbo].[Sales Data]
ADD OrderYear int

UPDATE[dbo].[Sales Data]
SET OrderYear = Year(OrderDate)

----------------Calculate total monthly sales  for the current year(2024)

SELECT  OrderMonth, 
	SUM(Revenue) as Total_Sales
FROM[dbo].[Sales Data]
WHERE OrderYear = 2024
GROUP BY OrderMonth

---------------Top 5 customers by Total Purchase

SELECT  Top 5 Customer_Id,SUM(Quantity) as Total_Purchase
FROM [dbo].[Sales Data]
GROUP BY Customer_Id
ORDER BY Total_Purchase DESC

-------------Calculate the percentage of total sales contributed by each region.

SELECT Region,SUM(Revenue) as Region_Sales,
(sum(Revenue) / (select sum(Revenue) from[dbo].[Sales Data])*100) as percentage_of_Revenue
from[dbo].[Sales Data]
group by Region

SELECT Region,SUM(Revenue) as Region_Sales,
Count(Revenue) * 100 / sum(count(Revenue)) over() as Percentage_of_Revenue
from[dbo].[Sales Data]
group by Region

--------------Identify products with no sales in Months 10, 11, and 12 (October to December)

SELECT Product,SUM(Quantity) AS Sales
FROM[dbo].[Sales Data]
WHERE MONTH(OrderDate) BETWEEN 10 AND 12
GROUP BY Product
HAVING SUM(Quantity)= 0
```
### Data Visualization
📈
#### Excel Dashboards
- Created interactive dashboards in Excel that highlight key sales metrics, including:
  - Sales trends over time
  - Top-selling products
  - Customer demographics

[Rev Table](https://github.com/user-attachments/assets/a136dd95-58ba-4894-8f0d-95060fb4d60b)

[Quantity Table](https://github.com/user-attachments/assets/04807086-07cd-4bc9-9c3a-ae52b2da1582)

[RegionTable](https://github.com/user-attachments/assets/7f18593d-62b8-4402-9122-fd4da928a29f)

[MonthTable](https://github.com/user-attachments/assets/dfc01191-0e83-47bb-b09d-ce72afdadef1)

[Bottom 3 Table](https://github.com/user-attachments/assets/a454c9d1-b924-4b0e-b693-3c43caa1378e)

[Top 3 Table](https://github.com/user-attachments/assets/22ca1098-a421-4372-89ec-a4138c33b22d)

[Ave Sales Table](https://github.com/user-attachments/assets/61e7c4c4-9ba4-46bd-b281-f6edfc0f0900)

[Product Table](https://github.com/user-attachments/assets/5965c1e3-2a41-4a3c-a47d-4fb6efc804bf)

[SalesTable](https://github.com/user-attachments/assets/2922e43f-a30f-4dc2-844e-4595d5ea860b)

[ProductTable](https://github.com/user-attachments/assets/da190a56-44a0-4718-ab78-7ed4767e1986)

[BarChart Bottom Product](https://github.com/user-attachments/assets/88db099a-9904-40b3-8b5c-e6558260a4de)

[PieChart Sales](https://github.com/user-attachments/assets/80351ec0-8290-4cd3-8ed8-9115cf2cf959)

[Chart Revenue Product](https://github.com/user-attachments/assets/fd886017-9b47-43fa-a92a-10f27842f46b)

[DonutChart UnitSold](https://github.com/user-attachments/assets/ed18bd0d-e8f2-4157-8a5f-6ebd82e520d6)

[BarChart](https://github.com/user-attachments/assets/283c72d0-e49d-4458-8c62-88d0b566f5c6)


#### Power BI Reports
- Developed comprehensive reports using Power BI, which included:
  - Visual representations of sales data (charts, graphs)
  - Filter options for deeper insights into product categories and customer segments

![Bottom-Performing Product](https://github.com/user-attachments/assets/57c0f751-ebad-48ba-ac73-f4f6b88b8135)

![Top Performing Product](https://github.com/user-attachments/assets/aeb941c1-05ea-46c8-9ed0-efce66ee2fd6)

![Unit Sold by Region](https://github.com/user-attachments/assets/bc3f9d2b-3456-4899-813e-14e42f562c62)

![Sales Region](https://github.com/user-attachments/assets/3ae18429-667e-46ea-b25a-eac4ae30be3c)

![Rev Year](https://github.com/user-attachments/assets/6853813b-79a8-40a6-bd77-23889fea7861)

![BarChart Unit Sold Product](https://github.com/user-attachments/assets/8695de0d-2385-4ab4-88d6-fc21c61febc3)

![LineChart Monthly Trend](https://github.com/user-attachments/assets/8b9cf32a-a3dc-419b-95b3-641393c0347b)


### Findings and Insights
---
- Identified peak sales periods and correlated them with marketing campaigns.
- Discovered underperforming product categories and suggested potential marketing strategies.
- Analyzed customer purchasing trends to recommend targeted promotions.

### Recommendations
---
1. **Focus on Best Sellers:**
   - Continue to promote and stock top-performing products.
   - Consider bundling these products with other items to increase sales.

2. **Enhance Regional Strategies:**
   - Investigate regions with lower sales performance to identify potential issues.
   - Tailor marketing efforts based on regional preferences and sales trends.

3. **Monitor Seasonal Trends:**
   - Analyze sales data seasonally to prepare for peak times and manage inventory effectively.

4. **Customer Feedback:**
   - Gather customer feedback on products to address any issues promptly, especially for top sellers.

5. **Cross-Selling Opportunities:**
   - Identify complementary products to recommend alongside best sellers to increase average order value.

### Areas of Discussion
---
- **Data Quality:**
  - Ensure data from Excel and SQL sources are accurate and up to date for reliable insights.
  
- **Sales Channel Performance:**
  - Discuss the effectiveness of different sales channels. Are online sales outperforming in-store, or vice versa? What strategies can enhance underperforming channels?

- **Customer Segmentation:**
  - Explore the demographics of buyers in high-performing regions versus low-performing ones.

### Conclusion
---
The dashboard serves as a vital tool for visualizing sales data, enabling stakeholders to make informed decisions. By focusing on top-performing products and understanding regional performance, businesses can optimize their strategies to drive sales growth. Continuous monitoring and adjustment based on data insights will help maintain competitive advantage and improve overall sales performance. 

This dashboard not only facilitates tracking of KPIs but also fosters discussions that can lead to actionable insights and strategic planning.

This project provided valuable experience in data analysis, from data cleaning to visualization and reporting. The skills acquired through this analysis will be instrumental in future data-driven projects.

