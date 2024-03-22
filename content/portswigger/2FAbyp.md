# 2FA Simple Bypass
- The objective of this lab is to bypass two-factor authentication when logging into a user's account.
- The lab gives access to a blog as shown below.

![image](https://github.com/LadyCaldlow/LadyCaldlow.github.io/assets/162819648/c9b95154-e26b-4dbd-9c06-f8bc361fd527)

- You have the credentials for the users **wiener** and **carlos**. Along with his credentials, you also have access to **wiener**'s email which means that you can check the verification code that is sent to him.
- Click on `My Account` and enter **wiener**'s credentials, `wiener:peter`. Open the email client so that you can see the verification code that has been requested.

![image](https://github.com/LadyCaldlow/LadyCaldlow.github.io/assets/162819648/1af78e32-8cec-496b-9b96-f33f9dbd34d7)

![image](https://github.com/LadyCaldlow/LadyCaldlow.github.io/assets/162819648/3c22f387-a2d9-474c-993e-a969d99d48a0)

 - Once you input **wiener**'s verification code, you are directed to his home page. Note the url. You will be using this information to bypass 2FA for **carlos**' account.  

![image](https://github.com/LadyCaldlow/LadyCaldlow.github.io/assets/162819648/98a2c9c1-1dc4-4be3-b71e-f86ee33765f5)

- Now, log out of this account and log in using **carlos**' credentials. You are prompted to input the verification code but you do not have access to **carlos**' account so are not privy to this information.

 ![image](https://github.com/LadyCaldlow/LadyCaldlow.github.io/assets/162819648/2250b0e7-0543-416c-878a-5f7c0f34254c)

- You need to adjust **carlos**' url to go directly to his home page by replacing `/login2` with `/my-account?id=carlos`. This redirects you to **carlos**' home page without having to input the verification code. In this way, you have bypassed 2FA.

![image](https://github.com/LadyCaldlow/LadyCaldlow.github.io/assets/162819648/0fc24060-e402-41e1-a7d5-65c7f0cccc03)




