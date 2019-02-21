---
title: "SQL Server Configuration Manager Missing in Windows 8.1"
date: "2014-01-25T17:11:00.000+02:00"
search: true
comments: true
published: true
tags:
- sql
- imported-post
---

I don't know if this is a very common issue. Once before I upgraded from Windows 8 to Windows 8.1 with SQL Server 2012 installed on my notebook. Afterwards SQL Server Configuration Manager disappeared. Back then I opened the installation manager and chose to repair the SQL install. Afterwards the I could open Configuration Manager again.<br/

Today, having Windows 8.1 installed already, I install SQL 2012 Express. After the install SQL Server Configuration Manager was nowhere to be found. Metro did not have it, nor did the All Programs menu.

Luckily if this has happened to you right click your desktop, choose new and then shortcut and point it to:
```
C:\Windows\SysWOW64\SQLServerManager11.msc
Note, use the whole string above use SQLServerManager**11**/**10** depending on your installation.
```
Have fun. 