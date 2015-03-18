---
layout: post
title: Really Weird DNS Issues with Office 365
tags: [microsoft, office365]
published: true
excerpt: "I provisioned a tenant for Office 365, and the first step is to set up your DNS. I ran into some weird issues, but they turned out to be not issues, but maybe a bug."
comments: true
---

In an effort to diversify my skill set, I have been spending more time working with Office 365, with the end-goal of taking the [MS-Exam 70-346: Managing Office 365 Identities and Requirements](https://www.microsoft.com/learning/en-us/mcsa-office365-certification.aspx) certification test. Subsequently, I would take the 70-347 if all goes well.

There are some great resources, but they're scattered out there. In another post I'll provide more detail about that, but I wanted to focus on an issue I encountered while provisioning Office 365. By the way, if you don't have a live environment with Office 365 available, [you can set up a demo environment for 90 days, for free](https://paulrobichaux.wordpress.com/2014/06/04/creating-an-office-365-demo-tenant/).


When your tenant is up and running (took me more than 24 hrs), the first thing you want to do is go through the Basic Setup process.

<figure>
    <img src="{{ site.url }}/images/setup.png" alt="basicsetup">
</figure>


You will go through the process of connecting your domain name (in my case, dareneiri.com) to Office 365. This way, instead of having some long address (i.e., @apismellifera.onmicrosoft.com), the addresses of your users in this demo can be @dareneiri.com). The Basic Setup process will guide you through this, which you can view in detail [here](https://support.office.com/en-us/article/Verify-your-domain-in-Office-365-6383f56d-3d09-4dcb-9b41-b5f5a5efd611).

The issue I had was that no matter what I did within hover.com to change my DND entries, I kept getting errors! The verification steps within the Manage DNS settings would not accept my DNS entries. What's more interesting is that the errors kept changing.

<figure>
    <img src="{{ site.url }}/images/officedns1.png" alt="basicsetup">
</figure>

...and here's the first change.

<figure>
    <img src="{{ site.url }}/images/officedns2.png" alt="basicsetup">
</figure>

...re-running it again causes different errors to occur...

<figure>
    <img src="{{ site.url }}/images/officedns3.png" alt="basicsetup">
</figure>


From what I can tell, there is really nothing wrong with my DNS entries, and Office 365 is reporting false-errors. I verified this from Outlook by emailing my private Gmail account from my admin@dareneiri.com, Office 365 account, and that worked fine. Additionally, using the [Microsoft Remote Connectivity Analyzer](https://testconnectivity.microsoft.com/) reported no issues with my DNS entries:


<figure>
    <img src="{{ site.url }}/images/testconnectivity.png" alt="basicsetup">
</figure>


I wasn't able to find much information about this online, and whether this is a common issue. But from what I can tell, if you experience the same problems, feel free to ignore the problem and check the "Do not check this domain for incorrect DNS records" option From Domains > [Your domain] and "Find and fix issues" link.

<figure>
    <img src="{{ site.url }}/images/dnscheck.png" alt="basicsetup">
</figure>
