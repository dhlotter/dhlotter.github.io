---
title: My Post Windows Install Todo Checklist
date: '2016-08-14T12:48:00.001+02:00'
search: true
comments: true
published: true
tags:
- windows
---

A while ago, my Windows 10 installation started giving some issues and today was the last straw. Since Windows free upgrades are not around any longer I decided to do something I have not done before, Reset Windows. This is new functionality that came with Windows 10 and I must say it was quite easy. 

Below my steps: 
Windows button and "I" key to bring up the Settings window. 
Click Update and recovery, and then Recovery. 
In the Remove everything and reinstall Windows section, click Get started. 

Roughly 40 minutes later my laptop restarted for the last time and I was able to run through the setup. Rather painless and to a happy place in regards to the operating system. This gave me a chance to test my "Todo after format" scripts all in succession. 

## Remove bundled Windows 10 apps 
Open powershell and run the following commands. This will remove most of the Windows 10 apps bundled with the install. (Feel free to remove packages you will be using from the list below.) 
```powershell
Get-AppxPackage *3d* | Remove-AppxPackage 
Get-AppxPackage *camera* | Remove-AppxPackage 
Get-AppxPackage *communi* | Remove-AppxPackage 
Get-AppxPackage *bing* | Remove-AppxPackage 
Get-AppxPackage *zune* | Remove-AppxPackage 
Get-AppxPackage *people* | Remove-AppxPackage 
Get-AppxPackage *phone* | Remove-AppxPackage 
Get-AppxPackage *photo* | Remove-AppxPackage 
Get-AppxPackage *solit* | Remove-AppxPackage 
Get-AppxPackage *onenote* | Remove-AppxPackage 
Get-AppxPackage *office* | Remove-AppxPackage 
Get-AppxPackage *skype* | Remove-AppxPackage 
Get-AppxPackage *candy* | Remove-AppxPackage 
Get-AppxPackage *twitter* | Remove-AppxPackage 
Get-AppxPackage *sway* | Remove-AppxPackage 
Get-AppxPackage *solita* | Remove-AppxPackage 
```

## Remove OneDrive from system Tray 
Make sure OneDrive does not run at system startup, right click OneDrive in the system tray, click settings and untick "Start OneDrive automatically when I sign in to Windows". 

**Remove OneDrive from Explorer side bar** 
For this I use a registry script found over at [How to Geek](http://www.howtogeek.com/225973/how-to-disable-onedrive-and-remove-it-from-file-explorer-on-windows-10/) 
which you can download [here](http://cdn3.howtogeek.com/wp-content/uploads/2015/08/Hide-OneDrive-From-File-Explorer.zip). 
Once downloaded, unzip and double click the appropriate version. 

That's about it. 