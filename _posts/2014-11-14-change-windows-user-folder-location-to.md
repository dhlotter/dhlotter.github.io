---
title: Change Windows User Folder Location to Different DRIVE
date: '2014-11-14T14:55:00.001+02:00'
search: true
comments: true
published: true
tags:
- howto
---

Not too long ago my girlfriend got herself a Dell XPS 15 to replace her old HP Piece-o-Shit. The HDD configuration included a 32Gb mSATA SSD and a 500Gb SATA drive. I actually thought about it for a while and decided to install Windows 8.1 on the 32Gb drive. Shortly after the install I realized what a big mistake this was as Windows quickly decided to take most of the drive space on this volume. In an effort to move some data to the slower space (and data that would not be access all that regularly), I performed this little hack and moved her user folder from the C: to D: drive. This is what I did. 
* Open run dialog, **Win+R** and copy/type **shutdown /r /o **to boot into 
recovery mode. 
* When the computer starts, choose **Troubleshoot**, **Advanced Options** 
then **Command Prompt**. 
* Copy user folder to new location: **xcopy /e /k /o /h /b c:\Users\username 
d:\Users\username** 
* Remove the original folder: **rd /s c:\Users\username** 
* Create a symbolic link: **mklink /d c:\Users\username d:\Users\username** 
Once done, reboot and everything should carry on exactly the way it did 
before. If for some reason you would like to go back to the way things were, 
you need to go back into recovery mode remove the symbolic link (**rmdir 
c:\Users\username**) and copy your data back to its original location. 