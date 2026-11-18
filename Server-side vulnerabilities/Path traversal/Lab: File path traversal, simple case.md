# Lab: File path traversal, simple case

> **Objective**: This lab contains a path traversal vulnerability in the display of product images. To solve the lab, retrieve the contents of the `/etc/passwd` file.

## Solution

1. **Observe the Application**: When accessing the lab, the main shopping page loads multiple product images.

<img width="1262" height="1349" alt="image" src="https://github.com/user-attachments/assets/47ef7790-f20c-44c4-99bb-98f8eb6ecc8f" />

2. **Intercept Traffic in Burp Suite**: Intercepting the webpage traffic reveals multiple `GET` requests fetching image files stored locally on the web server via a `filename` parameter.
   
<img width="1431" height="1135" alt="image" src="https://github.com/user-attachments/assets/80527e00-b350-4741-bc4f-bcd2e927225a" />

3. **Send Request to Repeater**: Sending one of the image `GET` requests to Burp Repeater allows us to modify and replay the request directly without reloading the entire page. This exposes the `filename` parameter for testing path traversal payloads.

<img width="1440" height="844" alt="image" src="https://github.com/user-attachments/assets/cc0a54de-4cd3-46bf-a5c5-51deb182fe39" />

4. **Exploit and Retrieve `/etc/passwd`**: Changing the `filename` parameter value to `../../../etc/passwd` steps out of the image directory to the root folder, returning the contents of the `passwd` file and solving the lab.

<img width="1440" height="1190" alt="image" src="https://github.com/user-attachments/assets/2028b1d4-c2e6-4d1f-a3c0-975809e0fda6" />
