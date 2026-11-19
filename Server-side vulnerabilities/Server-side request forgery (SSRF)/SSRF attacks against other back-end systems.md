# SSRF attacks against other back-end systems

In addition to attacking the local server (`127.0.0.1`), an attacker can use SSRF to force the application server to interact with other internal back-end systems on the private network that are not directly reachable by external users.

## Why Internal Back-End Systems Are Vulnerable

- **Non-Routable Private IPs**: Internal servers typically use private IP address ranges (such as `192.168.x.x`, `10.x.x.x`, or `172.16.x.x` – `172.31.x.x`) that cannot be routed over the public internet.

- `Reliance on Network Perimeter Security`: Because these systems are hidden behind firewalls and network topology, organizations often assume external attackers cannot reach them. As a result, internal servers frequently have a weaker security posture (e.g., missing authentication, unpatched software, or default credentials).

- `Unauthenticated Sensitive Functionality`: Many internal management panels, microservices, or databases grant full administrative access to any client capable of connecting to them on the internal network.

## How the Attack Works

Suppose an internal administrative interface is hosted on another machine inside the private network at `http://192.168.0.68/admin`. An external attacker cannot browse to this IP directly, as it is blocked by the firewall.

However, the public-facing web server is connected to the same internal network. By exploiting the SSRF vulnerability in the stock check feature, the attacker can force the server to fetch the internal admin page on their behalf:

```
POST /product/stock HTTP/1.0
Content-Type: application/x-www-form-urlencoded
Content-Length: 118

stockApi=http://192.168.0.68/admin
```

The vulnerable application server sends the request across the internal network to `192.168.0.68`, retrieves the administrative interface without needing credentials, and returns the response to the attacker.
