# Lab: Basic SSRF against another back-end system

> This lab has a stock check feature which fetches data from an internal system. To solve the lab, use the stock check functionality to scan the internal `192.168.0.X` range for an admin interface on port `8080`, then use it to delete the user `carlos`.

## Solution

1. **Identify the Vulnerable Request**: When checking stock availability via the UI and intercepting the traffic in Burp Suite, we observe a `POST` request to `/product/stock` containing the `stockApi` parameter:

`stockApi=http%3A%2F%2F192.168.0.1%3A8080%2Fproduct%2Fstock%2Fcheck%3FproductId%3D1%26storeId%3D1`

Decoded, this points to an internal IP address on port `8080`:

`http://192.168.0.1:8080/product/stock/check?productId=1&storeId=1`

<img width="1057" height="700" alt="image" src="https://github.com/user-attachments/assets/86c90642-5225-4c1f-9683-730829657d17" />

2. **Scan the Internal Subnet with Burp Intruder**: Since we do not know which internal IP address hosts the administrative interface, we can use **Burp Intruder** to brute-force the final octet (0 to 255) of the 192.168.0.X subnet.
   
  - Send the intercepted `POST /product/stock` request to **Burp Intruder**.
  - Update the `stockApi` parameter to target the `/admin` path and mark the last octet (`x`) as the payload position:

  ```
  stockApi=http://192.168.0.§x§:8080/admin
  ```
  - Under the Payloads tab, select the Numbers payload type and configure it to iterate from `0` to `255` with a step of `1`.

<img width="1440" height="807" alt="image" src="https://github.com/user-attachments/assets/18b617cb-a46d-4463-96a2-7d2eaa28481e" />

3. **Identify the Active Internal Host**: Start the Intruder attack and sort the results by Status code. While unreachable or invalid hosts return an error (such as `500` or `400`), one request returns a `200 OK` status code, revealing the live internal admin server at `192.168.0.247`:

<img width="1436" height="1075" alt="image" src="https://github.com/user-attachments/assets/e457cada-a9e2-4635-8c22-b564f47e9da5" />

4. **Access the Admin Interface and Delete carlos**: Send the request to Burp Repeater and set `stockApi` to `http://192.168.0.247:8080/admin`. Rendering the response confirms we have unauthenticated access to the admin panel, which exposes the user deletion endpoint (`/admin/delete?username=carlos`):
   
Next, modify the `stockApi` parameter to trigger the deletion endpoint on the internal host:

`stockApi=http://192.168.0.247:8080/admin/delete?username=carlos`

<img width="1279" height="841" alt="image" src="https://github.com/user-attachments/assets/3742b4f2-1aa7-401c-b8a0-0c3792a52f6c" />

<img width="1052" height="558" alt="image" src="https://github.com/user-attachments/assets/8f986c69-325b-4cab-a1c3-a7101e379de9" />


5. **Verify Lab Completion**: Finally, send one more request to `http://192.168.0.247:8080/admin` to confirm that `carlos` has been removed from the user list and the lab is solved:

<img width="1279" height="685" alt="image" src="https://github.com/user-attachments/assets/ad8a9a97-c069-4c30-a4b7-cb6514da9096" />
