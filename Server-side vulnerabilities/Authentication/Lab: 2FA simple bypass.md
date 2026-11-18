# Lab: 2FA simple bypass

> This lab's two-factor authentication can be bypassed. You have already obtained a valid username and password, but do not have access to the user's 2FA verification code. To solve the lab, access Carlos's account page.
> **Your credentials**: `wiener`:`peter`
> **Victim's credentials**: `carlos`:`montoya`

## Solution

1. **Log In as `wiener` to Map the Account URL**: Log in using your own credentials (`wiener`:`peter`) and retrieve your 2FA code from the provided email client. Once logged in, observe the URL structure for a normal authenticated account page (`/my-account?id=wiener`).

<img width="1281" height="634" alt="image" src="https://github.com/user-attachments/assets/e862b23a-446f-4965-b971-71a50aab03d0" />

2. **Log In with `carlos`'s Credentials**: Log out of your account and submit `carlos`'s username and password (`carlos`:`montoya`) on the login page. Because you do not have access to `carlos`'s email client, you cannot retrieve his 2FA code when prompted on the `/login2` page.
   
<img width="1276" height="425" alt="image" src="https://github.com/user-attachments/assets/3eb7d225-b785-4a78-9f94-35f03f1d0523" />

3. **Bypass the 2FA Prompt via Force Browsing**: Because the server creates a fully authenticated session immediately after the password check succeeds, simply replace `/login2` in the browser's address bar with `/my-account?id=carlos`.
   
<img width="1279" height="414" alt="image" src="https://github.com/user-attachments/assets/370330c9-5816-466d-869d-0150c67143dc" />

4. **Access Carlos's Account to Solve the Lab**: Navigating directly to `/my-account?id=carlos` skips the 2FA check completely, loads Carlos's account page, and solves the lab.
   
<img width="1280" height="659" alt="image" src="https://github.com/user-attachments/assets/7e39583f-f635-4b35-b508-e05f93a933ba" />
