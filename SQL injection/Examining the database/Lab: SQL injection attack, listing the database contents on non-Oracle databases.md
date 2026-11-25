# Lab: SQL injection attack, listing the database contents on non-Oracle databases

> This lab contains a SQL injection vulnerability in the product category filter. The results from the query are returned in the application's response so you can use a UNION attack to retrieve data from other tables. The application has a login function, and the database contains a table that holds usernames and passwords. You need to determine the name of this table and the columns it contains, then retrieve the contents of the table to obtain the username and password of all users. To solve the lab, log in as the `administrator` user.

## Solution

1. **Intercept the Category Filter Request**: Select a product category (such as `Gifts`) and intercept the outgoing `GET` request in Burp Suite (or send it to Burp Repeater). Inspecting the request reveals the `category` parameter in the URL query string, which serves as our SQL injection point:

<img width="660" height="495" alt="Screenshot 2026-11-25 at 14 33 48" src="https://github.com/user-attachments/assets/7d9e1f96-5ede-4959-ba9d-d18a6c7355b9" />

2. **Enumerate Column Count, String Compatibility, and Database Version**: Testing with `NULL` values and string probes confirms that the original query returns **2 string-compatible columns**. Injecting `' UNION SELECT version(), NULL--` succeeds and outputs `PostgreSQL 12.22` in the response, confirming we are targeting a PostgreSQL database:

<img width="1330" height="749" alt="Screenshot 2026-11-25 at 14 38 32" src="https://github.com/user-attachments/assets/9a5f07d6-c922-4167-83ea-02451b839d03" />

3. **List All Database Tables**: Because PostgreSQL supports the standard `information_schema` views, query `information_schema.tables` to discover the exact name of the table holding user credentials:

```
' UNION SELECT table_name, NULL FROM information_schema.tables--
```

Inspecting the rendered list of tables reveals a custom user table named `users_tvkila`:

<img width="1710" height="1033" alt="Screenshot 2026-11-25 at 14 44 50" src="https://github.com/user-attachments/assets/7f8b95df-49cd-473f-88f9-eebf165c652b" />

4. **Enumerate Columns in the `users_tvkila` Table**: Query `information_schema.columns` filtered by `table_name = 'users_tvkila'` to retrieve its column names and data types:

```
' UNION SELECT column_name, data_type FROM information_schema.columns WHERE table_name = 'users_tvkila'--
```

The response confirms three columns in the table: `username_bvbnyc`, `email`, and `password_uixack`:

<img width="1710" height="1034" alt="Screenshot 2026-11-25 at 14 50 47" src="https://github.com/user-attachments/assets/a79c1f4c-af50-4922-b359-c7bb27000dd2" />

5. **Extract User Credentials and Log In**: Query both the username and password columns directly from `users_tvkila`:

```
' UNION SELECT username_bvbnyc, password_uixack FROM users_tvkila--
```

This displays all user credentials in the application response, revealing the password for `administrator`. Logging in with these credentials on the My account page solves the lab:

<img width="1710" height="1033" alt="Screenshot 2026-11-25 at 14 54 42" src="https://github.com/user-attachments/assets/719222fe-00b6-4a2f-a80b-3f7dfaef2f1f" />
