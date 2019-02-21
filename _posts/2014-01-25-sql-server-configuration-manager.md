---
title: SQL Server Configuration Manager Missing in Windows 8.1
date: '2014-01-25T17:11:00.000+02:00'
search: true
author: Hermann Lotter
comments: true
tags:
- sql
published: true
---

I don't know if this is a very common issue. Once before I upgraded from 
Windows 8 to Windows 8.1 with SQL Server 2012 installed on my notebook. 
Afterwards SQL Server Configuration Manager disappeared. Back then I opened 
the installation manager and chose to repair the SQL install. Afterwards the I 
could open Configuration Manager again.<br/><br/>Today, having Windows 8.1 
installed already, I install SQL 2012 Express. After the install SQL Server 
Configuration Manager was nowhere to be found. Metro did not have it, nor did 
the All Programs menu.<br/><br/>Luckily if this has happened to you right 
click your desktop, choose new and then shortcut and point it 
to:<br/><pre>C:\Windows\SysWOW64\SQLServerManager11.msc</pre><br/>Note<br/>use 
the whole string above<br/>use SQLServerManager**11**/**10** depending on your 
installation.<br/><br/>Have fun. 