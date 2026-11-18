# Brute-forcing usernames

Usernames are often much easier to guess than passwords because they follow predictable patterns or appear publicly across an application.

## Common Username Patterns

- **Recognizable Formats**: Business logins frequently use predictable email structures, such as `firstname.lastname@somecompany.com`.

- **Default High-Privilege Accounts**: Administrators often use standard, easy-to-guess usernames like `admin` or `administrator`.

## Where to Find Disclosed Usernames During Auditing

Before running a brute-force wordlist, check if the application already leaks valid usernames:

- **Public User Profiles**: Check if you can view user profiles without logging in. Even when profile details are restricted, the display name or URL slug often matches the actual login username.

- **HTTP Responses and Source Code**: Inspect HTTP traffic, API responses, and HTML comments for leaked email addresses. Applications occasionally expose contact emails for high-privileged staff, such as administrators or IT support.
