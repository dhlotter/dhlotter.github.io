---
title: '"Process could not read the file" Change SQL replication snapshot folder'
date: '2014-04-25T13:21:00.000+02:00'
search: true
author: Hermann Lotter
comments: true
tags:
- sql
published: true
---

While setting up replication, you might walk into the below issue from time to 
time (more than once and you should have paid better attention the first time 
around). 
<pre>**Command attempted:** 

E:\SQL\Snapshots\unc\POCSQL001_BANKLINK_BANKLINK\20140424073004\fn_diagramobjects_267.pre 
(Transaction sequence number: 0x000219650000039E00F300000000, Command ID: 270) 

## Error messages: 
The process could not read file 
'E:\SQL\Snapshots\unc\POCSQL001_BANKLINK_BANKLINK\20140424073004\fn_diagramobjects_267.pre' 
due to OS error 3. 
(Source: MSSQL_REPL, Error number: MSSQL_REPL20024) 
Get help: http://help/MSSQL_REPL20024 
The system cannot find the path specified. 
(Source: MSSQL_REPL, Error number: MSSQL_REPL3) 
Get help: http://help/MSSQL_REPL3 
</pre> 
In short the subscriber cannot connect to the distributor to copy the database 
snapshot. Depending on how functional you want your replication, this might be 
a huge issue, but luckily fixing it is very easy. All you need to do is change 
your publication to store the snapshot in a UNC path. With SSMS log on to your 
distributor/publisher and follow the following steps. 

&gt; Expand **Replication** 

&gt; Expand **Local Publications** 

&gt; Right click the publication in question and choose **Properties** 

&gt; Select the **Snapshot** tab 

<div class="separator" style="clear: both; text-align: center;">[<img 
border="0" 
src="http://1.bp.blogspot.com/-PnziFHxXJNA/VHCo0Y6JBTI/AAAAAAABF4w/JFbmZXh7mbI/s1600/snapshot.png" 
height="574" width="640" 
/>](http://1.bp.blogspot.com/-PnziFHxXJNA/VHCo0Y6JBTI/AAAAAAABF4w/JFbmZXh7mbI/s1600/snapshot.png) 

You have a option to either the snapshots in the default folder or you can 
change it to specify a custom folder. Change it the option to a specific 
folder and enter the UNC path the folder which both servers can access. 

Once done, simply click **ok** and then start the snapshot agent. To do this: 

&gt; Right click the **Replication** menu in SSMS 

&gt; Choose **Launch Replication Monitor** 

&gt; Expand the tree completely and click on your Publication 

&gt; Select the **Agents** tab 

&gt; Double click the snapshot agent 

&gt; Choose the menu item **Action** and then click **Start Agent** 



This should resolve the issue you had before. 

<div class="separator" style="clear: both; text-align: center;">[<img 
border="0" 
src="http://1.bp.blogspot.com/-r8gXLCcV-3c/VHCo9hJFlaI/AAAAAAABF44/V0BtnEgkUhw/s1600/snapshot-completed.png" 
height="516" width="640" 
/>](http://1.bp.blogspot.com/-r8gXLCcV-3c/VHCo9hJFlaI/AAAAAAABF44/V0BtnEgkUhw/s1600/snapshot-completed.png) 