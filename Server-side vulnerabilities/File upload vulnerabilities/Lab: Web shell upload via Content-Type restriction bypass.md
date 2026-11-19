# Lab: Web shell upload via Content-Type restriction bypass

> This lab contains a vulnerable image upload function. It attempts to prevent users from uploading unexpected file types, but relies on checking user-controllable input to verify this. To solve the lab, upload a basic PHP web shell and use it to exfiltrate the contents of the file `/home/carlos/secret`. Submit this secret using the button provided in the lab banner. You can log in to your own account using the following credentials: `wiener`:`peter`

## Solution


1. **Identify the Upload Functionality**: Log in using the provided credentials (`wiener`:`peter`). On the My Account page, we find an avatar upload feature for our profile:

<img width="1284" height="853" alt="image" src="https://github.com/user-attachments/assets/54d71387-0792-40e8-a388-6a372ac41c30" />

2. **Attempt to Upload a PHP Web Shell**: Create a PHP web shell named `exploit.php` containing the following payload to read `/home/carlos/secret`:

`<?php echo file_get_contents('/home/carlos/secret'); ?>`

Attempt to upload `exploit.php` through the UI and intercept the `POST /my-account/avatar` request in Burp Suite (or send it to **Burp Repeater**). Notice that the server initially rejects the upload because the file's `Content-Type` header is set to `application/octet-stream` (or `application/x-php`) rather than an allowed image MIME type:

<img width="1061" height="881" alt="image" src="https://github.com/user-attachments/assets/40ec189d-baee-4140-b2bd-c94015863df5" />

3. **Bypass the Content-Type Restriction**: In Burp Repeater, locate the `Content-Type` header inside the `multipart/form-data` section for `filename="exploit.php"` and change it from `application/octet-stream` to `image/jpeg` (leaving the top-level request header `Content-Type: multipart/form-data; boundary=...` intact):

Send the modified request. Because the server only validates the client-supplied `Content-Type` header of the uploaded file part, the upload succeeds:

<img width="1058" height="852" alt="image" src="https://github.com/user-attachments/assets/1aca9f4f-65a6-4f37-ba5a-2991adf742d0" />

4. **Trigger the Web Shell and Solve the Lab**: Send a `GET` request to `/files/avatars/exploit.php` in Burp Repeater (or via your browser) to execute the uploaded PHP script. The server returns the contents of `/home/carlos/secret` in the response body:

<img width="1054" height="628" alt="image" src="https://github.com/user-attachments/assets/18a1d56b-4e47-4ed4-9dfd-545db277a5d7" />
