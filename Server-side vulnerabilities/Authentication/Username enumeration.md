# Username enumeration

Username enumeration occurs when an attacker can observe subtle changes in a website's behaviour or responses to confirm whether a specific username exists in the system.

## Where Username Enumeration Commonly Happens

- **Login Pages**: Submitting a valid username paired with an incorrect password triggers a noticeably different response than submitting an invalid username (such as a different error message, HTTP status code, or response time).

- **Registration Forms**: Entering a username or email address that already exists displays an error stating that the username is already taken.

## Why It Matters for Attackers

- **Faster Brute-Forcing**: Instead of guessing both usernames and passwords at the same time, an attacker can quickly filter a large wordlist down to a verified shortlist of valid usernames.

- **Targeted Password Attacks**: Once valid usernames are confirmed, the attacker can focus all their brute-force attempts specifically on cracking the passwords for those accounts.
