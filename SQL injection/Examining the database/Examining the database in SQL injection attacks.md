# Examining the database in SQL injection attacks

In most real-world SQL injection scenarios, you will not know the structure of the back-end database upfront. Before you can extract sensitive data (such as credentials or API keys), you must enumerate the environment to gather two critical pieces of information:

## Key Information to Enumerate

- **Database Type and Version**: Identifying the exact database management system (such as MySQL, PostgreSQL, Oracle, or Microsoft SQL Server) and its version dictates which SQL syntax, comment characters, string concatenation operators, and built-in functions you can use in your payloads. It also helps determine if the database software is outdated and vulnerable to known exploits.

- **Database Schema (Tables and Columns)**: Mapping out the names of the tables and their specific columns allows you to locate where sensitive data is stored (for example, finding out whether user credentials live in a table named `users`, `accounts`, or `tbl_admin_creds`) so you can craft targeted `SELECT` statements.

## Why Enumeration Matters

Different database vendors store metadata about their own versions and schemas in completely different built-in views or functions. By fingerprinting the database type first, you avoid guesswork and can systematically query the database's internal catalog to list every table and column available to the application's database user.
