# Error-based SQL injection

Error-based SQL injection is an exploitation technique where an attacker uses database error messages to either infer or directly extract sensitive data from a database. It is especially useful in **blind SQL injection** contexts where the application does not normally return query results in its HTTP responses. 

## How It Works

When a web application fails to properly handle database exceptions, the resulting errors can leak information. Depending on how the database and application are configured, an attacker can manipulate queries to intentionally force these errors. By analyzing whether an error occurs or by reading the contents of the error message itself the attacker can reconstruct hidden data. 

## Common Exploitation Techniques

- **Triggering Conditional Errors:** The attacker injects a crafted boolean condition into the query that forces the database to throw an error only when the condition evaluates to true (or false). For example, the payload might trigger a divide-by-zero error if the first character of an administrator's password matches a specific letter. By observing whether the application returns a generic error response (such as an HTTP `500 Internal Server Error`) or a normal page, the attacker can infer data one character at a time.

-  **Extracting Data via Verbose Error Messages:** If the application is configured to display detailed, unmasked database error messages directly in the response, the attacker can craft a query that forces the database to evaluate a subquery and include its result inside the error text (such as causing a type-conversion error when trying to convert a string value into an integer). This effectively turns a blind vulnerability into a visible, in-band SQL injection.
