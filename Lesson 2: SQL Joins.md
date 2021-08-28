# 📚 Lesson 2: SQL Joins

### INNER JOINs

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
	r.name AS region,
  s.name AS sales_rep, 
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
	r.name AS region,
  s.name AS sales_rep, 
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

4. Provide a table that provides the region for each sales_rep along with their associated accounts. This time only for accounts where the sales rep has a first name starting with S and in the Midwest region. Your final table should include three columns: the region name, the sales rep name, and the account name. Sort the accounts alphabetically (A-Z) according to account name. 

````sql
SELECT 
	r.name AS region,
  s.name AS sales_rep, 
  a.name AS account
FROM accounts a
JOIN sales_reps s
	ON a.sales_rep_id = s.id
JOIN region r
	ON s.region_id = r.id
WHERE s.name LIKE 'S%' 
	AND r.name = 'Midwest'
ORDER BY account;
````

5. Provide a table that provides the region for each sales_rep along with their associated accounts. This time only for accounts where the sales rep has a last name starting with K and in the Midwest region. Your final table should include three columns: the region name, the sales rep name, and the account name. Sort the accounts alphabetically (A-Z) according to account name.

````sql
SELECT 
	r.name AS region,
  s.name AS sales_rep, 
  a.name AS account
FROM accounts a
JOIN sales_reps s
	ON a.sales_rep_id = s.id
JOIN region r
	ON s.region_id = r.id
WHERE s.name LIKE '% K%' 
	AND r.name = 'Midwest'
ORDER BY account;
````

6. Provide the name for each region for every order, as well as the account name and the unit price they paid (total_amt_usd/total) for the order. However, you should only provide the results if the standard order quantity exceeds 100. Your final table should have 3 columns: region name, account name, and unit price. In order to avoid a division by zero error, adding .01 to the denominator here is helpful total_amt_usd/(total+0.01). 

````sql
SELECT 
	r.name AS region,
  s.name AS sales_rep, 
  (o.total_amt_usd/o.total) AS unit_price
FROM accounts a
JOIN orders o
	ON a.id = o.account_id
JOIN sales_reps s
	ON a.sales_rep_id = s.id
JOIN region r
	ON s.region_id = r.id
WHERE (o.standard_qty > 100)
	AND (o.total_amt_usd >= 0.01);
````

7. Provide the name for each region for every order, as well as the account name and the unit price they paid (total_amt_usd/total) for the order. However, you should only provide the results if the standard order quantity exceeds 100 and the poster order quantity exceeds 50. Your final table should have 3 columns: region name, account name, and unit price. Sort for the smallest unit price first. In order to avoid a division by zero error, adding .01 to the denominator here is helpful (total_amt_usd/(total+0.01). 

````sql
SELECT 
	r.name AS region,
  s.name AS sales_rep, 
  (o.total_amt_usd/o.total) AS unit_price
FROM accounts a
JOIN orders o
	ON a.id = o.account_id
JOIN sales_reps s
	ON a.sales_rep_id = s.id
JOIN region r
	ON s.region_id = r.id
WHERE (o.standard_qty > 100)
	AND (o.poster_qty > 50)
	AND (o.total_amt_usd >= 0.01);
````

8. Provide the name for each region for every order, as well as the account name and the unit price they paid (total_amt_usd/total) for the order. However, you should only provide the results if the standard order quantity exceeds 100 and the poster order quantity exceeds 50. Your final table should have 3 columns: region name, account name, and unit price. Sort for the largest unit price first. In order to avoid a division by zero error, adding .01 to the denominator here is helpful (total_amt_usd/(total+0.01). 

````sql
SELECT 
	r.name AS region,
  s.name AS sales_rep, 
  (o.total_amt_usd/o.total) AS unit_price
FROM accounts a
JOIN orders o
	ON a.id = o.account_id
JOIN sales_reps s
	ON a.sales_rep_id = s.id
JOIN region r
	ON s.region_id = r.id
WHERE (o.standard_qty > 100)
	AND (o.poster_qty > 50)
	AND (o.total_amt_usd >= 0.01)
ORDER BY unit_price DESC;
````

9. What are the different channels used by account id 1001? Your final table should have only 2 columns: account name and the different channels. You can try SELECT DISTINCT to narrow down the results to only the unique values.

````sql
SELECT 
  DISTINCT w.channel, 
  a.name
FROM accounts a
JOIN web_events w
	ON a.id = w.account_id
WHERE a.id = '1001';
````

10. Find all the orders that occurred in 2015. Your final table should have 4 columns: occurred_at, account name, order total, and order total_amt_usd.

````sql
SELECT 
  o.occurred_at, 
  a.name, 
  o.total, 
  o.total_amt_usd
FROM orders o
JOIN accounts a
	ON o.account_id = a.id
WHERE o.occurred_at BETWEEN '2015-01-01' AND '2016-01-01'
ORDER BY o.occurred_at DESC;
````

***
