---
layout: post
title: Creating A New User in Terminal (Mac OS X) 
published: true
comments: true
---

The following commands can be used to create a new user in Terminal via SSH:

<pre>dscl . -create /Users/new_user</pre>

<pre>dscl . -create /Users/new_user UserShell /bin/bash</pre>

<pre>dscl . -create /Users/new_user RealName “USER NAME“</pre>

<pre>dscl . -create /Users/new_user UniqueID 503</pre>

<pre>dscl . -create /Users/new_user PrimaryGroupID 20</pre>
PrimaryGroupID of 80 creates an Admin user. Change to PrimaryGroupID of 20 to create a Standard user.


<pre>dscl . -create /Users/new_user NFSHomeDirectory /Users/new_user</pre>
    
<pre>dscl . -passwd /Users/new_user changeme</pre>
    
<pre>dscl . append /Groups/admin GroupMembership new_user</pre>
    
You may need to create the home directory as well:

<pre>createhomedir -u new_user</pre>
