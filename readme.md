Normal Mode
-------------------

1) How many users are there?
    50, SELECT COUNT(*) FROM users;

2) What are the 5 most expensive items?
    60|Ergonomic Steel Car|Books & Outdoors|Enterprise-wide secondary firmware|9341
    40|Sleek Wooden Hat|Music & Baby|Quality-focused heuristic info-mediaries|9390
    100|Awesome Granite Pants|Toys & Books|Upgradable 24/7 access|9790
    83|Small Wooden Computer|Health|Re-engineered fault-tolerant adapter|9859
    25|Small Cotton Gloves|Automotive, Shoes & Beauty|Multi-layered modular service-desk|9984,
    SELECT * FROM items ORDER BY price LIMIT(5) OFFSET(95);

3) What’s the cheapest book? (Does that change for “category is exactly ‘book’” versus “category contains ‘book’”?)

    Category is exactly book: Ergonomic Granite Chair|1496, SELECT title, MIN(price) FROM items WHERE category = "Books";

    Category contains book: Ergonomic Granite Chair|1496, SELECT title, MIN(price) FROM items WHERE category LIKE '%book%';

4) Who lives at “6439 Zetta Hills, Willmouth, WY”? Do they have another address?

    First I got their user_id (40) using, SELECT user_id FROM addresses WHERE street = "6439 Zetta Hills";
    Next, I looked up the user name by their user_id, SELECT first_name, last_name FROM users WHERE id = 40;

    Corrine Little

    Yes, they have 2 addresses:
    40|6439 Zetta Hills|Willmouth|WY|15029
    40|54369 Wolff Forges|Lake Bryon|CA|31587

    SELECT * FROM addresses WHERE user_id = 40;

5) Correct Virginie Mitchell’s address to “New York, NY, 10108”.
    SELECT id FROM users WHERE last_name = "Mitchell"
    UPDATE addresses SET city = "New York" WHERE city = "Roxanehaven";
    UPDATE addresses SET zip = "10108" WHERE zip = "34705";

6) How much would it cost to buy one of each tool?
    7383, SELECT SUM(price) FROM items WHERE category LIKE "tools";

7) How many total items did we sell?
    2125, SELECT SUM(quantity) FROM orders;

8) How much was spent on books?

    SELECT SUM(price * quantity) FROM orders JOIN items ON items.id = orders.item_id AND category LIKE '%book%';


9)  Simulate buying an item by inserting a User for yourself and an Order for that User.

    INSERT INTO users (id, first_name, last_name, email) VALUES ((SELECT COUNT(*) FROM users) + 1, "Mike", "Pitre", "michaelepitre@gmail.com");
    INSERT INTO orders (user_id, item_id, quantity) VALUES (51, 15, 2);


Hard Mode
---------------------

What item was ordered most often? Grossed the most money?

What user spent the most?

What were the top 3 highest grossing categories?
