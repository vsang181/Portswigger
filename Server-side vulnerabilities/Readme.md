# Server-side vulnerabilities

Server-side vulnerabilities are security weaknesses in a web application's code, configuration, or underlying infrastructure that allow attackers to manipulate or exploit the back-end server.

## Path traversal

Path traversal (also known as directory traversal or dot-dot-slash) is a web application vulnerability that allows attackers to access restricted files and directories outside of the intended web root folder on a server.

- [What is path traversal?](https://github.com/vsang181/Portswigger/blob/main/Server-side%20vulnerabilities/Path%20traversal/What%20is%20path%20traversal%3F.md)
- [Reading arbitrary files via path traversal](https://github.com/vsang181/Portswigger/blob/main/Server-side%20vulnerabilities/Path%20traversal/Reading%20arbitrary%20files%20via%20path%20traversal.md)
- [Lab: File path traversal, simple case](https://github.com/vsang181/Portswigger/blob/main/Server-side%20vulnerabilities/Path%20traversal/Lab%3A%20File%20path%20traversal%2C%20simple%20case.md)

## Access control

Access control is a security process that regulates who or what can view, enter, or use physical spaces, digital networks, and data resources. It acts like a digital or physical bouncer, letting authorized people in while keeping unauthorized users out.

- What is access control?
- Vertical privilege escalation
- Unprotected functionality
- Lab: Unprotected admin functionality
- Unprotected functionality - Continued
- Lab: Unprotected admin functionality with unpredictable URL
- Parameter-based access control methods
- Lab: User role controlled by request parameter
- Horizontal privilege escalation
- Lab: User ID controlled by request parameter, with unpredictable user IDs
- Horizontal to vertical privilege escalation
- Lab: User ID controlled by request parameter with password disclosure

## Authentication

Authentication is the security process of verifying that a user, device, or system is genuinely who or what it claims to be. While identification asks "who are you?", authentication confirms "prove it" before granting access to systems, networks, or data.

- Authentication vulnerabilities
- What is the difference between authentication and authorization?
- Brute-force attacks
- Brute-forcing usernames
- Brute-forcing passwords
- Brute-forcing passwords - Continued
- Username enumeration
- Lab: Username enumeration via different responses
- Bypassing two-factor authentication
- Lab: 2FA simple bypass

## Server-side request forgery (SSRF)

Server-side request forgery (SSRF) is a web security vulnerability that allows an attacker to trick a server into making unauthorized network requests to unintended locations.

- What is SSRF?
- SSRF attacks against the server
- SSRF attacks against the server - Continued
- Lab: Basic SSRF against the local server
- SSRF attacks against other back-end systems
- Lab: Basic SSRF against another back-end system

## File upload vulnerabilities

File upload vulnerabilities occur when a web server allows users to upload files without properly validating their name, type, contents, or size.

- What are file upload vulnerabilities?
- How do file upload vulnerabilities arise?
- Exploiting unrestricted file uploads to deploy a web shell
- Lab: Remote code execution via web shell upload
- Exploiting flawed validation of file uploads
- Flawed file type validation
- Flawed file type validation - Continued
- Flawed file type validation - Continued
- Lab: Web shell upload via Content-Type restriction bypass

## OS command injection

OS command injection is a web security vulnerability that allows an attacker to execute arbitrary operating system commands on the server running an application.

- What is OS command injection?
- Useful commands
- Injecting OS commands
- Injecting OS commands - Continued
- Lab: OS command injection, simple case

## SQL injection

SQL injection (SQLi) is a web security vulnerability that allows an attacker to interfere with the queries an application makes to its database.

- What is SQL injection (SQLi)?
- How to detect SQL injection vulnerabilities
- Retrieving hidden data
- Retrieving hidden data - Continued
- Lab: SQL injection vulnerability in WHERE clause allowing retrieval of hidden data
- Subverting application logic
- Lab: SQL injection vulnerability allowing login bypass
  
