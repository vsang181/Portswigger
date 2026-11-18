# Lab: Unprotected admin functionality with unpredictable URL

> This lab has an unprotected admin panel located at an unpredictable path that is disclosed somewhere in the application. Solve the lab by accessing the admin panel and deleting the user `carlos`.

## Solution

1. **Inspect the Page Source Code**: Viewing the HTML source code of the main page reveals an inline JavaScript block that conditionally renders the admin link based on the `isAdmin` variable:

```
var isAdmin = false;
if (isAdmin) {
   var topLinksTag = document.getElementsByClassName("top-links")[0];
   var adminPanelTag = document.createElement('a');
   adminPanelTag.setAttribute('href', '/admin-ipsd5w');
   adminPanelTag.innerText = 'Admin panel';
   topLinksTag.append(adminPanelTag);
   var pTag = document.createElement('p');
   pTag.innerText = '|';
   topLinksTag.appendChild(pTag);
}
```

<img width="1278" height="1401" alt="image" src="https://github.com/user-attachments/assets/009097c4-9e73-4219-af36-3a30b6c87fc6" />

2. **Extract the Obfuscated Admin URL**: Even though `isAdmin` is set to `false`, the script exposes the exact path to the administrative panel: `/admin-ipsd5w`.

3. **Access the Admin Panel and Delete `carlos`**: Navigating directly to `/admin-ipsd5w` opens the unprotected admin interface. Deleting the user `carlos` completes the objective and solves the lab.

<img width="1278" height="435" alt="image" src="https://github.com/user-attachments/assets/bde28720-37ca-423a-bdb8-51e055c720d2" />
