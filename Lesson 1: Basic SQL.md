# 1️⃣ Lesson 1: Basic SQL

## LIMIT

Try using LIMIT yourself below by writing a query that displays all the data in the occurred_at, account_id, and channel columns of the web_events table, and limits the output to only the first 15 rows.

````sql
SELECT occurred_at, account_id, channel
FROM web_events
LIMIT 15;
````

<img width="740" alt="image" src="https://user-images.githubusercontent.com/81607668/129868696-65a2b366-837e-47aa-9962-a2a6b9741c0a.png">

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
<img width="749" alt="image" src="https://user-images.githubusercontent.com/81607668/129869176-6732d7f7-d44b-4fa3-aee0-7bac2637cf06.png">

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

<img width="635" alt="image" src="https://user-images.githubusercontent.com/81607668/129869548-ec7414c6-f4c9-4fb1-aee5-21a23fc50721.png">

### Part 2

1. Write a query that displays the order ID, account ID, and total dollar amount for all the orders, sorted first by the account ID (in ascending order), and then by the total dollar amount (in descending order). 

````sql
SELECT id, account_id, total_amt_usd
FROM orders
ORDER BY account_id, total_amt_usd DESC;
````

<img width="625" alt="image" src="https://user-images.githubusercontent.com/81607668/129870307-19000b56-84fc-4a16-8b06-29159a7c5b9b.png">

2. Now write a query that again displays order ID, account ID, and total dollar amount for each order, but this time sorted first by total dollar amount (in descending order), and then by account ID (in ascending order). 

````sql
SELECT id, account_id, total_amt_usd
FROM orders
ORDER BY total_amt_usd DESC, account_id;
````

<img width="601" alt="image" src="https://user-images.githubusercontent.com/81607668/129870411-74e545b7-98ad-4f0d-88f2-ae39c65a9eb0.png">

3. Compare the results of these two queries above. How are the results different when you switch the column you sort on first?

***

## WHERE


