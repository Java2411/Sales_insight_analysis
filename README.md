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

![data source](https://github.com/Java2411/Sales_insight_analysis/assets/133401917/5e093634-24b1-49b8-b27f-a4e94a91e468)


Create a new connection in mySQL Workbench and import the `db_dump.sql` database. This will create the entire database along with records in your system.

![database](https://github.com/Java2411/Sales_insight_analysis/assets/133401917/a2866c13-da35-485c-85bf-5564bd8a1c1b)


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

![data analysis using SQL](https://github.com/Java2411/Sales_insight_analysis/assets/133401917/c5ec03c6-b342-43ba-bf78-430d07e54723)


Data Analysis Using Power BI
============================

You have to pull your data from the database Get Data -> Database -> MySQL database

**Note**: If you download the latet version 8.0.33 whole mysql package for some update mismatch reason you cannot connect Power BI to Mysql sever. For that you have to only downgrade mysql-connector-net-8.0.33 to mysql-connector-net-8.0.28. 

![connection error](https://github.com/Java2411/Sales_insight_analysis/assets/133401917/eddfa874-ee37-480a-b6a3-d1d357613914)

Then establish connection between the 'sales' database running in MySQL server on local machine

![localhost and database name](https://github.com/Java2411/Sales_insight_analysis/assets/133401917/c9c77153-958f-4af5-a9c8-ac007b70803c)

Once successful you can select all the tables from the database for your data analysis purpose. You can perform transform ETL operations on the table before loading them onto the worksheet.

![database connection established](https://github.com/Java2411/Sales_insight_analysis/assets/133401917/c3c3359e-3d55-4be5-931b-a628bbf66532)

we are gonna see the data model or relationships betweeen the table. While importing by default it established relationship between the data as follows:

![data model](https://github.com/Java2411/Sales_insight_analysis/assets/133401917/e5149459-3364-46f3-9518-8ee552ee62b4)

##**Star achema**
Now we are gonna establish some relattionship manually. Just drag and drop markets_code on sales markets table to market_code on sales transactions table. Also drag and drop order_date of sales transactions table to date  column on sales date table. Now we have establishes a star schema. 






1. Formula to create norm_amount column

`= Table.AddColumn(#"Filtered Rows", "norm_amount", each if [currency] = "USD" or [currency] ="USD#(cr)" then [sales_amount]*75 else [sales_amount], type any)`
