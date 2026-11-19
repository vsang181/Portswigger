# Determining the number of columns required - Continued

## Method 2: Incrementing `UNION SELECT NULL` Payloads

The second technique for finding the column count involves injecting a series of `UNION SELECT` payloads and increasing the number of `NULL` values until the query succeeds without error:

```
' UNION SELECT NULL--
' UNION SELECT NULL,NULL--
' UNION SELECT NULL,NULL,NULL--
```

## Why `NULL` Is Used

Because a `UNION` query requires compatible data types across every column position, testing with arbitrary strings or integers early on could trigger a data-type mismatch error even when your column count is right.

- `NULL` is universally convertible to every common SQL data type (strings, integers, dates, booleans).
- Using `NULL` eliminates data-type conflicts, ensuring that any error you see is caused strictly by an incorrect column count.

## Interpreting the Application's Response

- **Incorrect Number of NULLs**: The database rejects the query and throws an error (either displayed verbosely or handled as a generic 500 error / empty page), such as:

```
All queries combined using a UNION, INTERSECT or EXCEPT operator must have an equal number of expressions in their target lists.
```

- **Matching Number of `NULLs`**: The database accepts the `UNION` and appends an extra row of `NULL` values to the result set. Depending on how the application processes those `NULL` values, you will observe one of three outcomes:
  - **Best Case**: The page renders normally and displays additional content (such as an extra blank row in an HTML table or product list).
  - **Application-Level Null Error**: The database query succeeds, but the application code crashes when trying to process a `NULL` field (e.g., throwing a `NullPointerException`), producing a noticeably different error than a SQL syntax error.
  - **Worst Case (Method Ineffective)**: If the application catches `NullPointerException` and returns the exact same generic error page as an invalid SQL query, you cannot tell the difference in which case you should fall back to Method 1 (`ORDER BY`).
