# What is blind SQL injection?

Blind SQL injection occurs when an application is vulnerable to SQL injection, but its HTTP responses do not return the results of the relevant SQL query or expose any verbose database error messages.

## Why Standard `UNION` Attacks Fail

Traditional `UNION`-based SQL injection relies on the application rendering query output directly inside the HTTP response. Because a blind SQL injection vulnerability executes the database query silently in the background without reflecting any data back to the user, standard `UNION SELECT` payloads cannot display extracted information on the page.

## Common Exploitation Techniques

- **Conditional Responses (Boolean-Based)**: Injecting a condition (such as `AND 1=1` vs. `AND 1=2`) that changes the application's HTTP response (e.g., displaying or hiding a `"Welcome back"` banner) depending on whether the injected SQL condition evaluates to `TRUE` or `FALSE`.

- **Conditional Errors (Error-Based)**: Forcing the database to intentionally throw an unhandled error (such as dividing by zero) only when a specific SQL condition evaluates to `TRUE`, allowing you to infer data from `500 Internal Server Error` vs. `200 OK` responses.

- **Time Delays (Time-Based)**: Injecting database-specific sleep functions (such as `pg_sleep(10)` or `WAITFOR DELAY '0:0:10'`) that pause the server's response for a set duration when a condition is `TRUE`, letting you infer data by measuring response times.

- **Out-of-Band (OAST) Techniques**: Triggering the database server to make an asynchronous DNS or HTTP network request to an external server you control (such as Burp Collaborator), carrying the extracted query results inside the subdomain or request path.
