---
title: SQL Server 2014 Upgrade Advisor Installation Issues
date: '2014-07-28T16:10:00.000+02:00'
search: true
comments: true
published: true
tags:
- sql
---

It's been a while since I pushed out an article and then today this happens to me on a SQL box. 
During the installation of SQL Server Upgrade Advisor, I ran into this box telling me I need prerequisite: 

![results](/images/sql-upgrade-advisor-001.png)

```Setup is missing prerequisites: 

-Microsoft SQL Server 2014 Transact-SQL ScriptDom, which is not installed by Upgrade Advisor Setup. To continue, install SQL Server 2014 Transact-SQL ScriptDom from below hyperlink and then run the Upgrade Advisor Setup operation again : 

Go to http://go.microsoft.com/fwlink/?LinkID=296473
```

This is a no brainer, we have forgotten to install ScriptDom which we can grab either from the [SQL server feature pack online](http://www.microsoft.com/en-za/download/details.aspx?id=42295) or copy SqlDom.msi from you SQL 2014 install media. Depending on your server setup during installation of ScriptDom you might run into the below error, which is slightly misleading and information on this is fairly sparse. 

![results](/images/sql-upgrade-advisor-002.png)

````
Error writing to file: Microsoft.SqlServer.TransactSql.ScriptDom.dll. Verify that you have access to that directory. 

Retry/Cancel
```

Now, you can press retry until you are blue in the face but you would be no closer to getting ScriptDom installed. What you want to do is install .Net 
Framework 4.0. Thinking back, it would have been nice if this check was included in the prerequisite check phase. 