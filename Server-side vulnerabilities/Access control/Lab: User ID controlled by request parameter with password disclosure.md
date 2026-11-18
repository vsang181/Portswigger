# Lab: User ID controlled by request parameter with password disclosure

> This lab has a user account page that contains the current user's existing password prefilled in a masked input field. To solve the lab, retrieve the administrator's password and use it to delete the user `carlos`.

**Credentials**: `wiener`:`peter`

## Solution

1. **Log In and Inspect the Masked Password**: Log in to the application using the provided credentials (wiener:peter). On the **My Account** page, the current user's password is prefilled inside a masked HTML password field.

<img width="1278" height="778" alt="image" src="https://github.com/user-attachments/assets/5409a808-67d2-46b8-928e-16413f74ca8f" />

2. **Verify How to Reveal the Password**: Opening the browser's developer tools (Inspector) or viewing the page source shows that the plaintext password is stored directly inside the `<value>` tag's `value` attribute.

<img width="1278" height="1002" alt="image" src="https://github.com/user-attachments/assets/981f4865-f366-4a3b-b0d7-e45ba2c5be7c" />

3. **Tamper with the id Parameter to Target `administrator`**: Notice that the URL uses an `id` parameter set to wiener (`/my-account?id=wiener`). Changing this parameter to `administrator` loads the administrator's account page. Inspecting the masked input field on this page reveals the administrator's plaintext password (`887rlun50gc8uo740eyg`).

<img width="1283" height="1377" alt="image" src="https://github.com/user-attachments/assets/3c61747f-bb6d-413d-8a7c-ec9fed8d835f" />

4. **Log In as `administrator` and Delete `carlos`**: Log out of `wiener`'s account and log back in using the newly discovered administrator credentials (`administrator`:`887rlun50gc8uo740eyg`). Open the Admin panel and delete the user `carlos` to solve the lab.
   
<img width="1278" height="492" alt="image" src="https://github.com/user-attachments/assets/e40859c4-81f7-40f3-9232-d35002cdcfba" />

