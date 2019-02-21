---
title: In Place Upgrade of Windows Server 2008 from Standard to Enterprise
date: '2014-04-14T15:52:00.000+02:00'
search: true
author: Hermann Lotter
comments: true
tags:
- sql
published: true
---

<div> 

Let’s say you’re building a TEST environment and, and let’s say you haven’t 
worked with Win 2008 in a while, so it’s only obvious that you forgot 
clustering only works in enterprise edition of Windows 2008. In this case it 
is more than possible that you asked the server guys for two times standard 
edition. Doh! If this is the case, you can still salvage the situation and not 
waste anyone else’s time even more. Just upgrade the server edition. Here is 
how. 


<div>Open elevated command prompt. To verify the current edition, type: 
<span style="font-family: Consolas, Monaco, monospace; font-size: 12px; 
line-height: 18px;">DISM /Online /Get-CurrentEdition 
<div><img alt="" 
src="file:///C:/Users/HERMAN~1.LOT/AppData/Local/Temp/enhtmlclip/1.PNG" 
/><div>To see which editions you can upgrade to type the following: 
<div><span style="font-family: Consolas, Monaco, monospace; font-size: 12px; 
line-height: 18px;">DISM /Online /Get-TargetEditions 
<div><img alt="" 
src="file:///C:/Users/HERMAN~1.LOT/AppData/Local/Temp/enhtmlclip/2.PNG" /> 
<div>To upgrade you need to execute the following command and specify your key 
(for KMS go to 
[[link](http://technet.microsoft.com/en-us/library/ff793421.aspx)] or check 
the product.ini in your sources folder).<div><span style="font-family: 
Consolas, Monaco, monospace; font-size: 12px; line-height: 18px;">DISM /Online 
/Set-Edition:ServerEnterprise /ProductKey:xxxxx-xxxxx-xxxxx-xxxxx-xxxxx 
<div><div class="separator" style="clear: both; text-align: center;">[<img 
border="0" 
src="http://3.bp.blogspot.com/-qWW3v6klIGU/VHCp-QBx6JI/AAAAAAABF5A/o8Ue84JH3Zc/s1600/31.png" 
height="300" width="640" 
/>](http://3.bp.blogspot.com/-qWW3v6klIGU/VHCp-QBx6JI/AAAAAAABF5A/o8Ue84JH3Zc/s1600/31.png) 