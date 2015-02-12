---
layout: post
title: Ditching Dashlane for KeePassX
published: true
excerpt: "Dashlane raised its subscription price to $29/year. It's time to ditch it for an open source alternative."
comments: true
---

{% include _toc.html %}


This past weekend, I received an email from Dashlane requesting to automatically renew my premium membership. Dashlane is password manager and "digital wallet," and it works pretty well. Using it on Mac OS X, the interface is clean, the extensions for the browsers work without any issues, and also includes two-factor authentication via SMS. But for a premium membership, which includes syncing across all your devices and browsers, the cost is quite steep at $29.99 per year. I bought mine for $19.99 per year but it seems like they increased the price, so the price increase made me rethink about whether Dashlane is even worth it anymore.

##What is a Password Manager? 

Why even pay for a password manager? Firefox, Chrome, and Safari already include password managers, but they are specific to the browser itself, and you cannot readily access those passwords if you are using a mobile app (i.e., banking apps that do not cache your password).

If you use only one or two passwords -- or even a handful of passwords -- that is not enough to keep yourself secure online. Ideally, every website you log into should have a unique password associated with it, and the longer and more random it is, the better. The only way to remember these passwords is to simply not remember them, and remember one master password that you use to access your password database. **Once you log into the password manager, then whenever you go to chase.com or amazon.com, your username and password will autofill.** More importantly, that password you use is unique to that website, and is probably 16 alpha-numeric characters in length. So next time [Ebay.com gets hacked into](http://www.npr.org/blogs/thetwo-way/2014/05/21/314579762/saying-it-was-hacked-ebay-urges-users-to-change-passwords), or another [data breach occurs for Amazon.com](http://time.com/3647988/amazon-xbox-hack-password/), you only need to change that single password and not worry about your other accounts.

The most important feature is that password managers encrypt/decrypt your password database locally. In other words, if your password database is synced online and needs to get downloaded, **the information is encrypted.** Even if the database gets stolen, assuming your master password is 16+ characters (like a sentence or phrase), then your passwords should remain encrypted.

And forget about complex passwords, because they're [not as safe as you might think](http://arstechnica.com/security/2013/06/password-complexity-rules-more-annoying-less-effective-than-length-ones/). xkcd also covered this topic:


![xkcd_comic](http://imgs.xkcd.com/comics/password_strength.png)
 

##Password Manager Options

There are quite a few password managers to choose from. I used LastPass a few years ago, but I found the interface a bit too cluttered and confusing, so I started using Dashlane.

LastPass offers a premium membership which includes across-device-syncing for $12 per year, so it is considerably cheaper than Dashlane's current $29 per year. However, from my personal experience, **at least on Mac OS X, LastPass is one of the most unstable applications I have used in quite some time.** The browser plug-in installer would stall (requiring a force quit), and the mutlifactor authenticator did not always work using [Sesame](https://helpdesk.lastpass.com/security-options/multifactor-authentication-options/sesame-multifactor-authentication-with-a-usb-thumb-drive/) (their own second authenticator). I did not see it as an option to replace Dashlane. From what I have read online, I am not the only one to experience this with their latest update.

There are a few other options, including [1Password](https://agilebits.com/onepassword). LifeHacker also very recently covered the "[Five Best Password Managers.](http://lifehacker.com/5529133/five-best-password-managers)"

I ended up settling on [KeePass](http://keepass.info/). It is open-source (free!), and it is cross-platform (Mac, Windows, Linux). Dashlane does not have support for Linux, but LastPass does. Syncing across all your devices is quite simple as well, as you can keep your encrypted password database synced using Dropbox, Google Drive, or any other cloud file-synchronization service. In the next post I will write up how to install and set up KeePass for Mac OS X -- it is not as straight-forward as you would expect.