# Lab: Remote code execution via web shell upload

> This lab contains a vulnerable image upload function. It doesn't perform any validation on the files users upload before storing them on the server's filesystem. To solve the lab, upload a basic PHP web shell and use it to exfiltrate the contents of the file `/home/carlos/secret`. Submit this secret using the button provided in the lab banner. You can log in to your own account using the following credentials: `wiener`:`peter`

## Solution

1. **Identify the Upload Functionality**: Log in using the provided credentials (`wiener`:`peter`). On the My Account page, we find an avatar upload feature that allows us to upload an image file for our profile:

<img width="1278" height="852" alt="image" src="https://github.com/user-attachments/assets/d66598bf-9d74-4ea0-986c-0b3da14e2ddf" />

2. **Create a PHP Web Shell**: Create a local file named `exploit.php` containing a PHP payload designed to read and output the target secret file (`/home/carlos/secret`):

`<?php echo file_get_contents('/home/carlos/secret'); ?>`

<img width="895" height="270" alt="image" src="https://github.com/user-attachments/assets/9c327a73-a239-490b-9935-1a3cc55d35c3" />

3. **Upload the Malicious File**: Select `exploit.php` using the avatar upload form and click Upload. Because the application performs no file validation, the server accepts and stores the PHP script without error:

<img width="938" height="207" alt="image" src="https://github.com/user-attachments/assets/92dfc93e-fdb7-4cde-bfd6-17bf8d642e92" />

4. **Locate and Trigger the Web Shell**: Return to the My Account page. Although the browser cannot render `exploit.php` as an image, inspecting the page source (or checking Burp HTTP history) reveals the exact directory path where the uploaded avatar is stored: `/files/avatars/exploit.php`.

Send a `GET` request to `/files/avatars/exploit.php` (via the browser or Burp Repeater) to trigger server-side execution of the script:

<img width="1056" height="669" alt="image" src="https://github.com/user-attachments/assets/69d2f69a-23c5-46cd-9154-ed4f981b3057" />

5. **Exfiltrate the Secret and Solve the Lab**: The server executes our PHP payload and returns the contents of `/home/carlos/secret` in the HTTP response body:

`JadSdcTQ3g4IZh5k7QYWKibkTbqW1TMf`

<img width="798" height="157" alt="image" src="https://github.com/user-attachments/assets/36f020b0-3d63-450f-a943-1d76518b14ee" />

