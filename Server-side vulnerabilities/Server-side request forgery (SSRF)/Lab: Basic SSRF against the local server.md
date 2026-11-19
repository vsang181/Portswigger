# Lab: Basic SSRF against the local server

> This lab has a stock check feature which fetches data from an internal system.
To solve the lab, change the stock check URL to access the admin interface at `http://localhost/admin` and delete the user `carlos`.

## Solution

1. **Identify the Vulnerable Request**: When checking stock availability via the UI, intercept the traffic in Burp Suite. We observe a `POST` request to `/product/stock` containing a `stockApi` parameter in its body. This parameter passes a URL-encoded back-end API endpoint for the server to fetch:

<img width="1280" height="1233" alt="image" src="https://github.com/user-attachments/assets/f7e5d62a-19b8-4670-a246-e9061e5228e2" />

<img width="1056" height="567" alt="image" src="https://github.com/user-attachments/assets/0d2bf6b2-b917-43e3-9bf3-26a619f05845" />

`stockApi=http%3A%2F%2Fstock.weliketoshop.net%3A8080%2Fproduct%2Fstock%2Fcheck%3FproductId%3D1%26storeId%3D1`

> _(Decoded: `http://stock.weliketoshop.net:8080/product/stock/check?productId=1&storeId=1`)_


2. **Access the Local Admin Interface**: Ammend the intercepted `POST` request in **Burp SUite**. To force the server to fetch its own local admin panel (`http://localhost/admin`), replace the `stockApi` value with the URL-encoded payload:

`stockApi=%68%74%74%70%3a%2f%2f%6c%6f%63%61%6c%68%6f%73%74%2f%61%64%6d%69%6e`

<img width="1262" height="601" alt="image" src="https://github.com/user-attachments/assets/dba08a13-6b43-4f8f-a2b0-56815f04d1e2" />

When the response renders, the admin interface appears directly inside the stock check response because the server implicitly trusts requests originating from `localhost`.

3. **Discover the Delete Endpoint**: If we try to click the Delete link for `carlos` directly in our browser, the application blocks the action because our external browser session is not authenticated as an administrator. However, inspecting the HTML response (or the attempted request URL) reveals the exact endpoint used to delete a user:

`/admin/delete?username=carlos`

<img width="1278" height="412" alt="image" src="https://github.com/user-attachments/assets/6455db2b-3b9a-4cb8-887b-374858a05ded" />


4. **Delete the User via SSRF**: Instead of requesting the admin page directly from our browser, we force the server to make the `GET` request to `/admin/delete?username=carlos` on our behalf through the vulnerable `POST /product/stock` endpoint.

In Burp Suite, ensure the outer request method is `POST` and update the `stockApi` parameter to the URL-encoded target (`http://localhost/admin/delete?username=carlos`):

`stockApi=%68%74%74%70%3a%2f%2f%6c%6f%63%61%6c%68%6f%73%74%2f%61%64%6d%69%6e%2f%64%65%6c%65%74%65%3f%75%73%65%72%6e%61%6d%65%3d%63%61%72%6c%6f%73`

<img width="1439" height="713" alt="image" src="https://github.com/user-attachments/assets/3ee15646-ae4e-4442-ba21-e140251464cc" />


5. **Verify Lab Completion**: Finally, send the `stockApi` request to `http://localhost/admin` one more time to confirm that `carlos` has been removed from the user list and the lab is solved:

<img width="1280" height="626" alt="image" src="https://github.com/user-attachments/assets/b9a43fe1-a03c-45bc-98dd-ab60d22def02" />


