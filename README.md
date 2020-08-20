# Data Retrival Exercise Using PostgreSQL

In this project, I was given access to company's purchase dataset through Mode Analytics. Available tables are order, item, user and event.
To accessthe dataset, use PDF file 'Connecting to Dataset'.

I used PostgreSQL to answer some questions.

## Question 1 - What are non-deleted users' email address?
```
SELECT u.id AS user_id, email_address 
FROM dsv1069.users
WHERE deleted_at ISNULL;
```

## Question 2 - How many items are in each category?
```
SELECT category, COUNT(id) AS item_count
FROM dsv1069.items
GROUP BY category
ORDER BY item_count DESC;
```

## Question 3 - What is the result when you join users and orders table?
```
SELECT * 
FROM dsv1069.orders AS o
INNER JOIN dsv1069.users AS u ON o.user_ID = u.id;
```

## Question 4 - What is the count of viewed item events?
```
SELECT COUNT(DISTINCT event_id) AS events 
FROM dsv1069.events
WHERE event_name = 'view_item'
```

## Question 5 - What is the number of items in the items table which have been ordered?
```
SELECT COUNT(DISTINCT o.item_id)
FROM dsv1069.orders AS o
INNER JOIN dsv1069.items AS i ON i.id = o.item_id;
```

## Question 6 - When was user's first purchase(IF a user has ordered something)? Return info for any of the users who haven’t ordered anything.
```
SELECT u.id, MIN(o.paid_at)
FROM dsv1069.users AS u
LEFT JOIN dsv1069.orders AS o ON u.id = o.user_id
GROUP BY u.id;
```
## Question 7 - What percent of users have ever viewed the user profile page?
```
SELECT
  (CASE WHEN first_view IS NULL THEN false ELSE true END),
  COUNT(user_id) AS users
FROM
  (SELECT users.id AS user_id, MIN(event_time) AS first_view
  FROM dsv1069.users
  LEFT JOIN dsv1069.events ON users.id = events.user_id AND event_name = 'view_user_profile'
  GROUP BY users.id)
  AS first_profile_views
GROUP BY
  (CASE WHEN first_view IS NULL THEN false ELSE true END);
```

This exercise was part of Data Wrangling, Analysis and AB Testing with SQL course though [Coursera](https://www.coursera.org/learn/data-wrangling-analysis-abtesting/home/info)
