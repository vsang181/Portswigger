# Exploiting the WHERE Clause to Expose Hidden Records

Because the application implements no defences against SQL injection, an attacker can manipulate the `category` parameter to alter the query logic and expose hidden data.

### 1. Stripping the `released = 1` Restriction with SQL Comments

By appending a single quote (`'`) followed by a double-dash comment indicator (`--`), the attacker closes the `Gifts` string literal early and comments out the rest of the original SQL query:

```
https://insecure-website.com/products?category=Gifts'--
```

This causes the database to execute:

```
SELECT * FROM products WHERE category = 'Gifts'--' AND released = 1
```

In SQL, `--` tells the database engine to ignore everything that follows on that line. Because `AND released = 1` is commented out, the database returns all products in the `Gifts` category including unreleased items where `released = 0`.

### 2. Dumping Every Category Using `OR 1=1`

To retrieve every product across all categories (even hidden or unknown categories), the attacker can inject an always-true boolean condition (`OR 1=1`) before the comment indicator:

```
https://insecure-website.com/products?category=Gifts'+OR+1=1--
```

> Note: `+` represents a URL-encoded space.

This results in the following SQL query:

```
SELECT * FROM products WHERE category = 'Gifts' OR 1=1--' AND released = 1
```

Because `1=1` always evaluates to True for every row in the `products` table, and the trailing `AND released = 1` check is commented out, the database returns the entire contents of the `products` table.

> **Warning**: Exercise caution when injecting `OR 1=1` into live applications. A single HTTP request parameter is often reused across multiple back-end SQL statements. If your `OR 1=1` payload reaches an `UPDATE` or `DELETE` query (e.g., `DELETE FROM logs WHERE category = '...' OR 1=1--`), the `WHERE` clause will match every single row, resulting in accidental mass data corruption or deletion.
