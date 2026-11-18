# Reading Arbitrary Files via Path Traversal

Path traversal occurs when an application takes user-supplied input (such as a filename) and appends it directly to a base directory without proper validation.

## How Normal Behavior Works

- **HTML Request**: A shopping site loads product images using a `filename` parameter:

```
<img src="/loadImage?filename=218.png">
```

- **Back-End Processing**: The application appends the `filename` value to its base image directory (`/var/www/images/`) and reads the file from the disk:

```
/var/www/images/218.png
```

## How the Exploit Works (Linux / Unix)

- **The `../` Sequence**: In file paths, `../` (dot-dot-slash) is a valid sequence that moves up one directory level.

- **Malicious Request**: Because there are no defenses, an attacker can manipulate the URL to step out of the base directory and reach the root folder:

```
https://insecure-website.com/loadImage?filename=../../../etc/passwd
```

- **Resolved File Path**: The three `../` sequences step up from `/var/www/images/` to the root directory (`/`), causing the server to read /etc/passwd instead of an image:

```
/var/www/images/../../../etc/passwd  -->  /etc/passwd
```

- **Target File (`/etc/passwd`)**: On Unix-based systems, this standard file lists all registered users on the server, making it a common proof-of-concept target.

## Windows Targets

- **Valid Sequences**: Windows accepts both forward slashes (`../`) and backslashes (`..\`) for directory traversal.

- **Malicious Request Example**: An equivalent attack against a Windows server targets standard system files like `win.ini`:

```
https://insecure-website.com/loadImage?filename=..\..\..\windows\win.ini
```
