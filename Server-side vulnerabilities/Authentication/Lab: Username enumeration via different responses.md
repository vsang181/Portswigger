# Lab: Username enumeration via different responses

This lab is vulnerable to username enumeration and password brute-force attacks. Using the provided wordlists, enumerate a valid username, brute-force that user's password, and access their account page.

**Wordlists**:

- [Candidate usernames](https://portswigger.net/web-security/authentication/auth-lab-usernames)
- [Candidate passwords](https://portswigger.net/web-security/authentication/auth-lab-passwords)

## Solution

1. **Intercept a Test Login Request**: Submit a dummy login attempt on the login page to capture the `POST /login` request in **Burp Suite**, then send it to Burp Intruder for testing.

<img width="1440" height="1124" alt="image" src="https://github.com/user-attachments/assets/bae6a51a-b690-4f3c-a530-e0aa96a0494e" />

2. **Enumerate Valid Usernames in Burp Intruder**: Configure a **Pitchfork** attack (or Sniper attack on the `username` parameter) using the Candidate usernames wordlist alongside dummy passwords.

<img width="527" height="1010" alt="image" src="https://github.com/user-attachments/assets/4d0a21df-10c9-49e3-ac69-c4d0f2fe0d8e" />

<img width="532" height="934" alt="image" src="https://github.com/user-attachments/assets/6a96162c-da90-4bc5-96e2-f0cf51212ebb" />

3. **Identify the Valid Username (`ec2-user`)**: Sort the Intruder results by Length. One request stands out with a different response length—inspecting the response reveals the error message `"Incorrect password"` instead of `"Invalid username"`, confirming that `ec2-user` is a valid account.

<img width="1436" height="1075" alt="image" src="https://github.com/user-attachments/assets/43b93bdc-8770-4488-99bf-b7c4ee323fe6" />

4. **Brute-Force the Password Using a Sniper Attack**: Set the `username` parameter to `ec2-user`, place a single payload marker on the `password` parameter, and run a Sniper attack using the Candidate passwords wordlist.

<img width="1440" height="1045" alt="image" src="https://github.com/user-attachments/assets/59d3bdbd-756a-4021-bfc7-94bcea7e261c" />

5. **Identify the Valid Password (`daniel`)**: Sort the Intruder results by **Status**. The valid password (`daniel`) triggers a `302 Found` redirect response instead of a `200 OK` with login error.

<img width="1437" height="1078" alt="image" src="https://github.com/user-attachments/assets/76d6c345-baab-4ff7-8c9f-ef49196bfd00" />

6. **Log In to Solve the Lab**: Log in to the application using the discovered credentials (`ec2-user`:`daniel`) to access the account page and complete the lab.

<img width="1279" height="718" alt="image" src="https://github.com/user-attachments/assets/6bdd1098-0b17-4a90-a8b1-fdefe0ec2f0c" />
