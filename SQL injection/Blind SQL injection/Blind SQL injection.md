# Blind SQL injection

Blind SQL injection occurs when an application is vulnerable to SQL injection, but its HTTP responses do not contain the results of the injected SQL query or any verbose database error messages. Because you cannot directly see the output of your query on the page, UNION-based data extraction techniques are ineffective.

## How It Works

Even without direct output, you can still exploit blind SQL injection to extract data one character at a time or trigger out-of-band interactions by observing indirect clues in how the application behaves.
