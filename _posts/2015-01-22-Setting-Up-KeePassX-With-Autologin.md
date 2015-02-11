---
layout: post
title: Setting Up KeePassX with Browser Support
published: true
---

_This post is intended for Mac users setting up KeePassX and getting autologin + browser (specifically, Chrome) support to work. At the time of this writing, the official build does not support autologin. However, there are other versions of KeePassX that are available to use, you just need to compile them._

## Requirements
- To make things simple, I recommend [installing XCode](https://developer.apple.com/xcode/downloads/). If you wish to install only the specific tools needed, you should install make, cmake, and clang
- Download the [KeePassX source from GitHub](https://github.com/jdachtera/keepassx). There is a "Download Zip" button on the right side of the page.
- Install [ChromeIPass browser extension](https://chrome.google.com/webstore/detail/chromeipass/ompiailgknfdndiefoaoiligalphfdae?hl=en)
- Download [Brew](http://brew.sh), or type the following in Terminal:
	<pre>ruby -e "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/master/install)"</pre>
	and then install:
    <pre>brew tap homebrew/dupes</pre>


## Compiling the Build
1. Once you download the source, make sure you know where it saved (i.e., your Downloads folder). Unzip it.
2. Then you need to open Terminal (Applications > Utilities > Terminal.app) and navigate to that folder. In Terminal, type:
	<pre>cd Downloads/keepassx-master</pre>
3. Then run: 
	<pre>brew install qt cmake libgcrypt zlib libmicrohttpd</pre>
    <pre>cmake -DCMAKE_INSTALL_PREFIX=$HOME/local/apps/keepassxhttp -DCMAKE_VERBOSE_MAKEFILE=ON</pre>
    <pre>make</pre>
    <pre>make install</pre>
4. Congrats! You compiled an app from source! Now, if you navigate to your /Users/USERNAME/local/apps/keepassxhttp, where USERNAME is your home directory name, then you will see the KeePassX application. To navigate to the /local folder quickly, make sure Finder is active and on the menu bar, select Go > Go to Folder...

## Setting up the ChromeIPass Browser Extension
1. Once you open the KeePassX application, ChromeIPass may need to establish a connection to the application.
	You will get notified by the extension to have KeePassHTTP connected. All you need to do is launch KeePassX, and click on the extension icon to establish the connection. 
    ![chromipass](http://dareneiri.github.io/downloads/Screen%20Shot%202015-01-22%20at%205.57.55%20AM.png)

## Resources
- [Forked repo of KeePassX with ChromeIPass support](https://github.com/jdachtera/keepassx)
- [Master repo of KeePassX](https://github.com/keepassx/keepassx)
- [KeePassX feature requeset tracker](https://www.keepassx.org/dev/issues/91#change-603) with details on compiling KeePassX from source


