# Subverting application logic

Beyond extracting hidden data, SQL injection can be used to subvert application logic altering how the application makes security decisions, such as authenticating users.

## Bypassing Authentication via SQL Injection

Consider an application that authenticates users via a login form accepting a `username` and `password`. When a user submits `wiener` and `bluecheese`, the back-end application verifies the credentials using the following SQL query:

```
SELECT * FROM users WHERE username = 'wiener' AND password = 'bluecheese'
```

- **If the query returns a matching user record**: The login succeeds, and the application creates an authenticated session for that user.

- **If the query returns zero records**: The login fails and is rejected.

## Exploiting the Login Query

Because the `username` input is concatenated directly into the query without parameterisation, an attacker can log in as any user without knowing their password. By submitting `administrator'--` as the username (with any or blank password), the resulting query becomes:

```
SELECT * FROM users WHERE username = 'administrator'--' AND password = ''
```

- The single quote (`'`) closes the `'administrator'` string literal early.
- The SQL comment indicator (`--`) causes the database engine to ignore the remainder of the query (`' AND password = ''`), completely removing the password verification check.
- The database simply looks up the user whose username is `administrator`, returns their account record, and logs the attacker in as the administrator.
  
