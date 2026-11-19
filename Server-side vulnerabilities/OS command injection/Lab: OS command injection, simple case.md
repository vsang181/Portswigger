# Lab: OS command injection, simple case

> This lab contains an OS command injection vulnerability in the product stock checker. The application executes a shell command containing user-supplied product and store IDs, and returns the raw output from the command in its response. To solve the lab, execute the whoami command to determine the name of the current user.

## Solution

1. **Identify the Vulnerable Request**: Use the product stock checker on any product page and intercept the `POST /product/stock` request in Burp Suite (or send it to Burp Repeater). Inspecting the request body reveals two user-controllable parameters, `productId` and `storeId`:

<img width="1056" height="643" alt="image" src="https://github.com/user-attachments/assets/91e0648e-f183-43cb-aa85-ea9829661615" />


2. **Inject the whoami Command**: Because `storeId` is the final argument passed to the back-end shell command, we can append a shell command separator (such as the pipe operator `|` or semicolon `;`) followed by `whoami`.

In Burp Suite, modify the storeId parameter value from `1` to `1|whoami`:

```
productId=1&storeId=1|whoami
```

Send the request. The server executes the original stock command, pipes its output into `whoami`, and returns the current system username directly in the HTTP response body solving the lab:

<img width="1156" height="360" alt="image" src="https://github.com/user-attachments/assets/1272e217-d1f2-40c6-bb0a-8e3b080ec03c" />
