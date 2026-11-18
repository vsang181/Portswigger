# Lab: User ID controlled by request parameter, with unpredictable user IDs

> This lab has a horizontal privilege escalation vulnerability on the user account page, but identifies users with GUIDs. To solve the lab, find the GUID for `carlos` and submit his API key.

**Credentials**: `wiener`:`peter`

## Solution

1. **Log In and Note Your Own GUID**: Log in to the application using the provided credentials (`wiener`:`peter`). The My Account page displays your API key and reveals your user GUID in the URL (`id=ccba0be4-ce7e-48c1-af69-745d9414c1f9`).

<img width="1280" height="759" alt="image" src="https://github.com/user-attachments/assets/4d8542fd-7511-4f10-8edd-3460024bc93c" />

2. **Locate `carlos` on the Blog Homepage**: Because GUIDs cannot be guessed, search the public blog posts on the homepage to find an article authored by `carlos`. Notice that his username is a clickable hyperlink.

<img width="1280" height="1071" alt="image" src="https://github.com/user-attachments/assets/c650a922-d088-4f3a-83a5-de6e2b802fb4" />

3. **Extract `carlos`'s GUID from His Profile UR**L: Clicking on `carlos`'s username opens his public author page showing all of his published posts. Inspecting the page URL leaks his unique user GUID (`id=58529387-1285-41fa-8cd6-adcab4dc95e8`).

<img width="1279" height="1022" alt="image" src="https://github.com/user-attachments/assets/0fc3b921-0452-4aa5-b7de-8a2bd431314d" />

4. **Swap the GUID and Retrieve the API Key**: Return to your My Account page URL and replace your `id` parameter value with `carlos`'s GUID (`58529387-1285-41fa-8cd6-adcab4dc95e8`). Loading the modified URL exposes `carlos`'s account page and API key, which you can submit to solve the lab.

<img width="1278" height="684" alt="image" src="https://github.com/user-attachments/assets/f2bf734d-91b3-4795-9ab2-0e1167900add" />
