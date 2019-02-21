---
title: SharePoint Setup Reboot Required Fix
date: '2014-02-10T16:08:00.000+02:00'
search: true
author: Hermann Lotter
comments: true
tags:
- sql
published: true
---

One of your clients actually goes through the process, logs a call in which 
they ask for a new install of SharePoint Foundation 2013. You sigh, pop on to 
their box and start installing the prerequisites, reboot and then hit 
SharePoint Foundation only to get a loveletter from Microsoft that goes like 
this: 

<div class="separator" style="clear: both; text-align: center;">[<img 
border="0" 
src="http://3.bp.blogspot.com/-Im96M31Rx-E/VHCqTvnrTlI/AAAAAAABF5I/572svMUviRk/s1600/error-message.png" 
height="402" width="640" 
/>](http://3.bp.blogspot.com/-Im96M31Rx-E/VHCqTvnrTlI/AAAAAAABF5I/572svMUviRk/s1600/error-message.png) 


<pre>Setup is unable to proceed due to the following error(s): 

A system restart from a previous installation or update is pending. Restart 
your computer and run setup to continue. 

For the list pre-requisites needed to install the product refer to: 
http://go.microsoft.com/fwlink/?LinkID=230806 

Correct the issue(s) listed above and re-run setup. 

You can install all the required prerequisite this product by selecting the 
'Install software prerequisites' option in the splash screen. See Help for 
more information. 

Once again the link does not tell us much and no matter how many times you 
reboot, the problem persist.</pre> 


Easy fix guys... Open the registry editor on this server/machine and head on 
over to: 
<pre>HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Control\Session 
Manager\</pre> 
Over here rename or delete "PendingFileRenameOperations" key and try the 
install again. It should work like charm. 