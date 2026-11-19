# What are file upload vulnerabilities?

File upload vulnerabilities occur when a web server allows users to upload files to its filesystem without properly validating attributes such as their name, type, contents, or size.

When these restrictions are missing or poorly enforced, even a simple feature like an avatar or image uploader can be abused to upload arbitrary, dangerous files—including server-side scripts (such as `.php`, `.jsp`, or `.asp`) that allow an attacker to achieve Remote Code Execution (RCE).

## What Developers Fail to Validate

To secure a file upload feature, a server must properly check four core properties:

- **File Name**: Failing to sanitize file names can allow path traversal sequences (e.g., `../../shell.php`) to overwrite critical system files or place scripts inside executable directories.

- **File Type**: Relying solely on easily spoofed metadata (such as the `Content-Type` header or file extension) can let attackers disguise malicious scripts as harmless images.

- **File Contents**: Not inspecting the actual binary signature (magic bytes) or structure of the file allows attackers to embed malicious code inside seemingly valid files.

- **File Size**: Failing to enforce strict size limits can allow attackers to exhaust server disk space or memory, causing a **Denial of Service** (**DoS**).

## How File Upload Attacks Are Triggered

Depending on how the server handles and stores uploaded files, exploitation typically happens in one of two ways:

- **Immediate Impact Upon Upload**: In some cases, the act of uploading the file itself causes damage for example, overwriting an existing configuration file, exhausting disk space, or triggering an unsafe parser during upload processing.

- **Two-Step Execution (Upload + Request)**: More commonly, the attacker uploads a malicious server-side script (a **web shell**) and then sends a follow-up HTTP GET request to the uploaded file's URL. When the web server processes that request, it executes the malicious script on the back-end server.
  
