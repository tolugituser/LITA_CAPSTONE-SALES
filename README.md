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
![14](https://github.com/user-attachments/assets/b960890c-8189-4ddf-b2ec-348eb6aa9ca6)
![15](https://github.com/user-attachments/assets/5d9eccf2-4899-4d15-9592-48926586310b)
![16](https://github.com/user-attachments/assets/79fc5d21-f705-49e2-bffb-4df1d83e3285)
![17](https://github.com/user-attachments/assets/8fc1d7cb-d005-4f29-b94b-0556ef13cb39)
![18](https://github.com/user-attachments/assets/be935807-f359-49cc-be56-f24e4fcf89e6)
![19](https://github.com/user-attachments/assets/b75fdb84-f9fc-4edd-a209-bafdbce4e825)
![20](https://github.com/user-attachments/assets/c804e3e1-1f2a-4e53-bee0-7ffaf56051fe)
![21](https://github.com/user-attachments/assets/5cd1d82a-d1b1-4baf-b168-bf3c9a48ab5d)
![22](https://github.com/user-attachments/assets/2a53275a-e95b-41da-bd51-73318e1c31e2)
![23](https://github.com/user-attachments/assets/0bc8bfd5-0d02-4a91-a214-d7cd504853af)
![9](https://github.com/user-attachments/assets/0e7113d2-e5de-4120-918f-e02fe2bca4f4)
![10](https://github.com/user-attachments/assets/c791e532-3040-4479-b291-b6f8c36e2512)
![11](https://github.com/user-attachments/assets/8fded4fa-2349-4873-93db-777ec90ab31b)
![12](https://github.com/user-attachments/assets/af1923f3-b688-4302-9550-e0cbfdc8a42a)
![13](https://github.com/user-attachments/assets/bc0e628f-986e-48d1-9bff-37aef115098f)



#### Power BI Reports
- Developed comprehensive reports using Power BI, which included:
  - Visual representations of sales data (charts, graphs)
  - Filter options for deeper insights into product categories and customer segments

![1](https://github.com/user-attachments/assets/9b6963be-b9b3-4b97-99cb-c569b16c182a)
![2](https://github.com/user-attachments/assets/5e4c8780-c29c-47e8-b659-7beb766d2b23)
![3](https://github.com/user-attachments/assets/2b1a690b-07d5-4d3a-b83d-457231648081)
![4](https://github.com/user-attachments/assets/29ece15f-7f0d-4140-861d-4a9cc6390043)
![5](https://github.com/user-attachments/assets/66e59075-5cc4-41e3-bef2-04cf2097ce5f)
![6](https://github.com/user-attachments/assets/80ab1fec-de9a-4070-814f-92684a889ccc)
![7](https://github.com/user-attachments/assets/fb3a6be5-0b1e-488a-81fd-b40559fef6d1)
![8](https://github.com/user-attachments/assets/ffb21785-762a-420c-b73c-7b0be09f98ab)



### Findings & Insights
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

