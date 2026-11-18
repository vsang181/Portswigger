# Path Traversal (Directory Traversal)

Path traversal is a web security vulnerability that allows an attacker to read arbitrary files on the server running an application. It is also commonly known as directory traversal.

## What an Attacker Can Read

When exploiting a read-only path traversal flaw, an attacker can access sensitive data stored on the server, including:
- **Application files**: Source code and internal application data.
- **Credentials**: Passwords, API keys, and tokens for back-end systems.
- **System files**: Sensitive operating system configuration files (such as /etc/passwd on Linux).

## High-Severity Impact (Arbitrary File Write)

- **Modifying behavior**: In some cases, the vulnerability allows an attacker to write to arbitrary files on the server, letting them alter application data or logic.
- **Full server takeover**: Writing malicious files (like web shells or SSH keys) can ultimately allow the attacker to gain complete control over the server.
