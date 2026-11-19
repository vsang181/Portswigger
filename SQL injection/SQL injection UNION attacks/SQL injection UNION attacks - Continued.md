# SQL injection UNION attacks - Continued

## Core Requirements for a `UNION` Query

For a SQL `UNION` query to execute successfully without causing a database error, two strict conditions must be satisfied:

1. **Matching Column Count**: The individual `SELECT` queries must return the exact same number of columns.

2. **Compatible Data Types**: The data types in each column position must be compatible between the original query and the injected query (for example, matching strings with text/varchar columns, or integers with numeric columns).

## Two-Step Preparation Before Extracting Data

Before you can append your own `UNION SELECT` query to dump sensitive tables (such as `users`), you must first probe the original query to determine:

- **Step 1 — Column Count**: How many columns are being returned by the original SELECT query?

- **Step 2 — Suitable Data Types (String Columns)**: Which of those returned columns can hold useful text/string data and are actually rendered in the application's HTTP response?
