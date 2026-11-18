# Unprotected Functionality (Security by Obscurity)

Sometimes, developers try to protect sensitive functionality by giving it an unpredictable, hard-to-guess URL rather than enforcing proper server-side access controls. This flawed approach is known as security **by obscurity**.

## Why Obfuscated URLs Are Not Secure

- **No Real Protection**: Hiding a URL does not prevent unauthorized users from accessing it once they find out what the URL is.

- **Unpredictable Path Example**: An application might host its admin panel at an obfuscated path like:

```
https://insecure-website.com/administrator-panel-yb556
```

## How Hidden URLs Leak

Even if an attacker cannot guess or brute-force the URL, the application often exposes it directly in client-side code:

- **Client-Side JavaScript Exposure**: Applications frequently load JavaScript that dynamically builds the user interface based on the user's role. Because this script is sent to every visitor's browser, anyone can inspect the page source and read the hidden admin URL:

```
<script>
    var isAdmin = false;
    if (isAdmin) {
        ...
        var adminPanelTag = document.createElement('a');
        adminPanelTag.setAttribute('href', 'https://insecure-website.com/administrator-panel-yb556');
        adminPanelTag.innerText = 'Admin panel';
        ...
    }
</script>
```

Even though `isAdmin` is `false` and the link is never rendered on screen, the hardcoded URL remains completely visible in the HTML/JavaScript source code.
