# SQL injection in different parts of the query

While most SQL injection vulnerabilities occur inside the `WHERE` clause of a `SELECT` query and most experienced testers look there first SQL injection can actually arise anywhere within a query and across any type of SQL statement.

Because SQL syntax rules vary depending on where user input is placed inside a statement, each injection location requires a slightly different exploitation approach.

## Common SQL Injection Locations Beyond `SELECT ... WHERE`

### `UPDATE` Statements (Updated Values or `WHERE` Clause):

- **Context**: Occurs when updating user profiles, settings, or records (e.g., `UPDATE users SET email = 'user_input' WHERE id = 123`).
- **Risk**: An attacker injecting into the SET clause can overwrite additional columns (such as `role = 'admin'` or `password = '...'`), while injecting into the WHERE clause without care can accidentally modify every row in the table.

### `INSERT` Statements (Inserted Values):

- **Context**: Occurs when creating new records, such as user registration, posting comments, or logging events (e.g., `INSERT INTO users (username, email) VALUES ('user_input', 'test@example.com')`).
- **Risk**: Attackers can break out of the `VALUES` tuple to inject subqueries (such as `(SELECT password FROM users WHERE username='administrator')`) into a visible field like their own profile bio or comment exfiltrating sensitive data when that record is later displayed back to them.

### `SELECT` Statements (Table or Column Names):

- **Context**: Occurs when dynamic queries allow users to choose which field or dataset to view (e.g., `SELECT user_input FROM products`).
- **Risk**: Standard parameterised queries (prepared statements) cannot bind table or column names they only parameterise data values. If developers concatenate user input directly into identifiers without a strict whitelist, attackers can extract arbitrary columns or pivot into entirely different tables.

### SELECT Statements (`ORDER BY` Clause):

- **Context**: Occurs in sorting features on tables or product listings (e.g., S`ELECT * FROM products ORDER BY user_input`).
- **Risk**: Like table and column names, `ORDER BY` targets cannot be parameterised using standard prepared statements. Attackers can exploit this using stacked expressions, `CASE WHEN` conditional statements (for Boolean-based or Time-based Blind SQLi), or column index numbers (`ORDER BY 1`, `ORDER BY 2`) to enumerate the number of columns in the query.
