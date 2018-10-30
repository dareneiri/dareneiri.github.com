---
title: Asus Chromebox with Full Linux Install
tags:
  - htpc
  - linux
published: true
excerpt: >-
  Walkthrough on installing Ubuntu Linux (14.04) on an Asus Chromebox. This will
  be used as an HTPC with Plex Home Theater.
comments: true
toc: true
---



_This post is made possible because of the resources that others have provided. The purpose of this walkthrough is to provide details on how I set my Chromebox for my own use -- with a standalone boot of Ubuntu Linux (14.04). I have also set up my Chromebox with VNC for local access (or remote desktop access) and Plex Home Theater, which I will go over as well._

## Home Setup
At home, I have a Synology DS212j, which has been updated with the [DS215j](https://www.synology.com/en-global/products/DS215j). The DS212j contains all my media (movies, tv shows, music, photographs) and works well hosting those files. It also runs perfectly fine running Plex Media Server (PMS). The limitation of running PMS is that the Synology DS212j (or DS215j) do not have the processing power to transcode my .mkv media. In otherwords, you cannot directly play a video from the Synology NAS unless the hardware (laptop, desktop) you are using to view the media is capable of transcoding the media. Using a tablet, phone, Chromecast, Roku with the Plex app will not work.

I previously used my primary desktop computer, which has Plex Home Theater (PHT) installed, to connect to the PMS on my Synology NAS. The computer was then connected to the TV via HDMI. This worked fine, but it was troublesome when I didn't want to leave my computer on all day, waste electricty, and generate extra heat during the summer.

## The Best HTPC For Me
There are several HTPCs available, but I wasn't looking to spend more than $150, and I wanted it with low power consumption, a small footprint, and the ability to boot into Linux directly. This is something that I would be comfortable running 24/7 without feeling like I'm wasting electricty.

The [Asus Chromebox](http://www.asus.com/us/ASUS_Chromebox/) fits the bill perfectly. There are resources available to set up standalone Linux easily, it doesn't consume too much power, but it is powerful enough to transcode media, and it's pretty inexpensive. The Asus Chromebox was released in March 2014. Ars Technica gave it [unfavorable reviews as an HTPC setup](http://arstechnica.com/gadgets/2014/03/review-asus-brings-chrome-os-to-mini-pcs-in-a-low-power-inexpensive-package/2/), but much has changed in ease of installing a standalone linux OS. I found it on eBay for ~$110, brand new. Currently, Amazon sells it for $159:
    <figure>
        <img src="{{ site.url }}/images/chromeboxpricewatch.png" alt="screenshot of chromebox camelcamelcamel">
    </figure>


## Requirements
If you aim to accomplish the same setup for your Chromebox as I have, follow the guide below. Again, this is for a standalone Linux Ubuntu boot on the Asus Chromebox. **This process will remove ChromeOS** and does not have the option to dual-boot. Once you have finished this process, you will have accomplished the following:

1. An Asus Chromebox with Ubuntu Linux 14.04, as a standalone boot.
2. Plex Home Theater installed on the Chromebox, accessing Plex Media Server on the Synology NAS
3. VNC server up and running, to remotely access the system

I am assuming you already have Plex Media Server working with all your media. I am also assuming that you are willing to risk bricking your Chromebox; definitely proceed at your own risk. With that said, serveral people have reported success with this process.

## Step-by-Step Walkthrough

### Chromebox Setup and Ubuntu Installation

Please note that the Kodi E-Z Setup Script is still in active development and options may change, or this process may no longer work. I wrote this in Feb 2015 and so the details of each step may have changed. I will try to keep this updated but please proceed at your own risk
{: .notice--warning} 

1. With your Chromebox unplugged, prepare your device for the linux installation by disabling the [firmware write protection](http://kodi.wiki/view/Chromebox#Disable_Firmware_Write_Protect).
    1. To open the Chromebox, you need to remove the four rubber footpads. I found it easiest to use a small flathead and lift up from the inner-rounded corner of the footpad
        <figure>
            <img src="{{ site.url }}/images/chromebox1.jpg" alt="chromebox footpad removal">
            <figcaption>Lift the flathead under the rubber foot, from the direction of the inner-rounded corner.</figcaption>
        </figure>
    2. In case of any doubt from the website link above, here is the screw that needs to be permanently removed for this installation to work.
        <figure>
            <img src="{{ site.url }}/images/chromebox2.jpg" alt="screw write protect">
        </figure>
    3. If you like, you can install additional RAM at this point. Do make sure your RAM is PC3L, and not PC3. Using the latter will result in issues upon bootup.
2. Follow the steps at this link to [get into developer mode](http://kodi.wiki/view/Chromebox#Put_in_Developer_Mode).
    1. **NOTE:** Carefully follow these instructions. Take your time at this step. STOP at "1.3 Perform Factory Reset." You do not need to follow that step.

3. You now want to download and run the EZ setup script, provided by Matt DeVillier. You can follow the [steps from the Kodi forums](http://forum.kodi.tv/showthread.php?tid=194362), but I will break it down here.
    1. **NOTE:** Most of these instructions are directly from the link above, but I want to separate those instructions to make it easier see what needs to be done.
   1. Power up your Chromebox, and set up the internet connection (the first screen). DO NOT continue with the set up prompts.
   2. Press CTRL-ALT-F2 to view the command prompt
   3. You will be prompted for a username. Enter:
        <pre>chronos</pre>
   4. Enter the following to download and run the EZ setup script:
        <pre>cd; curl -L -O https://mrchromebox.tech/setup-kodi.sh && sudo bash setup-kodi.sh</pre>

   5. You will be provided some options to choose from. ~~Enter **5**, for **Install/update: custom coreboot Firmware**~~ Enter **6** (as of ~2017), for **Install/Update: Custom UEFI Firmware**.
   6. Type **Y** to continue
   7. ~~You may be prompted to ask if you want to install the headless firmware. Go ahead and say no.~~. The headless option is no longer an option as of ~2017.
   8. Backup the ChromeOS firmware to a USB stick.
   9. Then download and setup a USB stick to liveboot Ubuntu on a [Mac](http://sourceforge.net/projects/mlul/) or [PC](http://www.linuxliveusb.com/). **Please note that with Ubuntu will probably not install the grub EFI shim to the default UEFI boot target and this will cause your Chromebox to boot up to a black screen which is the EFI shell. See [MrChromebox.tech's FAQ](https://mrchromebox.tech/#faq) which addresses how to resolve this. Otherwise you can use GalliumOS.
   10. Stick in the liveboot USB stick into the Chromebox, and reboot it.**
   11. You will have five seconds to press ESC key to display the boot menu. If you miss it simply reboot it again.
   12. Select the USB stick from the boot menu, and then you can proceed with installing Ubuntu.

### Setting up Ubuntu
1. Once you have Ubuntu installed, you can install the programs you need.
2. Run Updates first. See the [Maintenence commands from Ubuntu Documentation](https://help.ubuntu.com/community/AptGet/Howto#Maintenance_commands) for an overview of what to run
3. Installing Plex Home Theater
    1. Add the plexappp repository by following [this documentation](https://launchpad.net/~plexapp/+archive/ubuntu/plexht). If it's confusing, you should do the following commands in Terminal:
        <pre>sudo add-apt-repository ppa:plexapp/plexht </pre>
    2. Update the respositories:
        <pre>sudo apt-get update</pre>
    3. Install Plex Home Theater:
        <pre>sudo apt-get install plexhometheater</pre>
    4. Now all you need to do is configure PHT to talk to your PMS. I did this by configuring my server settings manually in Preferences.
4. Configuring VNC - Remote Desktop
    1. Ubuntu comes with Desktop Sharing by default. This sets up a VNC server.
    2. Type "Desktop Sharing" in the dash (the launcher/finder)
    3. Configure the settings so that the following in enabled as seen below:
    <figure>
        <img src="{{ site.url }}/images/remoteubuntuconfig.png" alt="ubuntuconfig">
        <figcaption>Enable the options seen above for remote desktop sharing</figcaption>
    </figure>  
    4. You then need to disable encryption, since having this enabled seems to be an issue.
        <pre>gsettings set org.gnome.Vino require-encryption false</pre>
    5. This change may not stay after reboot, so you can edit some settings by typing the following in Terminal:
        <pre>sudo apt-get install dconf-tools</pre>
    6. Search for dconf Editor in dash, then navigate to org > gnome > desktop > remote-access
    7. Some have reported unchecking "enabled" but others haven't had much success and [resorted to finding other solutions](http://discourse.ubuntu.com/t/remote-desktop-sharing-in-ubuntu-14-04/1640/4). Defintely review those options if you're haivng problems accessing VNC after rebooting. '

## Summary
What you've accomplished, if my documentation is thorough enough (if not please let me know) is setting up the Asus Chromebox as an HTPC, with Ubuntu 14.04 installed, along with Plex Home Theater and local VNC access. If you would like to have access to your Chromebox via remote desktop outside your network (e.g., at work or another house) then I *strongly* recommend setting up SSH tunneling for VNC; passwords are not encrypted over the network.
