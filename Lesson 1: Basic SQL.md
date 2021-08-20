# 📚 Lesson 1: Basic SQL

## ⚡️ Table of Contents

- [LIMIT](#limit)
- [ORDER BY](#order-by)
- [WHERE](#where)
- [Arithmetic Operators](#arithmetic-operators)
- [Logical Operators](#logical-operators)

***

## LIMIT

Try using LIMIT yourself below by writing a query that displays all the data in the occurred_at, account_id, and channel columns of the web_events table, and limits the output to only the first 15 rows.

````sql
SELECT 
  occurred_at, 
  account_id, 
  channel
FROM web_events
LIMIT 15;
````

<img width="681" alt="image" src="https://user-images.githubusercontent.com/81607668/129871211-9cdf5e7c-d017-43bb-b4b8-0121e88b66c4.png">

***

## ORDER BY

### Part 1

Let's get some practice using ORDER BY:

1. Write a query to return the 10 earliest orders in the orders table. Include the id, occurred_at, and total_amt_usd.

````sql
SELECT 
  id, 
  occurred_at, 
  total_amt_usd
FROM orders
ORDER BY occurred_at
LIMIT 10;
````
<img width="662" alt="image" src="https://user-images.githubusercontent.com/81607668/129871282-cf7719ce-14b4-4d11-bf27-bd65c3ad2794.png">

2. Write a query to return the top 5 orders in terms of largest total_amt_usd. Include the id, account_id, and total_amt_usd.

````sql
SELECT 
  id, 
  account_id, 
  total_amt_usd
FROM orders
ORDER BY total_amt_usd DESC
LIMIT 5;
````

<img width="619" alt="image" src="https://user-images.githubusercontent.com/81607668/129869368-5e1964e0-65ff-4f38-b446-b693b524e254.png">

3. Write a query to return the lowest 20 orders in terms of smallest total_amt_usd. Include the id, account_id, and total_amt_usd.
````sql
SELECT 
  id, 
  account_id, 
  total_amt_usd
FROM orders
ORDER BY total_amt_usd
LIMIT 20;
````

<img width="588" alt="image" src="https://user-images.githubusercontent.com/81607668/129871321-c1f40f9c-f459-4f46-a94e-987983365360.png">

### Part 2

1. Write a query that displays the order ID, account ID, and total dollar amount for all the orders, sorted first by the account ID (in ascending order), and then by the total dollar amount (in descending order). 

````sql
SELECT
  id, 
  account_id, 
  total_amt_usd
FROM orders
ORDER BY account_id, total_amt_usd DESC;
````

<img width="582" alt="image" src="https://user-images.githubusercontent.com/81607668/129871369-00124b76-294c-4114-ae18-cd2cd576d5e4.png">

2. Now write a query that again displays order ID, account ID, and total dollar amount for each order, but this time sorted first by total dollar amount (in descending order), and then by account ID (in ascending order). 

````sql
SELECT 
  id, 
  account_id, 
  total_amt_usd
FROM orders
ORDER BY total_amt_usd DESC, account_id;
````

<img width="589" alt="image" src="https://user-images.githubusercontent.com/81607668/129871439-817238f1-3c07-4794-b9af-f555e8a25fd0.png">

***

## WHERE

Write a query that:

1. Pulls the first 5 rows and all columns from the orders table that have a dollar amount of gloss_amt_usd greater than or equal to 1000.
````sql
SELECT *
FROM orders
WHERE gloss_amt_usd >= 1000
LIMIT 5;
````

2. Pulls the first 10 rows and all columns from the orders table that have a total_amt_usd less than 500.
````sql
SELECT *
FROM orders
WHERE total_amt_usd < 500
LIMIT 10;
````

3. Filter the accounts table to include the company name, website, and the primary point of contact (primary_poc) just for the Exxon Mobil company in the accounts table.
4. 
````sql
SELECT 
  name, 
  website, 
  primary_poc
FROM accounts
WHERE name = 'Exxon Mobil';
````

<img width="666" alt="image" src="https://user-images.githubusercontent.com/81607668/129872195-2e6fbcd5-9639-44b0-b2ad-d51eff58cd3b.png">

***

## Arithmetic Operators

Using the orders table:

1. Create a column that divides the standard_amt_usd by the standard_qty to find the unit price for standard paper for each order. Limit the results to the first 10 orders, and include the id and account_id fields. 

````sql
SELECT 
  id, 
  account_id, 
  standard_amt_usd/standard_qty AS unit_price
FROM orders
LIMIT 10;
````

<img width="555" alt="image" src="https://user-images.githubusercontent.com/81607668/129872915-5b70a589-de60-4973-b7b7-1c6200a277cc.png">

2. Write a query that finds the percentage of revenue that comes from poster paper for each order. You will need to use only the columns that end with _usd.

````sql
SELECT 
  id, 
  account_id, 
	ROUND(100 * poster_amt_usd/(standard_amt_usd + gloss_amt_usd + poster_amt_usd),2) AS poster_percentage
FROM orders
LIMIT 10;
````

<img width="557" alt="image" src="https://user-images.githubusercontent.com/81607668/129873291-cae4e079-b62b-4ab0-bc58-01617560712c.png">

***

## Logical Operators

### LIKE Operator

Use the accounts table to find:

1. All the companies whose names start with 'C'. 

````sql
SELECT *
FROM accounts
WHERE name LIKE 'C%';
````

<img width="508" alt="image" src="https://user-images.githubusercontent.com/81607668/129873667-f48944f0-44c7-47c2-aaa7-f0e0462cbab0.png">

2. All companies whose names contain the string 'one' somewhere in the name.

````sql
SELECT *
FROM accounts
WHERE name LIKE '%one%';
````

<img width="468" alt="image" src="https://user-images.githubusercontent.com/81607668/129873761-7b166e38-c4b5-4a73-8840-5cc5b269b398.png">

3. All companies whose names end with 's'.

````sql
SELECT *
FROM accounts
WHERE name LIKE '%s';
````

<img width="510" alt="image" src="https://user-images.githubusercontent.com/81607668/129873869-009663ba-863b-4362-afb9-59807dd07f0b.png">

### IN Operator

1. Use the accounts table to find the account name, primary_poc, and sales_rep_id for Walmart, Target, and Nordstrom.

````sql
SELECT 
  name, 
  primary_poc, 
  sales_rep_id
FROM accounts
WHERE name IN ('Walmart', 'Target', 'Nordstrom');
````

<img width="641" alt="image" src="https://user-images.githubusercontent.com/81607668/129874333-116b3d09-7881-41bd-8335-79c320b747c5.png">

2. Use the web_events table to find all information regarding individuals who were contacted via the channel of organic or adwords.

````sql
SELECT *
FROM web_events
WHERE channel IN ('organic', 'adwords');
````

<img width="744" alt="image" src="https://user-images.githubusercontent.com/81607668/129874495-c3f3ccd1-4597-415a-b529-e92e99042b06.png">

### NOT Operator

We can pull all of the rows that were excluded from the queries in the previous two concepts with our new operator.

1. Use the accounts table to find the account name, primary poc, and sales rep id for all stores except Walmart, Target, and Nordstrom.

````sql
SELECT 
  name, 
  primary_poc, 
  sales_rep_id
FROM accounts
WHERE name NOT IN ('Walmart', 'Target', 'Nordstrom');
````

2. Use the web_events table to find all information regarding individuals who were contacted via any method except using organic or adwords methods.

````sql
SELECT *
FROM web_events
WHERE channel NOT IN ('organic', 'adwords');
````

Use the accounts table to find:

1. All the companies whose names do not start with 'C'.

````sql
SELECT *
FROM accounts
WHERE name NOT LIKE 'C%';
````

2. All companies whose names do not contain the string 'one' somewhere in the name.

````sql
SELECT *
FROM accounts
WHERE name NOT LIKE '%one%';
````

3. All companies whose names do not end with 's'.

````sql
SELECT *
FROM accounts
WHERE name NOT LIKE '%s';
````

### AND and BETWEEN Operator

1. Write a query that returns all the orders where the standard_qty is over 1000, the poster_qty is 0, and the gloss_qty is 0.

````sql
SELECT *
FROM orders
WHERE standard_qty > 1000
	AND poster_qty = 0
 	AND gloss_qty = 0;
````

2. Using the accounts table, find all the companies whose names do not start with 'C' and end with 's'.

````sql
SELECT *
FROM accounts
WHERE name NOT LIKE 'C%' 
  AND name LIKE '%s';
````

3. When you use the BETWEEN operator in SQL, do the results include the values of your endpoints, or not? Figure out the answer to this important question by writing a query that displays the order date and gloss_qty data for all orders where gloss_qty is between 24 and 29. Then look at your output to see if the BETWEEN operator included the begin and end values or not.

Yes, BETWEEN operator includes the values of both endpoints which is 24 and 29.

````sql
SELECT 
  occurred_at, 
  gloss_qty
FROM orders
WHERE gloss_qty BETWEEN 24 AND 29
````

4. Use the web_events table to find all information regarding individuals who were contacted via the organic or adwords channels, and started their account at any point in 2016, sorted from newest to oldest.

````sql
SELECT *
FROM web_events
WHERE channel IN ('organic', 'adwords') 
	AND occurred_at BETWEEN '2016-01-01' AND '2017-01-01'
ORDER BY occurred_at DESC;
````

### OR Operator

1. Find list of orders ids where either gloss_qty or poster_qty is greater than 4000. Only include the id field in the resulting table.

````sql
SELECT id
FROM orders
WHERE gloss_qty > 4000 
  OR poster_qty > 4000;
````

2. Write a query that returns a list of orders where the standard_qty is zero and either the gloss_qty or poster_qty is over 1000.

````sql
SELECT id
FROM orders
WHERE standard_qty = 0 
  AND (gloss_qty > 1000 OR poster_qty > 1000);
````

3. Find all the company names that start with a 'C' or 'W', and the primary contact contains 'ana' or 'Ana', but it doesn't contain 'eana'.

````sql
SELECT *
FROM accounts
WHERE (name LIKE 'C%' OR name LIKE 'W%') 
  AND (primary_poc LIKE '%ana%' OR primary_poc LIKE '%Ana%') 
  AND primary_poc NOT LIKE '%eana%';
````

***
