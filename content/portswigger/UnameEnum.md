# Username Enumeration Via Different Responses
- The objective of this lab is to use username enumeration to find a valid username and then perform a passowrd brute-force attack to gain access to this username's account.
- The lab gives access to a blog as shown below.

![image](https://github.com/LadyCaldlow/LadyCaldlow.github.io/assets/162819648/35b35549-95e7-45bd-8306-996d633ea83e)

- First things first, you need to find a valid username. A list of usernames and passwords, one of which is valid for the site, has been provided. Copy the usernames as you are about to use them. Head on over to `My Account` and input a random username and a random password. While doing this, ensure that Burpsuite is open and Proxy Intercept is on. Also, turn on the Burp proxy on Foxy Proxy. Now, login with these random credentials and capture the request on Intercept.

![image](https://github.com/LadyCaldlow/LadyCaldlow.github.io/assets/162819648/7f82ae52-912c-4071-8dfd-a6ef206a364b)

- Once the request is on Intercept, right-click on the screen and send the request to Intruder. You will be performing username enumeration using Intruder. On Intruder, highlight the username and then click `Add §`.

![image](https://github.com/LadyCaldlow/LadyCaldlow.github.io/assets/162819648/b104e1ba-06ba-43c5-a426-536341b87098)

- Next, move to the Payload option on Intruder and paste the usernames you had already copied from the list provided. After doing this, click on `Start attack`

![image](https://github.com/LadyCaldlow/LadyCaldlow.github.io/assets/162819648/b0b3f1e2-16ee-44c6-b9a5-17d49367c4b1)

- All of the results have the same time length except one (root). You can try and log in to the site using this username and a random password to see if you will get a different response than before. 

![image](https://github.com/LadyCaldlow/LadyCaldlow.github.io/assets/162819648/7add198a-f490-4527-a6ac-4a423761ee08)

- When you use this username, you get the response below rather than `Invalid Username` which means this username is valid

![image](https://github.com/LadyCaldlow/LadyCaldlow.github.io/assets/162819648/ca6b4c6c-c429-45c9-89f8-d34037d4d6b9)

- Now, with this username, you can brute-force the passwords to find a valid password. Try to log in with this username and a random password, capture the request and send it to Intruder, highlight the password and use the list of passwords as a payload this time. One of the results will have a different time length and this will be the password for the user.

![image](https://github.com/LadyCaldlow/LadyCaldlow.github.io/assets/162819648/740e608c-7775-4ec3-89c9-e56e502e178a)

- You can now log in using the credentials you have obtained.

![image](https://github.com/LadyCaldlow/LadyCaldlow.github.io/assets/162819648/a3e706c5-4432-47ce-90f2-ecfb1e3a4d29)

Note that the valid username and password for the lab change with every instance. As such, do not copy the credentials used here as they may not work for you. 
