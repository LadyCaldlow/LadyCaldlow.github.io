# Basic SSRF Against the Local Server
- The objective of this lab is to perform server-side request forgery (SSRF) by altering the URL so that the HTTP request is made back to the server via its loopback network interface. You then need to delete the user `carlos`.
- The lab gives access to a shopping site as shown below.

![image](https://github.com/LadyCaldlow/LadyCaldlow.github.io/assets/162819648/996930ac-1965-426e-b418-02cde7d3e7ef)

- The instructions for this lab is to alter the stock check URL to access the admin interface at `http://localhost/admin`. Click on any of the items, change the location and then click on `Check stock` and capture this request on BurpSuite Proxy. 

![image](https://github.com/LadyCaldlow/LadyCaldlow.github.io/assets/162819648/34f44b73-da03-4711-82c9-3e95ab277670)

![image](https://github.com/LadyCaldlow/LadyCaldlow.github.io/assets/162819648/e11cf854-c76d-4bba-af6f-35386cb1afbb)

- Now, edit the `stockApi` to `http://localhost/admin`. Once you forwrad this request, you'll see that the Admin panel now appears at the bottom of the page.

![image](https://github.com/LadyCaldlow/LadyCaldlow.github.io/assets/162819648/5f66e4fb-53c4-42b7-bd53-6caeac72031c)

![image](https://github.com/LadyCaldlow/LadyCaldlow.github.io/assets/162819648/f5198145-06bd-431e-8de0-9b354e7e80b8)

- However, deleting the user `carlos` is not possible from here as you get the message below;

![image](https://github.com/LadyCaldlow/LadyCaldlow.github.io/assets/162819648/e94d940e-9681-453c-acea-be2b9f10ff74)

- Take note of the GET request on Proxy when you try to delete the user `carlos`. This request will be edited so that it is made directly to the admin panel from localhost. Now, go back to home, click on an item, check the stock and capture this request.

![image](https://github.com/LadyCaldlow/LadyCaldlow.github.io/assets/162819648/8d9c64cc-c33e-48df-ba4b-1dc96e58a37c)

- Once you forward this request, user `carlos` is deleted and you get the message;

![image](https://github.com/LadyCaldlow/LadyCaldlow.github.io/assets/162819648/013d71f9-097d-4b65-b4a7-325bdb607c33)


