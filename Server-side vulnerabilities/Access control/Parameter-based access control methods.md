# Parameter-based access control methods

Some applications determine a user's access rights or role at login and store that information in a client-side location that the user can control. Because the server trusts these submitted values to make access decisions, attackers can tamper with them to escalate their privileges.

## Where Role Information Is Insecurely Stored

Applications commonly expose role flags or IDs in user-controllable locations such as:
 
- **Hidden form fields**: Input tags with `type="hidden"` inside HTML forms.

- **Cookies**: Session or preference cookies stored in the browser (e.g., `Admin=false`).

- **Query string parameters**: URL parameters appended to requests.

## Example Attack Payloads

When the back-end server relies directly on URL parameters or cookies without verifying the user's true session permissions, an attacker can simply change the value to gain administrative access:

- **Boolean flag manipulation**:

```
https://insecure-website.com/login/home.jsp?admin=true
```

- **Role ID manipulation**:

```
https://insecure-website.com/login/home.jsp?role=1
```

## Why It Is Vulnerable

**Client-Side Trust**: Anything stored in the browser, URL, or HTTP request body can be intercepted and modified using a proxy tool like **Burp Suite** or browser developer tools.
