# Bypassing two-factor authentication

Sometimes, two-factor authentication (2FA) is implemented so poorly that an attacker can skip the second verification step altogether.

## How the Flaw Happens

- **Multi-Step Login Flow**: The application asks the user to enter their username and password first, and then redirects them to a separate page to enter a 2FA verification code.

- **Premature Session Creation**: Behind the scenes, the server marks the user as "logged in" immediately after the password check succeeds—before the 2FA code is ever verified.

- **Missing Step-2 Verification**: When the user requests protected pages, the server checks whether they have an active session, but forgets to check whether they actually completed the 2FA step.

## How to Test and Exploit

1. **Complete Step 1**: Log in with a valid username and password until the site prompts you for the 2FA verification code.

2. **Force Browse to Protected Pages**: Instead of entering the 2FA code, manually type the URL of a logged-in page (such as `/my-account` or `/dashboard`) directly into your browser's address bar.

3. **Check Access**: If the protected page loads normally, the 2FA check has been completely bypassed.
