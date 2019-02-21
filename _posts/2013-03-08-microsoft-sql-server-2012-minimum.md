---
title: Microsoft SQL Server 2012 Minimum Requirements Uninstall Error
date: '2013-03-08T10:56:00.000+02:00'
search: true
comments: true
published: true
tags:
- sql
- imported-post
---

This was kinda weird. I tried to uninstall SQL from my laptop and found myself 
looking at this strange popup I have surely seen before when trying to install 
SQL. 

> The operating system in this computer does not meet the minimum requirements for SQL Server 2012. For Windows Vista of Windows Server 2008 operating system, Service Pack 2 or later is required. For Windows 7 or Windows Server 2008 R2, Service Pack 1 or later is required. For more information, see Hardware and Software Requirements for installing SQL Server 2012 at:

> [http://go.microsoft.com/fwlink/?LinkID=195092](http://go.microsoft.com/fwlink/?LinkID=195092)

For some reason I tried it again expecting different results, nada. So I had to do some research on the matter. Found a connect article that explains the error and the workaround [here](http://connect.microsoft.com/SQLServer/feedback/details/707706/unable-to-uninstall-sql-server-2012-rc0-from-control-panel). 

[video](https://www.youtube.com/embed/pXlkLEB4osY)

For those of you who cannot be bothered to watch the video, this is what you I did. 

* Browse to your SQL setup bootstrap folder (depending on your major version). 
* For 2012 this is the path: 
> C:\Program Files\Microsoft SQL Server\110\Setup Bootstrap\SQLServer2012
* Right-click on setup.exe and choose properties. 
* Go to the compatibility tab and under compatibility mode and select [**Windows Vista (Service Pack 2)**]. 

The uninstall should now work. 