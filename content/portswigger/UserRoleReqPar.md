# User Role Controlled By Request Parameter Lab
The objective of this lab is to access the admin panel by way of a forgeable cookie and then deleting the user `carlos`. Credentials to log into the account of a non-admin user have been provided. Let's get started!
The lab gives access to a shopping site as shown below.

![image](https://github.com/LadyCaldlow/LadyCaldlow.github.io/assets/162819648/1e79075e-78ad-4741-bdd4-3f72aa4d5764)


The instructions indicate that the admin panel is at `/admin`. Let's try to access it. You get the following message. 

![image](https://github.com/LadyCaldlow/LadyCaldlow.github.io/assets/162819648/5526dd06-73cc-4e94-b778-92707eaea898)

Since you have no access to the admin panel in this, let's try to log in to the account of the non-admin user with the credentials given (wiener:peter). Enter these credentials after clicking on `My Account`. You get the following interface.

![image](https://github.com/LadyCaldlow/LadyCaldlow.github.io/assets/162819648/6a75e30e-d4b4-48db-9fa9-b1892061bc97)

I am using an extension known as _Cookie-Editor_ on my browser which, as the name suggests, let's me edit cookies. You can do the same using Burp Suite but I will use this extension due to easy access. By clicking on the extension while logged in as wiener, I see that there is a cookie for Admin which has been set to false.

![CK](https://github.com/LadyCaldlow/LadyCaldlow.github.io/assets/162819648/b49aaebf-49d0-43c3-9d22-61070f327aed)

You need to change the value to true. Doing so and then reloading the page adds a new option (Admin panel) on the top-right corner of the site. 

![image](https://github.com/LadyCaldlow/LadyCaldlow.github.io/assets/162819648/caf2a631-705a-49e5-b3f6-610acb8dcdb8)

Clicking on this option takes you to the admin panel where you can delete the user `carlos`

![image](https://github.com/LadyCaldlow/LadyCaldlow.github.io/assets/162819648/3a7fe0f1-3baf-4fdb-88cb-0ad4cf4539b3)

Following the deletion;

![image](https://github.com/LadyCaldlow/LadyCaldlow.github.io/assets/162819648/73735f1d-a5a4-4020-a628-e82680cb439f)
