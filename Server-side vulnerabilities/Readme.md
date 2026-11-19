# Server-side vulnerabilities

Server-side vulnerabilities are security weaknesses in a web application's code, configuration, or underlying infrastructure that allow attackers to manipulate or exploit the back-end server.

## Path traversal

Path traversal (also known as directory traversal or dot-dot-slash) is a web application vulnerability that allows attackers to access restricted files and directories outside of the intended web root folder on a server.

- [What is path traversal?](https://github.com/vsang181/Portswigger/blob/main/Server-side%20vulnerabilities/Path%20traversal/What%20is%20path%20traversal%3F.md)
- [Reading arbitrary files via path traversal](https://github.com/vsang181/Portswigger/blob/main/Server-side%20vulnerabilities/Path%20traversal/Reading%20arbitrary%20files%20via%20path%20traversal.md)
- [Lab: File path traversal, simple case](https://github.com/vsang181/Portswigger/blob/main/Server-side%20vulnerabilities/Path%20traversal/Lab%3A%20File%20path%20traversal%2C%20simple%20case.md)

## Access control

Access control is a security process that regulates who or what can view, enter, or use physical spaces, digital networks, and data resources. It acts like a digital or physical bouncer, letting authorized people in while keeping unauthorized users out.

- [What is access control?](https://github.com/vsang181/Portswigger/blob/main/Server-side%20vulnerabilities/Access%20control/What%20is%20access%20control%3F.md)
- [Vertical privilege escalation](https://github.com/vsang181/Portswigger/blob/main/Server-side%20vulnerabilities/Access%20control/Vertical%20privilege%20escalation.md)
- [Unprotected functionality](https://github.com/vsang181/Portswigger/blob/main/Server-side%20vulnerabilities/Access%20control/Unprotected%20functionality.md)
- [Lab: Unprotected admin functionality](https://github.com/vsang181/Portswigger/blob/main/Server-side%20vulnerabilities/Access%20control/Lab%3A%20Unprotected%20admin%20functionality.md)
- [Unprotected functionality - Continued](https://github.com/vsang181/Portswigger/blob/main/Server-side%20vulnerabilities/Access%20control/Unprotected%20functionality%20-%20Continued.md)
- [Lab: Unprotected admin functionality with unpredictable URL](https://github.com/vsang181/Portswigger/blob/main/Server-side%20vulnerabilities/Access%20control/Lab%3A%20Unprotected%20admin%20functionality%20with%20unpredictable%20URL.md)
- [Parameter-based access control methods](https://github.com/vsang181/Portswigger/blob/main/Server-side%20vulnerabilities/Access%20control/Parameter-based%20access%20control%20methods.md)
- [Lab: User role controlled by request parameter](https://github.com/vsang181/Portswigger/blob/main/Server-side%20vulnerabilities/Access%20control/Lab%3A%20User%20role%20controlled%20by%20request%20parameter.md)
- [Horizontal privilege escalation](https://github.com/vsang181/Portswigger/blob/main/Server-side%20vulnerabilities/Access%20control/Horizontal%20privilege%20escalation.md)
- [Lab: User ID controlled by request parameter, with unpredictable user IDs](https://github.com/vsang181/Portswigger/blob/main/Server-side%20vulnerabilities/Access%20control/Lab%3A%20User%20ID%20controlled%20by%20request%20parameter%2C%20with%20unpredictable%20user%20IDs.md)
- [Horizontal to vertical privilege escalation](https://github.com/vsang181/Portswigger/blob/main/Server-side%20vulnerabilities/Access%20control/Horizontal%20to%20vertical%20privilege%20escalation.md)
- [Lab: User ID controlled by request parameter with password disclosure](https://github.com/vsang181/Portswigger/blob/main/Server-side%20vulnerabilities/Access%20control/Lab%3A%20User%20ID%20controlled%20by%20request%20parameter%20with%20password%20disclosure.md)

## Authentication

Authentication is the security process of verifying that a user, device, or system is genuinely who or what it claims to be. While identification asks "who are you?", authentication confirms "prove it" before granting access to systems, networks, or data.

- [Authentication vulnerabilities](https://github.com/vsang181/Portswigger/blob/main/Server-side%20vulnerabilities/Authentication/Authentication%20vulnerabilities.md)
- [What is the difference between authentication and authorization?](https://github.com/vsang181/Portswigger/blob/main/Server-side%20vulnerabilities/Authentication/What%20is%20the%20difference%20between%20authentication%20and%20authorization%3F.md)
- [Brute-force attacks](https://github.com/vsang181/Portswigger/blob/main/Server-side%20vulnerabilities/Authentication/Brute-force%20attacks.md)
- [Brute-forcing usernames](https://github.com/vsang181/Portswigger/blob/main/Server-side%20vulnerabilities/Authentication/Brute-forcing%20usernames.md)
- [Brute-forcing passwords](https://github.com/vsang181/Portswigger/blob/main/Server-side%20vulnerabilities/Authentication/Brute-forcing%20passwords.md)
- [Brute-forcing passwords - Continued](https://github.com/vsang181/Portswigger/blob/main/Server-side%20vulnerabilities/Authentication/Brute-forcing%20passwords%20-%20Continued.md)
- [Username enumeration](https://github.com/vsang181/Portswigger/blob/main/Server-side%20vulnerabilities/Authentication/Username%20enumeration.md)
- [Lab: Username enumeration via different responses](https://github.com/vsang181/Portswigger/blob/main/Server-side%20vulnerabilities/Authentication/Lab%3A%20Username%20enumeration%20via%20different%20responses.md)
- [Bypassing two-factor authentication](https://github.com/vsang181/Portswigger/blob/main/Server-side%20vulnerabilities/Authentication/Bypassing%20two-factor%20authentication.md)
- [Lab: 2FA simple bypass](https://github.com/vsang181/Portswigger/blob/main/Server-side%20vulnerabilities/Authentication/Lab%3A%202FA%20simple%20bypass.md)

## Server-side request forgery (SSRF)

Server-side request forgery (SSRF) is a web security vulnerability that allows an attacker to trick a server into making unauthorized network requests to unintended locations.

- [What is SSRF?](https://github.com/vsang181/Portswigger/blob/main/Server-side%20vulnerabilities/Server-side%20request%20forgery%20(SSRF)/What%20is%20SSRF%3F.md)
- [SSRF attacks against the server](https://github.com/vsang181/Portswigger/blob/main/Server-side%20vulnerabilities/Server-side%20request%20forgery%20(SSRF)/SSRF%20attacks%20against%20the%20server.md)
- [SSRF attacks against the server - Continued](https://github.com/vsang181/Portswigger/blob/main/Server-side%20vulnerabilities/Server-side%20request%20forgery%20(SSRF)/SSRF%20attacks%20against%20the%20server%20-%20Continued.md)
- [Lab: Basic SSRF against the local server](https://github.com/vsang181/Portswigger/blob/main/Server-side%20vulnerabilities/Server-side%20request%20forgery%20(SSRF)/Lab%3A%20Basic%20SSRF%20against%20the%20local%20server.md)
- [SSRF attacks against other back-end systems](https://github.com/vsang181/Portswigger/blob/main/Server-side%20vulnerabilities/Server-side%20request%20forgery%20(SSRF)/SSRF%20attacks%20against%20other%20back-end%20systems.md)
- [Lab: Basic SSRF against another back-end system](https://github.com/vsang181/Portswigger/blob/main/Server-side%20vulnerabilities/Server-side%20request%20forgery%20(SSRF)/Lab%3A%20Basic%20SSRF%20against%20another%20back-end%20system.md)

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
  
