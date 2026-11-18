# Horizontal privilege escalation

Horizontal privilege escalation occurs when a user gains access to resources or data belonging to another user at the **same privilege level**, rather than only accessing their own resources.

## Key Characteristics

- **Moving "Sideways" in Privilege**: Instead of gaining admin powers, a regular user accesses another regular user's private account, profile, or records.

- **Real-World Example**: An employee can view the salary or HR records of other employees in addition to their own.

How the Attack Works (IDOR)

Horizontal privilege escalation often uses the same exploitation methods as vertical privilege escalation, such as tampering with URL parameters:

- **Normal Request**: A user accesses their own account page via a URL containing their user ID:

```
https://insecure-website.com/myaccount?id=123
```

- **Malicious Request**: Changing the `id` parameter to another number (such as `id=124`) loads another user's account page, exposing their private data and account functions.

- **Insecure Direct Object Reference (IDOR)**: This specific flaw is a classic example of an IDOR vulnerability, which happens when an application uses user-controllable input to access database records or objects directly without checking ownership.

## Bypassing Unpredictable Identifiers (GUIDs)

- **Why Sequential IDs Are Replaced**: Some applications replace simple incrementing numbers (`123`, `124`) with **Globally Unique Identifiers (GUIDs**) so attackers cannot easily guess or brute-force another user's ID.

- **How GUIDs Still Leak**: Even when GUIDs cannot be guessed, they are frequently exposed in public areas of the application where users are referenced, such as:
  - User profile links
  - Product reviews or comments
  - Public messages or forum posts
