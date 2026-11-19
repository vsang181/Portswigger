# SSRF attacks against the server

In an SSRF attack against the server, the attacker forces the application to send an HTTP request back to the exact same server hosting the application. This is done via the server's loopback network interface, typically by supplying a URL with a hostname like `127.0.0.1` (a reserved IP address pointing to the loopback adapter) or `localhost` (a common hostname for the same adapter).

## How the Attack Works

Consider a shopping application that checks item availability by querying back-end REST APIs. The front-end passes the API URL directly to the server via an HTTP request:

```
POST /product/stock HTTP/1.0
Content-Type: application/x-www-form-urlencoded
Content-Length: 118

stockApi=http://stock.weliketoshop.net:8080/product/stock/check%3FproductId%3D6%26storeId%3D1
```

The server fetches the data from the `stockApi` URL and returns the stock status to the user.

## Exploiting the Request

An attacker can intercept this request and modify the `stockApi` parameter to point to a local administrative endpoint on the server itself:

```
POST /product/stock HTTP/1.0
Content-Type: application/x-www-form-urlencoded
Content-Length: 118

stockApi=http://localhost/admin
```

Instead of checking stock, the server fetches the contents of its own /admin page and returns it in the HTTP response to the attacker.

## Why Applications Trust Localhost Requests

Normally, if an attacker visits `/admin` directly from their browser, the application blocks them or shows nothing of interest because they are not authenticated. However, when the request comes from `localhost`, the application often bypasses normal access controls for two main reasons:

- **Implicit Network Trust**: Access control checks may be handled by a front-end component (like a reverse proxy or load balancer). When a request originates from the local machine (`127.0.0.1`), it bypasses that front-end security layer completely.

- **Disaster Recovery / Convenience**: Developers sometimes configure applications to allow unauthenticated administrative access from the local machine so administrators can recover accounts or manage the system directly from the server without needing credentials.

## Common Loopback Targets to Test

When testing for SSRF against the local server, try pointing the vulnerable parameter to:

- `http://localhost/admin` or `http://127.0.0.1/admin`

- Different local ports running internal services (e.g., `http://127.0.0.1:8080`, `http://127.0.0.1:8000`, or `http://localhost:3000`)

- Server status or monitoring pages (e.g., `http://127.0.0.1/server-status`)
  
