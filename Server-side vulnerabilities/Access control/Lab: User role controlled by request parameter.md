# Lab: User role controlled by request parameter

> This lab has an admin panel at `/admin`, which identifies administrators using a forgeable cookie. Solve the lab by accessing the admin panel and deleting the user `carlos`.

**Credentials**: `wiener`:`peter`

## Solution

1. **Log In and Inspect Cookies**: Log in to the application using the provided credentials (`wiener`:`peter`). Opening the browser's developer tools (Storage / Application tab) reveals two cookies set for the session: `session` and `Admin` (currently set to `false`).

<img width="1280" height="949" alt="image" src="https://github.com/user-attachments/assets/6e453893-cf93-42f9-ac9d-e5e4a2ae817d" />

2. **Modify the Admin Cookie**: Double-click the `Admin` cookie value in the browser's inspector tools and change it from `false` to `true`. Refreshing or navigating to My Account reveals a newly unlocked Admin panel link in the top navigation bar between Home and My Account.

<img width="1278" height="675" alt="image" src="https://github.com/user-attachments/assets/c0e43970-52eb-4481-9e59-d0d297f34964" />

3. **Access the Admin Panel and Delete `carlos`**: Clicking the Admin panel link opens the administrative dashboard. Deleting the user `carlos` completes the objective and solves the lab.

<img width="1282" height="450" alt="image" src="https://github.com/user-attachments/assets/4f318dc9-c739-4183-aa3b-b0f2b7c990b4" />
