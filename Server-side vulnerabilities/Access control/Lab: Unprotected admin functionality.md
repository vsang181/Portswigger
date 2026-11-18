# Lab: Unprotected admin functionality

> Objective: This lab has an unprotected admin panel. Solve the lab by deleting the user `carlos`.

## Solution

1. **Check `robots.txt` for Hidden Paths**: Navigating to `/robots.txt` reveals an exposed configuration file listing a disallowed directory path (`/administrator-panel`):

```
User-agent: *
Disallow: /administrator-panel
```

<img width="794" height="132" alt="image" src="https://github.com/user-attachments/assets/389a1f57-c603-434a-90dc-fff0cd88b3fd" />

2. **Browse Directly to the Admin Endpoint**: Navigating to `/administrator-panel` in the browser loads the full administrative dashboard without requiring authentication or privilege checks.

<img width="1283" height="521" alt="image" src="https://github.com/user-attachments/assets/86cc4fab-62f8-4782-a116-8104d18254a2" />

3. **Delete the Target User**: Because the endpoint enforces no access control, clicking the delete button next to `carlos` removes the user account and solves the lab.
