# Blind SQL injection

Blind SQL injection occurs when an application is vulnerable to SQL injection, but its HTTP responses do not contain the results of the injected SQL query or any verbose database error messages. Because you cannot directly see the output of your query on the page, UNION-based data extraction techniques are ineffective.

## How It Works

Even without direct output, you can still exploit blind SQL injection to extract data one character at a time or trigger out-of-band interactions by observing indirect clues in how the application behaves.

## Common Exploitation Techniques

- **Conditional Responses (Boolean-Based)**: Injecting a condition (such as `AND 1=1` vs. `AND 1=2`) that changes the application's HTTP response (e.g., displaying or hiding a `"Welcome back"` banner) depending on whether the injected SQL condition evaluates to `TRUE` or `FALSE`.

- **Conditional Errors (Error-Based)**: Forcing the database to intentionally throw an unhandled error (such as dividing by zero) only when a specific SQL condition evaluates to `TRUE`, allowing you to infer data from `500 Internal Server Error` vs. `200 OK` responses.

- **Time Delays (Time-Based)**: Injecting database-specific sleep functions (such as `pg_sleep(10)` or `WAITFOR DELAY '0:0:10'`) that pause the server's response for a set duration when a condition is `TRUE`, letting you infer data by measuring response times.

- **Out-of-Band (OAST) Techniques**: Triggering the database server to make an asynchronous DNS or HTTP network request to an external server you control (such as Burp Collaborator), carrying the extracted query results inside the subdomain or request path.
