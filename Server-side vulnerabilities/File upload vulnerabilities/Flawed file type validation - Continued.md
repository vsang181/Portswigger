# Anatomy of a multipart/form-data Request

Consider a form containing fields for uploading an image, providing a description, and entering a username. Submitting this form produces an HTTP `POST` request structured like this:

```
POST /images HTTP/1.1
Host: normal-website.com
Content-Length: 12345
Content-Type: multipart/form-data; boundary=---------------------------012345678901234567890123456

---------------------------012345678901234567890123456
Content-Disposition: form-data; name="image"; filename="example.jpg"
Content-Type: image/jpeg

[...binary content of example.jpg...]

---------------------------012345678901234567890123456
Content-Disposition: form-data; name="description"

This is an interesting description of my image.

---------------------------012345678901234567890123456
Content-Disposition: form-data; name="username"

wiener
---------------------------012345678901234567890123456--
```

## Key Components of the Request Body

- **Boundary Delimiter (`boundary=...`)**: A unique string defined in the top-level Content-Type header that separates each form input into its own distinct block. The final boundary ends with two trailing hyphens (`--`) to signal the end of the request body.

- **`Content-Disposition` Header**: Included at the top of every part to identify the form field (`name="..."`). For file inputs, it also specifies the original name of the uploaded file (`filename="example.jpg"`).

- **Part-Level `Content-Type` Header**: Present on file parts to declare the **MIME** type (e.g., `image/jpeg` or `image/png`) of the submitted data. Simple text inputs like `description` and `username` omit this header and default to plain text.
