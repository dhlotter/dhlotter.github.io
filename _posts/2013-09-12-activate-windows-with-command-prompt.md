---
title: "Activate Windows with command prompt"
date: "2013-09-12T17:50:00.000+02:00"
search: true
comments: true
published: true
tags:
- windows
- operating system
- imported-post
---

I cannot tell you how many times I end up formatting my notebook. Eventually something always goes wrong and the prospect of troubleshooting seems way more daunting than a quick format. Besides, most of my information on the notebook is in the cloud, so I install the OS followed by a quick visit to [Ninite](http://ninite.com/) (a super service you should be using ), and then when Google drive installed, the wait begin for my files to re-download. Luckily some of us work for one of the largest ISP's in South Africa and down 
bandwidth is not a problem. 

Back to the reason for this post... 

![results](/images/activte-windows-with-cmd-001.png)

Once Windows 8 installed you can change the key and activate it as follows: 

Do the following. 
* Start an elevate command prompt and change working directory to System32 directory. 

> cd %WINDIR%\system32 

* Clear any KMS entries you may have. 

> slmgr.vbs –ckms 

![results](/images/activte-windows-with-cmd-002.png)

* Remove  any product keys installed 

![results](/images/activte-windows-with-cmd-003.png)

* Replace the X's with your product key. 

> slmgr.vbs -ipk XXXXX-XXXXX-XXXXX-XXXXX-XXXXX 

![results](/images/activte-windows-with-cmd-004.png)

* Activate your server/computer 

> slmgr.vbs –ato 

![results](/images/activte-windows-with-cmd-005.png)

Rejoice! Your operating system (Windows 8 / Windows Server) should now be activated. 