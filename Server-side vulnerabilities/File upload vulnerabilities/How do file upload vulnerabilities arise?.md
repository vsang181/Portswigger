# How do file upload vulnerabilities arise?

Because the risks of unrestricted file uploads are well known, it is rare to find modern websites with zero validation. Instead, file upload vulnerabilities typically arise because developers implement flawed validation logic that makes false assumptions and can be bypassed.

## Common Root Causes

- **Flawed Blacklisting of File Extensions**: Developers often try to block dangerous extensions (like `.php` or `.exe`) using a blacklist. However, blacklists frequently fail because:
  - Developers forget obscure or alternative executable extensions (such as `.php5`, `.phtml`, or `.phar`).
  - Parsing discrepancies occur between the validation code and the web server (e.g., case sensitivity like `.PhP`, trailing characters, or double extensions like `exploit.php.jpg`).

- **Trusting Easily Manipulated File Properties**: Some applications verify the file type by checking metadata sent in the HTTP request such as the `Content-Type` header (e.g., `image/jpeg`) rather than inspecting the actual file contents. Attackers can easily intercept and spoof these headers using tools like Burp Proxy or Burp Repeater.

- **Inconsistent Validation Across Infrastructure**: Even when strong validation rules exist, they are sometimes applied inconsistently across different servers, hosts, or directories within the same application. For example, an upload endpoint on a secondary subdomain or mobile API might lack the strict filters enforced on the main web portal.

- **Misconfigured Web Server Execution Rules**: Servers may store uploaded files inside a web-accessible directory without disabling script execution for that folder. If the server is configured to execute scripts wherever they are found, any bypassed upload check immediately leads to **Remote Code Execution (RCE)**.
