# Determining the number of columns required

Before constructing a `UNION SELECT` payload, you must first discover the exact number of columns returned by the original SQL query. There are two effective methods to determine the column count, starting with the `ORDER BY` method.

## Method 1: Incrementing `ORDER BY` Column Indexes

In SQL, an `ORDER BY` clause allows you to sort query results using a 1-based column index number (e.g., `ORDER BY 1` sorts by the first column, `ORDER BY 2` by the second) instead of needing to know the actual column names.

### Step-by-Step Technique

Assuming the injection point is inside a single-quoted string within a `WHERE` clause, submit a sequence of `ORDER BY` payloads while incrementing the index number until the application produces an error or anomalous response:

```
' ORDER BY 1--
' ORDER BY 2--
' ORDER BY 3--
```

### Interpreting the Application's Response

- **Valid Column Index (`1`, `2`, etc.)**: The query succeeds, and the application returns the normal page content (sorted differently).
- **Out-of-Range Index (Exceeds Actual Column Count)**: Once the index number exceeds the total number of columns in the `SELECT` list, the database throws an error such as:

```
The ORDER BY position number 3 is out of range of the number of items in the select list.
```

- **Confirming the Count**: If `' ORDER BY 2--` succeeds and `' ORDER BY 3--` triggers an error, you have confirmed that the original query returns 2 columns.

## Handling Suppressed Errors

Even if the application hides verbose database error messages, you can still infer the exact column count by watching for any systematic difference in the HTTP response once the index goes out of range, including:

- A generic HTTP `500 Internal Server Error` or custom error page.
- An empty result set (no products or items displayed on the page).
- A noticeable drop in response content length.
