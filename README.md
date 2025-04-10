## Sales Insights Data Analysis Project
In this project, i did data analysis with both SQL and Power Bi. I did data transformation too using Power Quesry Language by removing unnecessary columns, added other columns and others as explained below.


### Data Analysis Using SQL

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

2. Removed the rows with -1 and 0 in sales amount

`= Table.SelectRows(transactions_Table, each ([sales_amount] <> -1 and [sales_amount] <> 0))`

3. Added a conditional column for changing the USD to INR

   `= Table.AddColumn(#"Removed -1,0 in sales amount", "Custom", each if [currency] = "USD" then 1 else null)`

5. Since the INR and USD were repeated twice i.e INR\r, INR, USD, USD\r, i removed the rows that contained tthe least  number of rows so that it doesnt affect the dataset. I dd this by selecting only the two currencies i want which was the INR and USD and removed the INR\r and USD\r.


Dashboard 
============================

NB: This is a work in progress

![Screenshot 2025-04-10 035209](https://github.com/user-attachments/assets/e17de83d-af45-4b1f-82d3-67f04d51fc76)
