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
	<pre>cd Downloads/</pre>
3. Then run: 

	
2. item
3. item