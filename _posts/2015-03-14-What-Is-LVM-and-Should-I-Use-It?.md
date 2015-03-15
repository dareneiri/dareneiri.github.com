---
layout: post
title: What Is LVM and Should I Use It?
tags: [ubunut, linux]
published: true
excerpt: "You heard of using LVM as a good strategy for storage management, but what is it really, and should you use it?"
comments: true
---
{% include _toc.html %}

#Introduction
I'm quite used to navigating and futzing around Linux OS, primarily because of my exposure with Mac OS X and the similarities between Unix and Linux on file system navigation and terminal usage. However, I have recently been getting my hands quite dirty, and giving myself many headaches while I troubleshoot problems I come across.

There have been a few things that I kept coming across as I read more about Linux troubleshooting and the OS in general, one of them is LVM, or Logical Volume Management. I have also come across this when working on Macs, since you can come across logical volume groups. Not being very active in the sysadmin world for the past few years, I wasn't really aware of this change in Mac OS X. And logical volume groups were introduced with OS X Lion in 2011!

But logical volume groups in Mac OS X and logical volume management in Linux do not have the same features. [This wikipedia article on Core Storage](http://en.wikipedia.org/wiki/Core_Storage), the volume manager for Mac OS X, compares it to lacking Linux LVM's feature of easily expanding storage -- its raison d'être.

Don't let this confuse you, but know that there is a difference with the volume management in OS X and it is different than in Linux. However, *both* are methods of **virtually managing volumes.**

#Definition of LVM
Before we get to what an LVM is, let's define what a file system is. Michael Jang (author of the RHCSA/RHCE study guide book) considers the multiple meanings of a "file system":

1. It can be an individual volume, i.e, /dev/sda
2. A format, like ext4 or HFS+
3. Or even refers to the Basic File System Hierarchy Standard (FHS) directories, such as /boot, /home, or /media

But let's not think of LVMs as file systems, even though that is the #1 autocompletion result in Google:
<figure>
    <img src="{{ site.url }}/images/autocompletion.png" alt="google autocomplete">
</figure>

Think of LVMs as a **disk storage management strategy**. This was my initial mistake, and it's common to think of ["formatting an LVM partition"](http://unix.stackexchange.com/questions/64963/how-to-format-an-lvm-partition), just like we would when we format an ext4 partition (i.e, a file system).


#The Benefits of LVM
I'd like to emphasize that LVM is a disk storage management strategy because as a sysadmin, you have to wonder if it benefits setting your server up as an LVM or not. There are benefits to LVM, as opposed to strictly partitioning your volume as an ext4/HFS/NTFS/etc. You also need to consider *how* you set up your LVM.

###Storage Flexibility
The most commonly cited reason for using LVMs to manage your storage is that provides flexibility in expanding the storage space of a specific directory, or more specifically, a FHS directory (e.g., /home, /var). Let's use an fast-expanding business as an example. Say a company hosts a server for it's employees specifically used to store home directories. You allocate 1TB of space for your 300 or so employees. This might work initially, but then you need to think about the business expanding in size and the need to create more physical space for the /home directory. You also need to think about the increasing number of space existing users are using.

Under this scenario, without LVM, you would not be able to easily expand your 1TB of space for /home. You could pop in a new hard drive, but then that would create a mess managing a separate set of users on /home2, for example.

With LVM, you can *virtually expand* /home by popping in a new 4TB drive, and increase the initial 1TB dedicated to /home. The command would like similar to this;
<pre> lvextend -L+4000GB /dev/vg/home</pre>
The best part is that this would not involve downtime or a restart of your host. Pretty darn important in a production environment!

Let's drive the point that LVM is not strictly a file system format by noticing that this 4TB partition you popped in is formatted as ext4. In this sense, the file system of this 4TB drive is ext4, but the partition "type" is LVM. Actually, this is how Ubuntu references LVMs.

<figure>
    <img src="{{ site.url }}/images/filesystemtype.png" alt="fstype">
</figure>

I really enjoyed this explanation of the [benefits of LVMs through storage flexibility from tldp](http://www.tldp.org/HOWTO/LVM-HOWTO/benefitsoflvmsmall.html), particularly because it references having extra storage space after having moved his music from a 6GB partition to DVDs!

###Snapshots for VMs
When thinking about deploying virtual servers, the virtual hosts that are running can have "snapshots," allowing a user to restore a previous version, without taking up valuable storage space. If you have used VMWare Fusion, then you may have noticed that each snapshot (at least with my 20GB host) takes only 1GB of space.

<figure>
    <img src="{{ site.url }}/images/snapshots.png" alt="fstype">
</figure>

Speaking of VMs, using LVM on a VM has its own benefits. Once you extend the hard drive size in the VM host, you still need to extend it in Linux. Not using LVM seems to make extending your partition a bit more involved than it needs to be, [http://askubuntu.com/questions/294889/how-to-expand-the-ext4-primary-partition-size-in-a-vmware-player-virtual-disk](including a trip to BIOS, deleting partitions) (and possibly accidentally deleting your own!), or [booting from the live cd](http://askubuntu.com/questions/429576/increase-ubuntu-partition-size-under-virtual-machine) which isn't always convenient.

With LVM, extending your partition in Linux is pretty straight forward, especially if you follow a [walkthrough like this](https://www.justinrummel.com/resizing-a-vmware-fusion-ubuntu-server-logical-vhd-via-guided-partitioning/). It took me less than ten minutes and no restarts were required. Magic!

<figure>
    <img src="{{ site.url }}/images/extendvm.png" alt="fstype">
</figure>

###Sources
There are some other benefits to LVMs, including encryption and the ability to use RAID. Here are some resources you might find useful for additional discussion:

- [http://www.opensourceforu.com/2014/03/manage-storage-like-pro-lvm/](http://www.opensourceforu.com/2014/03/manage-storage-like-pro-lvm/)
- [http://xmodulo.com/use-lvm-linux.html](http://xmodulo.com/use-lvm-linux.html)
- [http://www.tldp.org/HOWTO/LVM-HOWTO/whatisvolman.html](http://www.tldp.org/HOWTO/LVM-HOWTO/whatisvolman.html)
- [http://askubuntu.com/questions/3596/what-is-lvm-and-what-is-it-used-for](http://askubuntu.com/questions/3596/what-is-lvm-and-what-is-it-used-for)

#Disadvantages of LVM(?)
I haven't found a consensus on whether there are downsides to using LVM in your environment, and I suppose this comes down to what you're specifically using it for, and how you're setting it up. I think partly this comes from what kernel of linux people are using. For example, there was a bug in 2.6.31 where write barriers were not supported (we're like... what 3.18.0-*? ). This meant that it wasn't guaranteed that file system corruption could be avoided/resolved, as ext3/4 offers through its journaling features:

- [https://bugzilla.kernel.org/show_bug.cgi?id=9554](https://bugzilla.kernel.org/show_bug.cgi?id=9554)
- [http://lwn.net/Articles/283161/](http://lwn.net/Articles/283161/)

Another common issue I have come across while reading about the disadvantages of LVM is the [claim of performance hits when using a LVM](http://www.linuxquestions.org/questions/linux-server-73/lvm-vs-no-lvm-811853/). But these claims of performance hits [seem to be negligible](http://unix.stackexchange.com/questions/7122/does-lvm-impact-performance).


#Final Thoughts
So should you use LVM as a storage strategy? One of the other mentioned disadvantages is the possible complexity of setting one up properly. However, if you have Virtual Box or another VM software, try it out and make mistakes. I think that's the only way to truly understand what you're doing. And listing this as a disadvantage should really be more of a consideration, and not a true disadvantage; understanding how to use the commands for setting up LVM is only temporary.

The purpose of writing this was to help myself structure my ideas and solidify my own learning process. However, I do hope that this may be of use to someone google-ing the same questions I was, and that this compilation of sources helps! I would appreciate any discussion on this topic, or any corrections that need to be made!
