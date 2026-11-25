# Lab: SQL injection UNION attack, retrieving data from other tables

> This lab contains a SQL injection vulnerability in the product category filter. The results from the query are returned in the application's response, so you can use a UNION attack to retrieve data from other tables. To construct such an attack, you need to combine some of the techniques you learned in previous labs. The database contains a different table called `users`, with columns called `username` and `password`. To solve the lab, perform a SQL injection UNION attack that retrieves all usernames and passwords, and use the information to log in as the `administrator` user.

## Solution

1. **Intercept the Category Filter Request**: Select a product category (such as `Lifestyle`) and intercept the outgoing `GET` request in Burp Suite (or send it to Burp Repeater). Inspecting the request reveals the `category` parameter in the URL query string, which serves as our SQL injection point:

<img width="665" height="510" alt="Screenshot 2026-11-25 at 12 45 22" src="https://github.com/user-attachments/assets/03ee465a-425d-4ff1-9016-7543e51fc3bf" />

2. **Determine the Column Count and String Compatibility**: Inject `NULL` values into the `category` parameter using `' UNION SELECT NULL,NULL--` (URL-encoded as `'+UNION+SELECT+NULL,NULL--`). Receiving a `200 OK` response confirms that the original query returns 2 columns (both of which accept string values, as verified by testing with `'a'`):

<img width="1330" height="835" alt="Screenshot 2026-11-25 at 12 46 41" src="https://github.com/user-attachments/assets/3950a518-acda-41d5-86d0-190a81a09d8e" />

3. **Extract Credentials from the `users` Table**: Because the lab description tells us that the database contains a table named `users` with `username` and `password` columns, we can query both columns directly in our UNION payload:

```
' UNION SELECT username, password FROM users--
```

Sending this payload renders the contents of the `users` table directly on the page, revealing the credentials for the `administrator` account:

<img width="1710" height="1034" alt="Screenshot 2026-11-25 at 12 51 47" src="https://github.com/user-attachments/assets/d9946fd3-079d-41f9-8042-2da99ceea5ad" />

4. **Log in as Administrator**: Navigate to the My account login page and sign in using the extracted `administrator` username and password to solve the lab.
   
