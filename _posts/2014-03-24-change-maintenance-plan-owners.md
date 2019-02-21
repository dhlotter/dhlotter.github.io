---
title: Change Maintenance Plan Owners
date: '2014-03-24T12:46:00.000+02:00'
search: true
author: Hermann Lotter
comments: true
tags:
- sql
published: true
---

Every now and then I happen upon a maintenance plan which was created under 
user credentials. As part of the maintenance plan, SQL agent jobs are created 
which then runs under the plan owner's credentials. To give you context, if I 
log onto a SQL instance with a username [backupuser] and create a maintenance 
plan, the SQL agent jobs will all have [backupuser] as their owner as well. 
Now this can easily be changed in the job, but whenever a change is made to 
the originating maintenance plan, the SQL agent job owner (that and every 
other change made to the agent job) will be replaced to the original. 

This is mildly frustrating and can be even more dangerous if the account used 
was an active directory account and becomes disabled. 

To prevent this from happening, always create maintenance plans with a SQL 
user which will never be changed/disabled. Sounds familiar? In the below 
example I show you how to identify maintenance plans created with the 
indicated user and then subsequently how to update them. I use user [sa] as 
the owner. 
<pre class="brush:sql"> </pre><pre class="brush:sql"></pre><style 
type="text/css"></style>  <code style="font-size: 12px;"><span style="color: 
black;"> 

 <span style="color: green;">-- identify maintenance plans not having sa as 
the owner 
 <span style="color: blue;">SELECT <span style="color: 
magenta;">SUSER_SNAME<span style="color: grey;">(<span style="color: 
black;">[ownersid]<span style="color: grey;">) <span style="color: blue;">AS 
<span style="color: red;">'owner'<span style="color: grey;">, <span 
style="color: black;">[ownersid]<span style="color: grey;">, * 
 <span style="color: blue;">FROM <span style="color: 
black;">[msdb].[dbo].[sysssispackages] 
 <span style="color: blue;">WHERE <span style="color: black;">[packagetype] 
<span style="color: blue;">= <span style="color: black;">6 <span style="color: 
grey;">AND <span style="color: black;">[ownersid] <span style="color: 
grey;">&lt;&gt; <span style="color: magenta;">SUSER_SID<span style="color: 
grey;">(<span style="color: red;">'sa'<span style="color: grey;">) 

 <span style="color: green;">-- updating these plans 
 <span style="color: blue;">UPDATE <span style="color: 
black;">[msdb].[dbo].[sysssispackages] 
 <span style="color: blue;">SET <span style="color: black;">[ownersid] <span 
style="color: blue;">= <span style="color: magenta;">SUSER_SID<span 
style="color: grey;">(<span style="color: red;">'sa'<span style="color: 
grey;">) 
 <span style="color: blue;">WHERE <span style="color: black;">[packagetype] 
<span style="color: blue;">= <span style="color: black;">6 <span style="color: 
grey;">AND <span style="color: black;">[ownersid] <span style="color: 
grey;">&lt;&gt; <span style="color: magenta;">SUSER_SID<span style="color: 
grey;">(<span style="color: red;">'sa'<span style="color: grey;">)</code> 