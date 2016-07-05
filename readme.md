* How many users are there?
50
SELECT COUNT(* ) FROM users;

* What are the 5 most expensive items?
ID: 25, 83, 100, 40, 60
SELECT * FROM items ORDER BY price DESC LIMIT 5;

* What's the cheapest book? (Does that change for "category is exactly 'book'" versus "category contains 'book'"?)
76|Ergonomic Granite Chair|Books|De-engineered bi-directional portal|1496
SELECT MIN(price) FROM items WHERE category LIKE "%Book%";
No items get returned for the exact category "book" because the category is named "books." But to answer the question, the end result still would not change in this case because the category of the cheapest book is "Books."

* Who lives at "6439 Zetta Hills, Willmouth, WY"? Do they have another address?
Corrine Little
SELECT * FROM users WHERE id = (SELECT user_id FROM addresses WHERE street = '6439 Zetta Hills' AND city = 'Willmouth' AND state = 'WY');
Yes, she also lives at 54369 Wolff Forges, Lake Bryon, CA 31587
SELECT * FROM addresses WHERE user_id = 40;

* Correct Virginie Mitchell's address to "New York, NY, 10108".
UPDATE addresses
SET city = 'New York', state ='NY', zip = 10108
WHERE id = 41;

* How much would it cost to buy one of each tool?
$467,488
SELECT DISTINCT SUM(price) FROM items;

* How many total items did we sell?
2125
SELECT SUM(quantity) FROM orders;

* How much was spent on books?
$10,045,128
SELECT SUM(price * quantity)
FROM items
INNER JOIN orders
ON items.id = orders.item_id;

* Simulate buying an item by inserting a User for yourself and an Order for that User.
INSERT INTO users (first_name, last_name, email) VALUES ('Kate', 'Walters', 'katew@email.com');
INSERT INTO orders (user_id, item_id, quantity, created_at) VALUES (51, 14, 3, CURRENT_TIMESTAMP);
