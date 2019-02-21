---
title: '"Process could not read the file" Change SQL replication snapshot folder'
date: '2014-04-25T13:21:00.000+02:00'
search: true
comments: true
published: true
tags:
- sql
published: true
---

While setting up replication, you might walk into the below issue from time to time (more than once and you should have paid better attention the first time around). 
```
**Command attempted:** 

E:\SQL\Snapshots\unc\POCSQL001_BANKLINK_BANKLINK\20140424073004\fn_diagramobjects_267.pre 
(Transaction sequence number: 0x000219650000039E00F300000000, Command ID: 270) 

## Error messages: 
The process could not read file 'E:\SQL\Snapshots\unc\POCSQL001_BANKLINK_BANKLINK\20140424073004\fn_diagramobjects_267.pre' due to OS error 3. (Source: MSSQL_REPL, Error number: MSSQL_REPL20024) 
Get help: http://help/MSSQL_REPL20024 
The system cannot find the path specified. 
(Source: MSSQL_REPL, Error number: MSSQL_REPL3) 
Get help: http://help/MSSQL_REPL3 
```

In short the subscriber cannot connect to the distributor to copy the database snapshot. Depending on how functional you want your replication, this might be a huge issue, but luckily fixing it is very easy. All you need to do is change your publication to store the snapshot in a UNC path. With SSMS log on to your distributor/publisher and follow the following steps. 

* Expand **Replication** 

* Expand **Local Publications** 

* Right click the publication in question and choose **Properties** 

* Select the **Snapshot** tab 

![results](/images/replication-process-could-not-read-file-001.png)


You have a option to either the snapshots in the default folder or you can 
change it to specify a custom folder. Change it the option to a specific 
folder and enter the UNC path the folder which both servers can access. 

Once done, simply click **ok** and then start the snapshot agent. To do this: 

* Right click the **Replication** menu in SSMS 

* Choose **Launch Replication Monitor** 

* Expand the tree completely and click on your Publication 

* Select the **Agents** tab 

* Double click the snapshot agent 

* Choose the menu item **Action** and then click **Start Agent** 



This should resolve the issue you had before. 

![results](/images/replication-process-could-not-read-file-002.png)
