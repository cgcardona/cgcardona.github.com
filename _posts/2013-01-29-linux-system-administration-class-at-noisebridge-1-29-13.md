---
layout: post
title: "Linux System Administration class at NoiseBridge 1 29 13"
description: ""
category: 
tags: ['linux', 'noisebridge']
---
{% include JB/setup %}

[Linux System Administration class](https://www.noisebridge.net/wiki/Linux_System_Administration_class) notes

## Steps

### Set up user/pass 

James set me up a user/pass on his shed.systemateka.com box.

### SSH into the box and change your password with these steps

1. `ssh username@shed.systemateka.com` 
2. Enter password to login 
3. Type the following command to change your password `passwd`
4. It will ask for your existing pass and your new password with confirm entry

### Clone the github repo

1. `git clone cgcardona@shed.systemateka.com:/data/kb`
2. Change directories into the new repo with `cd kd`
3. Create a new file and then run git status to see your changes `git status`