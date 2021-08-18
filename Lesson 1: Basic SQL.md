# 1️⃣ Lesson 1: Basic SQL

## LIMIT

Try using LIMIT yourself below by writing a query that displays all the data in the occurred_at, account_id, and channel columns of the web_events table, and limits the output to only the first 15 rows.

````sql
SELECT occurred_at, account_id, channel
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
SELECT id, occurred_at, total_amt_usd
FROM orders
ORDER BY occurred_at
LIMIT 10;
````
<img width="662" alt="image" src="https://user-images.githubusercontent.com/81607668/129871282-cf7719ce-14b4-4d11-bf27-bd65c3ad2794.png">

2. Write a query to return the top 5 orders in terms of largest total_amt_usd. Include the id, account_id, and total_amt_usd.

````sql
SELECT id, account_id, total_amt_usd
FROM orders
ORDER BY total_amt_usd DESC
LIMIT 5;
````

<img width="619" alt="image" src="https://user-images.githubusercontent.com/81607668/129869368-5e1964e0-65ff-4f38-b446-b693b524e254.png">

3. Write a query to return the lowest 20 orders in terms of smallest total_amt_usd. Include the id, account_id, and total_amt_usd.
````sql
SELECT id, account_id, total_amt_usd
FROM orders
ORDER BY total_amt_usd
LIMIT 20;
````

<img width="588" alt="image" src="https://user-images.githubusercontent.com/81607668/129871321-c1f40f9c-f459-4f46-a94e-987983365360.png">

### Part 2

1. Write a query that displays the order ID, account ID, and total dollar amount for all the orders, sorted first by the account ID (in ascending order), and then by the total dollar amount (in descending order). 

````sql
SELECT id, account_id, total_amt_usd
FROM orders
ORDER BY account_id, total_amt_usd DESC;
````

<img width="582" alt="image" src="https://user-images.githubusercontent.com/81607668/129871369-00124b76-294c-4114-ae18-cd2cd576d5e4.png">

2. Now write a query that again displays order ID, account ID, and total dollar amount for each order, but this time sorted first by total dollar amount (in descending order), and then by account ID (in ascending order). 

````sql
SELECT id, account_id, total_amt_usd
FROM orders
ORDER BY total_amt_usd DESC, account_id;
````

<img width="589" alt="image" src="https://user-images.githubusercontent.com/81607668/129871439-817238f1-3c07-4794-b9af-f555e8a25fd0.png">

3. Compare the results of these two queries above. How are the results different when you switch the column you sort on first?

***

## WHERE

Write a query that:

1. Pulls the first 5 rows and all columns from the orders table that have a dollar amount of gloss_amt_usd greater than or equal to 1000.

2. Pulls the first 10 rows and all columns from the orders table that have a total_amt_usd less than 500.
