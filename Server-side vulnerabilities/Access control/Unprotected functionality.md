# Unprotected functionality

At its most basic level, **vertical privilege escalation** occurs when an application fails to enforce any server-side access checks on sensitive endpoints. Instead, it relies entirely on hiding the links from standard users ("security through obscurity").

## How the Vulnerability Works

- **UI-Only Restrictions**: Administrative features are displayed on an admin's welcome page but hidden from a regular user's interface.

- **Direct URL Access**: Because the server does not verify the user's role when the endpoint is requested, any regular user can simply type the direct URL into their browser to access the admin panel:

```
https://insecure-website.com/admin
```

## How Attackers Find Hidden URLs

Even when sensitive URLs are not shown in the main user interface, attackers can discover them through several methods:

- **Information Disclosure (`robots.txt`)**: Sensitive paths are often accidentally listed in public configuration files to stop search engines from indexing them:

```
https://insecure-website.com/robots.txt
```

- **Directory Brute-Forcing**: If the URL is not disclosed anywhere, an attacker can use automated tools and wordlists (like Burp Intruder, Gobuster, or Dirb) to guess common administrative paths.
