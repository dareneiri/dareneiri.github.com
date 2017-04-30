---
published: true
layout: post
tags:
  - htpc
  - linux
  - windows
  - chromebox
excerpt: Walkthrough on installing Windows 10 over Ubuntu on a Chromebox
comments: true
---
## A Short Walkthrough to Installing Windows 10 on an Asus Chromebox


In [a previous post originally from 2015](http://dareneiri.github.io/Asus-Chromebox-With-Full-Linux-Install/), I provided a walkthough on how to set up an Asus Chromebox out of the box with Ubuntu. Now, I provide information on how I setup the same Chromebox with Windows 10, especially since I hit a few snags along the way. I hope this information helps just as many people my previous post seemed to help. 

My overall impressions with the Chromebox running Windows 10 are quite positive compared with my experience with Ubutnu. I am comfortable with both systems, but I was running into complications getting Plex to work consistently with Ubuntu, as well as Kodi itself. Both Plex and Kodi seem to run much better on Windows 10. 

Please note the following: 
- This is an Asus Chromebox with 1.4 GHz Intel Celeron 2955U Processor and 6GB of RAM
- I have already removed ChromeOS and removed the firmware write protection. If you haven't already done that, see [my previous post](http://dareneiri.github.io/Asus-Chromebox-With-Full-Linux-Install/) or [the original kodi posting with the walkthrough](http://forum.kodi.tv/showthread.php?tid=194362). 

### Setting up USB live boot drives with Ubuntu and Windows 10
You first need to have two usb drives (8GB is fine), one to boot Ubuntu and use the EZ setup script and install/update the Chromebox firmware, and another to install Windows 10. 
1. Download the iso for Ubuntu and Windows 10
2. Download [Rufus](https://rufus.akeo.ie/). 
3. Set up the first USB key with Ubuntu using Rufus
4. Set up the second USB key with Windows using [Microsoft's media tool](https://www.microsoft.com/en-us/software-download/windows10). I personally had issues getting Rufus to be bootable but I've heard it works well. 

### Update Chromebox firmware with Kodi E-Z Setup Script
Next we need to boot into Ubuntu and update the Chromebox firmware. 
1. Visit [Mr Chromebox's website](https://mrchromebox.tech/#kodi)
2. You essentially boot Ubuntu from your USB drive, and select the "Try Ubuntu" option to run it live. 
3. Open up Terminal and run the curl command from Mr Chromebox's website above. 
4. You may need to install curl, which you can do by typing `sudo apt install curl`
5. With the command line entered, you should be prompted to select an option. You want to *Install/Update Custom UEFI Firmware (Standalone)*. This should only take a minute or two. 
6. Once completed, restart (which may take a while to actually restart) and remove the Ubuntu usb drive. 
7. Now insert the Windows 10 USB drive and Chromebox should boot from it. If not, try resetting again and you should have a boot option prompt. 

### Some final notes
At this point you have updated Chromebox's firmware and you can now proceed to install Windows 10. With the firmware updated, audio over HDMI is supported. And while I had no problem with HDMI working with my monitor, HDMI was *not working* with my TV. I had no issue previously with the Chromebox running Ubuntu, but for some reason the Windows driver had no interest in working with my TV. I ended up installing the chipset drivers which you can grab [here](http://www.gigabyte.com/Mini-PcBarebone/GB-BXCEH-2955-rev-10#support-dl). 


![Grab the chipset drivers for Windows 10](http://dareneiri.github.io/images/chipset_driver_download.png)
