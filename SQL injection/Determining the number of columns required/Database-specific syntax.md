# Database-specific syntax

Different database management systems (DBMS) enforce unique SQL syntax rules. Understanding these variations is essential when crafting UNION attacks or commenting out the remainder of an original query, as standard payloads may trigger syntax errors depending on the back-end database.

## Oracle `FROM` Clause Requirement

Unlike databases such as MySQL, PostgreSQL, or Microsoft SQL Server, Oracle requires every `SELECT` statement to include a `FROM` clause specifying a valid table name. If you omit `FROM`, the database will reject the query with a syntax error.

- **The `DUAL` Table**: Oracle provides a built-in, single-row, single-column dummy table called `DUAL` specifically for queries that do not need to pull data from an actual user table.

- **Payload Example**: When determining column counts on an Oracle database, append `FROM DUAL` to your injected `SELECT` statement:

```
' UNION SELECT NULL FROM DUAL--
```

## Database Comment Syntax Variations

Comments are used in SQL injection payloads to strip out the rest of the original application query after the injection point so it does not cause syntax errors.

- **Standard Double-Dash (`--`)**: Works across most databases (such as Oracle, PostgreSQL, and Microsoft SQL Server) without needing anything after it.

- **MySQL Double-Dash (`-- `)**: On MySQL, the `--` comment sequence must be followed by at least one space or whitespace character (such as `-- ` or URL-encoded `--+`) to be recognized as a valid comment.

- **MySQL Hash (`#`)**: Alternatively, MySQL supports the `#` character (URL-encoded as `%23`) to denote a single-line comment without requiring a trailing space:

```
' UNION SELECT NULL, NULL#
```

## Quick Reference Table


| Database | Requires `FROM` in `SELECT`? | Valid Comment Syntax | Example Column-Count Payload |
| --- | --- | --- | --- |
| Oracle | Yes (`FROM DUAL`) | `--` | `' UNION SELECT NULL FROM DUAL--` |
| MySQL | No | `-- `(with space) or `#` | `' UNION SELECT NULL#` |
| PostgreSQL | No | `--` | `' UNION SELECT NULL--` |
| MS SQL Server | No | `--` | `' UNION SELECT NULL--` |

For more details of database-specific syntax, see the [SQL injection cheat sheet](https://portswigger.net/web-security/sql-injection/cheat-sheet).
