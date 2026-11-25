# Finding columns with a useful data type

Once you know the exact number of columns returned by the original query, the next step in a SQL injection `UNION` attack is to identify which of those columns can hold string data. Because sensitive information (such as usernames, passwords, or database version strings) is typically text-based, you need at least one column in the original query whose data type is compatible with strings so the application can render your extracted data in its response.

## How to Probe for String-Compatible Columns

To determine which columns accept string values, inject a test string (such as `'a'`) into each column position one by one while keeping the remaining positions as `NULL`.

Assuming the original query returns four columns, test each position sequentially using the following payloads:

```
' UNION SELECT 'a',NULL,NULL,NULL--
' UNION SELECT NULL,'a',NULL,NULL--
' UNION SELECT NULL,NULL,'a',NULL--
' UNION SELECT NULL,NULL,NULL,'a'--
```

> If targeting an Oracle database, remember to append `FROM DUAL` before the `--` comment.

## Interpreting the Application's Response

- **Incompatible Data Type (Error)**: If the tested column expects a non-string data type (such as an integer or date), the database will throw a type-conversion error (typically resulting in a `500 Internal Server Error` or a verbose error message), such as:

```
Conversion failed when converting the varchar value 'a' to data type int.
```

- **Compatible Data Type (Success)**: If the query executes without errors and the injected string (`a`) appears somewhere in the application's HTTP response, that column is string-compatible and can be used to exfiltrate text data in subsequent queries.
