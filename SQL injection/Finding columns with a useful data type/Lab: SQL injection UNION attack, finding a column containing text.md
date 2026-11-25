# Lab: SQL injection UNION attack, finding a column containing text

> This lab contains a SQL injection vulnerability in the product category filter. The results from the query are returned in the application's response, so you can use a UNION attack to retrieve data from other tables. To construct such an attack, you first need to determine the number of columns returned by the query. You can do this using a technique you learned in a previous lab. The next step is to identify a column that is compatible with string data. The lab will provide a random value that you need to make appear within the query results. To solve the lab, perform a SQL injection UNION attack that returns an additional row containing the value provided. This technique helps you determine which columns are compatible with string data.

## Solution

1. **Intercept the Category Filter Request**: Select any product category and intercept the outgoing `GET` request in Burp Suite (or send it to Burp Repeater). Inspecting the request reveals the vulnerable `category` parameter in the URL query string, which serves as our SQL injection point:

<img width="662" height="434" alt="Screenshot 2026-11-25 at 12 24 04" src="https://github.com/user-attachments/assets/cfd2982f-6b3c-447c-a177-cf35c31ba4bb" />

2. **Determine the Number of Columns**: Test the `category` parameter using NULL values (`' UNION SELECT NULL,NULL,NULL--`) until the server stops returning an error. A `200 OK` response confirms that the original query returns 3 columns:

<img width="1710" height="878" alt="Screenshot 2026-11-25 at 12 25 21" src="https://github.com/user-attachments/assets/62d21e63-209d-4c10-ae93-2efd49252ec0" />

3. **Identify the String-Compatible Column**: Probe each of the three column positions one by one by replacing `NULL` with a test string (`'a'`) to see which column accepts text data without throwing a type-conversion error:

- `' UNION SELECT 'a',NULL,NULL--` → Returns an error (incompatible data type).

- `' UNION SELECT NULL,'a',NULL--` → Returns a `200 OK` response and renders `'a'` on the page, confirming that the second column holds string data:

<img width="1710" height="1034" alt="Screenshot 2026-11-25 at 12 27 56" src="https://github.com/user-attachments/assets/4326136a-ede6-44dc-950c-702552546095" />

4. **Inject the Lab's Target String**: Replace the test string `'a'` with the random value provided in the lab banner (`'t7xqeP'`) using the following payload:

```
' UNION SELECT NULL,'t7xqeP',NULL--
```

Submitting this request injects the required value into the rendered page response and solves the lab:

<img width="1710" height="1034" alt="Screenshot 2026-11-25 at 12 29 53" src="https://github.com/user-attachments/assets/63b62e4c-fc49-4ac3-8eae-ecb0ead7f4d1" />
