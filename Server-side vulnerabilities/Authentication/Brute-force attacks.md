# Brute-force attacks

A brute-force attack occurs when an attacker uses systematic trial and error to guess valid user credentials.

## How Brute-Force Attacks Work

- **Automation and Speed**: Attackers rarely guess manually. Instead, they use automated tools (such as Burp Intruder or Hydra) paired with pre-compiled **wordlists** of common usernames and passwords to send thousands of login attempts per minute.

- **Educated Guessing**: Brute-forcing is not always random. Attackers often refine their wordlists using basic logic or publicly available information (such as leaked credentials, company names, or social media details) to make targeted, high-probability guesses.

## Why Applications Are Vulnerable

- **Single-Factor Reliance**: Websites that depend solely on a username and password without multi-factor authentication (MFA) are at high risk.

- **Missing Defenses**: Without proper protections such as account lockouts, rate limiting, or CAPTCHAs an attacker can keep guessing indefinitely until they find a valid login.
