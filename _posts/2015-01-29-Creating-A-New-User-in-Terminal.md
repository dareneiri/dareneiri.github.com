---
layout: post
title: Creating A New User in Terminal (Mac OS X) 
published: true
---

The following commands can be used to create a new user in Terminal via SSH:

	`dscl . -create /Users/new_user`

	`dscl . -create /Users/new_user UserShell /bin/bash`

	`dscl . -create /Users/new_user RealName “USER NAME“`

	`dscl . -create /Users/new_user UniqueID 503`

	`dscl . -create /Users/new_user PrimaryGroupID 20`
PrimaryGroupID of 80 creates an Admin user. Change to PrimaryGroupID of 20 to create a Standard user.


	`dscl . -create /Users/new_user NFSHomeDirectory /Users/new_user`
    
	`dscl . -passwd /Users/new_user changeme`
    
	`dscl . append /Groups/admin GroupMembership new_user`
    
You may need to create the home directory as well:
	'createhomedir -u new_user'
