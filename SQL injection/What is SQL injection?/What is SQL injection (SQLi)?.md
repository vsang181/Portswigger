# What is SQL injection (SQLi)?

SQL injection (SQLi) is a critical web security vulnerability that allows an attacker to interfere with the queries an application makes to its back-end database.

When an application inserts untrusted user input directly into a database query without proper sanitisation or parameterisation, an attacker can manipulate the SQL syntax to view, modify, or delete data they are not normally permitted to access.

## Key Security Impacts

- **Unauthorised Data Retrieval**: Attackers can view sensitive data belonging to other users (such as passwords, personal details, or payment information) or any other tables the database user can access.

- **Data Modification and Deletion**: In many cases, attackers can alter or delete records (using `UPDATE`, `INSERT`, or `DELETE` statements), causing persistent changes to the application's content or behaviour.

- **Authentication & Access Control Bypass**: Manipulating login or session queries can allow attackers to log in as arbitrary users including administrators without knowing a valid password.

- **Server & Infrastructure Compromise**: In certain database configurations (such as Microsoft SQL Server's `xp_cmdshell` or PostgreSQL's `COPY ... FROM PROGRAM`), attackers can escalate SQL injection to execute operating system commands and take over the underlying server.

- **Denial of Service (DoS)**: Attackers can drop critical tables, lock database resources, or trigger heavy queries that degrade or crash the database service.
