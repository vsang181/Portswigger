# Lab: SQL injection attack, querying the database type and version on MySQL and Microsoft

> This lab contains a SQL injection vulnerability in the product category filter. You can use a UNION attack to retrieve the results from an injected query. To solve the lab, display the database version string.

## Solution

1. **Intercept the Category Filter Request**: Select a product category (such as `Gifts`) and intercept the outgoing `GET` request in Burp Suite (or send it to Burp Repeater). Inspecting the request reveals the `category` parameter in the URL query string, which serves as our SQL injection point:

<img width="664" height="467" alt="Screenshot 2026-11-25 at 13 45 43" src="https://github.com/user-attachments/assets/32fca072-1efc-4d5a-90ac-3787e89facd0" />

2. **Determine the Column Count and Comment Syntax**: Testing standard payloads terminated with `--` (such as `' UNION SELECT NULL--`) results in errors because MySQL requires a trailing space after `--.` Switching the comment indicator to `#` (URL-encoded as `%23`) and testing with `' UNION SELECT NULL, NULL#` returns a `200 OK` response, confirming that the back-end database is MySQL and the original query returns **2 columns**:

<img width="1331" height="837" alt="Screenshot 2026-11-25 at 13 49 37" src="https://github.com/user-attachments/assets/4dcf51ec-e138-46c9-8a70-f4302d1f4855" />

3. **Identify String-Compatible Columns**: Probe the column positions by replacing `NULL` with a test string (`'test_string'`) to verify which columns accept string data without throwing a type-conversion error (note: both columns accept strings, allowing us to use either position):

<img width="1332" height="707" alt="Screenshot 2026-11-25 at 13 51 12" src="https://github.com/user-attachments/assets/2ad3726e-f015-4953-ba68-fb02fc2daf06" />

4. **Query the Database Version**: Now that we know the database is MySQL and accepts string output, inject the `@@version` system variable into our `UNION` payload:

```
' UNION SELECT @@version, NULL#
```

Submitting this request displays the database version string directly in the page response, solving the lab:

<img width="1333" height="829" alt="Screenshot 2026-11-25 at 13 58 15" src="https://github.com/user-attachments/assets/1db65a64-2e51-461e-b0c7-aa2ce744d03f" />
