# Exploiting Implicit Trust in the `Content-Type` Header

One common way websites attempt to validate file uploads is by checking that the input-specific `Content-Type` header inside the `multipart/form-data` part matches an expected MIME type. For example, if an upload feature expects only images, the server might enforce a whitelist that only accepts values such as `image/jpeg` or `image/png`.

## Why This Defense Fails

A critical vulnerability arises when the server **implicitly trusts** this header without performing any deeper validation such as inspecting the actual binary contents (magic bytes) or verifying the file extension.

Because the `Content-Type` header is simply text sent by the client in the HTTP request, an attacker can easily intercept the upload request using **Burp Proxy** or **Burp Repeater** and manually modify the header to spoof an allowed MIME type.

## Example Attack Flow

1. **Upload a Web Shell**: The attacker attempts to upload `exploit.php`. By default, the browser sets the part's header to `Content-Type: application/x-php` (or `application/octet-stream`), causing the server to reject the upload.

2. **Intercept and Spoof the Header**: In Burp Repeater, the attacker changes only the part-level `Content-Type` header to `image/jpeg` while keeping the `.php` filename and malicious PHP code intact:

```
Content-Disposition: form-data; name="avatar"; filename="exploit.php"
Content-Type: image/jpeg

<?php echo file_get_contents('/home/carlos/secret'); ?>
```

3. **Bypass and Execute**: The server sees `Content-Type: image/jpeg`, assumes the file is a safe image, and saves `exploit.php` to the upload directory. The attacker can then request `/files/avatars/exploit.php` to execute the web shell.
