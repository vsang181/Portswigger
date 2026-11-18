# Horizontal to vertical privilege escalation

A horizontal privilege escalation vulnerability can often be chained into vertical privilege escalation when an attacker targets a higher-privileged account (such as an administrator) rather than another standard user.

## How the Escalation Chain Works

1. **Horizontal Access (Account Tampering)**: An attacker uses a parameter-tampering flaw (IDOR) to access another user's account page:

```
https://insecure-website.com/myaccount?id=456
```

2. **Targeting an Administrator**: Instead of targeting a regular user, the attacker swaps the `id` parameter to match an application administrator's ID.

3. **Vertical Escalation (Admin Takeover)**: Loading the administrator's account page gives the attacker elevated control, allowing them to:
   
  - View or extract the administrator's password or API key.
  - Reset the administrator's password to take over the account directly.
  - Access privileged administrative functionality exposed on that page.
