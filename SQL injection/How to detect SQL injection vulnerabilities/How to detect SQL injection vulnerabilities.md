# How to detect SQL injection vulnerabilities

You can detect SQL injection manually by running a systematic set of tests against every user-controllable entry point in the application (including URL query parameters, `POST` body fields, cookies, and HTTP headers). Alternatively, you can automate the discovery of most SQL injection vulnerabilities quickly and reliably using Burp Scanner.

## Systematic Manual Detection Methodology

When testing an input parameter manually, work through these five core techniques:

### 1. Single Quote Syntax Testing (`'`):
	
- Submit a single quote character `'` (or `''`) and observe the application's response.
- Look for verbose database error messages (such as `Syntax error` or `Unclosed quotation mark`), `500 Internal Server` Error status codes, or unusual behavioural anomalies caused by breaking out of a SQL string literal.

> **Tip**: Submitting two single quotes (`''`) often restores valid syntax (`'` + `'` escapes the quote in SQL), confirming that the error was caused by SQL parsing rather than generic input validation.

### 2. SQL-Specific Evaluation Expressions:

- Submit SQL syntax that evaluates back to the original (base) value of the entry point, and compare it against syntax that evaluates to a different value.
- For example, if a parameter expects the string admin, compare `' || 'admin` (or `' + 'admin` depending on the database) against `' || 'different`. Look for systematic differences between the two responses.

### 3. Boolean Conditions (`OR 1=1` vs. `OR 1=2`):

- Inject logic conditions that always evaluate to True (`' OR 1=1--`) versus conditions that always evaluate to False (`' OR 1=2--`).
- Compare the HTTP responses (status codes, content length, or returned items). If `OR 1=1` returns extra data or normal page content while `OR 1=2` returns missing data or an empty result, the application is likely vulnerable to Boolean-based Blind SQLi.

### 4. Time-Delay Payloads (Time-Based Blind SQLi):

- Submit database-specific sleep functions (such as `pg_sleep(10)` on PostgreSQL, `SLEEP(10)` on MySQL, or `WAITFOR DELAY '0:0:10'` on MSSQL) designed to pause query execution.
- Measure the HTTP response time. A consistent delay matching your payload (e.g., 10 seconds) confirms SQL injection even when the application returns identical responses and suppresses all errors.

### 5. Out-of-Band Application Security Testing (OAST):

- Submit payloads designed to force the database server to trigger an external network interaction (such as a DNS lookup or HTTP request) to an attacker-controlled server (like Burp Collaborator).
- Monitor for incoming DNS or HTTP interactions. This technique is ideal for asynchronous SQL injection, where queries run in background threads and neither errors nor time delays affect the front-end HTTP response.
