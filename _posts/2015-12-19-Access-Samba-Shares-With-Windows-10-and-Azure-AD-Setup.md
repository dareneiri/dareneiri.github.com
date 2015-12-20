---
published: true
layout: post
tags: 
  - microsoft
  - windows 10
  - AzureAD
  - Samba
excerpt: "If you set up your Windows 10 device with a Microsoft Account, and not a local one, you may not have access to your Samba Shares. I tell you how to get that access back"
comments: true
---


**Symptoms:** 

1. You have Samba shares in your local network that you used to have access to, or have other devices on that network that can access those shares. 
2. You're using Windows 10 with an Azure AD corporate or Windows Account

**Resolution:**
This took me a few months to resolve, primarily because I just don't have time to troubleshoot my own personal network/PC issues. But it sure is a wonderful feeling when you find the solution needed after so long! Credit goes to the Synology forum user mtjerneld, who responeded with a [working solution](http://forum.synology.com/enu/viewtopic.php?f=49&t=98792#p385856). 


1. On your Windows 10 device, go to Start > and search for Credential Manager. 
2. Select Windows Credentials
3. Click on "Add a Windows credential"
   <figure>
    <img src="{{ site.url }}/images/credential-manager.png" alt="credential manager">
    </figure>
4. A new window will pop up. 
5. In the field for "Internet or Network address", type your samba share path (e.g., \\samba-share)
6. In the field for "User name", enter samba-share\{your_username}
7. For password, type in your password


Now, in my case, in Network from the Windows Explorer window, I was not able to see my samba shares. However, if I type in \\samba-share (in this example), I am able to see my files as expected. You can also use the Run command (Windows - R) and type in the samba share path to view your share.
