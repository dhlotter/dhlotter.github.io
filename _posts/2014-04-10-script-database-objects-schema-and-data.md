---
title: Script Database Objects (Schema and Data)
date: '2014-04-10T15:36:00.000+02:00'
search: true
author: Hermann Lotter
comments: true
tags:
- sql
published: true
---

Every now and then we need to create a full baseline for our current 
development environment (which is not a backup). Without looking for tools on 
Google, the easiest way to accomplish this is to use SSMS. 
<div> 
<div>Just right click on you database and point to **Tasks** &gt; **Generate 
Scripts...** 

<span style="line-height: 1.5em;">You are greeted with the trusty introduction 
page which you can just skip through. 
<span style="line-height: 1.5em;"> 
<span style="line-height: 1.5em;">In the [**Choose Objects**<span 
style="line-height: 1.5em;">] window, you can select the objects you would 
like to script out. In my case I was interested in the entire database. 
<span style="line-height: 1.5em;"> 
<span style="line-height: 1.5em;">The important section in this process is the 
[**Set Scripting Options**<span style="line-height: 1.5em;">] screen. This is 
where we find the advanced button which let us customize a couple of things. 
So go on hit the [**Advance**<span style="line-height: 1.5em;">] button. 
<span style="line-height: 1.5em;"> 
<span style="line-height: 1.5em;">This is where you can change the type of 
data to script from schema only, data only or schema and data. 
<div><div class="separator" style="clear: both; text-align: center;">[<img 
border="0" 
src="http://3.bp.blogspot.com/-CI-QdgEF7Z8/VHFq9CXS1jI/AAAAAAABF9c/c4ecXrDAito/s1600/5.png" 
height="595" width="640" 
/>](http://3.bp.blogspot.com/-CI-QdgEF7Z8/VHFq9CXS1jI/AAAAAAABF9c/c4ecXrDAito/s1600/5.png) 
<div> 
<div>Click Next/Finish and pick up your scripts in the folder specified. 
<div> 
<div style="display: inline !important;"><div class="separator" style="clear: 
both; text-align: center;"> 
<div class="separator" style="clear: both; text-align: center;"><div 
class="separator" style="clear: both; text-align: center;">[<img border="0" 
src="http://3.bp.blogspot.com/-y4QSKoqs-8E/VHFq9U83BJI/AAAAAAABF9g/7rgSiD1igi0/s1600/6.png" 
height="594" width="640" 
/>](http://3.bp.blogspot.com/-y4QSKoqs-8E/VHFq9U83BJI/AAAAAAABF9g/7rgSiD1igi0/s1600/6.png)<div 
class="separator" style="clear: both; text-align: center;">[<img border="0" 
src="http://2.bp.blogspot.com/-J2Hg0pfqPu0/VHFq9txaFEI/AAAAAAABF9k/uG0cddkZOlM/s1600/7.png" 
height="594" width="640" 
/>](http://2.bp.blogspot.com/-J2Hg0pfqPu0/VHFq9txaFEI/AAAAAAABF9k/uG0cddkZOlM/s1600/7.png) 

<div><img alt="" 
src="file:///C:/Users/HERMAN~1.LOT/AppData/Local/Temp/enhtmlclip/Image(14).png" 
/> 
<div> 
<div> 