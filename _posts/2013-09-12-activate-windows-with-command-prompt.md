---
title: Activate Windows with command prompt
date: '2013-09-12T17:50:00.000+02:00'
search: true
author: Hermann Lotter
comments: true
tags:
- tech
published: true
---

I cannot tell you how many times I end up formatting my notebook. Eventually 
something always goes wrong and the prospect of troubleshooting seems way more 
daunting than a quick format. Besides, most of my information on the notebook 
is in the cloud, so I install the OS followed by a quick visit to 
[Ninite](http://ninite.com/) (a super service you should be using ), and then 
when Google drive installed, the wait begin for my files to re-download. 
Luckily some of us work for one of the largest ISP's in South Africa and down 
bandwidth is not a problem. 

Back to the reason for this post... 

<div class="separator" style="clear: both; text-align: center;">[<img 
border="0" 
src="http://1.bp.blogspot.com/-rgdTQMNvyeY/VHFo3AFrXtI/AAAAAAABF8w/hJr2OKgzAMo/s1600/capture_1.png" 
height="74" width="320" 
/>](http://1.bp.blogspot.com/-rgdTQMNvyeY/VHFo3AFrXtI/AAAAAAABF8w/hJr2OKgzAMo/s1600/capture_1.png) 

Once Windows 8 installed you can change the key and activate it as follows: 

Do the following. 
<div class="separator" style="clear: both; text-align: center;"> 
<li>Start an elevate command prompt and change working directory to System32 
directory. 
<pre><span style="font-family: Courier New, Courier, monospace;"> cd 
%WINDIR%\system32 
</pre></li><li>Clear any KMS entries you may have. 
<pre><span style="font-family: Courier New, Courier, monospace;"> slmgr.vbs 
–ckms 
</pre>[<img border="0" 
src="http://4.bp.blogspot.com/-2ui0TdcqyNg/VHFpFwx14vI/AAAAAAABF9A/pXbIUebrpDw/s1600/1-ckms.png" 
height="124" width="320" 
/>](http://4.bp.blogspot.com/-2ui0TdcqyNg/VHFpFwx14vI/AAAAAAABF9A/pXbIUebrpDw/s1600/1-ckms.png)</li><li>Remove 
any product keys installed 
<span style="font-family: Courier New, Courier, monospace;"> slmgr.vbs –upk 
[<img border="0" 
src="http://1.bp.blogspot.com/-RwMVIQUMdCY/VHFo_cYfQxI/AAAAAAABF84/pU-oSA8lMow/s1600/upk.png" 
height="119" width="200" 
/>](http://1.bp.blogspot.com/-RwMVIQUMdCY/VHFo_cYfQxI/AAAAAAABF84/pU-oSA8lMow/s1600/upk.png)</li><li>Replace 
the X's with your product key. 
<span style="font-family: Courier New, Courier, monospace;"> slmgr.vbs -ipk 
XXXXX-XXXXX-XXXXX-XXXXX-XXXXX 
[<img border="0" 
src="http://1.bp.blogspot.com/-HJ6-iOv4cRs/VHFpOvnMX2I/AAAAAAABF9I/RJZXXo859Bc/s1600/ipk.png" 
height="114" width="320" 
/>](http://1.bp.blogspot.com/-HJ6-iOv4cRs/VHFpOvnMX2I/AAAAAAABF9I/RJZXXo859Bc/s1600/ipk.png)</li><li>Activate 
your server/computer 
<span style="font-family: Courier New, Courier, monospace;"> slmgr.vbs –ato 
[<img border="0" 
src="http://2.bp.blogspot.com/-U6OsYw4K31M/VHFpV0WmTAI/AAAAAAABF9Q/cuRlV4_0Uzk/s1600/ato.png" 
height="123" width="200" 
/>](http://2.bp.blogspot.com/-U6OsYw4K31M/VHFpV0WmTAI/AAAAAAABF9Q/cuRlV4_0Uzk/s1600/ato.png)</li>Your 
operating system (Windows 8 / Windows Server) should now be activated. 