# What is OS command injection?

OS command injection (also known as **shell injection**) is a critical web security vulnerability that allows an attacker to execute arbitrary operating system (OS) commands on the server hosting an application.
When exploited, an attacker can typically compromise the entire application and all of its underlying data. Furthermore, attackers often leverage OS command injection to compromise other parts of the hosting infrastructure and exploit internal trust relationships to pivot across other systems within the organization's network.

## How It Works

OS command injection occurs when an application passes unsafe, user-supplied data (such as form fields, cookies, HTTP headers, or URL parameters) directly into a system shell command without proper sanitization or validation.

For example, if a server runs a shell command like:

```
perl stockreport.pl <user_input>
```

And the attacker supplies an input containing a command separator (such as `&`, `&&`, `|`, `||`, or `;`), the operating system executes the original command followed immediately by the attacker's injected command:

```
perl stockreport.pl 123 & whoami
```

Key Security Impacts

- **Full Application & Data Compromise**: Injected commands run with the exact same privileges as the web application process, allowing attackers to read source code, steal database credentials, or modify files.

- **Infrastructure Takeover**: If the web application runs with elevated privileges (such as `root` or `SYSTEM`), or if local privilege escalation vulnerabilities exist on the host, the attacker can gain complete control over the underlying server.

- **Lateral Movement & Pivoting**: Using the compromised server as a foothold, an attacker can scan internal networks, access restricted services, and exploit trust relationships to compromise other internal systems.
