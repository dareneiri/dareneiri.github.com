---
layout: post
title: Ubuntu Woes&#58; Mouse, Keyboard, and Ethernet Not Recognized At Boot
published: true
excerpt: "You restarted Ubuntu and find that your mouse, keyboard, and/or Ethernet are no longer recognized. How do you fix this?"
comments: true
---

So I had an interesting problem that I encountered today, and the best part is that since I was able to fix it, I have learned quite a bit more about the inner-workings of Ubuntu Linux.

This single-boot desktop could no longer boot correctly into Ubuntu 14.04. By "correctly," I mean that it would boot to the normal screen, but the mouse, keyboard, and Ethernet would disconnect as soon as the kernel (and thus the boot screen) would load. Because of this, you couldn't log in, and even booting into the recovery kernel wouldn't work. The kernel causing issues was 3.13.0-46-generic.

Fortunately the previous kernel did work! This was 3.13.0-39-generic.

I'm not sure what caused the 3.13.0-46-generic to no longer work, only that in the kernel log output, the following would show up

<pre>nano /var/log/kernel.log</pre>
<pre>Your BIOS is broken; DMAR reported at address fed10000 returns all ones!</pre>

Apparently this issue is quite common:

- [Link to askubuntu.com](http://askubuntu.com/questions/432007/usb-keyboard-mouse-not-recognized-after-update-to-13-10-from-12-10)
- [Link to ubuntuforums.com](http://ubuntuforums.org/showthread.php?t=2114055&page=2)
- [Link to askubuntu.com](http://askubuntu.com/questions/413338/why-is-my-syslog-telling-me-that-my-bios-is-broken)
- [Link to hardforum.com](http://hardforum.com/showthread.php?t=1807755)


I obviously spent a lot of time reviewing possible solutions.

One of the solutions was to modify the `/etc/defaults/grub` file and UEFI:

- <pre>sudo gedit /etc/default/grub</pre>
- Change `GRUB_CMDLINE_LINUX="linux"` to `GRUB_CMDLINE_LINUX="iommu=soft"` near the top
- <pre>sudo update-grub</pre>
- Then find some setting in your UEFI regarding iommu and disable it.

Unfortunately I did not have any setting regarding the iommu and adding `iommu=soft` into my grub file did not do anything regarding the USB/Ethernet issue.

I attempted to update the kernel so that a new one would be used by default -- that didn't work either. Evidently the /boot partition size was only 56MB or so. Changing the partition size isn't easy, from what I found. There wasn't enough space to install the package after download the files I needed. This is also not unheard of:

- [Link to askubuntu.com](http://askubuntu.com/questions/298487/not-enough-free-disk-space-when-upgrading)

So what am I do to? There was one only kernel that was used previously, so two total kernels existed. I simply deleted the newest one. I already knew what kernel I wanted to remove, 3.13.0-46-generic, so I did the following:  
   <pre>sudo apt-get purge linux-image-3.13.0-46*.</pre>

If you don't know what kernels are available, first determine what you're currently using:
   <pre>uname -r</pre>

Then determine what kernel packages are available:
   <pre>sudo dpkg --list 'linux-image*'</pre>

Finally, knowing what you are currently using, and what you want want to remove, do the same command as earlier, where VERSION is whatever kernel version you want to remove:
   <pre>sudo apt-get purge linux-image-VERSION*.</pre>
