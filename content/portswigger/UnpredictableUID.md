# User ID Controlled By Request Parameter, with Unpredictable User IDs Lab
The objective of this lab is to perform horizontal privilege escalation using GUIDs (Global Unique Identifiers) to access carlos' account and find his API key.
The lab gives access to a blog site as shown below.

![image](https://github.com/LadyCaldlow/LadyCaldlow.github.io/assets/162819648/2d1937cc-df5d-4d1f-b432-47018cb1eec7)

You can try to log into wiener's account since his credentials have been provided. 

![image](https://github.com/LadyCaldlow/LadyCaldlow.github.io/assets/162819648/8609087d-e757-48bb-a1bd-32a7f872eaa2)

You can see his GUID indicated in the id part of the url and his API key is provided once you access his account. Now, let's try and find carlos' GUID. 
On the home page, there are a number of articles; some written by administrator, others by wiener and others by carlos. You can click on an article by wiener and view the source code.

![image](https://github.com/LadyCaldlow/LadyCaldlow.github.io/assets/162819648/09199ef1-e5fd-490a-bffc-c134cd18bb91)

You find the above id on the source code and this matches the GUID that was displayed when wiener's account was accessed. This means carlos' GUID can be found in the same way. Click on any article written by carlos and view the source code.

![image](https://github.com/LadyCaldlow/LadyCaldlow.github.io/assets/162819648/af26ba81-ae4b-4f8d-868d-78060a224eaa)

Carlos' GUID is referenced and this can be used to access his account. Now, log into wiener's account again and replace his GUID with carlos' and then refresh the page.

![image](https://github.com/LadyCaldlow/LadyCaldlow.github.io/assets/162819648/e966640a-5f7b-4936-879d-ec19b1ae6dd6)

You get access to his account and find his API key which you can submit to complete the lab.

![image](https://github.com/LadyCaldlow/LadyCaldlow.github.io/assets/162819648/dfe3c34a-e423-4b76-9b99-fdce321d4454)

