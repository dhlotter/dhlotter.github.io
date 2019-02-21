---
title: How to install .NET Framework 3.5 on Windows Server 2012 and WindowsServer
  2012 R2
date: '2013-10-18T17:44:00.000+02:00'
search: true
author: Hermann Lotter
comments: true
tags:
- tech
published: true
---

I bet you there is a bunch of you struggling with this issue and it's driving 
me crazy. I needed to perform these installs quite often and had to remember 
what I did last time. This post will act as my extended memory. 

Open an elevated command prompt and kick off the below command (changing the 
sources path to where your sources folder is located). 
<pre></pre><pre>dism /online /enable-feature /featurename:NetFX3 /all 
/Source:S:\sources\sxs /LimitAccess</pre> 
<span style="font-size: 14px; line-height: 1.5;">We have the folder stashed on 
a file server and merely map it to local machine. 

<div class="separator" style="clear: both; text-align: center;">[<img 
border="0" 
src="http://3.bp.blogspot.com/-WncCYa1wxbo/VHFoNQeF4QI/AAAAAAABF8g/cr8JnQd6ADY/s1600/11.png" 
height="412" width="640" 
/>](http://3.bp.blogspot.com/-WncCYa1wxbo/VHFoNQeF4QI/AAAAAAABF8g/cr8JnQd6ADY/s1600/11.png) 

And its as easy as that. 