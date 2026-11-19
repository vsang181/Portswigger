# What is SSRF?

Server-Side Request Forgery (SSRF) is a web security vulnerability that allows an attacker to force a server-side application to make HTTP requests to an unintended location.

## How It Works

Normally, a firewall or network segmentation blocks external attackers from directly reaching private internal infrastructure. However, a public-facing web application sits across that network boundary and is trusted to communicate with both external users and internal systems.

When an application accepts a user-supplied URL or hostname to fetch resources (such as webhooks, file imports, or API integrations) without proper validation, an attacker can manipulate that input. By exploiting SSRF, the attacker uses the vulnerable server as a proxy to bypass network restrictions and reach otherwise inaccessible targets.

## Common Attack Targets

- **Internal-Only Services**: The attacker forces the server to connect to private systems within the organization's infrastructure—such as internal admin panels, databases, `localhost` (`127.0.0.1`) services, or cloud metadata endpoints—that are normally hidden behind a firewall.

- **Arbitrary External Systems**: The attacker forces the server to send requests to external third-party systems or an attacker-controlled server. This can leak sensitive data (such as authorization credentials or API keys) or allow the attacker to pivot and launch attacks against third parties that appear to originate from the victim's server.

## Why It Matters

- **Bypassing Access Controls**: Attackers can access internal interfaces that lack authentication because they assume only trusted internal users can reach them.

- **Sensitive Data Exposure**: Attackers can read internal files, database records, or cloud instance credentials.

- **Remote Code Execution (RCE)**: In severe cases, interacting with vulnerable internal services can allow an attacker to execute arbitrary commands on back-end systems.

<img width="1381" height="804" alt="image" src="https://github.com/user-attachments/assets/77289fc4-f399-42c3-8d1f-27b947aaef15" />
