# SQL injection UNION attacks

When an application is vulnerable to SQL injection and the results of the query are returned directly within the application's HTTP responses (known as in-band SQL injection), you can use the UNION keyword to retrieve data from entirely different tables within the database. This technique is known as a SQL injection UNION attack.

## How the `UNION` Operator Works

The SQL `UNION` keyword enables you to execute one or more additional `SELECT` queries and append their results directly onto the result set of the original query.

For example:

```
SELECT a, b FROM table1 UNION SELECT c, d FROM table2
```

This combined SQL statement returns a single result set containing two columns:

- The first set of rows holds values from columns `a` and `b` in `table1`.
- The appended rows hold values from columns `c` and `d` in `table2`.

Because the application loops through the query's result set to render content on the web page, any data appended by your injected `UNION SELECT` query gets displayed directly in the application's response.

## The Two Golden Rules of UNION Attacks

For a `UNION` query to execute without triggering a database syntax or type error, two strict requirements must be met:

1. **Equal Number of Columns**: The injected `SELECT` query must return the exact same number of columns as the original query.

2. **Compatible Data Types**: The data types in each column of the injected query must be compatible with the corresponding columns in the original query (for example, placing string data into a column that expects text/varchar rather than an integer or date).
