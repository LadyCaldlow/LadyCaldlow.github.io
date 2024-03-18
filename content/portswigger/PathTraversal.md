# Server-Side Vulnerabilities-Path Traversal Lab
The objective of this lab is to perform a path traversal such that you are able to retrieve the contents of the `/etc/passwd` file.
Before attempting the lab, you should have a good understanding of what path traversal is.
A path traversal vulnerability is one whereby an attcker can access arbitrary files on a webserver that they should not have access to. This can be achieved by effectively using two dots (..) and a forward slash (/) in Linux-based servers. You can use the same in Windows-based servers, you can use the same or a backward slash (\) in place of the forward slash. 
In Linux, the two dots (..) moves one a step up to the previous directory. You can try this on your terminal as shown below.

![image](https://github.com/LadyCaldlow/LadyCaldlow.github.io/assets/162819648/f82eb026-c20c-47c5-bf04-f746f6790413)

The forward slash (/), on the other hand, indicates a directory. 
In the Path Traversal Lab, we have access to a shopping site as shown below.

![image](https://github.com/LadyCaldlow/LadyCaldlow.github.io/assets/162819648/9cf818c2-199c-406c-bb32-6feb5a216ea4)

The url to the site is;

![image](https://github.com/LadyCaldlow/LadyCaldlow.github.io/assets/162819648/a54fc8f4-adcf-4b17-b398-0a7d60ff19ab)

When you click on any of the images, you see that the url changes to; 

![image](https://github.com/LadyCaldlow/LadyCaldlow.github.io/assets/162819648/eb95afcd-7221-440b-b17f-31227bae3b77)

where the Id number will change depending on the image that is being referenced. You can get more specific information on the location of the image by Inspecting the image. You can do this by right-clicking on the image and then clicking `Inspect`

![image](https://github.com/LadyCaldlow/LadyCaldlow.github.io/assets/162819648/c99df363-8e51-4cc0-80fa-48c86dcf2872)

The highlighted section shows that the particular filename of the image is `54.jpg`. You do not know in what exact directory this file is located but you can make several attempts to get to the filesystem root and then access `etc/passwd`.
Close this Inspection window and then right-click on the image and open it in a new tab. Note the url of the image.

![image](https://github.com/LadyCaldlow/LadyCaldlow.github.io/assets/162819648/fd768190-86c0-4340-b697-1fc9f06b2044)

Now move up one directory and see if this gives you access to `/etc/passwd`

![image](https://github.com/LadyCaldlow/LadyCaldlow.github.io/assets/162819648/1428cbb1-aa4e-4875-82e4-ed31fa207488)

You get the response that this file does not exist. This means that in whatever directory you are in right now, there is no `passwd` file. Knowing that the `passwd` file is in the `etc` directory, this means that the `etc` directory is not here as well. 
You get the same response if you traverse up another directory again meaning that `/etc/passwd` is not here as well. When you traverse up another directory, however, you get the response;

![image](https://github.com/LadyCaldlow/LadyCaldlow.github.io/assets/162819648/d60be4b5-1957-4b06-83b5-7744a606fb69)

The response shows that `/etc/passwd` file exists but you cannot read it because it is a text file as opposed to an image file. This means that you have indeed been able to traverse to `/etc/passwd`. 

![image](https://github.com/LadyCaldlow/LadyCaldlow.github.io/assets/162819648/1dcb1bb9-625f-4648-9091-bdd395dded25)
