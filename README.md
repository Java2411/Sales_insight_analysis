## Sales Insights Data Analysis Project
### Introduction
This sales insight analysis pertains to Atliq Hardwares, an Indian company that sells hardware and has its headquarters in New Delhi.
### Problem Statement
. Failing to track sales in dynamic growing market

. Sales director needs insight of the sales across all the branches in India

. Actions should be made to increase sales, which have significantly decreased during the past few years
### **Project Planning**
AIMS Grid is a project managemnet and data discovery tool.It is employed to define the project's success criteria and conduct project planning brainstorming sessions. 

The project planning has four stages:

1. Purpose

2. Stakeholders

3. End result

4. Success criteria

### Purpose:
. To unlock sales insight that are not visible for the  sales team for future decision making. 

. To Automate and reduce manual time in data gathering for analysis.

### Stake Holders
. Sales Director

. Marketing team

, Customer service team

. Data Analysis team

. Software Engineer team

### End Result
* An automated dashboard providind quick and latest insights inorder to make data driven decisions

### Success criteria
* Dashboard uncovering sales order insightwith latest data available

* Sales team are able to make better decision prove 10% cost savings of total spend


* Sales analyst stop gathering data manually inorder to save 20 % of thier businesss time and reinvest them in other value added activities

### Instructions to setup mysql on your local computer

1. Follow step in this video to install mysql on your local computer
https://www.youtube.com/watch?v=WuBcTJnIuzo

1. SQL database dump is in db_dump.sql file above. Download `db_dump.sql` file to your local computer. The db_dump.sql is theself contained SQL file for sales across all the markets of Atliq hardwares.

Create a new connection in mySQL Workbench and import the `db_dump.sql` database. This will create the entire database along with records in your system.

![data source](https://github.com/Java2411/Sales_insight_analysis/assets/133401917/7087d039-5012-4190-a0ae-3626ba1d3c5c)



**Note**: If you download the latet version 8.0.33 whole mysql package for some update mismatch reason you cannot connect Power BI to Mysql sever. For that you have to only downgrade mysql-connector-net-8.0.33 to mysql-connector-net-8.0.28. 

![connection error](https://github.com/Java2411/Sales_insight_analysis/assets/133401917/eddfa874-ee37-480a-b6a3-d1d357613914)

### Data Analysis Using SQL to get some initial insights about the data available

1. Show all customer records

    `SELECT * FROM customers;`

1. Show total number of customers

    `SELECT count(*) FROM customers;`

1. Show transactions for Chennai market (market code for chennai is Mark001

    `SELECT * FROM transactions where market_code='Mark001';`

1. Show distrinct product codes that were sold in chennai

    `SELECT distinct product_code FROM transactions where market_code='Mark001';`

1. Show transactions where currency is US dollars

    `SELECT * from transactions where currency="USD"`

1. Show transactions in 2020 join by date table

    `SELECT transactions.*, date.* FROM transactions INNER JOIN date ON transactions.order_date=date.date where date.year=2020;`

1. Show total revenue in year 2020,

    `SELECT SUM(transactions.sales_amount) FROM transactions INNER JOIN date ON transactions.order_date=date.date where date.year=2020 and transactions.currency="INR\r" or transactions.currency="USD\r";`
	
1. Show total revenue in year 2020, January Month,

    `SELECT SUM(transactions.sales_amount) FROM transactions INNER JOIN date ON transactions.order_date=date.date where date.year=2020 and and date.month_name="January" and (transactions.currency="INR\r" or transactions.currency="USD\r");`

1. Show total revenue in year 2020 in Chennai

    `SELECT SUM(transactions.sales_amount) FROM transactions INNER JOIN date ON transactions.order_date=date.date where date.year=2020
and transactions.market_code="Mark001";`


Data Analysis Using Power BI
============================

1. Formula to create norm_amount column

`= Table.AddColumn(#"Filtered Rows", "norm_amount", each if [currency] = "USD" or [currency] ="USD#(cr)" then [sales_amount]*75 else [sales_amount], type any)`
