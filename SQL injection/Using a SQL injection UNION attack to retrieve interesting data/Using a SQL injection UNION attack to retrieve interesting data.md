# Using a SQL injection UNION attack to retrieve interesting data

Once you have determined the exact number of columns returned by the original query and identified which of those columns can hold string data, you are ready to extract sensitive information from other tables in the database.

## Prerequisites for Data Extraction

Before constructing the final `UNION SELECT` payload, verify the following conditions:

- **Column Count & Data Types**: You know how many columns the original query returns and which positions accept string values (e.g., two string-compatible columns).

- **Injection Context**: You know how to break out of the original query cleanly (e.g., closing a single quote within a `WHERE` clause and commenting out the remainder with `--`).

- **Target Table & Column Names**: You know the names of the target table and the specific columns you want to read (such as a `users` table containing `username` and `password` columns).

## Constructing the Payload

Suppose the original query returns **two string-compatible columns**, and the injection point is inside a single-quoted string in a `WHERE` clause. You can dump all usernames and passwords from the `users` table with the following payload:

```
' UNION SELECT username, password FROM users--
```

> If only one column in the original query accepts string data, you can leave the incompatible columns as `NULL` and either query one column at a time or concatenate multiple values into that single string column).

## Discovering Unknown Table and Column Names

In real-world scenarios, you will rarely know the exact names of tables and columns upfront. Rather than guessing, you can query the database's built-in metadata views (such as `information_schema.tables` and `information_schema.columns` on MySQL, PostgreSQL, and MS SQL Server, or `all_tables` and `all_tab_columns` on Oracle) to map out the database structure before extracting the data.
