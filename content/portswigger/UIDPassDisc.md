# User ID Controlled By Request Parameter With Password Disclosure
The objective of this lab is to retrieve the administrator's password and then use it to delete the user `carlos`
The lab gives access to a shopping site as shown below.

![image](https://github.com/LadyCaldlow/LadyCaldlow.github.io/assets/162819648/e0fc3019-8c28-4aaa-8e92-9cd07dc11071)

Wiener's account can be accessed with the credentials provided.

![image](https://github.com/LadyCaldlow/LadyCaldlow.github.io/assets/162819648/60ba82e0-d733-4f86-a133-593c4cab17c0)

From the above image, it is clear that wiener's password is masked. The password may, however, be found in its unmasked form in the source code. 

![image](https://github.com/LadyCaldlow/LadyCaldlow.github.io/assets/162819648/b6d8b2ca-815f-4ca6-a4d1-7dfa2b2b3a0f)

You can see the password's value as `peter`. You should be able to find the administrator's actual password in this manner. Now, change the `id` parameter in the url from `wiener` to `administrator` to access the admin account.

![image](https://github.com/LadyCaldlow/LadyCaldlow.github.io/assets/162819648/e825026a-b9a8-4a45-b08d-baff400e07a3)

Once in the administrator account, you can view the source code to find the administrator's password.

![image](https://github.com/LadyCaldlow/LadyCaldlow.github.io/assets/162819648/9d061818-e75a-43c6-98f7-9893705427ef)

You can see the value of the password is `tgcrwax3ag2rebpop1ck`. You can use this to log into the administrator's account. Loggin in to the account gives access to the admin panel from where carlos' account can be deleted.

![image](https://github.com/LadyCaldlow/LadyCaldlow.github.io/assets/162819648/1f40c854-8a43-4ff0-87f6-c8a1192094e2)

Once you delete the account,you get;

![image](https://github.com/LadyCaldlow/LadyCaldlow.github.io/assets/162819648/a2b62d12-6d8e-4119-9575-53c7f249c30d)
