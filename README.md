# postgresql_ucdavis
In this project, I was given access to dataset through Mode Analytics.
I used PostgreSQL to retrieve data.

To accessthe dataset, use PDF file 'Connecting to Dataset'.

\*\* Exercise 1
Pull a list of user email addresses. Edit the query to pull emailaddresses, but only for non-deleted users.

SQL code:
SELECT u.id AS user_id, email_address FROM dsv1069.users
WHERE deleted_at ISNULL;
