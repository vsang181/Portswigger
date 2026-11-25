# Lab: SQL injection UNION attack, determining the number of columns returned by the query

> This lab contains a SQL injection vulnerability in the product category filter. The results from the query are returned in the application's response, so you can use a UNION attack to retrieve data from other tables. The first step of such an attack is to determine the number of columns that are being returned by the query. You will then use this technique in subsequent labs to construct the full attack. To solve the lab, determine the number of columns returned by the query by performing a SQL injection UNION attack that returns an additional row containing null values.

## Solution

1. **Identify the Filter Functionality**: On the main shop page, the application provides an option to filter products by category, as shown in the screenshot below:

<img width="1710" height="1033" alt="Screenshot 2026-11-25 at 10 26 51" src="https://github.com/user-attachments/assets/086ab261-78c1-43d7-a63a-7c162d193dbe" />

2. **Intercept the Category Filter Request**: Select any product category and intercept the outgoing `GET` request in Burp Suite (or send it to Burp Repeater). Inspecting the request reveals the vulnerable `category` parameter in the URL query string:

<img width="664" height="460" alt="Screenshot 2026-11-25 at 10 27 57" src="https://github.com/user-attachments/assets/ed5344d1-2035-44a9-80f5-285bc4e5ee50" />

3. **Determine the Number of Columns Using `NULL` Values**: For a `UNION SELECT` query to succeed, it must return the exact same number of columns as the original query. Using `NULL` values avoids data-type mismatch errors because NULL is convertible to every common data type. Modify the `category` parameter by iteratively adding `NULL` values until the server stops returning an error:

- `' UNION SELECT NULL--` → Returns an `Internal Server Error (500)`, indicating the original query returns more than one column.
- `' UNION SELECT NULL,NULL--` → Still returns an `Internal Server Error (500)`.
- `' UNION SELECT NULL,NULL,NULL--` → Returns a `200 OK` response and renders an additional empty row in the application's response, solving the lab:

<img width="1294" height="642" alt="Screenshot 2026-11-25 at 10 31 51" src="https://github.com/user-attachments/assets/6bd0cd6f-eb7a-422f-a210-f6df08c51988" />

4. **Confirm the Column Count**: Testing with a fourth `NULL` value (`' UNION SELECT NULL,NULL,NULL,NULL--`) triggers an `Internal Server Error (500)` again, confirming that the original database query returns **3 columns**.
