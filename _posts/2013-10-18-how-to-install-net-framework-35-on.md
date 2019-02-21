---
title: How to install .NET Framework 3.5 on Windows Server 2012 and WindowsServer
  2012 R2
date: '2013-10-18T17:44:00.000+02:00'
search: true
comments: true
published: true
tags:
- windows
- imported-post
---

I bet you there is a bunch of you struggling with this issue and it's driving me crazy. I needed to perform these installs quite often and had to remember what I did last time. This post will act as my extended memory. 

Open an elevated command prompt and kick off the below command (changing the sources path to where your sources folder is located). 
> dism /online /enable-feature /featurename:NetFX3 /all /Source:S:\sources\sxs /LimitAccess

We have the folder stashed on a file server and merely map it to local machine. 

![results](/images/dot-net-install-windows-server-2012-001.png)

And its as easy as that. 