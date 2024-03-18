# Unprotected Admin Functionality with Unpredictable URL Lab
The objective of this lab is to find an unprotected admin panel located in an unpredictable location and then delete the user `carlos`.
The lab gives access to a shopping site as shown below.

![image](https://github.com/LadyCaldlow/LadyCaldlow.github.io/assets/162819648/a7799263-521d-47d9-9490-b5e15bdffe71)

Take a look at the source code to see if you might find any useful information. You can do this by right-clicking on the site and then clicking on `View Page Source`
![image](https://github.com/LadyCaldlow/LadyCaldlow.github.io/assets/162819648/e78dfc00-0e7d-42d7-ad8a-4e32bcd61dbf)
![image](https://github.com/LadyCaldlow/LadyCaldlow.github.io/assets/162819648/fad345f8-493b-45e1-9057-ce6037213a4d)

You are presented with multiple lines of code but lines 73-83 hold information that is relevant to this lab. In those lines is a JavaScript script that defines logic for the admin panel. In line 77, in particular, you see the admin directory indicated towards the end of the line as `/admin-p2yvns`

![image](https://github.com/LadyCaldlow/LadyCaldlow.github.io/assets/162819648/6c8636ca-de1e-4c65-b86d-c7e383ea4524)

Let's go ahead and access this directory. You'll find that it takes you to the administrator panel. 

![image](https://github.com/LadyCaldlow/LadyCaldlow.github.io/assets/162819648/caa7d70f-343f-4649-bd10-e51c86f83ca1)

Once there, you can delete the user `carlos`

![image](https://github.com/LadyCaldlow/LadyCaldlow.github.io/assets/162819648/d1fc1979-7a15-4182-b38b-c60b32d716d3)
