# Unprotected Admin Functionality Lab
The objective of this lab is to find the unprotected admin panel and delete the user `carlos`. Let's get started.
The lab gives you access to a shopping site as seen below. 

![image](https://github.com/LadyCaldlow/LadyCaldlow.github.io/assets/162819648/201fec8c-646f-432c-a052-0dbd0945ba9b)

I clicked on `My account` and it took me to a log in page as shown below. 

![image](https://github.com/LadyCaldlow/LadyCaldlow.github.io/assets/162819648/ca3d3b37-4011-4db9-9ba9-d21713800b11)

Here, I tried a number of default admin credentials (e.g admin:admin, admin:password,administrator:administrator,administrator:password1) but none of them worked. If the administrator's account was using default credentials, you would get a through pass to the admin panel. Unfortunately, that technique bore no success here.

You can run a gobuster scan to find directories in the site. Gobuster is a bruteforce scanner used to find URIs (files and directories) in websites, among other uses. I ran gobuster as shown.

![image](https://github.com/LadyCaldlow/LadyCaldlow.github.io/assets/162819648/e30f6b96-e309-4d00-a3a2-54f9b821e5e1)

`dir` indicates that you're trying to find directories in the site

`-u` represents the url of the website which is being subjected to the bruteforce

`-w` indicates the wordlist that will be used which has potential directory names 

While I forgot to add it, you should add `--no-error` flag so that error messages are not displayed. Otherwise, the response can get messy when there are many error messages. 
The results are as shown below.

![image](https://github.com/LadyCaldlow/LadyCaldlow.github.io/assets/162819648/2a91b254-296b-4bd3-b54f-db129511ee34)

Here, you see a number of directories in the site that we can acccess but the ones of interest in accessing the admin panel are `/robots.txt` and `administrator-panel`
The easy and direct option here is the latter but let's take a look at what's in `robots.txt`

![image](https://github.com/LadyCaldlow/LadyCaldlow.github.io/assets/162819648/274658c5-4b46-4565-ab14-8cce4ee35532)

This indicates to web crawlers that they should not access and display `/administrator-panel` on search results. This also means that this is a page with sensitive information. So let's head on there and see what can be found.

![image](https://github.com/LadyCaldlow/LadyCaldlow.github.io/assets/162819648/142b14e9-ad7b-4a4f-a159-48b3d9304123)

Would you look at that? You have found the unprotected admin panel. Now all you need to do is to click on `Delete` next to carlos' name and voila!

![image](https://github.com/LadyCaldlow/LadyCaldlow.github.io/assets/162819648/6469e383-a3af-4570-8281-31421bdacbe6)
