# Lab: SQL injection UNION attack, retrieving multiple values in a single column

> This lab contains a SQL injection vulnerability in the product category filter. The results from the query are returned in the application's response so you can use a UNION attack to retrieve data from other tables. The database contains a different table called `users`, with columns called `username` and `password`. To solve the lab, perform a SQL injection UNION attack that retrieves all usernames and passwords, and use the information to log in as the `administrator` user.

## Solution

1. **Intercept the Category Filter Request**: Select a product category (such as `Pets` or `Accessories`) and intercept the outgoing `GET` request in Burp Suite (or send it to Burp Repeater). Inspecting the request reveals the vulnerable `category` parameter in the URL query string, which serves as our SQL injection point:

<img width="666" height="465" alt="Screenshot 2026-11-25 at 13 18 41" src="https://github.com/user-attachments/assets/75c947ae-1e0f-4783-9b98-42a33c5fc1eb" />

2. **Determine the Number of Columns**: Inject `NULL` values into the `category` parameter using `' UNION SELECT NULL,NULL--`. Receiving a `200 OK` response confirms that the original query returns **2 columns**:

<img width="1332" height="833" alt="Screenshot 2026-11-25 at 13 20 17" src="https://github.com/user-attachments/assets/fec8d8e1-3410-4f94-9b0f-52319ffafe4b" />

3. **Identify the String-Compatible Column**: Probe both column positions by replacing `NULL` with a test string (`'a'`). Testing `' UNION SELECT NULL,'a'--` returns a `200 OK` response and renders `'a'` on the page (whereas placing `'a'` in the first column triggers an error), confirming that only the second column holds string data:

<img width="1330" height="833" alt="Screenshot 2026-11-25 at 13 21 52" src="https://github.com/user-attachments/assets/9d20e9dc-a1ac-4cbe-aee7-dd240d7a59ee" />

4. **Concatenate and Extract Credentials from the `users` Table**: Because only one column accepts string data, we can concatenate the `username` and `password` columns together using the double-pipe (`||`) operator and a `~` separator:

```
' UNION SELECT NULL,username||'~'||password FROM users--
```

Submitting this payload outputs all rows from the `users` table in `username~password` format, revealing the `administrator` credentials:

<img width="1329" height="833" alt="Screenshot 2026-11-25 at 13 26 47" src="https://github.com/user-attachments/assets/b76c40b3-a798-49a2-9e72-e057590f5d05" />

5. **Log in as Administrator**: Navigate to the My account login page and sign in using the extracted `administrator` username and password to solve the lab.
