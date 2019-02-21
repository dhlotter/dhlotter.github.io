---
title: "In Place Upgrade of Windows Server 2008 from Standard to Enterprise"
date: "2014-04-14T15:52:00.000+02:00"
search: true
comments: true
published: true
tags:
- sql
published: true
---

Let’s say you’re building a TEST environment and, and let’s say you haven’t worked with Win 2008 in a while, so it’s only obvious that you forgot clustering only works in enterprise edition of Windows 2008. In this case it is more than possible that you asked the server guys for two times standard edition. Doh! If this is the case, you can still salvage the situation and not waste anyone else’s time even more. Just upgrade the server edition. Here is how. 


Open elevated command prompt. To verify the current edition, type: 
```
DISM /Online /Get-CurrentEdition
```

To see which editions you can upgrade to type the following: 
```
DISM /Online /Get-TargetEditions
```

To upgrade you need to execute the following command and specify your key (for KMS go to 
[[link](http://technet.microsoft.com/en-us/library/ff793421.aspx)] or check the product.ini in your sources folder).

```
DISM /Online /Set-Edition:ServerEnterprise /ProductKey:xxxxx-xxxxx-xxxxx-xxxxx-xxxxx 
```
![results](/images/in-place-windows-server-upgrade-001.png)
