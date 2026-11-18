# What is Access Control?

Access control is the enforcement of rules that restrict who or what is authorized to perform actions or access specific resources.

## How Web Access Control Works

In web applications, access control relies directly on two foundational processes:

- **Authentication**: Confirms that the user is actually who they claim to be (e.g., logging in with a username and password).

- **Session Management**: Tracks and identifies which subsequent HTTP requests belong to that same authenticated user.

- **Access Control**: Determines whether that specific user has permission to carry out the action or view the resource they are requesting.

## Common Attack Scenarios

When access controls are broken, an attacker can bypass restrictions to reach unauthorized endpoints:

- **Vertical Privilege Escalation**: Accessing sensitive administrative functions without admin privileges (e.g., visiting `https://insecure-website.com/admin` to delete users).

- **Horizontal Privilege Escalation**: Accessing another regular user's private data or account controls by manipulating URLs or parameters (e.g., visiting `https://insecure-website.com/accounts/ab12345/accountmenu.jsp` to view balances or transfer funds).

<img width="1295" height="757" alt="image" src="https://github.com/user-attachments/assets/db4a1027-07ca-41d2-b9a2-fa0b953c90c8" />

## Why Broken Access Controls Happen

- **Critical Severity**: Broken access control is a very common and high-impact web security vulnerability.

- **Human Error**: Designing access rules requires translating complex business, organizational, and legal policies into technical code. Because these design decisions are made by humans, the risk of misconfiguration or oversight is high.
