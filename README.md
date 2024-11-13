# Overall_Sales_Performance_Analysis_for_a_Telecom_Company_USA
A Data Analysis Project that Analyzed the sales performance of a Telecommunication company based in the United State. The company’s sales transaction data generated over the past years was used for this analysis.

## Project Overview:
This Data Analysis Project aims to provide insights into the sales performance of a Telecommunication company Based in the United State. 

__About the Company__: The Telecommunication Company operates a B2B business model and sells a wide variety of cell phones and devices, including __smartphones, tablets, smartwatches__. They offer devices from all of the major manufacturers, such as Apple, Samsung, Google, and Motorola.

Various aspects of the company’s sales transaction data generated over the past years was analysed to gain insights into their Customer Behaviour, Product Popularity, Top Performing  Channel of Marketing, Regional Performance and Revenue Trends of the company since it began. 

We seek to identify Top performing customers, products, channels of sales, region, trends, and the overall performance of the company, to enable the company to make data-driven decisions/recommendations and to gain a deeper understanding of the company’s overall performance. 

## Table of Content:
[Data Sources](Data-Sources)<br> <br>
[Data Analysis Tools Used](Data-Analysis-Tools-Used)<br> <br>
[Data Collection](Data-Collection)<br> <br>
[Data Cleaning](Data-Cleaning)<br> <br>
[Loading Data into Power BI](Loading-Data-into-Power-BI)<br> <br>
[Exploratory Data Analysis (EDA)](Exploratory-Data-Analysis-(EDA))<br> <br>
[Data Analysis](Data-Analysis)<br> <br>
[Results and Findings](Results-and-Findings)<br> <br>
[Recommendations](Recommendations)<br> <br>
## Data Sources: 
__Sales Transaction Data__: The primary dataset used for this data analysis project was sales transaction data, containing detailed information about each sales made by the company and was extracted from the company’s database using SQL codes. 

Several SQL complex queries were written to the company’s database in order to extract the required data for this data analysis project. 

Each SQL complex query was used to extract a particular aspect of the company’s sales data. 

The results were downloaded and saved as the following csv files below:

1. __customers_behaviour.csv__<br> <br>
2. __channel performance.csv__<br> <br>
3. __region performance.csv__<br> <br>
4. __yearly revenue performance trend.csv__<br> <br>

## Data Analysis Tools Used:
- __SQL (PostgreSQL)__  - for Data Collection , Data Cleaning and Data Analysis 
- __Power BI__ - for Data Modelling, Data Analysis, Data Visualization and Creating an Interactive Report.
  
## Data Collection: 
- __Database Inspection__ : In the initial data collection phase, I inspected the company’s database using SQL code to check for missing data (NULL) in each of the tables in the company’s database.
- I extracted the required data for the purpose of the data analysis project using SQL complex query and SQL data aggregation.
  
## Data Cleaning: 
I used SQL codes to clean and format the data to conform to the required data format.
I downloaded the result of my SQL Queries from the company’s database as a csv file to my PC. 

## Loading Data into Power BI:
I loaded the downloaded csv files into Power BI for the purpose of Data Visualization and Building interactive dashboard/report.

## Exploratory Data Analysis (EDA): 
EDA involves exploring the sales data in order to answer some key questions such as : 
- Who are the top 10 customers of the company?
- What particular products are the Top customers buying? 
- Comparative analysis to find out  the top selling product?
- What Is the Total quantity of items a particular customer has ever bought from the company? 
- What is the Total revenue generated by the company from a particular customer? 
- What are the top performing channels of sales? 
- What is the Total quantity of items sold through a particular channel?
- What is the  Total Revenue generated  through a particular channel?
- Which region is the best performing region? 
- What is the Total quantity of items sold in a particular region?
- What is the  Total Revenue generated  in a particular region?
- What is the peak sales period? 
- What is the sales performance at a particular given time (year, month, day)?  
- What is the sales trend between a particular period of time? 
- What is the overall sales Trend of the company over the years? 
- What is the overall sales performance of the company?

## Data Analysis :
```SQL
--SQL SOLUTION 1--

SELECT a.name AS customer_name,
       SUM(o.smartphones_qty) AS smartphone_qty ,
       SUM(o.smartwatches_qty) AS smartwatches_qty ,
       SUM(o.tablets_qty) AS tablets_qty ,
       COUNT(a.name)  AS No_of_Transaction,
       SUM(o.total)  AS total_quantity,
       SUM(o.total_amt_usd) AS total_revenue_usd
FROM accounts a
JOIN orders o
ON a.id = o.account_id
GROUP BY customer_name
ORDER BY total_revenue_usd  DESC


--SQL SOLUTION 2--
SELECT w.channel AS channel_name,  
	   COUNT(w.channel) AS No_of_transactions,
	   SUM(o.total) AS total_quantity, 
	   SUM(o.total_amt_usd) AS total_revenue_usd
FROM orders o 
JOIN accounts a 
ON a.id = o.account_id 
JOIN web_events w 
ON a.id = w.account_id 
GROUP BY channel_name
ORDER BY total_revenue_usd DESC 




--SQL SOLUTION 3--
SELECT r.name AS region_name,  
	   COUNT(r.name) AS No_of_transactions,
	   SUM(o.total) AS total_quantity, 
	   SUM(o.total_amt_usd) AS total_revenue_usd
FROM orders o 
JOIN accounts a 
ON a.id = o.account_id 
JOIN sales_reps s
ON a.sales_rep_id = s.id 
JOIN region r
ON s.region_id = r.id
GROUP BY region_name
ORDER BY total_revenue_usd DESC 



--SQL SOLUTION 4--
SELECT DATE_TRUNC('year', occurred_at) AS year,  
	   COUNT(occurred_at) AS No_of_transactions,
	   SUM(total) AS total_quantity, 
	   SUM(total_amt_usd) AS total_revenue_usd
FROM orders 
GROUP BY year
ORDER BY year ASC


```


![Customer behaviour_ screenshot](https://github.com/user-attachments/assets/3914b49f-bc8b-4c00-b557-68e3c3eb58d7)

![Channel Performance_Screenshot](https://github.com/user-attachments/assets/0604a558-1ba7-483e-bb5d-9d249abd3c86)

![Regional Performance_ Screenshot](https://github.com/user-attachments/assets/0e60f0dc-f4ed-480e-b1a7-bedc8c94eeb5)


![Yearly Revenue Trends_ Screenshot](https://github.com/user-attachments/assets/c3624acb-4016-40a7-b390-101111794460)



## Results and Findings: 

The Analysis Results is summarised as follows: 

- The Company’s Top 3  Customers by ranking are 
 - -  1st: EOG Resources : Bought a total of 56,410 items and has generated a Total revenue of  $382,870
 - -  2nd: Mosaic : Bought a total of 49,246 items and has generated a Total revenue of $345,620
 - -  3rd: IBM : Bought a total of 47,506 items and has generated a Total revenue of $326,820
- The top 10 customers are buying smartphones and smartwatches is almost the same proportion with a slightly higher preference for smartphones .
- The Overall Top selling product is smartphones, accounting for over 52% percent of total sales and Revenue. 
- The top performing channel of sales is Direct channel, accounting for over 61 % percent of total  Sales and Revenue. 
- The best performing region is the Northeast Region , accounting for over 33 % percent of total  Sales and Revenue. 
- The company’s sales have been steadily increasing over the past years  with a noticeable peak in the holiday season in  2016, followed by a sudden decline in sales from 2017.  
 
## Recommendations: 
Based on the findings/results of this data analysis project I strongly recommend the following actions : 
- The company should focus on expanding and promoting the smartphone product category. 
- The company should invest in marketing and promotions during peak sales season to maximise revenue. 
- The company should implement a customer segmentation strategy to target smartphones and smartwatches customers effectively. 
- The company should allocate more budget and resources to their Direct sales channel to maximise revenue. 
- The company should invest more resources in their Northeast Region of operation to maximise revenue. 

