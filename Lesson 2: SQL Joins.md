# 📚 Lesson 2: SQL Joins

## 💡 Table of Contents

***

### Your First JOIN

Try pulling all the data from the accounts table, and all the data from the orders table. Try pulling standard_qty, gloss_qty, and poster_qty from the orders table, and the website and the primary_poc from the accounts table.

````sql
SELECT 
  a.website, a.primary_poc, 
  o.standard_qty, o.gloss_qty, o.poster_qty
FROM accounts a
JOIN orders o
  ON a.id = o.account_id;
````

***

### JOIN Questions Part 1

1. Provide a table for all web_events associated with account name of Walmart. There should be three columns. Be sure to include the primary_poc, time of the event, and the channel for each event. Additionally, you might choose to add a fourth column to assure only Walmart events were chosen. 

````sql
SELECT 
  a.name, a.primary_poc, 
  w.occurred_at, w.channel
FROM web_events w
JOIN accounts a
	ON w.account_id = a.id
WHERE a.name = 'Walmart';
````

2. Provide a table that provides the region for each sales_rep along with their associated accounts. Your final table should include three columns: the region name, the sales rep name, and the account name. Sort the accounts alphabetically (A-Z) according to account name. 

````sql
SELECT 
  r.name AS region_name,
	s.name AS sales_rep_name, 
  a.name AS account
FROM accounts a
JOIN sales_reps s
	ON a.sales_rep_id = s.id
JOIN region r
	ON s.region_id = r.id
ORDER BY account;
````

3. Provide the name for each region for every order, as well as the account name and the unit price they paid (total_amt_usd/total) for the order. Your final table should have 3 columns: region name, account name, and unit price. A few accounts have 0 for total, so I divided by (total + 0.01) to assure not dividing by zero.  

````sql
SELECT 
  r.name AS region_name,
	s.name AS sales_rep_name, 
  (o.total_amt_usd/o.total) AS unit_price
FROM accounts a
JOIN orders o
	ON a.id = o.account_id
JOIN sales_reps s
	ON a.sales_rep_id = s.id
JOIN region r
	ON s.region_id = r.id
WHERE o.total_amt_usd >= 0.01;
````

***

